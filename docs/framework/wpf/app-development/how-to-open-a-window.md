---
title: '방법: 창 열기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- windows [WPF], opening
- opening windows [WPF]
ms.assetid: 6b91b2bb-fda7-491d-a72e-139dd630a5b0
ms.openlocfilehash: 9ce7ffb3f46dd869fda7893745b531bd02d18ee1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947682"
---
# <a name="how-to-open-a-window"></a>방법: 창 열기
이 예제에는 창을 여는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 인스턴스화하여 창이 열리기 <xref:System.Windows.Window> 호출을 <xref:System.Windows.Window.Show%2A> 메서드. <xref:System.Windows.Window.Show%2A> 창을 열고 새 창이 닫힐 때까지 기다리지 않고 즉시 반환 합니다. 이 창 유형에 라고도 *모덜리스* 창 하며 사용자 입력을 제한 하지 않습니다.  
  
 [!code-csharp[HOWTOWindowManagementSnippets#OpenNewWindowCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#opennewwindowcode)]
 [!code-vb[HOWTOWindowManagementSnippets#OpenNewWindowCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#opennewwindowcode)]  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 인스턴스화 <xref:System.Windows.Window> 안전 하지 않은 네이티브 메서드를 호출 하기 위한 권한이 필요 (참조 <xref:System.Windows.Window.%23ctor%2A>).
