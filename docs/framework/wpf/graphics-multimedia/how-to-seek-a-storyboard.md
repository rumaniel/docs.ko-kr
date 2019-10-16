---
title: '방법: 스토리보드 검색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], seeking
- seeking Storyboards [WPF]
ms.assetid: 887bb39a-0c2a-4ae8-956d-1d9f6f8ebbfc
ms.openlocfilehash: a57272c17a5bc6f5baaa21fb77233fc5693d1914
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651222"
---
# <a name="how-to-seek-a-storyboard"></a>방법: 스토리보드 검색
다음 예제에서는 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 메서드를 <xref:System.Windows.Media.Animation.Storyboard> storyboard 애니메이션에서 임의 위치로 이동 합니다.  
  
## <a name="example"></a>예제  
 다음은 샘플에 대한 XAML 태그입니다.  
  
 [!code-xaml[SeekStoryboard_snip#SeekStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/SeekStoryboard_snip/CSharp/SeekStoryboardExample.xaml#seekstoryboardexamplewholepage)]  
  
## <a name="example"></a>예제  
 다음은 위의 XAML 코드와 함께 사용되는 코드입니다.  
  
 [!code-csharp[SeekStoryboard_snip#SeekStoryboardCodeBehindExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/SeekStoryboard_snip/CSharp/SeekStoryboardExample.xaml.cs#seekstoryboardcodebehindexamplewholepage)]
 [!code-vb[SeekStoryboard_snip#SeekStoryboardCodeBehindExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SeekStoryboard_snip/VisualBasic/SeekStoryboardExample.xaml.vb#seekstoryboardcodebehindexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [동기적으로 Storyboard 검색](how-to-seek-a-storyboard-synchronously.md)
