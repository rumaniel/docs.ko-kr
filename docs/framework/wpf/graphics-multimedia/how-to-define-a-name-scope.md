---
title: '방법: 이름 범위 정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- name scope [WPF], defining
- Storyboards [WPF], animating in procedural code
- animation [WPF], Storyboards [WPF], in procedural code
ms.assetid: 4f361925-6a08-40dc-8231-a61111c6b28b
ms.openlocfilehash: a03f477dd31909e8cb9dde9cd29da6f38d665758
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904152"
---
# <a name="how-to-define-a-name-scope"></a>방법: 이름 범위 정의
애니메이션 효과 주려는 <xref:System.Windows.Media.Animation.Storyboard> 코드에서 만들어야 합니다를 <xref:System.Windows.NameScope> 하 고 해당 이름 범위를 소유 하는 요소를 사용 하 여 대상 개체의 이름을 등록 합니다. 다음 예제에서는 <xref:System.Windows.NameScope> 만들어집니다 `myMainPanel`합니다. 두 개의 단추 `button1` 및 `button2`, 패널 및 이름을 등록에 추가 됩니다. 여러 애니메이션 및 <xref:System.Windows.Media.Animation.Storyboard> 만들어집니다. 스토리 보드의 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드는 애니메이션을 시작 하는 데 사용 됩니다.  
  
 때문에 `button1`, `button2`, 및 `myMainPanel` 모두 동일한 이름 범위를 공유, 이들 중 하나가 사용 될 수 있습니다 합니다 <xref:System.Windows.Media.Animation.Storyboard> <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 애니메이션을 시작 하는 방법입니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[StoryboardBeginAnimation_procedural_snip#NameScopeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/CSharp/ScopeExample.cs#namescopeexample)]
 [!code-vb[StoryboardBeginAnimation_procedural_snip#NameScopeExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/visualbasic/scopeexample.vb#namescopeexample)]  
  
## <a name="see-also"></a>참고자료

- [Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)
- [애니메이션 개요](animation-overview.md)
