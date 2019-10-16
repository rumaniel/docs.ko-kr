---
title: SQL 추적
ms.date: 03/30/2017
ms.assetid: bcaebeb1-b9e5-49e8-881b-e49af66fd341
ms.openlocfilehash: 24cc484bf11d7cedab949d61c63f805a28a9f849
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038064"
---
# <a name="sql-tracking"></a>SQL 추적
이 샘플에서는 SQL 데이터베이스에 추적 레코드를 기록하는 사용자 지정 SQL 추적 참가자를 작성하는 방법을 보여 줍니다. WF (Windows Workflow Foundation)는 워크플로 인스턴스 실행에 대 한 가시성을 확보 하기 위해 워크플로 추적을 제공 합니다. 추적 런타임에서는 워크플로를 실행하는 동안 워크플로 추적 레코드를 내보냅니다. 워크플로 추적에 대 한 자세한 내용은 [워크플로 추적 및 추적](../workflow-tracking-and-tracing.md)을 참조 하세요.

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. SQL Server 2008 또는 SQL Server 2008 Express 이상 버전이 설치되어 있는지 확인합니다. 샘플과 함께 제공되는 스크립트에서는 로컬 컴퓨터에 SQL Express 인스턴스가 사용되는 것으로 가정합니다. 로컬 컴퓨터에 다른 인스턴스를 사용하고 있으면 샘플을 실행하기 전에 데이터베이스 관련 스크립트를 수정해야 합니다.

2. 스크립트 디렉터리(\WF\Basic\Tracking\SqlTracking\CS\Scripts)에서 Trackingsetup.cmd를 실행하여 SQL Server 추적 데이터베이스를 만듭니다. 이렇게 하면 TrackingSample이라는 데이터베이스가 생성됩니다.

    > [!NOTE]
    > 이 스크립트에서는 SQL Express의 기본 인스턴스를 기반으로 데이터베이스를 만듭니다. 다른 데이터베이스 인스턴스를 기반으로 이를 설치하려면 Trackingsetup.cmd 스크립트를 편집합니다.  
  
3. Visual Studio 2010에서 SqlTrackingSample .sln을 엽니다.  
  
4. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
5. F5 키를 눌러 애플리케이션을 실행합니다.  
  
     브라우저 창이 열리고 응용 프로그램의 디렉터리 목록이 표시됩니다.  
  
6. 브라우저에서 StockPriceService.xamlx를 클릭합니다.  
  
7. 브라우저에 StockPriceService 페이지가 표시됩니다. 이 페이지에는 로컬 서비스 WSDL 주소가 포함되어 있습니다. 이 주소를 복사합니다.  
  
     로컬 서비스 WSDL 주소의 `http://localhost:65193/StockPriceService.xamlx?wsdl`예는입니다.  
  
8. 파일 탐색기를 사용 하 여 WCF 테스트 클라이언트 (Wcftestclient.exe)를 실행 합니다. 이는 Microsoft Visual Studio 10.0\Common7\IDE 디렉터리에 있습니다.  
  
9. WCF 테스트 클라이언트에서 **파일** 메뉴를 클릭 하 고 **서비스 추가**를 선택 합니다. 로컬 서비스 주소를 텍스트 상자에 붙여넣습니다. **확인** 을 클릭 하 여 대화 상자를 닫습니다.  
  
10. WCF 테스트 클라이언트에서 **GetStockPrice**를 두 번 클릭 합니다. 그러면 하나의 매개 `GetStockPrice` 변수를 사용 하는 작업이 열리고 값 `Contoso` 에을 입력 하 고 **호출**을 클릭 합니다.  
  
11. 내보낸 추적 레코드가 SQL 데이터베이스에 기록됩니다. 추적 레코드를 보려면 SQL Management Studio에서 TrackingSample 데이터베이스를 열고 테이블을 찾습니다. SQL Server Management Studio에 대 한 자세한 내용은 [SQL Server Management Studio 소개](https://go.microsoft.com/fwlink/?LinkId=165645)를 참조 하세요. SQL Server 2008 Management Studio Express는 [여기](https://go.microsoft.com/fwlink/?LinkId=180520)에서 다운로드할 수 있습니다. 테이블에 대해 선택 쿼리를 실행하면 해당 테이블에 저장되어 있는 추적 레코드 내의 데이터가 표시됩니다.  
  
#### <a name="to-uninstall-the-sample"></a>샘플을 제거하려면  
  
1. 샘플 디렉터리(\WF\Basic\Tracking\SqlTracking)에서 Trackingcleanup.cmd 스크립트를 실행합니다.  
  
    > [!NOTE]
    > Trackingcleanup.cmd가 로컬 컴퓨터 SQL Express에서 데이터베이스를 삭제하려고 시도합니다. 다른 SQL Server 인스턴스를 사용하는 경우 Trackingcleanup.cmd를 편집합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\SqlTracking`  
  
## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
