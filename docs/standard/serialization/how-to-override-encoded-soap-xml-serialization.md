---
title: "如何：重写编码的 SOAP XML 序列化"
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
- overriding XML serialization
- SOAP, overriding encoded XML serialization
ms.assetid: d0791df8-04e3-46b4-a6be-fe0ed09267e8
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 0dea6233f2a13bd3b6c7e33ebf9ee1c96dae7577
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-override-encoded-soap-xml-serialization"></a><span data-ttu-id="83407-102">如何：重写编码的 SOAP XML 序列化</span><span class="sxs-lookup"><span data-stu-id="83407-102">How to: Override Encoded SOAP XML Serialization</span></span>
[<span data-ttu-id="83407-103">代码示例</span><span class="sxs-lookup"><span data-stu-id="83407-103">Code Example</span></span>](#tskhowtooverrideencodedsoapxmlserializationanchor1)  
  
 <span data-ttu-id="83407-104">将对象的 XML 序列化重写为 SOAP 消息的过程类似于重写标准 XML 序列化的过程。</span><span class="sxs-lookup"><span data-stu-id="83407-104">The process for overriding XML serialization of objects as SOAP messages is similar to the process for overriding standard XML serialization.</span></span> <span data-ttu-id="83407-105">有关重写标准 XML 序列化的信息，请参见[如何：指定 XML 流的备用元素名称](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md)。</span><span class="sxs-lookup"><span data-stu-id="83407-105">For information about overriding standard XML serialization, see [How to: Specify an Alternate Element Name for an XML Stream](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md).</span></span>  
  
### <a name="to-override-serialization-of-objects-as-soap-messages"></a><span data-ttu-id="83407-106">将对象的序列化重写为 SOAP 消息</span><span class="sxs-lookup"><span data-stu-id="83407-106">To override serialization of objects as SOAP messages</span></span>  
  
1.  <span data-ttu-id="83407-107">创建 <xref:System.Xml.Serialization.SoapAttributeOverrides> 类的一个实例。</span><span class="sxs-lookup"><span data-stu-id="83407-107">Create an instance of the <xref:System.Xml.Serialization.SoapAttributeOverrides> class.</span></span>  
  
2.  <span data-ttu-id="83407-108">为正在序列化的每个类成员创建 `SoapAttributes`。</span><span class="sxs-lookup"><span data-stu-id="83407-108">Create a `SoapAttributes` for each class member that is being serialized.</span></span>  
  
3.  <span data-ttu-id="83407-109">对正在序列化的成员适当创建影响 XML 序列化的一个或多个特性的实例。</span><span class="sxs-lookup"><span data-stu-id="83407-109">Create an instance of one or more of the attributes that affect XML serialization, as appropriate, to the member being serialized.</span></span> <span data-ttu-id="83407-110">有关更多信息，请参见“用来控制编码的 SOAP 序列化的特性”。</span><span class="sxs-lookup"><span data-stu-id="83407-110">For more information, see "Attributes That Control Encoded SOAP Serialization".</span></span>  
  
4.  <span data-ttu-id="83407-111">将 `SoapAttributes` 的相应属性设置为在步骤 3 中创建的特性。</span><span class="sxs-lookup"><span data-stu-id="83407-111">Set the appropriate property of `SoapAttributes` to the attribute created in step 3.</span></span>  
  
5.  <span data-ttu-id="83407-112">将 `SoapAttributes` 添加到 `SoapAttributeOverrides`。</span><span class="sxs-lookup"><span data-stu-id="83407-112">Add `SoapAttributes` to `SoapAttributeOverrides`.</span></span>  
  
6.  <span data-ttu-id="83407-113">使用 `XmlTypeMapping` 创建 `SoapAttributeOverrides`。</span><span class="sxs-lookup"><span data-stu-id="83407-113">Create an `XmlTypeMapping` using the `SoapAttributeOverrides`.</span></span> <span data-ttu-id="83407-114">使用 `SoapReflectionImporter.ImportTypeMapping` 方法。</span><span class="sxs-lookup"><span data-stu-id="83407-114">Use the `SoapReflectionImporter.ImportTypeMapping` method.</span></span>  
  
7.  <span data-ttu-id="83407-115">使用 `XmlSerializer` 创建 `XmlTypeMapping`。</span><span class="sxs-lookup"><span data-stu-id="83407-115">Create an `XmlSerializer` using `XmlTypeMapping`.</span></span>  
  
8.  <span data-ttu-id="83407-116">序列化或反序列化对象。</span><span class="sxs-lookup"><span data-stu-id="83407-116">Serialize or deserialize the object.</span></span>  
  
## <a name="example"></a><span data-ttu-id="83407-117">示例</span><span class="sxs-lookup"><span data-stu-id="83407-117">Example</span></span>  
 <span data-ttu-id="83407-118">下面的代码示例以两种方式序列化文件：第一种方式，不重写 `XmlSerializer` 类的行为；第二种方式，重写该行为。</span><span class="sxs-lookup"><span data-stu-id="83407-118">The following code example serializes a file in two ways: first, without overriding the `XmlSerializer` class's behavior, and second, by overriding the behavior.</span></span> <span data-ttu-id="83407-119">示例包含带有几个成员的名为 `Group` 的类。</span><span class="sxs-lookup"><span data-stu-id="83407-119">The example contains a class named `Group` with several members.</span></span> <span data-ttu-id="83407-120">已将各个特性（如 `SoapElementAttribute`）应用于类成员。</span><span class="sxs-lookup"><span data-stu-id="83407-120">Various attributes, such as the `SoapElementAttribute`, have been applied to class members.</span></span> <span data-ttu-id="83407-121">当已使用 `SerializeOriginal` 方法序列化该类时，特性会控制 SOAP 消息的内容。</span><span class="sxs-lookup"><span data-stu-id="83407-121">When the class is serialized with the `SerializeOriginal` method, the attributes control the SOAP message content.</span></span> <span data-ttu-id="83407-122">调用 `SerializeOverride` 方法后，`XmlSerializer` 的行为会被重写，方法是创建各个特性并根据需要将 `SoapAttributes` 的属性设置为这些特性。</span><span class="sxs-lookup"><span data-stu-id="83407-122">When the `SerializeOverride` method is called, the behavior of the `XmlSerializer` is overridden by creating various attributes and setting the properties of a `SoapAttributes` to those attributes (as appropriate).</span></span>  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Serialization;  
using System.Xml.Schema;  
  
public class Group  
{  
    [SoapAttribute (Namespace = "http://www.cpandl.com")]  
    public string GroupName;  
  
    [SoapAttribute(DataType = "base64Binary")]  
    public Byte [] GroupNumber;  
  
    [SoapAttribute(DataType = "date", AttributeName = "CreationDate")]  
    public DateTime Today;  
    [SoapElement(DataType = "nonNegativeInteger", ElementName = "PosInt")]  
    public string PostitiveInt;  
    // This is ignored when serialized unless it is overridden.  
    [SoapIgnore]   
    public bool IgnoreThis;  
  
    public GroupType Grouptype;  
  
    [SoapInclude(typeof(Car))]  
    public Vehicle myCar(string licNumber)  
    {  
        Vehicle v;  
        if(licNumber == "")  
            {  
                v = new Car();  
            v.licenseNumber = "!!!!!!";  
        }  
        else  
        {  
            v = new Car();  
            v.licenseNumber = licNumber;  
        }  
        return v;  
    }  
}  
  
public abstract class Vehicle  
{  
    public string licenseNumber;  
    public DateTime makeDate;  
}  
  
public class Car: Vehicle  
{  
}  
  
public enum GroupType  
{  
    // These enums can be overridden.  
    small,  
    large  
}  
  
public class Run  
{  
    public static void Main()  
    {  
        Run test = new Run();  
        test.SerializeOriginal("SoapOriginal.xml");  
        test.SerializeOverride("SoapOverrides.xml");  
        test.DeserializeOriginal("SoapOriginal.xml");  
        test.DeserializeOverride("SoapOverrides.xml");  
  
    }  
    public void SerializeOriginal(string filename)  
    {  
        // Creates an instance of the XmlSerializer class.  
        XmlTypeMapping myMapping =   
        (new SoapReflectionImporter().ImportTypeMapping(  
        typeof(Group)));  
        XmlSerializer mySerializer =    
        new XmlSerializer(myMapping);  
  
        // Writing the file requires a TextWriter.  
        TextWriter writer = new StreamWriter(filename);  
  
        // Creates an instance of the class that will be serialized.  
        Group myGroup = new Group();  
  
        // Sets the object properties.  
        myGroup.GroupName = ".NET";  
  
        Byte [] hexByte = new Byte[2]{Convert.ToByte(100),  
        Convert.ToByte(50)};  
        myGroup.GroupNumber = hexByte;  
  
        DateTime myDate = new DateTime(2002,5,2);  
        myGroup.Today = myDate;  
  
        myGroup.PostitiveInt= "10000";  
        myGroup.IgnoreThis=true;  
        myGroup.Grouptype= GroupType.small;  
        Car thisCar =(Car)  myGroup.myCar("1234566");  
  
        // Prints the license number just to prove the car was created.  
        Console.WriteLine("License#: " + thisCar.licenseNumber + "\n");  
  
        // Serializes the class and closes the TextWriter.  
        mySerializer.Serialize(writer, myGroup);  
        writer.Close();  
    }  
  
    public void SerializeOverride(string filename)  
    {  
        // Creates an instance of the XmlSerializer class  
        // that overrides the serialization.  
        XmlSerializer overRideSerializer = CreateOverrideSerializer();  
  
        // Writing the file requires a TextWriter.  
        TextWriter writer = new StreamWriter(filename);  
  
        // Creates an instance of the class that will be serialized.  
        Group myGroup = new Group();  
  
        // Sets the object properties.  
        myGroup.GroupName = ".NET";  
  
        Byte [] hexByte = new Byte[2]{Convert.ToByte(100),  
        Convert.ToByte(50)};  
        myGroup.GroupNumber = hexByte;  
  
        DateTime myDate = new DateTime(2002,5,2);  
        myGroup.Today = myDate;  
  
        myGroup.PostitiveInt= "10000";  
        myGroup.IgnoreThis=true;  
        myGroup.Grouptype= GroupType.small;  
        Car thisCar =(Car)  myGroup.myCar("1234566");  
  
        // Serializes the class and closes the TextWriter.  
        overRideSerializer.Serialize(writer, myGroup);  
         writer.Close();  
    }  
  
    public void DeserializeOriginal(string filename)  
    {  
        // Creates an instance of the XmlSerializer class.  
        XmlTypeMapping myMapping =   
        (new SoapReflectionImporter().ImportTypeMapping(  
        typeof(Group)));  
        XmlSerializer mySerializer =    
        new XmlSerializer(myMapping);  
  
        TextReader reader = new StreamReader(filename);  
  
        // Deserializes and casts the object.  
        Group myGroup;   
        myGroup = (Group) mySerializer.Deserialize(reader);  
  
        Console.WriteLine(myGroup.GroupName);  
        Console.WriteLine(myGroup.GroupNumber[0]);  
        Console.WriteLine(myGroup.GroupNumber[1]);  
        Console.WriteLine(myGroup.Today);  
        Console.WriteLine(myGroup.PostitiveInt);  
        Console.WriteLine(myGroup.IgnoreThis);  
        Console.WriteLine();  
    }  
  
    public void DeserializeOverride(string filename)  
    {  
        // Creates an instance of the XmlSerializer class.  
        XmlSerializer overRideSerializer = CreateOverrideSerializer();  
        // Reading the file requires a TextReader.  
        TextReader reader = new StreamReader(filename);  
  
        // Deserializes and casts the object.  
        Group myGroup;   
        myGroup = (Group) overRideSerializer.Deserialize(reader);  
  
        Console.WriteLine(myGroup.GroupName);  
        Console.WriteLine(myGroup.GroupNumber[0]);  
        Console.WriteLine(myGroup.GroupNumber[1]);  
        Console.WriteLine(myGroup.Today);  
        Console.WriteLine(myGroup.PostitiveInt);  
        Console.WriteLine(myGroup.IgnoreThis);  
    }  
  
    private XmlSerializer CreateOverrideSerializer()  
    {  
        SoapAttributeOverrides mySoapAttributeOverrides =   
        new SoapAttributeOverrides();  
        SoapAttributes soapAtts = new SoapAttributes();  
  
        SoapElementAttribute mySoapElement = new SoapElementAttribute();  
        mySoapElement.ElementName = "xxxx";  
        soapAtts.SoapElement = mySoapElement;  
        mySoapAttributeOverrides.Add(typeof(Group), "PostitiveInt",   
        soapAtts);  
  
        // Overrides the IgnoreThis property.  
        SoapIgnoreAttribute myIgnore = new SoapIgnoreAttribute();  
        soapAtts = new SoapAttributes();  
        soapAtts.SoapIgnore = false;        
        mySoapAttributeOverrides.Add(typeof(Group), "IgnoreThis",   
        soapAtts);  
  
        // Overrides the GroupType enumeration.  
        soapAtts = new SoapAttributes();  
        SoapEnumAttribute xSoapEnum = new SoapEnumAttribute();  
        xSoapEnum.Name = "Over1000";  
        soapAtts.SoapEnum = xSoapEnum;  
  
        // Adds the SoapAttributes to the   
        // mySoapAttributeOverridesrides.  
        mySoapAttributeOverrides.Add(typeof(GroupType), "large",   
        soapAtts);  
  
        // Creates a second enumeration and adds it.  
        soapAtts = new SoapAttributes();  
        xSoapEnum = new SoapEnumAttribute();  
        xSoapEnum.Name = "ZeroTo1000";  
        soapAtts.SoapEnum = xSoapEnum;  
        mySoapAttributeOverrides.Add(typeof(GroupType), "small",   
        soapAtts);  
  
        // Overrides the Group type.  
        soapAtts = new SoapAttributes();  
        SoapTypeAttribute soapType = new SoapTypeAttribute();  
        soapType.TypeName = "Team";  
        soapAtts.SoapType = soapType;  
        mySoapAttributeOverrides.Add(typeof(Group),soapAtts);  
  
        // Creates an XmlTypeMapping that is used to create an instance   
        // of the XmlSerializer class. Then returns the XmlSerializer.  
        XmlTypeMapping myMapping = (new SoapReflectionImporter(  
        mySoapAttributeOverrides)).ImportTypeMapping(typeof(Group));  
  
        XmlSerializer ser = new XmlSerializer(myMapping);  
        return ser;  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="83407-123">另请参阅</span><span class="sxs-lookup"><span data-stu-id="83407-123">See Also</span></span>  
 <span data-ttu-id="83407-124">[XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="83407-124">[XML and SOAP Serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md) </span></span>  
 <span data-ttu-id="83407-125">[控制编码的 SOAP 序列化的特性](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="83407-125">[Attributes That Control Encoded SOAP Serialization](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md) </span></span>  
 <span data-ttu-id="83407-126">[使用 XML Web 服务进行 XML 序列化](../../../docs/standard/serialization/xml-serialization-with-xml-web-services.md) </span><span class="sxs-lookup"><span data-stu-id="83407-126">[XML Serialization with XML Web Services](../../../docs/standard/serialization/xml-serialization-with-xml-web-services.md) </span></span>  
 <span data-ttu-id="83407-127">[如何：序列化对象](../../../docs/standard/serialization/how-to-serialize-an-object.md) </span><span class="sxs-lookup"><span data-stu-id="83407-127">[How to: Serialize an Object](../../../docs/standard/serialization/how-to-serialize-an-object.md) </span></span>  
 <span data-ttu-id="83407-128">[如何：反序列化对象](../../../docs/standard/serialization/how-to-deserialize-an-object.md) </span><span class="sxs-lookup"><span data-stu-id="83407-128">[How to: Deserialize an Object](../../../docs/standard/serialization/how-to-deserialize-an-object.md) </span></span>  
 [<span data-ttu-id="83407-129">如何：将对象序列化为 SOAP 编码的 XML 流</span><span class="sxs-lookup"><span data-stu-id="83407-129">How to: Serialize an Object as a SOAP-Encoded XML Stream</span></span>](../../../docs/standard/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
