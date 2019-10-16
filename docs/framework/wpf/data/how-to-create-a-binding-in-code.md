---
title: '방법: 코드에서 바인딩 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binding data [WPF], creating
- data binding [WPF], creating
ms.assetid: 1a606db9-cf5f-42ed-a1c5-9e4722ec77a0
ms.openlocfilehash: 57ec845c5c9a5bddb801428b9ecde035a97cf447
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931627"
---
# <a name="how-to-create-a-binding-in-code"></a>방법: 코드에서 바인딩 만들기
만들고 설정 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Data.Binding> 코드에서입니다.  
  
## <a name="example"></a>예제  
 합니다 <xref:System.Windows.FrameworkElement> 클래스 및 <xref:System.Windows.FrameworkContentElement> 둘 다 노출 하는 클래스를 `SetBinding` 메서드. 이러한 클래스 중 하나를 상속 하는 요소에 바인딩하는 경우 호출할 수 있습니다는 <xref:System.Windows.FrameworkElement.SetBinding%2A> 메서드를 직접.  
  
 다음 예제에서는 라는 클래스를 만듭니다 `MyData`에 라는 속성이 포함 된 `MyDataProperty`합니다.  
  
 [!code-csharp[CodeOnlyBinding#DataObject](~/samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/MyData.cs#dataobject)]
 [!code-vb[CodeOnlyBinding#DataObject](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/MyData.vb#dataobject)]  
  
 다음 예제에서는 바인딩의 원본을 설정 하려면 바인딩 개체를 만드는 방법을 보여 줍니다.  예제에서는 <xref:System.Windows.FrameworkElement.SetBinding%2A> 바인딩할 합니다 <xref:System.Windows.Controls.TextBlock.Text%2A> 속성을 `myText`는 <xref:System.Windows.Controls.TextBlock> 컨트롤에 `MyDataProperty`.  
  
 [!code-csharp[CodeOnlyBinding#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#1)]
 [!code-vb[CodeOnlyBinding#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#1)]  
  
 전체 코드 샘플을 보려면 [코드 전용 Binding 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771500(v=vs.90))합니다.  
  
 호출 하는 대신 <xref:System.Windows.FrameworkElement.SetBinding%2A>를 사용할 수는 <xref:System.Windows.Data.BindingOperations.SetBinding%2A> 의 정적 메서드는 <xref:System.Windows.Data.BindingOperations> 클래스입니다. 다음 예에서는 호출 <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType> of <xref:System.Windows.FrameworkElement.SetBinding%2A?displayProperty=nameWithType> 바인딩할 `myText` 에 `myDataProperty`입니다.  
  
 [!code-csharp[CodeOnlyBinding#BOSetBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#bosetbinding)]
 [!code-vb[CodeOnlyBinding#BOSetBinding](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#bosetbinding)]  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
