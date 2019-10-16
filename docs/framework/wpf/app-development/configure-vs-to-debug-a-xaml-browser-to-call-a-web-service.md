---
title: '방법: Visual Studio를 구성하여 웹 서비스를 호출하는 XAML 브라우저 응용 프로그램 디버깅'
ms.date: 03/30/2017
helpviewer_keywords:
- debugging XBAPs that call a Web service [WPF]
- debugging security exceptions for XBAPs [WPF]
- security exception for XBAPs [WPF], debugging
- configuring Visual Studio to debug XAML browser applications [WPF]
- configuring Visual Studio to debug XBAPs [WPF]
ms.assetid: fd1db082-a7bb-4c4b-9331-6ad74a0682d0
ms.openlocfilehash: 8ec278f2bc66d9b40786123af684f6468b6a9d83
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005678"
---
# <a name="how-to-configure-visual-studio-to-debug-a-xaml-browser-application-to-call-a-web-service"></a>방법: Visual Studio를 구성하여 웹 서비스를 호출하는 XAML 브라우저 응용 프로그램 디버깅
[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]은 인터넷 영역 권한 집합으로 제한 된 부분 신뢰 보안 샌드박스 내에서 실행 됩니다. 이 권한 집합은 @no__t 0 응용 프로그램의 원본 사이트에 있는 웹 서비스로만 웹 서비스 호출을 제한 합니다. 그러나 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]이 Visual Studio 2005에서 디버그 되는 경우 참조 하는 웹 서비스와 동일한 원본 사이트를 포함 하지 않는 것으로 간주 됩니다. 이렇게 하면 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]에서 웹 서비스를 호출 하려고 할 때 보안 예외가 발생 합니다. 그러나 Visual Studio 2005 [!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)] 프로젝트는 디버깅 하는 동안 호출 하는 웹 서비스와 동일한 원본 사이트를 시뮬레이션 하도록 구성할 수 있습니다. 이렇게 하면 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]에서 보안 예외를 발생 시 키 지 않고 웹 서비스를 안전 하 게 호출할 수 있습니다.

## <a name="configuring-visual-studio"></a>Visual Studio 구성
 웹 서비스를 호출 하는 @no__t 0을 디버깅 하도록 Visual Studio 2005를 구성 하려면:

1. **솔루션 탐색기**에서 프로젝트를 선택한 상태에서 **프로젝트** 메뉴에서 **속성**을 클릭합니다.

2. **프로젝트 디자이너**에서 **디버그** 탭을 클릭 합니다.

3. **시작 작업** 섹션에서 **시작 외부 프로그램** 을 선택 하 고 다음을 입력 합니다.

     `C:\WINDOWS\System32\PresentationHost.exe`

4. **시작 옵션** 섹션에서 **명령줄 인수** 텍스트 상자에 다음을 입력 합니다.

     `-debug`  *filename*

     **-Debug** 매개 변수에 대 한 *파일 이름* 값은 xbap 파일 이름입니다. 예를 들어:

     `-debug c:\example.xbap`

> [!NOTE]
> Visual Studio 2005 [!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)] 프로젝트 템플릿을 사용 하 여 만든 솔루션에 대 한 기본 구성입니다.

1. **솔루션 탐색기**에서 프로젝트를 선택한 상태에서 **프로젝트** 메뉴에서 **속성**을 클릭합니다.

2. **프로젝트 디자이너**에서 **디버그** 탭을 클릭 합니다.

3. **시작 옵션** 섹션의 명령줄 **인수** 텍스트 상자에 다음 명령줄 매개 변수를 추가 합니다.

     `-debugSecurityZoneURL`  *URL*

     **-DebugSecurityZoneURL** 매개 변수에 대 한 *URL* 값은 응용 프로그램의 출처를 시뮬레이션 하는 데 사용할 위치에 대 한 @no__t 2입니다.

 예를 들어 다음 URL을 사용 하 여 웹 서비스를 사용 하는 [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]을 고려 합니다.

 `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`

 이 웹 서비스의 원본 사이트 URL은 다음과 같습니다.

 `http://services.msdn.microsoft.com`

 따라서 **debugSecurityZoneURL** 명령줄 매개 변수 및 값은 다음과 같습니다.

 `-debugSecurityZoneURL http://services.msdn.microsoft.com`

## <a name="see-also"></a>참조

- [WPF 호스트(PresentationHost.exe)](wpf-host-presentationhost-exe.md)
