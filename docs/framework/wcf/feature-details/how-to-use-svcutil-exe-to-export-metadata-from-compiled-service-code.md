---
title: '방법: Svcutil.exe를 사용하여 컴파일된 서비스 코드에서 메타데이터 내보내기'
ms.date: 03/30/2017
ms.assetid: 95d0aed3-16a2-4398-89bb-39418eeb7355
ms.openlocfilehash: 2d1b70931fe70dfd605e182d4b23a151bc8130a3
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991176"
---
# <a name="how-to-use-svcutilexe-to-export-metadata-from-compiled-service-code"></a>방법: Svcutil.exe를 사용하여 컴파일된 서비스 코드에서 메타데이터 내보내기
Svcutil.exe에서는 다음과 같이 컴파일된 어셈블리에 있는 서비스, 계약 및 데이터 형식에 대한 메타데이터를 내보낼 수 있습니다.  
  
- Svcutil.exe를 사용하는 어셈블리 집합의 컴파일된 모든 서비스 계약에 대한 메타데이터를 내보내려면 어셈블리를 입력 매개 변수로 지정합니다. 이는 기본 동작입니다.  
  
- Svcutil.exe를 사용하는 컴파일된 서비스에 대한 메타데이터를 내보내려면 서비스 어셈블리 또는 어셈블리를 입력 매개 변수로 지정합니다. 내보낼 서비스의 구성 이름을 나타내려면 `/serviceName` 옵션을 사용해야 합니다. Svcutil.exe에서는 지정된 실행 가능한 어셈블리에 대한 구성 파일을 자동으로 로드합니다.  
  
- 어셈블리 집합 내의 모든 데이터 계약 형식을 내보내려면 `/dataContractOnly` 옵션을 사용합니다.  
  
> [!NOTE]
> 종속 어셈블리의 파일 경로를 지정하려면 `/reference` 옵션을 사용합니다.  
  
### <a name="to-export-metadata-for-compiled-service-contracts"></a>컴파일된 서비스 계약에 대한 메타데이터를 내보내려면  
  
1. 서비스 계약 구현을 하나 이상의 클래스 라이브러리로 컴파일합니다.  
  
2. Svcutil.exe를 컴파일된 어셈블리에서 실행합니다.  
  
    > [!NOTE]
    > 종속 어셈블리의 파일 경로를 지정하려면 `/reference` 스위치를 사용해야 할 수 있습니다.  
  
    ```console
    svcutil.exe Contracts.dll  
    ```  
  
### <a name="to-export-metadata-for-a-compiled-service"></a>컴파일된 서비스에 대한 메타데이터를 내보내려면  
  
1. 서비스 구현을 실행 가능한 어셈블리로 컴파일합니다.  
  
2. 서비스 실행 파일의 구성 파일을 만들고 서비스 구성을 추가합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name="MyService" >  
            <endpoint address="finder" contract="IPeopleFinder" binding="wsHttpBinding" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
3. 서비스의 구성 이름을 지정하려면 `/serviceName` 스위치를 사용하여 Svcutil.exe를 컴파일된 서비스 실행 파일에서 실행합니다.  
  
    > [!NOTE]
    > 종속 어셈블리의 파일 경로를 지정하려면 `/reference` 스위치를 사용해야 할 수 있습니다.  
  
    ```console  
    svcutil.exe /serviceName:MyService Service.exe /reference:path/Contracts.dll  
    ```  
  
### <a name="to-export-metadata-for-compiled-data-contracts"></a>컴파일된 데이터 계약에 대한 메타데이터를 내보내려면  
  
1. 데이터 계약 구현을 하나 이상의 클래스 라이브러리로 컴파일합니다.  
  
2. 데이터 계약의 메타데이터만 생성되어야 함을 지정하려면 `/dataContract` 스위치를 사용하여 Svcutil.exe를 컴파일된 어셈블리에서 실행합니다.  
  
    > [!NOTE]
    > 종속 어셈블리의 파일 경로를 지정하려면 `/reference` 스위치를 사용해야 할 수 있습니다.  
  
    ```console  
    svcutil.exe /dataContractOnly Contracts.dll  
    ```  
  
## <a name="example"></a>예제  
 다음 예제에서는 단순 서비스 구현 및 구성에 대한 메타데이터를 생성하는 방법을 보여 줍니다.  
  
 서비스 계약에 대한 메타데이터를 내보내려면  
  
```console  
svcutil.exe Contracts.dll  
```  
  
 데이터 계약에 대한 메타데이터를 내보내려면  
  
```console  
svcutil.exe /dataContractOnly Contracts.dll  
```  
  
 서비스 구현에 대한 메타데이터를 내보내려면  
  
```console  
svcutil.exe /serviceName:MyService Service.exe /reference:<path>/Contracts.dll  
```  
  
 `<path>`는 Contracts.dll의 경로입니다.  
  
```csharp
// The following service contract and data contracts are compiled into
// Contracts.dll.  
[ServiceContract(ConfigurationName="IPeopleFinder")]  
public interface IPersonFinder  
{  
    [OperationContract]  
    Address GetAddress(Person s);  
}  
  
[DataContract]  
public class Person  
{  
    [DataMember]  
    public string firstName;  
    [DataMember]  
    public string lastName;  
    [DataMember]  
    public int age;  
}  
  
[DataContract]  
public class Address  
{  
    [DataMember]  
    public string city;  
    [DataMember]  
    public string state;  
    [DataMember]  
    public string street;  
    [DataMember]  
    public int zipCode;  
    [DataMember]  
    public Person person;  
}  
```

```csharp
// The following service implementation is compiled into Service.exe.
// This service uses the contracts specified in Contracts.dll.  
[ServiceBehavior(ConfigurationName = "MyService")]  
public class MyService : IPersonFinder  
{  
    public Address GetAddress(Person person)  
    {  
        Address address = new Address();  
        address.person = person;  
        return address;  
    }  
}  
```

```xml  
<!-- The following is the configuration file for Service.exe. -->  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="MyService">  
         <endpoint  address="finder"  
                    binding="basicHttpBinding"  
                    contract="IPeopleFinder"/>  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
- [메타데이터 내보내기 및 가져오기](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)
