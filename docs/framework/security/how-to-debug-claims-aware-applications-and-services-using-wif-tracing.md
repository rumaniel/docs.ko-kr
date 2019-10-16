---
title: '방법: WIF 추적을 사용하여 클레임 인식 애플리케이션 및 서비스 디버그'
ms.date: 03/30/2017
ms.assetid: 3d51ba59-3adb-4ca4-bd33-5027531af687
author: BrucePerlerMS
ms.openlocfilehash: 604ebf5ad71197f6614ffa45b6d7c181d474e1aa
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990476"
---
# <a name="how-to-debug-claims-aware-applications-and-services-using-wif-tracing"></a>방법: WIF 추적을 사용하여 클레임 인식 애플리케이션 및 서비스 디버그
## <a name="applies-to"></a>적용 대상  
  
- Microsoft® Windows® Identity Foundation(WIF)  
  
- Service Trace Viewer 도구(SvcTraceViewer.exe)  
  
- 문제 해결 및 WIF 응용 프로그램 디버그  
  
## <a name="summary"></a>요약  
 이 방법에서는 WIF 추적을 구성하고 추적 로그를 수집하는 방법 및 추적 뷰어 도구를 사용하여 추적 로그를 분석하는 방법의 필수 단계를 설명합니다. WIF와 관련된 문제를 해결하는 데 필요한 작업에 추적 항목을 매핑하는 일반적인 방법을 제공합니다.  
  
## <a name="contents"></a>목차  
  
- 목표  
  
- 단계 요약  
  
- 1단계 - Web.config 구성 파일을 사용하여 WIF 추적 구성  
  
- 2단계 - 추적 뷰어 도구를 사용하여 WIF 추적 파일 분석  
  
- 3단계 - WIF 관련 문제를 해결할 수 있는 솔루션 식별  
  
- 관련 항목  
  
## <a name="objectives"></a>목표  
  
- WIF 추적을 구성합니다.  
  
- 추적 뷰어 도구에서 추적 로그를 봅니다.  
  
- 추적 로그에서 WIF 관련 문제를 식별합니다.  
  
- 추적 로그에서 발견된 WIF 관련 문제에 정정 작업을 적용합니다.  
  
## <a name="summary-of-steps"></a>단계 요약  
  
- 1단계 - Web.config 구성 파일을 사용하여 WIF 추적 구성  
  
- 2단계 - 추적 뷰어 도구를 사용하여 WIF 추적 파일 분석  
  
- 3단계 - WIF 관련 문제를 해결할 수 있는 솔루션 식별  
  
## <a name="step-1--configure-wif-tracing-using-webconfig-configuration-file"></a>1단계 - Web.config 구성 파일을 사용하여 WIF 추적 구성  
 이 단계에서는 WIF가 해당 이벤트를 추적하고 추적 로그에 저장할 수 있도록 하는 변경 내용을 *Web.config* 파일의 구성 섹션에 추가합니다.  
  
#### <a name="to-configure-wif-tracing-using-webconfig-configuration-file"></a>Web.config 구성 파일을 사용하여 WIF 추적을 구성하려면  
  
1. Visual Studio 편집기의 **솔루션 탐색기**에서 루트 **Web.config** 또는 **App.config** 구성 파일을 두 번 클릭하여 엽니다. 솔루션에 **Web.config** 또는 **App.config** 구성 파일이 없는 경우 **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목...** 을 차례로 클릭하여 추가합니다. **새 항목** 대화 상자의 목록에서 **App.config**에 대해 **응용 프로그램 구성 파일**을 선택하거나 **Web.config**에 대해 **웹 구성 파일**을 선택하고 **확인**을 클릭합니다.  
  
2. 구성 파일의 끝에 있는 **\<configuration>** 노드 내에 다음과 비슷한 구성 항목을 추가합니다.  
  
    ```xml  
    <system.diagnostics>  
        <sources>  
            <source name="System.IdentityModel" switchValue="Verbose">  
                <listeners>  
                    <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="WIFTrace.e2e"/>  
                </listeners>  
            </source>  
        </sources>  
        <trace autoflush="true"/>  
    </system.diagnostics>  
    ```  
  
3. 위의 구성은 WIF에 자세한 추적 이벤트를 생성하고 *WIFTrace.e2e* 파일에 기록하도록 지시합니다. **Switchvalue** 스위치에 대 한 값의 전체 목록은 다음 항목에서 찾을 수 있는 추적 수준 표를 참조 하세요. [추적 구성](../wcf/diagnostics/tracing/configuring-tracing.md).  
  
## <a name="step-2--analyze-wif-trace-files-using-trace-viewer-tool"></a>2단계 - 추적 뷰어 도구를 사용하여 WIF 추적 파일 분석  
 이 단계에서는 추적 뷰어 도구(SvcTraceViewer.exe)를 사용하여 WIF 추적 로그를 분석합니다.  
  
#### <a name="to-analyze-wif-trace-logs-using-trace-viewer-tool-svctraceviewerexe"></a>추적 뷰어 도구(SvcTraceViewer.exe)를 사용하여 WIF 추적 로그를 분석하려면  
  
1. 추적 뷰어 도구(SvcTraceViewer.exe)는 Windows SDK의 일부로 제공됩니다. Windows SDK를 아직 설치 하지 않은 경우 다음 위치에서 다운로드할 수 있습니다. [Windows SDK](https://www.microsoft.com/download/en/details.aspx?id=8279).  
  
2. 추적 뷰어 도구(SvcTraceViewer.exe)를 실행합니다. 일반적으로 설치 경로의 **Bin** 폴더에서 사용할 수 있습니다.  
  
3. 메뉴에서 **파일**, **열기...** 옵션을 선택하거나 **Ctrl+O** 바로 가기를 사용하여 WIF 추적 로그 파일(예: WIFTrace.e2e)을 엽니다. 추적 로그 파일이 추적 뷰어 도구에서 열립니다.  
  
4. **작업** 탭에서 항목을 검토합니다. 각 항목에는 작업 수, 기록된 추적 수, 작업 기간, 시작 및 종료 타임스탬프가 포함되어야 합니다.  
  
5. **작업** 탭을 클릭합니다. 자세한 추적 항목이 도구의 주 영역에 표시됩니다. 메뉴의 **수준** 드롭다운 목록을 사용 하 여 특정 추적 수준을 필터링 할 수 있습니다. 예를 들면 다음과 같습니다. **모든**, **경고**, **오류**, **정보**등  
  
6. 특정 추적 항목을 클릭하여 도구의 아래쪽 영역에서 세부 정보를 검토합니다. 해당 탭을 선택하여 **서식 있음** 및 **XML** 뷰에서 세부 정보를 볼 수 있습니다.  
  
## <a name="step-3--identify-solutions-to-fix-wif-related-issues"></a>3단계 - WIF 관련 문제를 해결할 수 있는 솔루션 식별  
 이 단계에서는 WIF 추적 로그 및 추적 뷰어 도구를 사용하여 식별된 WIF 관련 문제에 대한 솔루션을 식별할 수 있습니다. 문제 해결을 위해 WIF 관련 예외를 잠재적인 솔루션이나 필수 작업에 매핑하는 일반적인 매핑을 간략하게 설명합니다.  
  
#### <a name="to-identify-solutions-to-fix-wif-related-issues"></a>WIF 관련 문제를 해결할 수 있는 솔루션을 식별하려면  
  
1. WIF 예외 및 필수 작업이 포함된 다음 표를 검토하여 문제를 해결합니다.  
  
|**오류 ID**|**오류 메시지**|**오류를 해결하는 데 필요한 작업**|  
|-|-|-|  
|ID4175|보안 토큰의 발급자가 IssuerNameRegistry에서 인식되지 않았습니다.  이 발급자의 보안 토큰을 수락하려면 이 발급자에 대한 유효한 이름을 반환하도록 IssuerNameRegistry를 구성합니다.|MMC 스냅인에서 지문을 복사하고 *Web.config* 파일에 붙여넣으면 이 오류가 발생할 수 있습니다. 특히, 인증서 속성 창에서 복사하는 경우 텍스트 문자열에서 인쇄할 수 없는 추가 문자를 가져올 수 있습니다. 이 문자를 추가 하면 지문 일치가 실패 합니다. 지문을 올바르게 복사 하는 절차는 [웹에 대 한 클레임 기반 Single sign-on 및 Microsoft Azure](https://docs.microsoft.com/previous-versions/msp-n-p/ff359102%28v=pandp.10%29)에서 찾을 수 있습니다.|  
  
## <a name="related-items"></a>관련 항목  
  
- [Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결](../wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
