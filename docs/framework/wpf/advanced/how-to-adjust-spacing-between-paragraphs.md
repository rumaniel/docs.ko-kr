---
title: '방법: 단락 사이 간격 조정'
ms.date: 03/30/2017
helpviewer_keywords:
- spacing between paragraphs [WPF]
- paragraphs [WPF], spacing between
- documents [WPF], adjusting spacing between paragraphs
ms.assetid: 7cd2f2ac-0e19-4587-bfb6-7f5b18c9536e
ms.openlocfilehash: e2a6ba34e3ab15eb316671fef7c11bea03d53c73
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777015"
---
# <a name="how-to-adjust-spacing-between-paragraphs"></a>방법: 단락 사이 간격 조정
이 예제에서는 유동 콘텐츠에 단락 사이 간격을 줄이거나 조정 하는 방법을 보여 줍니다.  
  
 유동 콘텐츠를 단락 사이 나타나는 추가 공간이 여백 이러한 단락은; 설정의 결과 따라서 이러한 단락에 여백을 조정 하 여 단락 사이 간격을 제어할 수 있습니다.  두 단락 사이의 추가 간격을 완전히 제거 하려면 단락의 여백을 설정할 **0**합니다.  전체에서 단락 사이의 일정 한 간격을 달성 하기 위해 <xref:System.Windows.Documents.FlowDocument>, 모든 단락에 대해 균일 한 여백이 값을 설정 하는 스타일을 사용 합니다 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 인접 한 두 단락에 대 한 여백 됩니다 "축소"를 참고 하는 두 가지 여백 중 더 큰 것이 아니라 두 배가 사항을 두는 것이 반드시 합니다. 따라서 인접 한 두 단락이 20 픽셀이 고 40 픽셀의 여백을 각각 단락 사이의 간격은 두 여백 값 중 더 큰 40 픽셀입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 스타일 지정을 사용 하 여 모든 여백을 설정 하려면 <xref:System.Windows.Documents.Paragraph> 의 요소를 <xref:System.Windows.Documents.FlowDocument> 에 **0**, 단락 사이 공백의 효과적으로 제거는 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 [!code-xaml[BlockSnippets#_ParagraphSpacingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/BlockSnippets/CSharp/Window1.xaml#_paragraphspacingxaml)]
