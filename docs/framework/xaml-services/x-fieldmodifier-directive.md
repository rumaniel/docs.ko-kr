---
title: x:FieldModifier 지시문
ms.date: 03/30/2017
helpviewer_keywords:
- FieldModifier attribute in XAML [XAML Services]
- x:FieldModifier attribute [XAML Services]
- XAML [XAML Services], x:FieldModifier attribute
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
ms.openlocfilehash: 646ad1ca99d83f9fb2994f3c394eca27a60c0eac
ms.sourcegitcommit: 4b9c2d893b45d47048c6598b4182ba87759b1b59
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68484730"
---
# <a name="xfieldmodifier-directive"></a>x:FieldModifier 지시문
명명 된 개체 참조에 대 한 필드가 <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> 기본 동작 대신 access로 정의 되도록 XAML 컴파일 동작을 수정 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object x:FieldModifier="Public".../>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|*공개*|<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> 지정<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> 하기 위해 전달 하는 정확한 문자열은 사용 되는 코드 지향 프로그래밍 언어에 따라 달라 집니다. 설명 부분을 참조하세요.|  
  
## <a name="dependencies"></a>종속성  
 Xaml 프로덕션에서 아무 곳 `x:FieldModifier` 이나 사용 하는 경우 해당 xaml 프로덕션의 루트 요소는 [x:Class 지시문](x-class-directive.md)을 선언 해야 합니다.  
  
## <a name="remarks"></a>설명  
 `x:FieldModifier`는 클래스 또는 해당 멤버의 일반 액세스 수준을 선언 하는 것과 관련이 없습니다. Xaml 프로덕션의 일부인 특정 XAML 개체가 처리 되 고 응용 프로그램의 개체 그래프에서 잠재적으로 액세스할 수 있는 개체가 되는 경우 XAML 처리 동작과 관련이 있습니다. 기본적으로 이러한 개체에 대 한 필드 참조는 private으로 유지 되므로 컨트롤 소비자는 개체 그래프를 직접 수정할 수 없습니다. 대신, 컨트롤 소비자는 레이아웃 루트, 자식 요소 컬렉션, 전용 공용 속성 등을 가져오는 등의 프로그래밍 모델에 사용 되는 표준 패턴을 사용 하 여 개체 그래프를 수정 해야 합니다.  
  
 `x:FieldModifier` 특성의 값은 프로그래밍 언어에 따라 다르며 용도는 특정 프레임 워크에 따라 다를 수 있습니다. 사용할 문자열은 각 언어 <xref:System.CodeDom.Compiler.CodeDomProvider> 에서 및 <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>에 대 한 <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> 의미를 정의 하기 위해 반환 하는 형식 변환기와 해당 언어가 대/소문자를 구분 하는지 여부에 따라 달라 집니다.  
  
- 의 C#경우를 지정 <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> 하기 위해 전달할 문자열은 `public`입니다.  
  
- Microsoft Visual Basic .net의 경우를 지정 <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> `Public`하기 위해 전달할 문자열은입니다.  
  
- /Cli C++의 경우 XAML에 대 한 대상이 현재 존재 하지 않습니다. 따라서 전달할 문자열이 정의 되지 않습니다.  
  
 ( <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> `Friend` <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> `NotPublic` 의 경우 C#) Visual Basic를 지정할 수도 있지만, 동작이 이미 기본값 이기 때문에를 지정 하는 것은 비정상입니다.`internal`  
  
 <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>는 XAML을 컴파일한 어셈블리 외부의 코드에는 XAML 생성 요소에 대 한 액세스 권한이 필요 하기 때문에 기본 동작입니다. WPF 보안 아키텍처는 XAML 컴파일 동작과 함께 공용 액세스 `x:FieldModifier` 를 허용 하도록를 특별히 설정 하지 않는 한, 요소 인스턴스를 공용으로 저장 하는 필드를 선언 하지 않습니다.  
  
 `x:FieldModifier`는 public 인 필드를 참조 하는 데 사용 되므로 [X:Name 지시문](x-name-directive.md) 이 있는 요소에만 해당 됩니다.  
  
 기본적으로 루트 요소에 대 한 partial 클래스는 public입니다. 그러나 [X:classmodifier 지시어](x-classmodifier-directive.md)를 사용 하 여 public을 만들 수 있습니다. [X:classmodifier 지시문](x-classmodifier-directive.md) 은 루트 요소 클래스 인스턴스의 액세스 수준에도 영향을 줍니다. Root 요소에 및 `x:Name` `x:FieldModifier` 를 둘 다 넣을 수 있지만이 경우 root 요소의 public 필드 복사본만 적용 됩니다 .이는 true 루트 요소 클래스 액세스 수준이 [x:classmodifier 지시문](x-classmodifier-directive.md)에 의해 제어 됩니다.  
  
## <a name="see-also"></a>참고자료

- [WPF에 대한 XAML 및 사용자 지정 클래스](../wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [WPF의 코드 숨김 및 XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [x:Name 지시문](x-name-directive.md)
- [WPF 응용 프로그램 빌드(WPF)](../wpf/app-development/building-a-wpf-application-wpf.md)
- [x:ClassModifier 지시문](x-classmodifier-directive.md)
