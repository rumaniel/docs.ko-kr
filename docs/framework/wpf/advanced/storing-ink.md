---
title: 잉크 저장
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ISF (Ink Serialized Format)
- storing ink [WPF]
- ink [WPF], storing
- retrieving ink [WPF]
- Ink Serialized Format (ISF)
ms.assetid: a3f6d16b-d682-4680-9965-907332b4d2b8
ms.openlocfilehash: 4089aa7942105c14eb628c75edb7f53ffacfaeb0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053376"
---
# <a name="storing-ink"></a>잉크 저장
<xref:System.Windows.Ink.StrokeCollection.Save%2A> 메서드 잉크로 잉크 직렬화 형식 ISF ()를 저장 하는 것에 대 한 지원을 제공 합니다. 에 대 한 생성자는 <xref:System.Windows.Ink.StrokeCollection> 클래스 잉크 데이터를 읽기 위한 지원을 제공 합니다.  
  
## <a name="ink-storage-and-retrieval"></a>잉크 저장 및 검색  
 이 섹션에 저장 하 고 잉크를 검색 하는 방법에 설명 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 플랫폼입니다.  
  
 다음 예제에서는 파일 저장 대화 상자를 사용 하 여 사용자를 표시 하 고에서 잉크를 저장 하는 단추 클릭 이벤트 처리기를 구현 하는 <xref:System.Windows.Controls.InkCanvas> 파일로 아웃 합니다.  
  
 [!code-csharp[DigitalInkTopics#12](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#12)]
 [!code-vb[DigitalInkTopics#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#12)]  
  
 다음 예제에서는 구현 파일에서 잉크를 읽고 파일 열기 대화 상자를 사용 하 여 사용자를 표시 하는 단추 클릭 이벤트 처리기는 <xref:System.Windows.Controls.InkCanvas> 요소입니다.  
  
 [!code-csharp[DigitalInkTopics#13](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#13)]
 [!code-vb[DigitalInkTopics#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#13)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.InkCanvas>
- [Windows Presentation Foundation](../index.md)
