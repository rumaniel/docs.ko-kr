---
title: UI 자동화를 사용하여 텍스트 이동
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, traversing text
- text, traversing
- traversing text
ms.assetid: 3ddb3b7b-1d6b-4dba-8678-5a68e868aadb
author: Xansky
ms.author: mhopkins
ms.openlocfilehash: ad903efcf03eae346233f4eb84e61ca407336de9
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205245"
---
# <a name="traverse-text-using-ui-automation"></a>UI 자동화를 사용하여 텍스트 이동
> [!NOTE]
>  이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에 대한 최신 정보는 [Windows 자동화 API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746)를 참조하세요.  
  
 이 항목에서는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 을 사용하여 <xref:System.Windows.Automation.Text.TextUnit> 씩 증가시켜 문서의 텍스트 내용을 트래버스하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 UI 자동화 텍스트 공급자의 콘텐츠를 트래버스하는 방법을 보여 줍니다. <xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 메서드는 <xref:System.Windows.Automation.Text.TextPatternRange>의 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 및 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 엔드포인트를 이동합니다. 이 텍스트 범위는 일반적으로 텍스트 삽입 지점을 나타내는 중복 제거 범위입니다.  
  
> [!NOTE]
>  텍스트 기반의 포함된 개체만 텍스트 스트림의 일부로 간주되므로, 이미지 등과 같은 포함된 개체는 `Move` 또는 해당 반환 값에 영향을 주지 않습니다.  
  
[!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
[!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#Navigate](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#navigate)]
[!code-vb[FindText#Navigate](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#navigate)]  
  
 제공된 <xref:System.Windows.Automation.Text.TextUnit> 이 컨트롤에서 지원되지 않으면 <xref:System.Windows.Automation.Text.TextUnit> 를 사용하는 모든 메서드는 다음으로 큰 크기의 지원되는 <xref:System.Windows.Automation.Text.TextUnit> 을 따릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [UI 자동화 TextPattern 개요](../../../docs/framework/ui-automation/ui-automation-textpattern-overview.md)  
 [UI 자동화를 사용하여 텍스트 상자에 콘텐츠 추가](../../../docs/framework/ui-automation/add-content-to-a-text-box-using-ui-automation.md)  
 [UI 자동화를 사용하여 텍스트 찾기 및 강조](../../../docs/framework/ui-automation/find-and-highlight-text-using-ui-automation.md)  
 [UI 자동화 컨트롤 패턴 개요](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)  
 [클라이언트용 UI 자동화 컨트롤 패턴](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
