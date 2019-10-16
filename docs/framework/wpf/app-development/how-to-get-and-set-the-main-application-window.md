---
title: '방법: 기본 애플리케이션 창 가져오기 및 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- windows objects [WPF], setting
- setting windows objects [WPF]
- windows objects [WPF], getting
- getting windows objects [WPF]
ms.assetid: ec902bc4-4a59-46f5-8ec1-963b46789356
ms.openlocfilehash: ea8333aa82f1159afb438215940ee1e7c2605e96
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947799"
---
# <a name="how-to-get-and-set-the-main-application-window"></a>방법: 기본 애플리케이션 창 가져오기 및 설정
이 예제에서는 기본 응용 프로그램 창 가져오기 및 설정 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 첫 번째 <xref:System.Windows.Window> 에서 응용 프로그램은 자동으로 설정 하는 Windows Presentation Foundation (WPF) 내에서 인스턴스화한 <xref:System.Windows.Application> 주 응용 프로그램 창으로 합니다. 첫 번째 <xref:System.Windows.Window> 인스턴스화된는 가능성이 가장 높은 수의 시작으로 지정 된 창에 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] (참조 <xref:System.Windows.Application.StartupUri%2A>).  
  
 첫 번째 <xref:System.Windows.Window> 코드를 사용 하 여 인스턴스화될 수 없습니다. 한 가지 예로 다음과 같은 응용 프로그램을 시작 하는 동안 창을 엽니다.  
  
 [!code-csharp[HOWTOWindowManagementSnippets#FirstWindowUsingCodeCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/App.xaml.cs#firstwindowusingcodecodebehind)]
 [!code-vb[HOWTOWindowManagementSnippets#FirstWindowUsingCodeCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/application.xaml.vb#firstwindowusingcodecodebehind)]  
  
 경우에 따라 첫 번째 인스턴스화된 <xref:System.Windows.Window> 는 실제로 기본 응용 프로그램 창 예: 시작 화면입니다. 이 경우 다음과 같은 태그를 사용 하는 기본 응용 프로그램 창을 지정할 수 있습니다.  
  
 [!code-xaml[ApplicationMainWindowSnippets#SetApplicationMainWindowXAML](~/samples/snippets/xaml/VS_Snippets_Wpf/ApplicationMainWindowSnippets/XAML/App.xaml#setapplicationmainwindowxaml)]  
  
 주 창에서 주 창 자동 또는 수동으로 지정 하는지 여부를 가져올 수 있습니다 <xref:System.Windows.Application.MainWindow%2A> 다음과 같이 다음 코드를 사용 합니다.  
  
 [!code-csharp[ApplicationMainWindowSnippets#GetApplicationMainWindowCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationMainWindowSnippets/CSharp/App.xaml.cs#getapplicationmainwindowcode)]
 [!code-vb[ApplicationMainWindowSnippets#GetApplicationMainWindowCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationMainWindowSnippets/visualbasic/application.xaml.vb#getapplicationmainwindowcode)]
