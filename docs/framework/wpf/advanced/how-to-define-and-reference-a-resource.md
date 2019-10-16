---
title: '방법: 리소스 정의 및 참조'
ms.date: 03/30/2017
helpviewer_keywords:
- resources [WPF], defining
- defining resources [WPF]
- resources [WPF], referencing
- referencing resources [WPF]
ms.assetid: b86b876b-0a10-489b-9a5d-581ea9b32406
ms.openlocfilehash: 80be1460906100072e6263c967c213df7968c705
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776508"
---
# <a name="how-to-define-and-reference-a-resource"></a>방법: 리소스 정의 및 참조

이 예제에서는 리소스 정의의 특성을 사용 하 여 참조 하는 방법을 보여 줍니다 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]합니다.

## <a name="example"></a>예제

다음 예제에서는 두 가지 유형의 리소스를 정의 합니다:는 <xref:System.Windows.Media.SolidColorBrush> 리소스 및 여러 <xref:System.Windows.Style> 리소스입니다. 합니다 <xref:System.Windows.Media.SolidColorBrush> 리소스 `MyBrush` 는 몇 가지 속성의 값을 제공 하는 데 사용 되는 <xref:System.Windows.Media.Brush> 값을 입력 합니다. <xref:System.Windows.Style> 리소스 `PageBackground`, `TitleText` 고 `Label` 각 대상 특정 컨트롤 형식입니다. 해당 스타일 리소스가 리소스 키로 참조 되 고 설정 하는 경우 스타일은 대상된 컨트롤에서 다양 한 속성을 설정 합니다 <xref:System.Windows.FrameworkElement.Style%2A> 속성으로 정의 된 몇 가지 특정 컨트롤 요소의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다.

setter 내 참고 속성 중 하나는 `Label` 스타일 참조를 `MyBrush` 앞에서 정의한 리소스입니다. 이 일반적인 기술 이지만 리소스 구문 분석 되 고 제공 된 순서로 리소스 사전에 입력을 고려해 야 합니다. 리소스 또한 사용 하는 경우 사전 내에서 발견 되는 순서로 요청을 [StaticResource 태그 확장](staticresource-markup-extension.md) 다른 리소스 내에서 참조 합니다. 참조 하는 모든 리소스는 해당 리소스가 요청 보다 리소스 컬렉션 내에서 이전 정의 되어 있는지 확인 합니다. 하는 경우 필요에 따라 해결할 수 있습니다 리소스 참조의 엄격한 생성 순서를 사용 하 여는 [DynamicResource 태그 확장](dynamicresource-markup-extension.md) 런타임 시 리소스를 대신 참조 하도록 알아야 하지만이 DynamicResource 기술 성능 결과가 발생 합니다. 자세한 내용은 참조 하세요 [XAML 리소스](xaml-resources.md)합니다.

[!code-xaml[FEResource#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResource/CS/default.xaml#xaml)]

## <a name="see-also"></a>참고자료

- [XAML 리소스](xaml-resources.md)
- [스타일 지정 및 템플릿](../controls/styling-and-templating.md)
