---
title: '방법: DataContractJsonSerializer 사용'
ms.date: 03/25/2019
ms.assetid: 88abc1fb-8196-4ee3-a23b-c6934144d1dd
ms.openlocfilehash: 5e521621dd3ec8e82a860590e66c1c4da95fd3b8
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180216"
---
# <a name="how-to-use-datacontractjsonserializer"></a>방법: DataContractJsonSerializer 사용
JSON(JavaScript Object Notation)은 클라이언트 브라우저 및 AJAX 사용 웹 서비스 간에 소량의 데이터를 신속하게 교환할 수 있는 효율적인 데이터 인코딩 형식입니다.  
  
 이 문서에서는 .NET 형식 개체를 JSON으로 인코딩된 데이터로 serialize 한 다음 JSON 형식의 데이터를 다시 .NET 형식의 인스턴스로 deserialize 하는 방법을 보여 줍니다. 이 예제에서는 데이터 계약을 사용 하 여 사용자 정의 @no__t 0 형식의 serialization 및 deserialization을 보여 주고 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>을 사용 합니다.  
  
 일반적으로 JSON serialization 및 deserialization은 AJAX 사용 끝점을 통해 노출 되는 서비스 작업의 데이터 계약 형식을 사용할 때 WCF (Windows Communication Foundation)에 의해 자동으로 처리 됩니다. 그러나 경우에 따라 JSON 데이터를 직접 사용 해야 할 수도 있습니다.

> [!NOTE]
> 이 문서는 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>입니다. JSON 직렬화 및 역직렬화를 포함 하는 대부분의 시나리오에서는 system.xml [네임 스페이스](../../../standard/serialization/system-text-json-overview.md)의 도구를 권장 합니다. 
  
 이 문서는 [DataContractJsonSerializer 샘플](../samples/json-serialization.md)을 기반으로 합니다.  
  
## <a name="to-define-the-data-contract-for-a-person-type"></a>사용자 형식에 대 한 데이터 계약을 정의 하려면 
  
1. `Person`를 클래스에 연결하고 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 serialize할 멤버에 연결하여 <xref:System.Runtime.Serialization.DataMemberAttribute>에 대한 데이터 계약을 정의합니다. 데이터 계약에 대 한 자세한 내용은 [서비스 계약 디자인](../designing-service-contracts.md)을 참조 하세요.  
  
    ```csharp  
    [DataContract]  
    internal class Person  
    {  
        [DataMember]  
        internal string name;  
  
        [DataMember]  
        internal int age;  
    }  
    ```  
  
## <a name="to-serialize-an-instance-of-type-person-to-json"></a>형식 Person의 인스턴스를 JSON으로 serialize하려면  
  
> [!NOTE]
> 서버에서 보내는 회신을 직렬화 하는 동안 오류가 발생 하거나 다른 이유로 인해 오류가 발생 하는 경우 클라이언트에 오류로 반환 되지 않을 수 있습니다.  

1. `Person` 형식의 인스턴스를 만듭니다.  
  
    ```csharp  
    var p = new Person();  
    p.name = "John";  
    p.age = 42;  
    ```  
  
2. @No__t-1을 사용 하 여 `Person` 개체를 메모리 스트림으로 Serialize 합니다.  
  
    ```csharp  
    var stream1 = new MemoryStream();  
    var ser = new DataContractJsonSerializer(typeof(Person));  
    ```  
  
3. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A> 메서드를 사용하여 JSON 데이터를 스트림에 씁니다.  
  
    ```csharp  
    ser.WriteObject(stream1, p);  
    ```  
  
4. JSON 출력을 표시합니다.  
  
    ```csharp  
    stream1.Position = 0;  
    var sr = new StreamReader(stream1);  
    Console.Write("JSON form of Person object: ");  
    Console.WriteLine(sr.ReadToEnd());  
    ```  
  
## <a name="to-deserialize-an-instance-of-type-person-from-json"></a>JSON에서 형식 Person의 인스턴스를 deserialize하려면  
  
1. `Person`의 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject%2A> 메서드를 사용하여 JSON 인코딩된 데이터를 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>의 새 인스턴스로 deserialize합니다.  
  
    ```csharp  
    stream1.Position = 0;  
    var p2 = (Person)ser.ReadObject(stream1);  
    ```  
  
2. 결과를 표시합니다.  
  
    ```csharp  
    Console.WriteLine($"Deserialized back, got name={p2.name}, age={p2.age}");  
    ```  
  
## <a name="example"></a>예제  
  
```csharp  
// Create a User object and serialize it to a JSON stream.  
public static string WriteFromObject()  
{  
    // Create User object.  
    var user = new User("Bob", 42);  
  
    // Create a stream to serialize the object to.  
    var ms = new MemoryStream();  
  
    // Serializer the User object to the stream.  
    var ser = new DataContractJsonSerializer(typeof(User));  
    ser.WriteObject(ms, user);  
    byte[] json = ms.ToArray();  
    ms.Close();  
    return Encoding.UTF8.GetString(json, 0, json.Length);  
}  
  
// Deserialize a JSON stream to a User object.  
public static User ReadToObject(string json)  
{  
    var deserializedUser = new User();  
    var ms = new MemoryStream(Encoding.UTF8.GetBytes(json));  
    var ser = new DataContractJsonSerializer(deserializedUser.GetType());  
    deserializedUser = ser.ReadObject(ms) as User;  
    ms.Close();  
    return deserializedUser;  
}  
```  
  
> [!NOTE]
> JSON serializer는 다음 샘플 코드에서처럼 동일한 이름의 여러 멤버를 가진 데이터 계약에 대한 serialization 예외를 throw합니다.  
  
```csharp  
[DataContract]  
public class TestDuplicateDataBase  
{  
    [DataMember]  
    public int field1 = 123;  
}

[DataContract]  
public class TestDuplicateDataDerived : TestDuplicateDataBase  
{  
    [DataMember]  
    public new int field1 = 999;  
}  
```  
  
## <a name="see-also"></a>참조

- [.NET의 JSON serialization](../../../standard/serialization/system-text-json-overview.md)

