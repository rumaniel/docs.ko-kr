---
title: '방법: 서비스 모니커 등록 및 구성'
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], configure service monikers
- COM [WCF], register service monikers
ms.assetid: e5e16c80-8a8e-4eef-af53-564933b651ef
ms.openlocfilehash: 547e507b4a1115de81532263c34964cd20f15d4e
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972141"
---
# <a name="how-to-register-and-configure-a-service-moniker"></a>방법: 서비스 모니커 등록 및 구성
형식화 된 계약을 사용 하 여 COM 응용 프로그램 내에서 WCF (Windows Communication Foundation) 서비스 모니커를 사용 하려면 먼저 필요한 특성을 사용 하는 형식을 COM에 등록 하 고 필요한 바인딩을 사용 하 여 COM 응용 프로그램 및 모니커를 구성 해야 합니다. 구성.  
  
### <a name="to-register-the-required-attributed-types-with-com"></a>필요한 특성을 사용하는 형식을 COM에 등록하려면  
  
1. [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 도구를 사용 하 여 WCF 서비스에서 메타 데이터 계약을 검색할 수 있습니다. 이렇게 하면 WCF 클라이언트 어셈블리와 클라이언트 응용 프로그램 구성 파일에 대 한 소스 코드가 생성 됩니다.  
  
2. 어셈블리의 형식이 `ComVisible`로 표시되는지 확인합니다. 이렇게 하려면 Visual Studio 프로젝트의 AssemblyInfo.cs 파일에 다음 특성을 추가합니다.  
  
    ```csharp
    [assembly: ComVisible(true)]  
    ```  
  
3. 관리 되는 WCF 클라이언트를 강력한 이름의 어셈블리로 컴파일합니다. 이렇게 하려면 암호화된 키 쌍으로 서명해야 합니다. 자세한 내용은 .NET 개발자 가이드에서 [강력한 이름으로 어셈블리 서명](https://go.microsoft.com/fwlink/?LinkId=94874) 을 참조 하세요.  
  
4. 어셈블리 등록(Regasm.exe) 도구에 `/tlb` 옵션을 사용하여 어셈블리의 형식을 COM에 등록합니다.  
  
5. 전역 어셈블리 캐시(Gacutil.exe) 도구를 사용하여 어셈블리를 전역 어셈블리 캐시에 추가합니다.  
  
    > [!NOTE]
    > 어셈블리에 서명하고 전역 어셈블리 캐시에 추가하는 것은 선택적 단계이지만 런타임에 올바른 위치에서 어셈블리를 로드하는 프로세스를 단순화할 수 있습니다.  
  
### <a name="to-configure-the-com-application-and-the-moniker-with-the-required-binding-configuration"></a>필요한 바인딩 구성을 사용하여 COM 애플리케이션과 모니커를 구성하려면  
  
- 클라이언트 응용 프로그램의 구성 파일에 생성 된 클라이언트 응용 프로그램 구성 파일에서 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 통해 생성 된 바인딩 정의를 저장 합니다. 예를 들어 이름이 CallCenterClient.exe인 Visual Basic 6.0 실행 파일에 대해 실행 파일과 동일한 디렉터리 내의 CallCenterConfig.exe.config 파일에 구성을 저장해야 합니다. 이제 클라이언트 애플리케이션에서 모니커를 사용할 수 있습니다. WCF에서 제공 하는 표준 바인딩 형식 중 하나를 사용 하는 경우에는 바인딩 구성이 필요 하지 않습니다.  
  
     다음 형식이 등록됩니다.  
  
    ```csharp  
    using System.ServiceModel;  
  
    [ServiceContract]   
    public interface IMathService   
    {  
    [OperationContract]  
    public int Add(int x, int y);  
    [OperationContract]  
    public int Subtract(int x, int y);  
    }  
    ```  
  
     애플리케이션은 `wsHttpBinding` 바인딩을 사용하여 노출됩니다. 지정된 형식과 애플리케이션 구성에 대해 다음 예제 모니커 문자열이 사용됩니다.  
  
    ``` 
    service4:address=http://localhost/MathService, binding=wsHttpBinding, bindingConfiguration=Binding1  
    ```  
  
     `or`  
  
    ``` 
    service4:address=http://localhost/MathService, binding=wsHttpBinding, bindingConfiguration=Binding1, contract={36ADAD5A-A944-4d5c-9B7C-967E4F00A090}  
    ```  
  
     다음 샘플 코드와 같이 `IMathService` 형식을 포함하는 어셈블리에 대한 참조를 추가한 후 Visual Basic 6.0 애플리케이션 내에서 이러한 모니커 문자열 중 하나를 사용할 수 있습니다.  
  
    ```vb  
    Dim MathProxy As IMathService  
    Dim result As Integer  
  
    Set MathProxy = GetObject( _  
            "service4:address=http://localhost/MathService, _  
            binding=wsHttpBinding, _  
            bindingConfiguration=Binding1")  
  
    result = MathProxy.Add(3, 5)  
    ```  
  
     이 예제에서 바인딩 구성 `Binding1`의 정의는 클라이언트 애플리케이션에 대한 적절한 이름의 구성 파일(예: vb6appname.exe.config)에 저장됩니다.  
  
    > [!NOTE]
    > C#, C++ 또는 다른 모든 .NET 언어 애플리케이션으로 유사한 코드를 사용할 수 있습니다.  
  
    > [!NOTE]
    > : 모니커의 형식이 잘못 되었거나 서비스를 사용할 수 없는 경우를 `GetObject` 호출 하면 "구문이 잘못 되었습니다" 라는 오류가 반환 됩니다. 이 오류가 발생하면 사용하고 있는 모니커가 올바르고 서비스를 사용할 수 있는지 확인하세요.  
  
     이 항목에서는 VB 6.0 코드의 서비스 모니커 사용에 중점을 두지만 다른 언어에서 서비스 모니커를 사용할 수 있습니다. C++ 코드에서 모니커를 사용하는 경우 다음 코드와 같이 "no_namespace named_guids raw_interfaces_only"를 사용하여 Svcutil.exe에서 생성된 어셈블리를  가져와야 합니다.  
  
    ```cpp
    #import "ComTestProxy.tlb" no_namespace named_guids  
    ```  
  
     모든 메서드에서 `HResult`를 반환하도록 가져온 인터페이스 정의를 수정합니다. 다른 모든 반환 값은 출력 매개 변수로 변환됩니다. 전체 메서드 실행은 동일하게 유지됩니다. 이 경우 프록시에서 메서드를 호출할 때 예외의 원인을 확인할 수 있습니다. 이 기능은 C++ 코드에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
