---
title: '방법: 대화 상자 결과 반환'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dialog boxes [WPF], returning results
ms.assetid: 4c5cf286-746b-4052-934d-d80cbf8acba3
ms.openlocfilehash: 5e3670006762bcd09634b29314ecf2d05b1a44da
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968239"
---
# <a name="how-to-return-a-dialog-box-result"></a>방법: 대화 상자 결과 반환
이 예제에서는를 호출 <xref:System.Windows.Window.ShowDialog%2A>하 여 연 창에 대 한 대화 상자 결과를 검색 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 대화 상자를 닫기 전에 해당 <xref:System.Windows.Window.DialogResult%2A> 속성은 사용자가 대화 상자를 닫은 방법을 나타내는 <xref:System.Nullable%601> <xref:System.Boolean> 로 설정 되어야 합니다. 이 값은 클라이언트 코드 <xref:System.Windows.Window.ShowDialog%2A> 에서 대화 상자를 닫은 방법과 결과를 처리 하는 방법을 결정할 수 있도록에 의해 반환 됩니다.  
  
> [!NOTE]
> <xref:System.Windows.Window.DialogResult%2A>창이를 호출 <xref:System.Windows.Window.ShowDialog%2A>하 여 열린 경우에만 설정할 수 있습니다.  
  
 [!code-csharp[HOWTOWindowManagementSnippets#GetDialogResultCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#getdialogresultcode)]
 [!code-vb[HOWTOWindowManagementSnippets#GetDialogResultCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#getdialogresultcode)]  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 를 <xref:System.Windows.Window.ShowDialog%2A> 호출 하려면 제한 없이 모든 창과 사용자 입력 이벤트를 사용할 수 있는 권한이 필요 합니다.
