---
title: '방법: 연결된 속성 등록'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- attached properties [WPF], registering
- registering attached properties [WPF]
ms.assetid: eb47bd94-0451-4f8d-8fb6-95f7812ac05b
ms.openlocfilehash: 4c678a64b62b8f4db24cf39ffbafac52e56c9982
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768682"
---
# <a name="how-to-register-an-attached-property"></a>방법: 연결된 속성 등록
이 예제에서는 연결된 속성을 등록하고 public 접근자를 제공하여 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]과 코드의 속성을 사용하는 방법을 보여 줍니다. 연결된 속성은 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]에서 정의한 구문 개념입니다. 대부분의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 형식에 연결된 속성도 종속성 속성으로 구현됩니다. 종속성 속성을 사용 하 여 모든 <xref:System.Windows.DependencyObject> 형식입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 연결된 된 속성을 사용 하 여 종속성 속성으로 등록 하는 방법의 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 메서드. 공급자 클래스에는 속성이 다른 클래스에 사용될 때 해당 클래스의 메타데이터를 재정의하지 않는 한 적용 가능한 속성에 대한 기본 메타데이터를 제공하는 옵션이 있습니다. 이 예제에서는 `IsBubbleSource` 속성의 기본값은 `false`로 설정됩니다.  
  
 종속성 속성으로 등록되지 않은 경우를 포함하여 연결된 속성에 대한 공급자 클래스는 명명 규칙 `Set`*[AttachedPropertyName]* 및 `Get`*[AttachedPropertyName]* 를 따르는 정적 get 및 set 접근자를 제공해야 합니다. 활성 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 판독기가 속성을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 특성으로 인식하고 적절한 형식을 확인할 수 있도록 이러한 접근자가 필요합니다.  
  
 [!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
 [!code-vb[WPFAquariumSln#RegisterAttachedBubbler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.DependencyProperty>
- [종속성 속성 개요](dependency-properties-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
- [방법 항목](properties-how-to-topics.md)
