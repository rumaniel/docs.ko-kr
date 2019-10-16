---
title: '방법: XmlSerializer를 사용하여 WCF 클라이언트 애플리케이션의 시작 시간 향상'
ms.date: 03/30/2017
ms.assetid: 21093451-0bc3-4b1a-9a9d-05f7f71fa7d0
ms.openlocfilehash: f8766a5dfa2bcfc715a0f0e21274f7c6ac04ad15
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69944888"
---
# <a name="how-to-improve-the-startup-time-of-wcf-client-applications-using-the-xmlserializer"></a>방법: XmlSerializer를 사용하여 WCF 클라이언트 애플리케이션의 시작 시간 향상
<xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize할 수 있는 데이터 형식을 사용하는 서비스 및 클라이언트 응용 프로그램은 런타임에 해당 데이터 형식에 대한 serialization 코드를 생성하고 컴파일합니다. 이로 인해 시작 시 성능이 저하될 수 있습니다.  
  
> [!NOTE]
> 미리 생성된 serialization 코드는 서비스가 아닌 클라이언트 응용 프로그램에서만 사용할 수 있습니다.  
  
 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 는 응용 프로그램에 대해 컴파일된 어셈블리에서 필요한 serialization 코드를 생성 하 여 이러한 응용 프로그램의 시작 성능을 향상 시킬 수 있습니다. Svcutil.exe는 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize될 수 있는 컴파일된 애플리케이션 어셈블리에서 서비스 계약에 사용하는 모든 데이터 형식에 대한 serialization 코드를 생성합니다. <xref:System.Xml.Serialization.XmlSerializer>를 사용하는 서비스 및 작업 계약은 <xref:System.ServiceModel.XmlSerializerFormatAttribute>와 함께 표시됩니다.  
  
### <a name="to-generate-xmlserializer-serialization-code"></a>XmlSerializer serialization 코드를 생성하려면  
  
1. 서비스 또는 클라이언트 코드를 하나 이상의 어셈블리로 컴파일합니다.  
  
2. SDK 명령 프롬프트를 엽니다.  
  
3. 명령 프롬프트에서 다음 형식을 사용하여 Svcutil.exe 도구를 실행합니다.  
  
    ```  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     `assemblyPath` 인수는 서비스 계약 형식이 포함된 어셈블리의 경로를 지정합니다. Svcutil.exe는 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize될 수 있는 컴파일된 애플리케이션 어셈블리에서 서비스 계약에 사용하는 모든 데이터 형식에 대한 serialization 코드를 생성합니다.  
  
     Svcutil.exe는 C# serialization 코드만 생성할 수 있습니다. 각 입력 어셈블리에 대해서 하나의 소스 코드 파일이 생성됩니다. **/Language** 스위치를 사용 하 여 생성 된 코드의 언어를 변경할 수 없습니다.  
  
     종속 어셈블리의 경로를 지정 하려면 **/reference** 옵션을 사용 합니다.  
  
4. 다음 옵션 중 하나를 사용하여 생성된 serialization 코드를 애플리케이션에서 사용할 수 있도록 합니다.  
  
    1. 생성 된 serialization 코드를 이름 [*원본 어셈블리*]를 사용 하 여 별도의 어셈블리로 컴파일합니다. XmlSerializers .dll (예: Myapp.exe). 애플리케이션에서 어셈블리를 로드할 수 있어야 하며, 해당 어셈블리는 원본 어셈블리와 동일한 키로 서명되어야 합니다. 원본 어셈블리를 다시 컴파일하면 serialization 어셈블리도 다시 생성해야 합니다.  
  
    2. 생성된 serialization 코드를 별도의 어셈블리로 컴파일하고 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute>를 사용하는 서비스 계약에 <xref:System.ServiceModel.XmlSerializerFormatAttribute>를 사용합니다. 컴파일된 serialization 어셈블리를 가리키기 위해 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> 또는 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> 속성을 설정합니다.  
  
    3. 생성된 serialization 코드를 애플리케이션 어셈블리로 컴파일하고 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute>를 사용하는 서비스 계약에 <xref:System.ServiceModel.XmlSerializerFormatAttribute>를 추가합니다. <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> 또는 <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> 속성은 설정하지 마십시오. 기본 serialization 어셈블리가 현재 어셈블리로 간주됩니다.  
  
### <a name="to-generate-xmlserializer-serialization-code-in-visual-studio"></a>Visual Studio에서 XmlSerializer serialization 코드를 생성 하려면  
  
1. Visual Studio에서 WCF 서비스 및 클라이언트 프로젝트를 만듭니다. 그런 다음 서비스 참조를 클라이언트 프로젝트에 추가 합니다.  
  
2.  -> 클라이언트앱프로젝트의 *reference.cs* 파일에서 **serviceReference** **참조**의 서비스 계약에 를추가합니다.<xref:System.ServiceModel.XmlSerializerFormatAttribute> 이러한 파일을 보려면 **솔루션 탐색기** 의 모든 파일을 표시 해야 합니다.  
  
3. 클라이언트 앱을 빌드합니다.  
  
4. [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 명령을 사용 하 여 미리 생성 된 serializer *.cs* 파일을 만듭니다.  
  
    ```  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     AssemblyPath 인수는 WCF 클라이언트 어셈블리에 대 한 경로를 지정 합니다.  
  
     예:  
  
    ```  
    svcutil.exe /t:xmlSerializer wcfclient.exe  
    ```  
  
     *WCFClient.XmlSerializers.dll.cs* 파일이 생성 됩니다.  
  
5. 미리 생성 된 serialization 어셈블리를 컴파일합니다.  
  
     이전 단계의 예제에 따라 compile 명령은 다음과 같습니다.  
  
    ```  
    csc /r:wcfclient.exe /out:WCFClient.XmlSerializers.dll /t:library WCFClient.XmlSerializers.dll.cs  
    ```  
  
     생성 된 *WCFClient* 가 클라이언트 앱과 동일한 디렉터리에 있는지 확인 합니다 .이 경우에는 *WCFClient* 입니다.  
  
6. 평소와 같이 클라이언트 앱을 실행 합니다. 미리 생성 된 serialization 어셈블리가 사용 됩니다.  
  
## <a name="example"></a>예제  
 다음 명령은 어셈블리의 모든 서비스 계약이 사용하는 `XmlSerializer` 형식에 대해 serialization 형식을 생성합니다.  
  
```  
svcutil /t:xmlserializer myContractLibrary.exe  
```  
  
## <a name="see-also"></a>참고자료

- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
