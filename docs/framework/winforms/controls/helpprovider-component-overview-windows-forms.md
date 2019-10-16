---
title: HelpProvider 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- HelpProvider
helpviewer_keywords:
- HelpProvider component [Windows Forms], about HelpProvider component
- Help [Windows Forms], adding to Windows applications
- F1 Help [Windows Forms], adding to Windows Forms
- dialog boxes [Windows Forms], context-sensitive Help
- Windows Forms, context-sensitive Help
ms.assetid: 6b10c2cc-c577-4cb5-9669-e37b33416af9
ms.openlocfilehash: cefc590bb3011b282392504a78ac5c393c58493e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965690"
---
# <a name="helpprovider-component-overview-windows-forms"></a>HelpProvider 구성 요소 개요(Windows Forms)
Windows Forms [HelpProvider](helpprovider-component-windows-forms.md) 구성 요소는 Windows 응용 프로그램에서 html 도움말 1.x 도움말 파일 (Html 도움말 워크숍을 사용 하 여 생성 된 .chm 파일 또는 .htm 파일)을 연결 하는 데 사용 됩니다. 다음과 같은 다양 한 방법으로 도움말을 제공할 수 있습니다.  
  
- Windows Forms의 컨트롤에 대 한 상황에 맞는 도움말을 제공 합니다.  
  
- 특정 대화 상자 또는 대화 상자의 특정 컨트롤에 대 한 상황에 맞는 도움말을 제공 합니다.  
  
- 목차, 인덱스 또는 검색 함수의 기본 페이지와 같은 특정 영역에 대 한 도움말 파일을 엽니다.  
  
## <a name="using-the-help-provider"></a>도움말 공급자 사용  
 Windows form에 <xref:System.Windows.Forms.HelpProvider> 구성요소를추가하면양식의다른컨트롤이구성요소의도움말속성을<xref:System.Windows.Forms.HelpProvider> 노출할 수 있습니다. 이렇게 하면 Windows Form의 컨트롤에 대 한 도움말을 제공할 수 있습니다. 속성<xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 을 사용 하 여 도움말 파일을 <xref:System.Windows.Forms.HelpProvider> 구성 요소와 연결할 수 있습니다. 를 호출 <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> 하 고 지정 된 컨트롤에 대 한 <xref:System.Windows.Forms.HelpNavigator> 열거형의 값을 제공 하 여 제공 되는 도움말 형식을 지정 합니다. 메서드를 <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> 호출 하 여 도움말에 대 한 키워드 또는 항목을 제공 합니다.  
  
 필요에 따라 특정 도움말 문자열을 다른 컨트롤과 연결 하려면 <xref:System.Windows.Forms.HelpProvider.SetHelpString%2A> 메서드를 사용 합니다. 이 메서드를 사용 하는 컨트롤을 사용 하 여 연결 하는 문자열은 컨트롤에 포커스가 있는 동안 사용자가 F1 키를 누를 때 팝업 창에 표시 됩니다.  
  
 가 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 설정 되지 않은 경우를 사용 <xref:System.Windows.Forms.HelpProvider.SetHelpString%2A> 하 여 도움말 텍스트를 제공 해야 합니다. 및 도움말 문자열을 모두 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 설정한 경우에는에 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 기반한 도움말이 우선적으로 적용 됩니다.  
  
> [!NOTE]
> 컨트롤의 <xref:System.Windows.Forms.Help.ShowHelp%2A> 메서드 또는 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 속성에서 도움말 파일의 경로를 지정 하는 경우 상대 경로를 사용 하는 데 문제가 발생할 수 있습니다. <xref:System.Windows.Forms.HelpProvider> 따라서 절대 파일 경로를 사용 하 여 도움말 파일을 지정 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms 응용 프로그램의 도움말 시스템](../advanced/help-systems-in-windows-forms-applications.md)
