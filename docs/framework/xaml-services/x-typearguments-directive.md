---
title: x:TypeArguments 지시문
ms.date: 03/30/2017
f1_keywords:
- x:TypeArguments
- xTypeArguments
- TypeArguments
helpviewer_keywords:
- x:TypeArguments attribute [XAML Services]
- TypeArguments attribute in XAML [XAML Services]
- XAML [XAML Services], x:TypeArguments attribute
ms.assetid: 86561058-d393-4a44-b5c3-993a4513ea74
ms.openlocfilehash: a2a960870d368e57272b3368e69eb38ebbe2ba5d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053710"
---
# <a name="xtypearguments-directive"></a>x:TypeArguments 지시문
제네릭의 제약 조건 형식 인수를 제네릭 형식의 생성자에 전달 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object x:TypeArguments="typeString" .../>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`object`|CLR 제네릭 형식에 의해 지원 되는 XAML 형식의 개체 요소 선언입니다. 가 `object` 기본 xaml 네임 스페이스에 없는 xaml 형식을 참조 하는 경우에 `object` 는가 있는 xaml 네임 스페이스 `object` 를 나타내는 접두사가 필요 합니다.|  
|`typeString`|하나 이상의 XAML 형식 이름을 문자열로 선언 하는 문자열로, CLR 제네릭 형식에 대 한 형식 인수를 제공 합니다. 추가 구문 정보는 설명 부분을 참조 하십시오.|  
  
## <a name="remarks"></a>설명  
 대부분의 경우 `typeString` 문자열에서 정보 항목으로 사용 되는 XAML 형식에는 접두사가 붙습니다. 일반적인 형식의 clr 제네릭 제약 조건 (예: <xref:System.Int32> 및 <xref:System.String>)은 clr 기본 클래스 라이브러리에서 제공 됩니다. 이러한 라이브러리는 일반적인 프레임 워크 특정 기본 XAML 네임 스페이스에 매핑되지 않으므로 XAML 사용을 위해 접두사 매핑이 필요 합니다.  
  
 쉼표 구분 기호를 사용 하 여 둘 이상의 XAML 형식 이름을 지정할 수 있습니다.  
  
 제네릭 제약 조건 자체가 제네릭 형식을 사용 하는 경우 중첩 된 제약 조건 형식 인수는 괄호 ()에 포함 될 수 있습니다.  
  
 의 `x:TypeArguments` 이 정의는 .NET Framework XAML 서비스 및 CLR 지원 사용에만 적용 됩니다. 언어 수준 정의는 [ \[MS-XAML\] 섹션 5.3.11](https://go.microsoft.com/fwlink/?LinkId=114525)에서 찾을 수 있습니다.  
  
## <a name="usage-examples"></a>사용 예  
 이러한 예제에서는 다음 XAML 네임 스페이스 정의가 선언 된 것으로 가정 합니다.  
  
```xaml  
xmlns:sys="clr-namespace:System;assembly=mscorlib"  
xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
```  
  
### <a name="liststring"></a>목록\<문자열 >  
 `<scg:List x:TypeArguments="sys:String" ...>`<xref:System.String> 형식 인수를 <xref:System.Collections.Generic.List%601> 사용 하 여 새를 인스턴스화합니다.  
  
### <a name="dictionarystringstring"></a>사전\<문자열, 문자열 >  
 `<scg:Dictionary x:TypeArguments="sys:String,sys:String" ...>`두 개의 <xref:System.Collections.Generic.Dictionary%602> <xref:System.String> 형식 인수를 사용 하 여 새를 인스턴스화합니다.  
  
### <a name="queuekeyvaluepairstringstring"></a>큐 < KeyValuePair\<string, string > >  
 `<scg:Queue x:TypeArguments="scg:KeyValuePair(sys:String,sys:String)" ...>`내부 제약 조건 <xref:System.Collections.Generic.Queue%601> 형식 인수 <xref:System.String> 및 <xref:System.Collections.Generic.KeyValuePair%602> <xref:System.String>를 사용 하는 제약 조건이 있는 새를 인스턴스화합니다.  
  
## <a name="xaml-2006-and-wpf-generic-xaml-usages"></a>XAML 2006 및 WPF 일반 XAML 사용  
 WPF 응용 프로그램에 사용 되는 xaml 2006 사용 및 xaml의 경우 일반적인 xaml의 제네릭 형식 `x:TypeArguments` 사용에 대 한 다음과 같은 제한 사항이 있습니다.  
  
- XAML 파일의 루트 요소만 제네릭 형식을 참조 하는 일반 XAML 사용을 지원할 수 있습니다.  
  
- 루트 요소는 하나 이상의 형식 인수가 있는 제네릭 형식에 매핑되어야 합니다. 예제입니다. <xref:System.Windows.Navigation.PageFunction%601> 페이지 함수는 WPF의 XAML 제네릭 사용 지원에 대 한 주요 시나리오입니다.  
  
- 제네릭의 루트 요소 XAML 개체 요소는를 사용 하 여 `x:Class`partial 클래스도 선언 해야 합니다. WPF 빌드 작업을 정의 하는 경우에도 마찬가지입니다.  
  
- `x:TypeArguments`중첩 된 제네릭 제약 조건을 참조할 수 없습니다.  
  
## <a name="xaml-2009-or-xaml-2006-with-no-wpf-30-or-wpf-35-dependency"></a>WPF 3.0 또는 WPF 3.5 종속성이 없는 XAML 2009 또는 XAML 2006  
 Xaml 2006 또는 xaml 2009에 대 한 .NET Framework XAML 서비스에서는 제네릭 XAML 사용에 대 한 WPF 관련 제한이 완화 됩니다. 지원 형식 시스템 및 개체 모델에서 지원할 수 있는 XAML 태그의 임의 위치에서 제네릭 개체 요소를 인스턴스화할 수 있습니다.  
  
 CLR 기본 형식을 매핑하여 공용 언어 기본 형식에 대 한 XAML 형식을 가져오는 대신 XAML 2009를 사용 하는 `typeString`경우 [일반적인 xaml 언어 기본 형식에 대 한 기본 제공 형식을](built-in-types-for-common-xaml-language-primitives.md) 의 정보 항목으로 사용할 수 있습니다. 예를 들어 다음을 선언할 수 있습니다 (접두사 매핑은 표시 되지 않지만 x는 XAML 2009에 대 한 XAML 언어 XAML 네임 스페이스).  
  
```xaml  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
 WPF 및 .NET Framework 4를 대상으로 지정 하는 경우 xaml 2009 기능을와 `x:TypeArguments` 함께 사용할 수 있지만 느슨한 xaml (태그 컴파일되지 않은 xaml)에 대해서만 사용할 수 있습니다. WPF에 대한 태그로 컴파일된 XAML 및 BAML 형식의 XAML은 현재 XAML 2009 키워드 및 기능을 지원하지 않습니다. XAML 태그를 표시 해야 하는 경우 "XAML 2006 및 WPF Generic XAML 사용" 섹션에 설명 된 제한에 따라 작업 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [x:Class 지시문](x-class-directive.md)
- [x:Type 태그 확장](x-type-markup-extension.md)
- [공용 XAML 언어 기본 형식에 대한 기본 제공 형식](built-in-types-for-common-xaml-language-primitives.md)
- [XAML의 제네릭](generics-in-xaml.md)
