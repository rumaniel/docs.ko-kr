---
title: 데이터 계약 확인자 사용
ms.date: 03/30/2017
ms.assetid: 2e68a16c-36f0-4df4-b763-32021bff2b89
ms.openlocfilehash: b1c545d84db68f4b13925dd9088cc9d81050b5e7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61918569"
---
# <a name="using-a-data-contract-resolver"></a>데이터 계약 확인자 사용
데이터 계약 확인자를 사용하면 알려진 형식을 동적으로 구성할 수 있습니다. 알려진 형식은 데이터 계약에 필요하지 않은 형식을 serialize하거나 deserialize할 때 필요합니다. 알려진된 형식에 대 한 자세한 내용은 참조 하세요. [데이터 계약 알려진 형식을](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)합니다. 알려진 형식은 일반적으로 정적으로 지정됩니다. 즉, 작업을 구현하는 동안 작업이 받을 수 있는 가능한 형식을 모두 알고 있어야 합니다. 이에 해당하지 않고 알려진 형식을 동적으로 지정하는 기능이 중요한 시나리오도 있습니다.  
  
## <a name="creating-a-data-contract-resolver"></a>데이터 계약 확인자 만들기  
 데이터 계약 확인자를 만드는 작업에는 <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> 및 <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> 메서드를 구현하는 작업이 포함됩니다. 이러한 두 메서드는 serialization 및 deserialization 중에 사용되는 콜백을 각각 구현합니다. <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> 메서드는 serialization 중에 호출되며 데이터 계약 형식을 받아서 `xsi:type` 이름 및 네임스페이스에 매핑합니다. <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> 메서드는 deserialization 중에 호출되며 `xsi:type` 이름 및 네임스페이스를 받아서 데이터 계약 형식으로 확인합니다. 이러한 두 메서드에는 구현에서 기본 알려진 형식 확인자를 사용하기 위해 사용할 수 있는 `knownTypeResolver` 매개 변수가 있습니다.  
  
 다음 예제에서는 <xref:System.Runtime.Serialization.DataContractResolver>를 구현하여 `Customer` 데이터 계약 형식에서 파생된 `Person`라는 데이터 계약 형식에 매핑하거나 이 데이터 계약 형식에서 매핑하는 방법을 보여 줍니다.  
  
```csharp  
public class MyCustomerResolver : DataContractResolver  
{  
    public override bool TryResolveType(Type dataContractType, Type declaredType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        if (dataContractType == typeof(Customer))  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add("SomeCustomer");  
            typeNamespace = dictionary.Add("http://tempuri.com");  
            return true;  
        }  
        else  
        {  
            return knownTypeResolver.TryResolveType(dataContractType, declaredType, null, out typeName, out typeNamespace);  
        }  
    }  
  
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        if (typeName == "SomeCustomer" && typeNamespace == "http://tempuri.com")  
        {  
            return typeof(Customer);  
        }  
        else  
        {  
            return knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        }  
    }  
}  
```  
  
 <xref:System.Runtime.Serialization.DataContractResolver>를 정의한 후에는 다음 예제와 같이 이를 <xref:System.Runtime.Serialization.DataContractSerializer> 생성자에 전달하여 사용할 수 있습니다.  
  
```  
XmlObjectSerializer serializer = new DataContractSerializer(typeof(Customer), null, Int32.MaxValue, false, false, null, new MyCustomerResolver());  
```  
  
 다음 예제와 같이 <xref:System.Runtime.Serialization.DataContractResolver> 또는 <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A?displayProperty=nameWithType> 메서드를 호출할 때 <xref:System.Runtime.Serialization.DataContractSerializer.WriteObject%2A?displayProperty=nameWithType>를 지정할 수 있습니다.  
  
```  
MemoryStream ms = new MemoryStream();  
DataContractSerializer serializer = new DataContractSerializer(typeof(Customer));  
XmlDictionaryWriter writer = XmlDictionaryWriter.CreateDictionaryWriter(XmlWriter.Create(ms));  
serializer.WriteObject(writer, new Customer(), new MyCustomerResolver());  
writer.Flush();  
ms.Position = 0;  
Console.WriteLine(((Customer)serializer.ReadObject(XmlDictionaryReader.CreateDictionaryReader(XmlReader.Create(ms)), false, new MyCustomerResolver()));  
```  
  
 또는 다음 예제와 같이 이를 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>에 설정할 수 있습니다.  
  
```  
ServiceHost host = new ServiceHost(typeof(MyService));  
  
ContractDescription cd = host.Description.Endpoints[0].Contract;  
OperationDescription myOperationDescription = cd.Operations.Find("Echo");  
  
DataContractSerializerOperationBehavior serializerBehavior = myOperationDescription.Behaviors.Find<DataContractSerializerOperationBehavior>();  
if (serializerBehavior == null)  
{  
    serializerBehavior = new DataContractSerializerOperationBehavior(myOperationDescription);  
    myOperationDescription.Behaviors.Add(serializerBehavior);  
}  
  
SerializerBehavior.DataContractResolver = new MyCustomerResolver();  
```  
  
 서비스에 적용할 수 있는 특성을 구현하여 데이터 계약 확인자를 선언적으로 지정할 수 있습니다.  자세한 내용은 참조는 [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md) 샘플입니다. 이 샘플에는 "knownassembly" 특성은 구현 사용자 지정 데이터 계약 확인자 서비스의 동작을 추가 합니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 계약 알려진 형식](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)
- [DataContractSerializer 샘플](../../../../docs/framework/wcf/samples/datacontractserializer-sample.md)
- [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md)
