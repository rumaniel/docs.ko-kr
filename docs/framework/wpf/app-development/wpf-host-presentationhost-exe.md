---
title: WPF 호스트(PresentationHost.exe)
ms.date: 03/30/2017
helpviewer_keywords:
- WPF Host application [WPF]
- PresentationHost.exe
ms.assetid: 3215bfa1-722c-4ac8-a7c5-bdd02d30afbd
ms.openlocfilehash: c1c26b49a33a58189f66e7b938333f362e467853
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002155"
---
# <a name="wpf-host-presentationhostexe"></a>WPF 호스트(PresentationHost.exe)
Windows Presentation Foundation (WPF) 호스트 (Presentationhost.exe)는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 응용 프로그램을 호환 되는 브라우저 (Microsoft Internet Explorer 6 이상 포함)에서 호스팅할 수 있도록 하는 응용 프로그램입니다. 기본적으로 Windows Presentation Foundation (WPF) 호스트는 다음을 포함 하 여 브라우저에서 호스팅되는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 콘텐츠에 대 한 셸 및 MIME 처리기로 등록 됩니다.  
  
- 느슨하게 압축되지 않은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일(.xaml).  
  
- [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)](.xbap).  
  
 이러한 형식의 파일에 대해서는 WPF (Windows Presentation Foundation) 호스트:  
  
- Windows Presentation Foundation (WPF) 콘텐츠를 호스팅하기 위해 등록 된 HTML 처리기를 시작 합니다.  
  
- 필요한 CLR (공용 언어 런타임) 및 Windows Presentation Foundation (WPF) 어셈블리의 올바른 버전을 로드 합니다.  
  
- 배포 영역에 대해 적절한 권한 수준이 설정되어 있는지 확인합니다.  
  
 이 항목에서는 PresentationHost.exe에서 사용할 수 있는 명령줄 매개 변수를 설명합니다.  
  
## <a name="usage"></a>용도  
 `PresentationHost.exe [parameters] uri|filename`  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|filename|활성화할 파일의 경로입니다. [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]가 될 수도 있습니다.|  
|-debug|애플리케이션을 활성화할 때 저장소에서 커밋하거나 실행하지 않습니다. 이는 로컬 파일이 활성화된 경우에만 작동합니다.|  
|-debugSecurityZoneURL \<url>|URL 값과 함께 사용 하 여 지정 된 URL에서 응용 프로그램을 배포 하는 것 처럼 응용 프로그램을 Presentationhost.exe에 지정 합니다. 이를 통해 배포 영역과 원본 사이트가 모두 결정됩니다.|  
|-embedding|OLE에 필요합니다. `-event` 또는 `-debug` 매개 변수가 지정된 경우 `-embedding` 매개 변수가 내부적으로 설정되기 때문에 해당 매개 변수를 지정할 필요가 없습니다.|  
|-event \<eventname>|이 이름으로 이벤트를 연 다음 PresentationHost.exe가 초기화되고 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 콘텐츠를 호스팅할 준비가 되면 이 이벤트에 신호를 보냅니다. 이벤트가 아직 만들어지지 않은 등의 이유로 인해 이벤트를 여는 데 오류가 발생하면 PresentationHost.exe가 종료됩니다.|  
|-launchApplication \<url>|지정 된 URL에서 독립 실행형 ClickOnce 응용 프로그램을 시작 합니다. .NET 응용 프로그램과 관련 된 Internet Explorer 및 WinINet 보안 정책이 적용 됩니다.|  
  
## <a name="scenarios"></a>시나리오  
  
### <a name="shell-handler"></a>셸 처리기  
 `PresentationHost.exe example.xbap`  
  
### <a name="mime-handler"></a>MIME 처리기  
 `PresentationHost.exe -embedding example.xbap`  
  
### <a name="visual-studio-debugging"></a>Visual Studio 디버깅  
 `PresentationHost.exe -debug example.xbap`  
  
### <a name="visual-studio-debugging-in-zone"></a>영역에서 Visual Studio 디버깅  
 `PresentationHost.exe -debug -debugSecurityZoneURL http://www.example.com c:\folderpath\example.xbap`  
  
## <a name="see-also"></a>참조

- [보안](../security-wpf.md)
