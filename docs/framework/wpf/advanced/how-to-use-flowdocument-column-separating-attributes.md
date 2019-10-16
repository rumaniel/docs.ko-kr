---
title: '방법: FlowDocument 열 구분 특성 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- FlowDocument column-separating attributes
- column-separating attributes
- documents [WPF], FlowDocument column-separating attributes
ms.assetid: c7a822f8-aeca-45bd-a258-2852ff28005c
ms.openlocfilehash: 27491b21da587fa198061ba52d8daed5d3f28de3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032045"
---
# <a name="how-to-use-flowdocument-column-separating-attributes"></a>방법: FlowDocument 열 구분 특성 사용
열 구분 기능을 사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 정의 <xref:System.Windows.Documents.FlowDocument>를 설정 합니다 <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>, <xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A>, 및 <xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> 특성.  <xref:System.Windows.Documents.FlowDocument> 단일 단락 샘플 콘텐츠를 포함 합니다.  
  
 [!code-xaml[FlowDocumentSnippets#_FlowDocumentColumnStuffXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml#_flowdocumentcolumnstuffxaml)]  
  
 다음 그림의 효과 보여 줍니다.는 <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>, <xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A>, 및 <xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> 렌더링된 된 특성 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 ![FlowDocument 내부 열 특성을 보여 주는 스크린샷.](./media/how-to-use-flowdocument-column-separating-attributes/flowdocument-intra-column.png)
