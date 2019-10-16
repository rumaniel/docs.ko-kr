---
title: x:Null 태그 확장
ms.date: 03/30/2017
f1_keywords:
- NullExtension
- x:NullExtension
- x:Null
- "Null"
- xNull
helpviewer_keywords:
- Null markup extension in XAML [XAML Services]
- x:Null markup extension [XAML Services]
- XAML [XAML Services], x:Null markup extension
ms.assetid: 2e3ccc21-4996-481d-91b5-3910d8b3bfa3
ms.openlocfilehash: 7dbea2c7d4010d8defc572dbdc14a0dfd6d7601e
ms.sourcegitcommit: 4b9c2d893b45d47048c6598b4182ba87759b1b59
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68484716"
---
# <a name="xnull-markup-extension"></a>x:Null 태그 확장
을 `null` XAML 멤버에 대 한 값으로 지정 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object property="{x:Null}" .../>  
```  
  
## <a name="remarks"></a>설명  
 및 C# C++ 의 null 참조에 대 한 키워드가 null 인 경우 Null 참조 `Nothing`의 Microsoft Visual Basic 키워드는 이지만, xaml과 연결 하는 `{x:Null}` 코드 기반 언어에 관계 없이 항상 xaml 사용으로를 사용 합니다.  
  
 `x:Null` 태그 확장에 설정 가능한 속성이 없습니다.  
  
 Null 사용은 종종 CLR <xref:System.Nullable%601> 값의 XAML 멤버 노출에 연결 됩니다.  
  
 모든 `x:Null` XAML 태그 확장과 마찬가지로 태그 확장은 중괄호 (`{,}`)를 사용 하 여 특성 값의 처리를 리터럴 또는 이벤트 처리기 참조 이외의 값으로 이스케이프 합니다. 특성 구문은이 태그 확장에서 가장 자주 사용 되는 구문입니다. 개체 요소 구문은 `<x:Null />` 기술적으로 가능 하지만 `x:Null` 태그 확장에 위치 매개 변수 또는 생성 인수가 없기 때문에 거의 사용 되지 않습니다.  
  
 태그 확장에 대 한 자세한 내용은 [태그 확장 및 WPF XAML](../wpf/advanced/markup-extensions-and-wpf-xaml.md)을 참조 하세요.  
  
 .NET Framework XAML 서비스에서이 태그 확장에 대 한 처리는 <xref:System.Windows.Markup.NullExtension> 클래스에 의해 정의 됩니다.  
  
## <a name="wpf-usage-notes"></a>WPF 사용 정보  
 는 참조 형식 종속성 속성에 대 한 초기 설정 해제 값 이아닐수도있습니다.`null` 초기 기본값은 각 종속성 속성에 따라 다를 수 있으며 속성 관련 메타 데이터를 기반으로 할 수 있습니다. 많은 종속성 속성은 유효성 검사 `null` 콜백 구현 때문에 태그 또는 코드를 통해 값으로 허용 되지 않습니다. 종속성 속성에 대 한 자세한 내용은 [종속성 속성 개요](../wpf/advanced/dependency-properties-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.DependencyProperty.UnsetValue>
- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](../wpf/advanced/markup-extensions-and-wpf-xaml.md)
