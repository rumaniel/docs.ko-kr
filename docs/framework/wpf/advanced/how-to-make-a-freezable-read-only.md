---
title: '방법: Freezable을 읽기 전용으로 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Freezable objects [WPF], making read-only
ms.assetid: 6c544b7d-d3c9-4736-aa90-4b8728234ccb
ms.openlocfilehash: 5748b7929db18578bbe00e3217b1578ac5fbc0f4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614599"
---
# <a name="how-to-make-a-freezable-read-only"></a>방법: Freezable을 읽기 전용으로 설정
확인 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Freezable> 를 호출 하 여 읽기 전용으로 해당 <xref:System.Windows.Freezable.Freeze%2A> 메서드.  
  
 고정할 수 없습니다는 <xref:System.Windows.Freezable> 경우 다음 조건 중 하나는 개체 `true` 개체에 대 한 합니다.  
  
- 애니메이션 효과가 적용 또는 데이터 바인딩된 속성입니다.  
  
- 동적 리소스에 의해 설정 된 속성이 있습니다. 동적 리소스에 대 한 자세한 내용은 참조는 [XAML 리소스](xaml-resources.md)합니다.  
  
- 포함 된 <xref:System.Windows.Freezable> 고정할 수 없는 하위 개체입니다.  
  
 이러한 조건이 `false` 에 대 한 프로그램 <xref:System.Windows.Freezable> 개체 숨기지 않으려면 수정, 성능 이점을 얻을 수 고정 하는 것이 좋습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 고정 된 <xref:System.Windows.Media.SolidColorBrush>의 형식인 <xref:System.Windows.Freezable> 개체입니다.  
  
 [!code-csharp[freezablesample_procedural#FreezeExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#freezeexample1)]
 [!code-vb[freezablesample_procedural#FreezeExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#freezeexample1)]  
  
 에 대 한 자세한 내용은 <xref:System.Windows.Freezable> 개체를 참조 합니다 [Freezable 개체 개요](freezable-objects-overview.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Freezable>
- <xref:System.Windows.Freezable.CanFreeze%2A>
- <xref:System.Windows.Freezable.Freeze%2A>
- [Freezable 개체 개요](freezable-objects-overview.md)
- [방법 항목](base-elements-how-to-topics.md)
