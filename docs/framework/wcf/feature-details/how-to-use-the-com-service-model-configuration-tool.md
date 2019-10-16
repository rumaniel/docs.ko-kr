---
title: '방법: COM+ 서비스 모델 구성 도구 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], using service model configuration tool
ms.assetid: 7e68cd8d-5fda-4641-b92f-290db874376e
ms.openlocfilehash: 67bacade0435f1c63bc79b3282f6bded55b67304
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991579"
---
# <a name="how-to-use-the-com-service-model-configuration-tool"></a>방법: COM+ 서비스 모델 구성 도구 사용
적절한 호스팅 모드를 선택한 다음 COM+ 서비스 모델 구성 명령줄 도구(ComSvcConfig.exe)를 사용하여 웹 서비스로 노출될 애플리케이션 인터페이스를 구성합니다.  
  
> [!NOTE]
> 다음 작업을 수행하려면 컴퓨터의 관리자여야 합니다.  
  
 Windows 7 컴퓨터에서 ComSvcConfig.exe를 사용하여 웹 서비스가 최신 서비스 모델 버전(현재 v4.5)을 사용하도록 구성하려면 다음 단계를 따르십시오.  
  
1. 레지스트리 키 `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` 를 DWORD 값 0x00000001로 설정 합니다.  
  
2. Comsvcconfig.exe를 실행합니다.  
  
3. 1단계에서 추가한 레지스트리 키를 원래 값으로 되돌리거나, 원래 값이 없었던 경우에는 삭제합니다.  
  
> [!IMPORTANT]
> 이 레지스트리 키를 되돌리는 것은 중요합니다. 이 키는 호환성 키이므로 변경 내용을 되돌리지 않으면 컴퓨터에서 실행 중인 다른 .NET 애플리케이션에 문제가 발생할 수 있습니다.  
  
> [!WARNING]
> Windows 8 컴퓨터에서 Comsvcconfig.exe/install을 사용 하는 경우 ".NET Framework 3.5이 설치 되어 있지 않으면 PC의 앱에 다음 Windows 기능이 필요 합니다. .NET Framework 3.5 (.NET 2.0 및 .NET 3.0 포함)을 나타내는 대화 상자가 표시 됩니다. 이 대화 상자는 무시해도 됩니다. 또는 OnlyUseLatestCLR 레지스트리 키를 DWORD 값 0x00000001로 설정해도 됩니다.  
  
## <a name="to-add-an-interface-to-the-set-of-interfaces-exposed-as-web-services-using-the-com-hosting-mode"></a>COM + 호스팅 모드를 사용 하 여 웹 서비스로 노출 되는 인터페이스 집합에 인터페이스를 추가 하려면  
  
- 다음 예제에서처럼 `/install` 및 `/hosting:complus` 옵션을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose  
    ```  
  
     이 명령은 OnlineStore COM+ 애플리케이션에 있는 `IFinances` 구성 요소의 `ItemOrders.IFinancial` 인터페이스를 웹 서비스로 노출될 인터페이스 집합에 추가합니다. 이 서비스는 COM+ 호스팅 모드를 사용하므로 명시적으로 애플리케이션을 활성화해야 합니다.  
  
     와일드 카드 별표 (\*) 문자는 구성 요소와 인터페이스에 사용할 수 있지만 선택한 기능만 웹 서비스로 노출 하려는 경우에는 사용 하지 마십시오. 이 구성 요소의 다음 버전으로 실행하는 경우 와일드카드를 사용하면 구성 구문을 확인했을 때 표시되지 않은 인터페이스를 실수로 노출할 수도 있습니다.  
  
     /verbose 옵션은 도구에 경고와 오류를 표시하도록 지시합니다.  
  
     노출된 서비스에 대한 계약에 `IFinances` 인터페이스의 모든 메서드가 포함됩니다.  
  
## <a name="to-add-only-specific-methods-from-an-interface-to-the-set-of-interfaces-exposed-as-web-services-using-the-com-hosting-mode"></a>COM + 호스팅 모드를 사용 하 여 인터페이스의 특정 메서드만 웹 서비스로 노출 되는 인터페이스 집합에 추가 하려면  
  
- 다음 예제에서처럼 `/install` 및 `/hosting:complus` 옵션에 필수 메서드의 명시적 명명을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{Credit,Debit} /hosting:complus /verbose  
    ```  
  
     이 명령은 `Credit` 인터페이스의 `Debit` 및 `IFinances` 메서드만 노출된 서비스 계약에 작업으로 추가합니다. 인터페이스의 다른 모든 메서드는 계약에서 생략되고 웹 서비스 클라이언트에서 호출될 수 없습니다.  
  
## <a name="to-add-an-interface-to-the-set-of-interfaces-exposed-as-web-services-using-the-web-hosting-mode"></a>웹 호스팅 모드를 사용 하 여 웹 서비스로 노출 되는 인터페이스 집합에 인터페이스를 추가 하려면  
  
- 다음 예제에서처럼 `/install` 옵션 및 `/hosting:was` 옵션을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse /mex /verbose  
    ```  
  
     이 명령은 OnlineWarehouse COM+ 애플리케이션에 있는 `IStockLevels` 구성 요소의 `ItemInventory.Warehouse` 인터페이스를 웹 서비스로 노출될 인터페이스의 집합에 추가합니다. 이 서비스는 COM+가 아닌 IIS의 OnlineWarehouse 가상 디렉터리에서 웹 호스팅되므로 필요한 경우 애플리케이션이 자동으로 활성화됩니다.  
  
     웹 호스팅 in-process 구성을 사용하려면 구성 요소 서비스 관리 콘솔을 사용하여 서버 애플리케이션이 아닌 라이브러리 애플리케이션으로 실행되도록 COM+ 애플리케이션을 구성해야 합니다. 서버 애플리케이션으로 구성된 애플리케이션은 표준 웹 호스팅 모드를 사용하고 프로세스 홉을 수행하여 각 요청을 처리합니다.  
  
     `/mex` 옵션은 같은 전송을 응용 프로그램의 서비스 끝점으로 사용하는 MEX(메타데이터 교환) 서비스 끝점을 추가하여 서비스에서 계약 정의를 검색하려는 클라이언트를 지원합니다.  
  
## <a name="to-remove-a-web-service-for-a-specified-interface"></a>지정된 인터페이스에 대한 웹 서비스를 제거하려면  
  
- 다음 예제에서처럼 `/uninstall` 옵션을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /uninstall /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus  
    ```  
  
     이 명령은 OnlineStore COM+ 애플리케이션의 `IFinances` 구성 요소에서 `ItemOrders.Financial` 인터페이스를 제거합니다.  
  
## <a name="to-list-currently-exposed-interfaces"></a>현재 노출된 인터페이스를 나열하려면  
  
- 다음 예제에서처럼 `/list` 옵션을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /list  
    ```  
  
     이 명령은 현재 노출된 인터페이스와 함께 로컬 컴퓨터에 적용되는 해당 주소 및 바인딩 세부 내용을 나열합니다.  
  
## <a name="to-list-specific-currently-exposed-interfaces"></a>현재 노출된 특정 인터페이스를 나열하려면  
  
- 다음 예제에서처럼 `/list` 옵션을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /list /application:OnlineStore /hosting:complus  
    ```  
  
     이 명령은 현재 노출된 COM+ 호스팅 인터페이스와 함께 로컬 컴퓨터의 OnlineStore COM+ 애플리케이션에 대한 해당 주소 및 바인딩 세부 내용을 나열합니다.  
  
## <a name="to-display-help-on-the-options-that-can-be-used-with-the-utility"></a>유틸리티에 사용할 수 있는 옵션에 대한 도움말을 표시하려면  
  
- 다음 예제에서처럼 /? 옵션을 사용하여 ComSvcConfig를 실행합니다.  
  
    ```console  
    ComSvcConfig.exe /?  
    ```  
  
## <a name="see-also"></a>참고자료

- [COM+ 애플리케이션과 통합 개요](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications-overview.md)
