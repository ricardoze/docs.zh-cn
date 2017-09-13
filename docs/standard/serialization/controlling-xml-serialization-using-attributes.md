---
title: "使用属性控制 XML 序列化"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- classes, serializing
- XML serialization, examples
- derived classes, serializing
- arrays, serializing
- XML serialization, attributes
- preventing serialization
- attributes [.NET Framework], XML serialization
- serialization, examples
- serialization, attributes
ms.assetid: 47d4c39d-30e1-4c7b-8a2e-301325390647
caps.latest.revision: 4
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: c00ceea5e9700b0e964b799684eea743c540992d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="controlling-xml-serialization-using-attributes"></a><span data-ttu-id="2789a-102">使用属性控制 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="2789a-102">Controlling XML Serialization Using Attributes</span></span>
<span data-ttu-id="2789a-103">使用属性可以控制对象的 XML 序列化，还可以利用同一组类创建其他 XML 流。</span><span class="sxs-lookup"><span data-stu-id="2789a-103">Attributes can be used to control the XML serialization of an object or to create an alternate XML stream from the same set of classes.</span></span> <span data-ttu-id="2789a-104">有关创建其他 XML 流的详细信息，请参见[如何：指定 XML 流的替代元素名称](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md)。</span><span class="sxs-lookup"><span data-stu-id="2789a-104">For more details about creating an alternate XML stream, see [How to: Specify an Alternate Element Name for an XML Stream](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2789a-105">如果生成的 XML 必须符合万维网联合会 (www.w3.org) 文档“简单对象访问协议 (SOAP) 1.1”第 5 节的内容，则需使用 [控制编码的 SOAP 序列化的特性](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md) 中所列的特性。</span><span class="sxs-lookup"><span data-stu-id="2789a-105">If the XML generated must conform to section 5 of the World Wide Web Consortium (www.w3.org) document titled "Simple Object Access Protocol (SOAP) 1.1," use the attributes listed in [Attributes That Control Encoded SOAP Serialization](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md).</span></span>  
  
 <span data-ttu-id="2789a-106">默认情况下，XML 元素名称由类或成员名称确定。</span><span class="sxs-lookup"><span data-stu-id="2789a-106">By default, an XML element name is determined by the class or member name.</span></span> <span data-ttu-id="2789a-107">在名为 `Book` 的简单类中，名为 `ISBN` 的字段将生成 XML 元素标记 \<ISBN>，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-107">In a simple class named `Book`, a field named `ISBN` will produce an XML element tag \<ISBN>, as shown in the following example.</span></span>  
  
```vb  
Public Class Book  
    Public ISBN As String  
End Class  
' When an instance of the Book class is serialized, it might   
' produce this XML:  
' <ISBN>1234567890</ISBN>.  
```  
  
```csharp  
public class Book  
{  
    public string ISBN;  
}  
// When an instance of the Book class is serialized, it might   
// produce this XML:  
// <ISBN>1234567890</ISBN>.  
```  
  
 <span data-ttu-id="2789a-108">若要重新命名元素，可以更改这种默认行为。</span><span class="sxs-lookup"><span data-stu-id="2789a-108">This default behavior can be changed if you want to give the element a new name.</span></span> <span data-ttu-id="2789a-109">下面的代码演示属性 (Attribute) 如何通过设置 <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A> 的 <xref:System.Xml.Serialization.XmlElementAttribute> 属性 (Property) 实现此目的。</span><span class="sxs-lookup"><span data-stu-id="2789a-109">The following code shows how an attribute enables this by setting the <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A> property of a <xref:System.Xml.Serialization.XmlElementAttribute>.</span></span>  
  
```vb  
Public Class TaxRates  
   < XmlElement(ElementName = "TaxRate")> _  
    Public ReturnTaxRate As Decimal  
End Class  
```  
  
```csharp  
public class TaxRates{  
    [XmlElement(ElementName = "TaxRate")]  
    public decimal ReturnTaxRate;  
}  
```  
  
 <span data-ttu-id="2789a-110">有关属性的详细信息，请参阅[属性](../../../docs/standard/attributes/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2789a-110">For more information about attributes, see [Attributes](../../../docs/standard/attributes/index.md).</span></span> <span data-ttu-id="2789a-111">有关控制 XML 序列化的特性的列表，请参阅[控制 XML 序列化的特性](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="2789a-111">For a list of attributes that control XML serialization, see [Attributes That Control XML Serialization](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md).</span></span>  
  
## <a name="controlling-array-serialization"></a><span data-ttu-id="2789a-112">控制数组序列化</span><span class="sxs-lookup"><span data-stu-id="2789a-112">Controlling Array Serialization</span></span>  
 <span data-ttu-id="2789a-113"><xref:System.Xml.Serialization.XmlArrayAttribute> 和 <xref:System.Xml.Serialization.XmlArrayItemAttribute> 属性旨在用于控制数组的序列化。</span><span class="sxs-lookup"><span data-stu-id="2789a-113">The <xref:System.Xml.Serialization.XmlArrayAttribute> and the <xref:System.Xml.Serialization.XmlArrayItemAttribute> attributes are designed to control the serialization of arrays.</span></span> <span data-ttu-id="2789a-114">使用这些特性可以控制元素名称、命名空间以及 XML 架构 (XSD) 数据类型（在万维网联合会 [www.w3.org] 文档“XML 架构第 2 部分：数据类型”中进行了定义）。</span><span class="sxs-lookup"><span data-stu-id="2789a-114">Using these attributes, you can control the element name, namespace, and XML Schema (XSD) data type (as defined in the World Wide Web Consortium [www.w3.org] document titled "XML Schema Part 2: Datatypes").</span></span> <span data-ttu-id="2789a-115">此外，还可以指定数组所能包含的类型。</span><span class="sxs-lookup"><span data-stu-id="2789a-115">You can also specify the types that can be included in an array.</span></span>  
  
 <span data-ttu-id="2789a-116">对于序列化数组时生成的封闭 XML 元素，其属性将由 <xref:System.Xml.Serialization.XmlArrayAttribute> 确定。</span><span class="sxs-lookup"><span data-stu-id="2789a-116">The <xref:System.Xml.Serialization.XmlArrayAttribute> will determine the properties of the enclosing XML element that results when an array is serialized.</span></span> <span data-ttu-id="2789a-117">例如，默认情况下，序列化下面的数组时，将会生成名为 `Employees` 的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="2789a-117">For example, by default, serializing the array below will result in an XML element named `Employees`.</span></span> <span data-ttu-id="2789a-118">`Employees` 元素将包含在数组类型 `Employee` 之后命名的一系列元素。</span><span class="sxs-lookup"><span data-stu-id="2789a-118">The `Employees` element will contain a series of elements named after the array type `Employee`.</span></span>  
  
```vb  
Public Class Group  
    Public Employees() As Employee  
End Class  
Public Class Employee  
    Public Name As String  
End Class  
```  
  
```csharp  
public class Group{  
    public Employee[] Employees;  
}  
public class Employee{  
    public string Name;  
}  
```  
  
 <span data-ttu-id="2789a-119">序列化实例可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-119">A serialized instance might resemble the following.</span></span>  
  
```xml  
<Group>  
<Employees>  
    <Employee>  
        <Name>Haley</Name>  
    </Employee>  
</Employees >  
</Group>  
```  
  
 <span data-ttu-id="2789a-120">通过应用 <xref:System.Xml.Serialization.XmlArrayAttribute>，可以按照以下方式更改 XML 元素的名称。</span><span class="sxs-lookup"><span data-stu-id="2789a-120">By applying a <xref:System.Xml.Serialization.XmlArrayAttribute>, you can change the name of the XML element, as follows.</span></span>  
  
```vb  
Public Class Group  
    <XmlArray("TeamMembers")> _  
    Public Employees() As Employee  
End Class  
```  
  
```csharp  
public class Group{  
    [XmlArray("TeamMembers")]  
    public Employee[] Employees;  
}  
```  
  
 <span data-ttu-id="2789a-121">生成的 XML 可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-121">The resulting XML might resemble the following.</span></span>  
  
```xml  
<Group>  
<TeamMembers>  
    <Employee>  
        <Name>Haley</Name>  
    </Employee>  
</TeamMembers>  
```  
  
 <span data-ttu-id="2789a-122">另一方面，<xref:System.Xml.Serialization.XmlArrayItemAttribute> 可以控制如何序列化数组中包含的项。</span><span class="sxs-lookup"><span data-stu-id="2789a-122">The <xref:System.Xml.Serialization.XmlArrayItemAttribute>, on the other hand, controls how the items contained in the array are serialized.</span></span> <span data-ttu-id="2789a-123">请注意，该特性将应用于返回数组的字段。</span><span class="sxs-lookup"><span data-stu-id="2789a-123">Note that the attribute is applied to the field returning the array.</span></span>  
  
```vb  
Public Class Group  
    <XmlArrayItem("MemberName")> _  
    Public Employee() As Employees  
End Class  
```  
  
```csharp  
public class Group{  
    [XmlArrayItem("MemberName")]  
    public Employee[] Employees;  
}  
```  
  
 <span data-ttu-id="2789a-124">生成的 XML 可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-124">The resulting XML might resemble the following.</span></span>  
  
```xml  
<Group>  
<Employees>  
    <MemberName>Haley</MemberName>  
</Employees>  
</Group>  
```  
  
## <a name="serializing-derived-classes"></a><span data-ttu-id="2789a-125">序列化派生类</span><span class="sxs-lookup"><span data-stu-id="2789a-125">Serializing Derived Classes</span></span>  
 <span data-ttu-id="2789a-126"><xref:System.Xml.Serialization.XmlArrayItemAttribute> 的另一种用法是，允许序列化派生类。</span><span class="sxs-lookup"><span data-stu-id="2789a-126">Another use of the <xref:System.Xml.Serialization.XmlArrayItemAttribute> is to allow the serialization of derived classes.</span></span> <span data-ttu-id="2789a-127">例如，可将派生自 `Manager` 的另一个名为 `Employee` 的类添加至上一示例中。</span><span class="sxs-lookup"><span data-stu-id="2789a-127">For example, another class named `Manager` that derives from `Employee` can be added to the previous example.</span></span> <span data-ttu-id="2789a-128">如果没有应用 <xref:System.Xml.Serialization.XmlArrayItemAttribute>，代码将在运行时失败，原因是无法识别派生类类型。</span><span class="sxs-lookup"><span data-stu-id="2789a-128">If you do not apply the <xref:System.Xml.Serialization.XmlArrayItemAttribute>, the code will fail at run time because the derived class type will not be recognized.</span></span> <span data-ttu-id="2789a-129">若要解决这个问题，每次为每个可接受类型（基类和派生类）设置 <xref:System.Xml.Serialization.XmlArrayItemAttribute.Type%2A> 属性时，需要应用该特性两次。</span><span class="sxs-lookup"><span data-stu-id="2789a-129">To remedy this, apply the attribute twice, each time setting the <xref:System.Xml.Serialization.XmlArrayItemAttribute.Type%2A> property for each acceptable type (base and derived).</span></span>  
  
```vb  
Public Class Group  
    <XmlArrayItem(Type:=GetType(Employee)), _  
    XmlArrayItem(Type:=GetType(Manager))> _  
    Public Employees() As Employee  
End Class  
Public Class Employee  
    Public Name As String  
End Class  
Public Class Manager  
Inherits Employee  
    Public Level As Integer  
End Class  
```  
  
```csharp  
public class Group{  
    [XmlArrayItem(Type = typeof(Employee)),  
    XmlArrayItem(Type = typeof(Manager))]  
    public Employee[] Employees;  
}  
public class Employee{  
    public string Name;  
}  
public class Manager:Employee{  
    public int Level;  
}  
```  
  
 <span data-ttu-id="2789a-130">序列化实例可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-130">A serialized instance might resemble the following.</span></span>  
  
```xml  
<Group>  
<Employees>  
    <Employee>  
        <Name>Haley</Name>  
    </Employee>  
    <Employee xsi:type = "Manager">  
        <Name>Ann</Name>  
        <Level>3</Level>  
    <Employee>  
</Employees >  
</Group>  
```  
  
## <a name="serializing-an-array-as-a-sequence-of-elements"></a><span data-ttu-id="2789a-131">将数组作为元素序列进行序列化</span><span class="sxs-lookup"><span data-stu-id="2789a-131">Serializing an Array as a Sequence of Elements</span></span>  
 <span data-ttu-id="2789a-132">通过将 <xref:System.Xml.Serialization.XmlElementAttribute> 应用于返回数组的字段，还可以将该数组作为 XML 元素的平面序列进行序列化，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-132">You can also serialize an array as a flat sequence of XML elements by applying a <xref:System.Xml.Serialization.XmlElementAttribute> to the field returning the array as follows.</span></span>  
  
```vb  
Public Class Group  
    <XmlElement> _  
    Public Employees() As Employee  
End Class  
```  
  
```csharp  
public class Group{  
    [XmlElement]  
    public Employee[] Employees;  
}  
```  
  
 <span data-ttu-id="2789a-133">序列化实例可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-133">A serialized instance might resemble the following.</span></span>  
  
```xml  
<Group>  
<Employees>  
    <Name>Haley</Name>  
</Employees>  
<Employees>  
    <Name>Noriko</Name>  
</Employees>  
<Employees>  
    <Name>Marco</Name>  
</Employees>  
</Group>  
```  
  
 <span data-ttu-id="2789a-134">区别两种 XML 流的另一个方法是，使用 XML 架构定义工具，从编译好的代码生成 XML 架构 (XSD) 文档文件。</span><span class="sxs-lookup"><span data-stu-id="2789a-134">Another way to differentiate the two XML streams is to use the XML Schema Definition tool to generate the XML Schema (XSD) document files from the compiled code.</span></span> <span data-ttu-id="2789a-135">（有关使用该工具的详细信息，请参见[XML 架构定义工具和 XML 序列化](../../../docs/standard/serialization/the-xml-schema-definition-tool-and-xml-serialization.md)。）没有将属性应用于字段时，架构会以下列方式描述元素。</span><span class="sxs-lookup"><span data-stu-id="2789a-135">(For more details on using the tool, see [The XML Schema Definition Tool and XML Serialization](../../../docs/standard/serialization/the-xml-schema-definition-tool-and-xml-serialization.md).) When no attribute is applied to the field, the schema describes the element in the following manner.</span></span>  
  
```xml  
<xs:element minOccurs="0" maxOccurs ="1" name="Employees" type="ArrayOfEmployee" />  
```  
  
 <span data-ttu-id="2789a-136">将 <xref:System.Xml.Serialization.XmlElementAttribute> 应用于字段时，生成的架构会以下列方式描述元素。</span><span class="sxs-lookup"><span data-stu-id="2789a-136">When the <xref:System.Xml.Serialization.XmlElementAttribute> is applied to the field, the resulting schema describes the element as follows.</span></span>  
  
```xml  
<xs:element minOccurs="0" maxOccurs="unbounded" name="Employees" type="Employee" />   
```  
  
## <a name="serializing-an-arraylist"></a><span data-ttu-id="2789a-137">序列化 ArrayList</span><span class="sxs-lookup"><span data-stu-id="2789a-137">Serializing an ArrayList</span></span>  
 <span data-ttu-id="2789a-138"><xref:System.Collections.ArrayList> 类可能包含各种不同对象的集合。</span><span class="sxs-lookup"><span data-stu-id="2789a-138">The <xref:System.Collections.ArrayList> class can contain a collection of diverse objects.</span></span> <span data-ttu-id="2789a-139">因此，可以按照使用数组的类似方式使用 <xref:System.Collections.ArrayList>。</span><span class="sxs-lookup"><span data-stu-id="2789a-139">You can therefore use a <xref:System.Collections.ArrayList> much as you use an array.</span></span> <span data-ttu-id="2789a-140">您可以创建返回单个 <xref:System.Collections.ArrayList> 的字段，而不用创建返回类型化对象的数组的字段。</span><span class="sxs-lookup"><span data-stu-id="2789a-140">Instead of creating a field that returns an array of typed objects, however, you can create a field that returns a single <xref:System.Collections.ArrayList>.</span></span> <span data-ttu-id="2789a-141">但是，与数组相同的是，必须将 <xref:System.Xml.Serialization.XmlSerializer> 包含的对象的类型告知 <xref:System.Collections.ArrayList>。</span><span class="sxs-lookup"><span data-stu-id="2789a-141">However, as with arrays, you must inform the <xref:System.Xml.Serialization.XmlSerializer> of the types of objects the <xref:System.Collections.ArrayList> contains.</span></span> <span data-ttu-id="2789a-142">为此，需要为该字段分配 <xref:System.Xml.Serialization.XmlElementAttribute> 的多个实例，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="2789a-142">To accomplish this, assign multiple instances of the <xref:System.Xml.Serialization.XmlElementAttribute> to the field, as shown in the following example.</span></span>  
  
```vb  
Public Class Group  
    <XmlElement(Type:=GetType(Employee)), _  
    XmlElement(Type:=GetType(Manager))> _  
    Public Info As ArrayList  
End Class  
```  
  
```csharp  
public class Group{  
    [XmlElement(Type = typeof(Employee)),   
    XmlElement(Type = typeof(Manager))]  
    public ArrayList Info;  
}  
```  
  
## <a name="controlling-serialization-of-classes-using-xmlrootattribute-and-xmltypeattribute"></a><span data-ttu-id="2789a-143">使用 XmlRootAttribute 和 XmlTypeAttribute 控制类的序列化</span><span class="sxs-lookup"><span data-stu-id="2789a-143">Controlling Serialization of Classes Using XmlRootAttribute and XmlTypeAttribute</span></span>  
 <span data-ttu-id="2789a-144">能且只能应用于一个类的特性有下面两种：<xref:System.Xml.Serialization.XmlRootAttribute> 和 <xref:System.Xml.Serialization.XmlTypeAttribute>。</span><span class="sxs-lookup"><span data-stu-id="2789a-144">There are two attributes that can be applied to a class (and only a class): <xref:System.Xml.Serialization.XmlRootAttribute> and <xref:System.Xml.Serialization.XmlTypeAttribute>.</span></span> <span data-ttu-id="2789a-145">这两种特性非常相似。</span><span class="sxs-lookup"><span data-stu-id="2789a-145">These attributes are very similar.</span></span> <span data-ttu-id="2789a-146"><xref:System.Xml.Serialization.XmlRootAttribute> 只能应用于一个类：序列化时，该类表示 XML 文档的开始和结束元素，也就是根元素。</span><span class="sxs-lookup"><span data-stu-id="2789a-146">The <xref:System.Xml.Serialization.XmlRootAttribute> can be applied to only one class: the class that, when serialized, represents the XML document's opening and closing element—in other words, the root element.</span></span> <span data-ttu-id="2789a-147">另一方面，<xref:System.Xml.Serialization.XmlTypeAttribute> 可以应用于任何一个类，包括根类。</span><span class="sxs-lookup"><span data-stu-id="2789a-147">The <xref:System.Xml.Serialization.XmlTypeAttribute>, on the other hand, can be applied to any class, including the root class.</span></span>  
  
 <span data-ttu-id="2789a-148">例如，在上面的示例中，`Group` 类就是根类，而其所有的公共字段和属性变成 XML 文档中的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="2789a-148">For example, in the previous examples, the `Group` class is the root class, and all its public fields and properties become the XML elements found in the XML document.</span></span> <span data-ttu-id="2789a-149">因此，只能有一个根类。</span><span class="sxs-lookup"><span data-stu-id="2789a-149">Therefore, there can be only one root class.</span></span> <span data-ttu-id="2789a-150">通过应用 <xref:System.Xml.Serialization.XmlRootAttribute>，可以控制 <xref:System.Xml.Serialization.XmlSerializer> 所生成的 XML 流。</span><span class="sxs-lookup"><span data-stu-id="2789a-150">By applying the <xref:System.Xml.Serialization.XmlRootAttribute>, you can control the XML stream generated by the <xref:System.Xml.Serialization.XmlSerializer>.</span></span> <span data-ttu-id="2789a-151">例如，可以更改元素名称和命名空间。</span><span class="sxs-lookup"><span data-stu-id="2789a-151">For example, you can change the element name and namespace.</span></span>  
  
 <span data-ttu-id="2789a-152">使用 <xref:System.Xml.Serialization.XmlTypeAttribute> 可以控制所生成 XML 的架构。</span><span class="sxs-lookup"><span data-stu-id="2789a-152">The <xref:System.Xml.Serialization.XmlTypeAttribute> allows you to control the schema of the generated XML.</span></span> <span data-ttu-id="2789a-153">需要通过 XML Web services 发布架构时，这项功能很有用。</span><span class="sxs-lookup"><span data-stu-id="2789a-153">This capability is useful when you need to publish the schema through an XML Web service.</span></span> <span data-ttu-id="2789a-154">下面的示例将 <xref:System.Xml.Serialization.XmlTypeAttribute> 和 <xref:System.Xml.Serialization.XmlRootAttribute> 同时应用于同一个类。</span><span class="sxs-lookup"><span data-stu-id="2789a-154">The following example applies both the <xref:System.Xml.Serialization.XmlTypeAttribute> and the <xref:System.Xml.Serialization.XmlRootAttribute> to the same class.</span></span>  
  
```vb  
<XmlRoot("NewGroupName"), _  
XmlType("NewTypeName")> _  
Public Class Group  
    Public Employees() As Employee  
End Class  
```  
  
```csharp  
[XmlRoot("NewGroupName")]  
[XmlType("NewTypeName")]  
public class Group{  
    public Employee[] Employees;  
}  
```  
  
 <span data-ttu-id="2789a-155">如果对该类进行编译，并且使用 XML 架构定义工具生成其架构，可能会找到下面描述 `Group` 的 XML。</span><span class="sxs-lookup"><span data-stu-id="2789a-155">If this class is compiled, and the XML Schema Definition tool is used to generate its schema, you would find the following XML describing `Group`.</span></span>  
  
```xml  
<xs:element name="NewGroupName" type="NewTypeName">  
```  
  
 <span data-ttu-id="2789a-156">相比之下，如果是对该类的实例进行序列化，则只能在 XML 文档中找到 `NewGroupName`。</span><span class="sxs-lookup"><span data-stu-id="2789a-156">In contrast, if you were to serialize an instance of the class, only `NewGroupName` would be found in the XML document.</span></span>  
  
```xml  
<NewGroupName>  
    . . .  
</NewGroupName>  
```  
  
## <a name="preventing-serialization-with-the-xmlignoreattribute"></a><span data-ttu-id="2789a-157">使用 XmlIgnoreAttribute 防止序列化</span><span class="sxs-lookup"><span data-stu-id="2789a-157">Preventing Serialization with the XmlIgnoreAttribute</span></span>  
 <span data-ttu-id="2789a-158">可能会出现公共属性或字段无需进行序列化的情况。</span><span class="sxs-lookup"><span data-stu-id="2789a-158">There might be situations when a public property or field does not need to be serialized.</span></span> <span data-ttu-id="2789a-159">例如，字段或属性可能用于包含元数据。</span><span class="sxs-lookup"><span data-stu-id="2789a-159">For example, a field or property could be used to contain metadata.</span></span> <span data-ttu-id="2789a-160">在这样的情况下，可将 <xref:System.Xml.Serialization.XmlIgnoreAttribute> 应用于该字段或属性，而 <xref:System.Xml.Serialization.XmlSerializer> 将跳过它。</span><span class="sxs-lookup"><span data-stu-id="2789a-160">In such cases, apply the <xref:System.Xml.Serialization.XmlIgnoreAttribute> to the field or property and the <xref:System.Xml.Serialization.XmlSerializer> will skip over it.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2789a-161">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2789a-161">See Also</span></span>  
 <span data-ttu-id="2789a-162">[控制 XML 序列化的特性](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="2789a-162">[Attributes That Control XML Serialization](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md) </span></span>  
 <span data-ttu-id="2789a-163">[控制编码的 SOAP 序列化的特性](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="2789a-163">[Attributes That Control Encoded SOAP Serialization](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md) </span></span>  
 <span data-ttu-id="2789a-164">[XML 序列化简介](../../../docs/standard/serialization/introducing-xml-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="2789a-164">[Introducing XML Serialization](../../../docs/standard/serialization/introducing-xml-serialization.md) </span></span>  
 <span data-ttu-id="2789a-165">[XML 序列化示例](../../../docs/standard/serialization/examples-of-xml-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="2789a-165">[Examples of XML Serialization](../../../docs/standard/serialization/examples-of-xml-serialization.md) </span></span>  
 <span data-ttu-id="2789a-166">[如何：指定 XML 流的替代元素名称](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md) </span><span class="sxs-lookup"><span data-stu-id="2789a-166">[How to: Specify an Alternate Element Name for an XML Stream](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md) </span></span>  
 <span data-ttu-id="2789a-167">[如何：序列化对象](../../../docs/standard/serialization/how-to-serialize-an-object.md) </span><span class="sxs-lookup"><span data-stu-id="2789a-167">[How to: Serialize an Object](../../../docs/standard/serialization/how-to-serialize-an-object.md) </span></span>  
 [<span data-ttu-id="2789a-168">如何：反序列化对象</span><span class="sxs-lookup"><span data-stu-id="2789a-168">How to: Deserialize an Object</span></span>](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
