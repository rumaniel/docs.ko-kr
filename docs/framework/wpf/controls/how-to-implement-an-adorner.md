---
title: '방법: 표시기(Adorner) 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], implementing
ms.assetid: 56ae32b6-0599-455c-b52f-2ff97e6f1ec2
ms.openlocfilehash: da318fee42b4628351217774de2a2225cfb21ee1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770983"
---
# <a name="how-to-implement-an-adorner"></a>방법: 표시기(Adorner) 구현
이 예제에서는 최소 표시기 구현을 보여 줍니다.  
  
## <a name="notes-for-implementers"></a>구현자 참고 사항  
 표시기에는 고유 렌더링 동작이 포함되어 있지 않음에 유의해야 합니다. 표시기를 렌더링하는 것은 표시기 구현자의 책임입니다.   렌더링 동작을 구현 하는 일반적인 방법은 재정의 하는 것을 <xref:System.Windows.UIElement.OnRender%2A> 메서드 및 사용법 하나 이상의 <xref:System.Windows.Media.DrawingContext> (이 예제 에서처럼) 필요에 따라 표시기의 시각적 개체를 렌더링 하는 개체입니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 추상에서 상속 되는 클래스를 구현 하 여 사용자 지정 표시기 만들어집니다 <xref:System.Windows.Documents.Adorner> 클래스입니다.  표시기 예제에서는의 모서리를 원으로 간단히 표시를 <xref:System.Windows.UIElement> 재정의 하 여 원으로 <xref:System.Windows.UIElement.OnRender%2A> 메서드.  
  
### <a name="code"></a>코드  
 [!code-csharp[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_simplecircleadornerbody)]
 [!code-vb[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_simplecircleadornerbody)]  
  
## <a name="see-also"></a>참고자료

- [표시기 개요](adorners-overview.md)
