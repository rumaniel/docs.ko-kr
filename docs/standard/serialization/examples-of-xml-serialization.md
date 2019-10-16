---
title: XML Serialization 예제
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, examples
- arrays, serializing
- ICollection interface, serializing
- XmlSerializer class, serializing
- serialization, examples
- DataSet class, serializing
- XML Schema, serializing
ms.assetid: eec46337-9696-435b-a375-dc5effae6992
ms.openlocfilehash: f92f3c0f8d7b849772f96415d03b0924b1e341a3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61922527"
---
# <a name="examples-of-xml-serialization"></a>XML Serialization 예제

XML serialization은 간단한 것부터 복잡한 것까지 여러 형태를 가집니다. 예를 들어 [XML Serialization 소개](../../../docs/standard/serialization/introducing-xml-serialization.md)에서처럼 공용 필드와 속성으로 간단하게 구성된 클래스를 직렬화할 수 있습니다. 다음 코드 예제에서는 XML serialization을 사용하여 특정 XML 스키마(XSD) 문서를 따르는 XML 스트림을 생성하는 방법을 포함한 여러 가지 고급 시나리오를 보여 줍니다.

## <a name="serializing-a-dataset"></a>데이터 세트 serialize

공용 클래스의 인스턴스를 serialize하는 것 이외에 다음 코드 예제에서 볼 수 있는 것처럼 <xref:System.Data.DataSet>의 인스턴스도 serialize할 수 있습니다.

```vb
Private Sub SerializeDataSet(filename As String)
    Dim ser As XmlSerializer = new XmlSerializer(GetType(DataSet))
    ' Creates a DataSet; adds a table, column, and ten rows.
    Dim ds As DataSet = new DataSet("myDataSet")
    Dim t As DataTable = new DataTable("table1")
    Dim c As DataColumn = new DataColumn("thing")
    t.Columns.Add(c)
    ds.Tables.Add(t)
    Dim r As DataRow
    Dim i As Integer
    for i = 0 to 10
        r = t.NewRow()
        r(0) = "Thing " &  i
        t.Rows.Add(r)
    Next
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, ds)
    writer.Close()
End Sub
```

```csharp
private void SerializeDataSet(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(DataSet));

    // Creates a DataSet; adds a table, column, and ten rows.
    DataSet ds = new DataSet("myDataSet");
    DataTable t = new DataTable("table1");
    DataColumn c = new DataColumn("thing");
    t.Columns.Add(c);
    ds.Tables.Add(t);
    DataRow r;
    for(int i = 0; i<10;i++){
        r = t.NewRow();
        r[0] = "Thing " + i;
        t.Rows.Add(r);
    }
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, ds);
    writer.Close();
}
```

## <a name="serializing-an-xmlelement-and-xmlnode"></a>XmlElement 및 XmlNode serialize

인스턴스를 serialize 할 수도 있습니다는 <xref:System.Xml.XmlElement> 또는 <xref:System.Xml.XmlNode> 클래스에 다음 코드 예제에 표시 된 대로 합니다.

```vb
private Sub SerializeElement(filename As String)
    Dim ser As XmlSerializer = new XmlSerializer(GetType(XmlElement))
    Dim myElement As XmlElement = _
    new XmlDocument().CreateElement("MyElement", "ns")
    myElement.InnerText = "Hello World"
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, myElement)
    writer.Close()
End Sub

Private Sub SerializeNode(filename As String)
    Dim ser As XmlSerializer = _
    new XmlSerializer(GetType(XmlNode))
    Dim myNode As XmlNode = new XmlDocument(). _
    CreateNode(XmlNodeType.Element, "MyNode", "ns")
    myNode.InnerText = "Hello Node"
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, myNode)
    writer.Close()
End Sub
```

```csharp
private void SerializeElement(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(XmlElement));
    XmlElement myElement=
    new XmlDocument().CreateElement("MyElement", "ns");
    myElement.InnerText = "Hello World";
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, myElement);
    writer.Close();
}

private void SerializeNode(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(XmlNode));
    XmlNode myNode= new XmlDocument().
    CreateNode(XmlNodeType.Element, "MyNode", "ns");
    myNode.InnerText = "Hello Node";
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, myNode);
    writer.Close();
}
```

## <a name="serializing-a-class-that-contains-a-field-returning-a-complex-object"></a>복잡한 개체를 반환하는 필드가 포함된 클래스 serialize

속성 또는 필드가 복잡한 개체(예: 배열 또는 클래스 인스턴스)를 반환하는 경우 <xref:System.Xml.Serialization.XmlSerializer>는 그 개체를 주 XML 문서 내의 중첩된 요소로 변환합니다. 예를 들어, 다음 코드 예제의 첫째 클래스는 둘째 클래스의 인스턴스를 반환합니다.

```vb
Public Class PurchaseOrder
    Public MyAddress As Address
End Class

Public Class Address
    Public FirstName As String
End Class
```

```csharp
public class PurchaseOrder
{
    public Address MyAddress;
}
public class Address
{
    public string FirstName;
}
```

serialize된 XML 출력은 다음과 같을 수 있습니다.

```xml
<PurchaseOrder>
    <MyAddress>
        <FirstName>George</FirstName>
    </MyAddress>
</PurchaseOrder>
```

## <a name="serializing-an-array-of-objects"></a>개체 배열 serialize

다음 코드 예제에서처럼 개체 배열을 반환하는 필드를 serialize할 수도 있습니다.

```vb
Public Class PurchaseOrder
    public ItemsOrders () As Item
End Class

Public Class Item
    Public ItemID As String
    Public ItemPrice As decimal
End Class
```

```csharp
public class PurchaseOrder
{
    public Item [] ItemsOrders;
}

public class Item
{
    public string ItemID;
    public decimal ItemPrice;
}
```

두 항목이 순서 지정된 경우 serialize된 클래스 인스턴스는 다음과 같을 수 있습니다.

```xml
<PurchaseOrder xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <ItemsOrders>
        <Item>
            <ItemID>aaa111</ItemID>
            <ItemPrice>34.22</ItemPrice>
        <Item>
        <Item>
            <ItemID>bbb222</ItemID>
            <ItemPrice>2.89</ItemPrice>
        <Item>
    </ItemsOrders>
</PurchaseOrder>
```

## <a name="serializing-a-class-that-implements-the-icollection-interface"></a>ICollection 인터페이스를 구현하는 클래스 serialize

<xref:System.Collections.ICollection> 인터페이스를 구현하여 컬렉션 클래스를 직접 만들고 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 이러한 클래스의 인스턴스를 serialize할 수 있습니다. 클래스가 <xref:System.Collections.ICollection> 인터페이스를 구현할 때 클래스에 의해 포함된 컬렉션만 serialize됩니다. 클래스에 추가된 모든 공용 속성이나 필드는 serialize되지 않습니다. 클래스에는 직렬화될 **Add** 메서드 및 **Item** 속성(C# 인덱서)이 포함되어야 합니다.

```vb
Imports System
Imports System.IO
Imports System.Collections
Imports System.Xml.Serialization

Public Class Test
    Shared Sub Main()
        Dim t As Test= new Test()
        t.SerializeCollection("coll.xml")
    End Sub

    Private Sub SerializeCollection(filename As String)
        Dim Emps As Employees  = new Employees()
        ' Note that only the collection is serialized -- not the
        ' CollectionName or any other public property of the class.
        Emps.CollectionName = "Employees"
        Dim John100 As Employee = new Employee("John", "100xxx")
        Emps.Add(John100)
        Dim x As XmlSerializer = new XmlSerializer(GetType(Employees))
        Dim writer As TextWriter = new StreamWriter(filename)
        x.Serialize(writer, Emps)
        writer.Close()
    End Sub
End Class

Public Class Employees
    Implements ICollection
    Public CollectionName As String
    Private empArray As ArrayList = new ArrayList()

    Public ReadOnly Default Overloads _
    Property Item(index As Integer) As Employee
        get
        return CType (empArray(index), Employee)
        End Get
    End Property

    Public Sub CopyTo(a As Array, index As Integer) _
    Implements ICollection.CopyTo
        empArray.CopyTo(a, index)
    End Sub

    Public ReadOnly Property Count () As integer Implements _
    ICollection.Count
        get
            Count = empArray.Count
        End Get

    End Property

    Public ReadOnly Property SyncRoot ()As Object _
    Implements ICollection.SyncRoot
        get
        return me
        End Get
    End Property

    Public ReadOnly Property IsSynchronized () As Boolean _
    Implements ICollection.IsSynchronized
        get
        return false
        End Get
    End Property

    Public Function GetEnumerator() As IEnumerator _
    Implements IEnumerable.GetEnumerator

        return empArray.GetEnumerator()
    End Function

    Public Function Add(newEmployee As Employee) As Integer
        empArray.Add(newEmployee)
        return empArray.Count
    End Function
End Class

Public Class Employee
    Public EmpName As String
    Public EmpID As String

    Public Sub New ()
    End Sub

    Public Sub New (newName As String , newID As String )
        EmpName = newName
        EmpID = newID
    End Sub
End Class
```

```csharp
using System;
using System.IO;
using System.Collections;
using System.Xml.Serialization;

public class Test {
    static void Main(){
        Test t = new Test();
        t.SerializeCollection("coll.xml");
    }

    private void SerializeCollection(string filename){
        Employees Emps = new Employees();
        // Note that only the collection is serialized -- not the
        // CollectionName or any other public property of the class.
        Emps.CollectionName = "Employees";
        Employee John100 = new Employee("John", "100xxx");
        Emps.Add(John100);
        XmlSerializer x = new XmlSerializer(typeof(Employees));
        TextWriter writer = new StreamWriter(filename);
        x.Serialize(writer, Emps);
    }
}
public class Employees:ICollection {
    public string CollectionName;
    private ArrayList empArray = new ArrayList();

    public Employee this[int index]{
        get{return (Employee) empArray[index];}
    }

    public void CopyTo(Array a, int index){
        empArray.CopyTo(a, index);
    }
    public int Count{
        get{return empArray.Count;}
    }
    public object SyncRoot{
        get{return this;}
    }
    public bool IsSynchronized{
        get{return false;}
    }
    public IEnumerator GetEnumerator(){
        return empArray.GetEnumerator();
    }

    public void Add(Employee newEmployee){
        empArray.Add(newEmployee);
    }
}

public class Employee {
    public string EmpName;
    public string EmpID;
    public Employee(){}
    public Employee(string empName, string empID){
        EmpName = empName;
        EmpID = empID;
    }
}
```

## <a name="purchase-order-example"></a>구매 주문 예제

다음 예제 코드를 잘라내어 파일 이름 확장명이 .cs 또는 .vb 텍스트 파일에 붙여넣을 수 있습니다. C# 또는 Visual Basic 컴파일러를 사용하여 파일을 컴파일합니다. 그런 다음 실행 파일의 이름을 입력하여 실행합니다.

이 예제에서는 간단한 시나리오를 사용하여 개체 인스턴스를 만들고 <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A> 메서드를 사용하여 파일 스트림으로 serialize하는 방법을 보여 줍니다. XML 스트림은 파일에 저장되고 <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> 메서드를 사용하여 동일한 파일을 읽어서 원본 개체의 복사본으로 재생성합니다.

이 예제에서는 `PurchaseOrder`라는 클래스를 serialize한 다음 deserialize합니다. `Address`라는 public 필드를 `ShipTo`로 설정해야 하기 때문에 `Address`라는 두 번째 클래스도 포함해야 합니다. 마찬가지로 `OrderedItem` 개체의 배열을 `OrderedItem` 필드로 설정해야 하기 때문에 `OrderedItems` 클래스도 포함했습니다. 마지막으로 `Test`라는 클래스에는 클래스를 serialize하고 deserialize하는 코드가 포함됩니다.

`CreatePO` 메서드는 `PurchaseOrder`, `Address` 및 `OrderedItem` 클래스 개체를 만들고 public 필드 값을 설정합니다. 메서드는 <xref:System.Xml.Serialization.XmlSerializer>를 serialize하고 deserialize하는 데 사용되는 `PurchaseOrder` 클래스의 인스턴스도 생성합니다. 코드는 serialize될 클래스 형식을 생성자에 전달합니다. 또한 코드는 XML 스트림을 XML 문서에 쓰는 데 사용되는 `FileStream`도 만듭니다.

`ReadPo` 메서드는 조금 더 간단합니다. deserialize할 개체를 만들고 그 값을 읽습니다. 와 마찬가지로 합니다 `CreatePo` 메서드를 먼저 구성 해야는 <xref:System.Xml.Serialization.XmlSerializer>를 생성자에 deserialize 할 클래스의 형식을 전달 합니다. 또한 XML 문서를 읽기 위해 <xref:System.IO.FileStream>이 필요합니다. 개체를 deserialize하기 위해 <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A>을 인수로 사용하여 <xref:System.IO.FileStream> 메서드를 호출합니다. deserialize된 개체는 `PurchaseOrder` 형식의 개체 변수로 캐스팅되어야 합니다. 그런 다음 코드는 deserialize된 `PurchaseOrder`의 값을 읽습니다. 작성된 PO.xml 파일을 읽어 실제 XML 출력을 볼 수 있습니다.

```vb
Imports System
Imports System.Xml
Imports System.Xml.Serialization
Imports System.IO
Imports Microsoft.VisualBasic

' The XmlRoot attribute allows you to set an alternate name
' (PurchaseOrder) for the XML element and its namespace. By
' default, the XmlSerializer uses the class name. The attribute
' also allows you to set the XML namespace for the element. Lastly,
' the attribute sets the IsNullable property, which specifies whether
' the xsi:null attribute appears if the class instance is set to
' a null reference.
<XmlRoot("PurchaseOrder", _
 Namespace := "http://www.cpandl.com", IsNullable := False)> _
Public Class PurchaseOrder
    Public ShipTo As Address
    Public OrderDate As String
    ' The XmlArrayAttribute changes the XML element name
    ' from the default of "OrderedItems" to "Items".
    <XmlArray("Items")> _
    Public OrderedItems() As OrderedItem
    Public SubTotal As Decimal
    Public ShipCost As Decimal
    Public TotalCost As Decimal
End Class

Public Class Address
    ' The XmlAttribute attribute instructs the XmlSerializer to serialize the
    ' Name field as an XML attribute instead of an XML element (XML element is
    ' the default behavior).
    <XmlAttribute()> _
    Public Name As String
    Public Line1 As String

    ' Setting the IsNullable property to false instructs the
    ' XmlSerializer that the XML attribute will not appear if
    ' the City field is set to a null reference.
    <XmlElement(IsNullable := False)> _
    Public City As String
    Public State As String
    Public Zip As String
End Class

Public Class OrderedItem
    Public ItemName As String
    Public Description As String
    Public UnitPrice As Decimal
    Public Quantity As Integer
    Public LineTotal As Decimal

    ' Calculate is a custom method that calculates the price per item
    ' and stores the value in a field.
    Public Sub Calculate()
    LineTotal = UnitPrice * Quantity
    End Sub
End Class

Public Class Test
        Public Shared Sub Main()
    ' Read and write purchase orders.
    Dim t As New Test()
    t.CreatePO("po.xml")
    t.ReadPO("po.xml")
    End Sub

    Private Sub CreatePO(filename As String)
        ' Creates an instance of the XmlSerializer class;
        ' specifies the type of object to serialize.
        Dim serializer As New XmlSerializer(GetType(PurchaseOrder))
        Dim writer As New StreamWriter(filename)
        Dim po As New PurchaseOrder()

        ' Creates an address to ship and bill to.
        Dim billAddress As New Address()
        billAddress.Name = "Teresa Atkinson"
        billAddress.Line1 = "1 Main St."
        billAddress.City = "AnyTown"
        billAddress.State = "WA"
        billAddress.Zip = "00000"
        ' Set ShipTo and BillTo to the same addressee.
        po.ShipTo = billAddress
        po.OrderDate = System.DateTime.Now.ToLongDateString()

        ' Creates an OrderedItem.
        Dim i1 As New OrderedItem()
        i1.ItemName = "Widget S"
        i1.Description = "Small widget"
        i1.UnitPrice = CDec(5.23)
        i1.Quantity = 3
        i1.Calculate()

        ' Inserts the item into the array.
        Dim items(0) As OrderedItem
        items(0) = i1
        po.OrderedItems = items
        ' Calculates the total cost.
        Dim subTotal As New Decimal()
        Dim oi As OrderedItem
        For Each oi In  items
            subTotal += oi.LineTotal
        Next oi
        po.SubTotal = subTotal
        po.ShipCost = CDec(12.51)
        po.TotalCost = po.SubTotal + po.ShipCost
        ' Serializes the purchase order, and close the TextWriter.
        serializer.Serialize(writer, po)
        writer.Close()
    End Sub

    Protected Sub ReadPO(filename As String)
        ' Creates an instance of the XmlSerializer class;
        ' specifies the type of object to be deserialized.
        Dim serializer As New XmlSerializer(GetType(PurchaseOrder))
        ' If the XML document has been altered with unknown
        ' nodes or attributes, handles them with the
        ' UnknownNode and UnknownAttribute events.
        AddHandler serializer.UnknownNode, AddressOf serializer_UnknownNode
        AddHandler serializer.UnknownAttribute, AddressOf _
        serializer_UnknownAttribute

        ' A FileStream is needed to read the XML document.
        Dim fs As New FileStream(filename, FileMode.Open)
        ' Declare an object variable of the type to be deserialized.
        Dim po As PurchaseOrder
        ' Uses the Deserialize method to restore the object's state
        ' with data from the XML document.
        po = CType(serializer.Deserialize(fs), PurchaseOrder)
        ' Reads the order date.
        Console.WriteLine(("OrderDate: " & po.OrderDate))

        ' Reads the shipping address.
        Dim shipTo As Address = po.ShipTo
        ReadAddress(shipTo, "Ship To:")
        ' Reads the list of ordered items.
        Dim items As OrderedItem() = po.OrderedItems
        Console.WriteLine("Items to be shipped:")
        Dim oi As OrderedItem
        For Each oi In items
            Console.WriteLine((ControlChars.Tab & oi.ItemName & _
            ControlChars.Tab & _
                oi.Description & ControlChars.Tab & oi.UnitPrice & _
                ControlChars.Tab & _
                oi.Quantity & ControlChars.Tab & oi.LineTotal))
        Next oi
        ' Reads the subtotal, shipping cost, and total cost.
        Console.WriteLine((ControlChars.Cr & New String _
        (ControlChars.Tab, 5) & _
        " Subtotal" & ControlChars.Tab & po.SubTotal & ControlChars.Cr & _
        New String(ControlChars.Tab, 5) & " Shipping" & ControlChars.Tab & _
        po.ShipCost & ControlChars.Cr &  New String(ControlChars.Tab, 5) & _
        " Total" & New String(ControlChars.Tab, 2) & po.TotalCost))
    End Sub

    Protected Sub ReadAddress(a As Address, label As String)
        ' Reads the fields of the Address.
        Console.WriteLine(label)
        Console.Write((ControlChars.Tab & a.Name & ControlChars.Cr & _
        ControlChars.Tab & a.Line1 & ControlChars.Cr & ControlChars.Tab & _
        a.City & ControlChars.Tab & a.State & ControlChars.Cr & _
        ControlChars.Tab & a.Zip & ControlChars.Cr))
    End Sub

    Protected Sub serializer_UnknownNode(sender As Object, e As _
    XmlNodeEventArgs)
        Console.WriteLine(("Unknown Node:" & e.Name & _
        ControlChars.Tab & e.Text))
    End Sub

    Protected Sub serializer_UnknownAttribute(sender As Object, _
    e As XmlAttributeEventArgs)
        Dim attr As System.Xml.XmlAttribute = e.Attr
        Console.WriteLine(("Unknown attribute " & attr.Name & "='" & _
        attr.Value & "'"))
    End Sub 'serializer_UnknownAttribute
End Class 'Test
```

```csharp
using System;
using System.Xml;
using System.Xml.Serialization;
using System.IO;

// The XmlRoot attribute allows you to set an alternate name
// (PurchaseOrder) for the XML element and its namespace. By
// default, the XmlSerializer uses the class name. The attribute
// also allows you to set the XML namespace for the element. Lastly,
// the attribute sets the IsNullable property, which specifies whether
// the xsi:null attribute appears if the class instance is set to
// a null reference.
[XmlRoot("PurchaseOrder", Namespace="http://www.cpandl.com",
IsNullable = false)]
public class PurchaseOrder
{
    public Address ShipTo;
    public string OrderDate;
    // The XmlArray attribute changes the XML element name
    // from the default of "OrderedItems" to "Items".
    [XmlArray("Items")]
    public OrderedItem[] OrderedItems;
    public decimal SubTotal;
    public decimal ShipCost;
    public decimal TotalCost;
}

public class Address
{
    // The XmlAttribute attribute instructs the XmlSerializer to serialize the
    // Name field as an XML attribute instead of an XML element (XML element is
    // the default behavior).
    [XmlAttribute]
    public string Name;
    public string Line1;

    // Setting the IsNullable property to false instructs the
    // XmlSerializer that the XML attribute will not appear if
    // the City field is set to a null reference.
    [XmlElement(IsNullable = false)]
    public string City;
    public string State;
    public string Zip;
}

public class OrderedItem
{
    public string ItemName;
    public string Description;
    public decimal UnitPrice;
    public int Quantity;
    public decimal LineTotal;

    // Calculate is a custom method that calculates the price per item
    // and stores the value in a field.
    public void Calculate()
    {
        LineTotal = UnitPrice * Quantity;
    }
}

public class Test
{
    public static void Main()
    {
        // Read and write purchase orders.
        Test t = new Test();
        t.CreatePO("po.xml");
        t.ReadPO("po.xml");
    }

    private void CreatePO(string filename)
    {
        // Creates an instance of the XmlSerializer class;
        // specifies the type of object to serialize.
        XmlSerializer serializer =
        new XmlSerializer(typeof(PurchaseOrder));
        TextWriter writer = new StreamWriter(filename);
        PurchaseOrder po=new PurchaseOrder();

        // Creates an address to ship and bill to.
        Address billAddress = new Address();
        billAddress.Name = "Teresa Atkinson";
        billAddress.Line1 = "1 Main St.";
        billAddress.City = "AnyTown";
        billAddress.State = "WA";
        billAddress.Zip = "00000";
        // Sets ShipTo and BillTo to the same addressee.
        po.ShipTo = billAddress;
        po.OrderDate = System.DateTime.Now.ToLongDateString();

        // Creates an OrderedItem.
        OrderedItem i1 = new OrderedItem();
        i1.ItemName = "Widget S";
        i1.Description = "Small widget";
        i1.UnitPrice = (decimal) 5.23;
        i1.Quantity = 3;
        i1.Calculate();

        // Inserts the item into the array.
        OrderedItem [] items = {i1};
        po.OrderedItems = items;
        // Calculate the total cost.
        decimal subTotal = new decimal();
        foreach(OrderedItem oi in items)
        {
            subTotal += oi.LineTotal;
        }
        po.SubTotal = subTotal;
        po.ShipCost = (decimal) 12.51;
        po.TotalCost = po.SubTotal + po.ShipCost;
        // Serializes the purchase order, and closes the TextWriter.
        serializer.Serialize(writer, po);
        writer.Close();
    }

    protected void ReadPO(string filename)
    {
        // Creates an instance of the XmlSerializer class;
        // specifies the type of object to be deserialized.
        XmlSerializer serializer = new XmlSerializer(typeof(PurchaseOrder));
        // If the XML document has been altered with unknown
        // nodes or attributes, handles them with the
        // UnknownNode and UnknownAttribute events.
        serializer.UnknownNode+= new
        XmlNodeEventHandler(serializer_UnknownNode);
        serializer.UnknownAttribute+= new
        XmlAttributeEventHandler(serializer_UnknownAttribute);

        // A FileStream is needed to read the XML document.
        FileStream fs = new FileStream(filename, FileMode.Open);
        // Declares an object variable of the type to be deserialized.
        PurchaseOrder po;
        // Uses the Deserialize method to restore the object's state
        // with data from the XML document. */
        po = (PurchaseOrder) serializer.Deserialize(fs);
        // Reads the order date.
        Console.WriteLine ("OrderDate: " + po.OrderDate);

        // Reads the shipping address.
        Address shipTo = po.ShipTo;
        ReadAddress(shipTo, "Ship To:");
        // Reads the list of ordered items.
        OrderedItem [] items = po.OrderedItems;
        Console.WriteLine("Items to be shipped:");
        foreach(OrderedItem oi in items)
        {
            Console.WriteLine("\t"+
            oi.ItemName + "\t" +
            oi.Description + "\t" +
            oi.UnitPrice + "\t" +
            oi.Quantity + "\t" +
            oi.LineTotal);
        }
        // Reads the subtotal, shipping cost, and total cost.
        Console.WriteLine(
        "\n\t\t\t\t\t Subtotal\t" + po.SubTotal +
        "\n\t\t\t\t\t Shipping\t" + po.ShipCost +
        "\n\t\t\t\t\t Total\t\t" + po.TotalCost
        );
    }

    protected void ReadAddress(Address a, string label)
    {
        // Reads the fields of the Address.
        Console.WriteLine(label);
        Console.Write("\t"+
        a.Name +"\n\t" +
        a.Line1 +"\n\t" +
        a.City +"\t" +
        a.State +"\n\t" +
        a.Zip +"\n");
    }

    protected void serializer_UnknownNode
    (object sender, XmlNodeEventArgs e)
    {
        Console.WriteLine("Unknown Node:" +   e.Name + "\t" + e.Text);
    }

    protected void serializer_UnknownAttribute
    (object sender, XmlAttributeEventArgs e)
    {
        System.Xml.XmlAttribute attr = e.Attr;
        Console.WriteLine("Unknown attribute " +
        attr.Name + "='" + attr.Value + "'");
    }
}
```

XML 출력은 다음과 같을 수 있습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<PurchaseOrder xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://www.cpandl.com">
    <ShipTo Name="Teresa Atkinson">
        <Line1>1 Main St.</Line1>
        <City>AnyTown</City>
        <State>WA</State>
        <Zip>00000</Zip>
    </ShipTo>
    <OrderDate>Wednesday, June 27, 2001</OrderDate>
    <Items>
        <OrderedItem>
            <ItemName>Widget S</ItemName>
            <Description>Small widget</Description>
            <UnitPrice>5.23</UnitPrice>
            <Quantity>3</Quantity>
            <LineTotal>15.69</LineTotal>
        </OrderedItem>
    </Items>
    <SubTotal>15.69</SubTotal>
    <ShipCost>12.51</ShipCost>
    <TotalCost>28.2</TotalCost>
</PurchaseOrder>
```

## <a name="see-also"></a>참고자료

- [XML serialization 소개](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [특성을 사용하여 XML serialization 제어](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md)
- [XML serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md)
- [XmlSerializer 클래스](xref:System.Xml.Serialization.XmlSerializer)
- [방법: 개체 serialize](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [방법: 개체 deserialize](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
