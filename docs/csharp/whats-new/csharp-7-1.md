---
title: "什么是 C# 7.1 中的新增功能"
description: "C# 7.1 中的新增功能概述。"
keywords: "C# 语言设计，7.1，Visual Studio 2017，"
author: billwagner
ms.author: wiwagn
ms.date: 08/16/2017
ms.topic: article
ms.prod: .net
ms.devlang: devlang-csharp
ms.openlocfilehash: 02f1f8fc8f0a3221e00e2a3c43ce06423ca43672
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="whats-new-in-c-71"></a>什么是 C# 7.1 中的新增功能

C# 7.1 是 C# 语言的第一个点版本。 标记着语言增加的发布节奏加快。 你可以使用新的功能更快，理想情况下准备每个新功能时。 C# 7.1 添加了配置以匹配的指定的版本的语言编译器的功能。 它使你可以将分隔从判定升级语言版本升级工具的决策。

C# 7.1 添加[语言版本选择](#language-version-selection)配置元素、 三个新的语言功能和新的编译器行为。

在此版本中的新语言功能包括：

* [`async` `Main`方法](#async-main)
  - 应用程序的入口点可以具有`async`修饰符。
* [`default`文本表达式](#default-literal-expressions)
  - 可以推断的目标类型时，可以在默认值表达式中使用默认文本表达式。
* [推断元组元素名称](#inferred-tuple-element-names)
  - 可以从在许多情况下的元组初始化推断的元组元素的名称。

最后，编译器具有两个选项`/refout`和`/refonly`该控件[引用程序集生成](#reference-assembly-generation)。

## <a name="language-version-selection"></a>语言版本选择

C# 编译器支持 C# 7.1 从 Visual Studio 2017 版本 15.3 或.NET 核心 SDK 2.0。 但是，7.1 功能将关闭默认情况下。 若要启用的 7.1 功能，你需要更改你的项目的语言版本设置。

在 Visual Studio 中，右键单击解决方案资源管理器中的项目节点，然后选择**属性**。 选择**生成**选项卡并选择**高级**按钮。 在下拉列表中，选择**C# 最新次要版本 （最新）**，或特定版本**C# 7.1**在映像下面的示例所示。 `latest`值表示你想要在当前计算机上使用的最新次版本。 `C# 7.1`意味着你想要使用 C# 7.1、，甚至在较新的次要版本发布之后。

![设置的语言版本](./media/csharp-7-1/advanced-build-settings.png)

或者，你可以编辑"csproj"文件和添加或修改以下行：

```xml
<PropertyGroup>
  <LangVersion>latest</LangVersion>
</PropertyGroup>
```

> [!NOTE]
> 如果使用 Visual Studio IDE 来更新 csproj 文件，IDE 将创建单独的节点，每个生成配置。 你将通常设置的值相同在所有生成配置，但你需要将其显式设置每个生成配置，或修改此设置时选择"所有配置"。 在 csproj 文件中，你将看到以下：

```xml
<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
  <LangVersion>latest</LangVersion>
</PropertyGroup>

<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">
  <LangVersion>latest</LangVersion>
</PropertyGroup>
```

有效设置`LangVersion`元素：

* `ISO-1`
* `ISO-2`
* `3`
* `4`
* `5`
* `6`
* `7`
* `7.1`
* `default`
* `latest`

特殊字符串`default`和`latest`解析为分别在生成计算机上安装的最新主要和次要语言版本。

此设置将分离选择以包含在项目中的新语言功能的开发环境中安装新版本的 SDK 和工具。 你可以在生成计算机上安装的最新的 SDK 和工具。 每个项目可以配置要用于其生成的特定版本的语言。

## <a name="async-main"></a>异步主要

*异步主要*方法使您能够使用`await`中你`Main`方法。
以前，你需要编写：

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

您现在可以编写：

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

如果你的程序不返回退出代码，你可以声明`Main`返回方法<xref:System.Threading.Tasks.Task>:

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

你可以阅读更多有关中的详细信息[异步主要](../programming-guide/main-and-command-args/index.md)编程指南中的主题。

## <a name="default-literal-expressions"></a>默认文本表达式

默认文本表达式是一项增强功能的默认值表达式。
这些表达式初始化为默认值的变量。 其中以前编写：

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

现在，则可以省略的初始化的右侧类型：

```csharp
Func<string, bool> whereClause = default;
```

你可以了解有关 C# 编程指南主题中的此增强功能的详细信息上[默认值表达式](../programming-guide/statements-expressions-operators/default-value-expressions.md)。

此增强功能也会更改某些的分析规则[default 关键字](../language-reference/keywords/default.md)。

## <a name="inferred-tuple-element-names"></a>推断元组元素名称

此功能是在 C# 7.0 中引入的元组功能小增强功能。 很多时候时初始化元组，使用分配的左右两边的变量是你想要为元组元素的名称相同：

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count: count, label: label);
```

用于初始化的元组 7.1 C# 中的变量中推断的元组元素的名称：

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

你可以了解有关此功能的详细[元组](../tuples.md)主题。

## <a name="reference-assembly-generation"></a>引用程序集生成

有两个新的编译器选项生成*仅引用程序集*: [/refout](../language-reference/compiler-options/refout-compiler-option.md)和[/refonly](../language-reference/compiler-options/refonly-compiler-option.md)。
链接的主题介绍了这些选项以及更多详细信息中的引用程序集。
