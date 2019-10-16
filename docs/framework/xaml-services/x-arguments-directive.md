---
title: x:Arguments 지시문
ms.date: 03/30/2017
helpviewer_keywords:
- x:Arguments directive [XAML Services]
- Arguments directive in XAML [XAML Services]
- XAML [XAML Services], x:Arguments directive
ms.assetid: 87cc10b0-b610-4025-b6b0-ab27ca27c92e
ms.openlocfilehash: a18de9a07839f5b01620311832b85667680c12ad
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053828"
---
# <a name="xarguments-directive"></a>x:Arguments 지시문
XAML에서 매개 변수가 없는 생성자 개체 요소 선언 또는 팩터리 메서드 개체 선언의 패키지 생성 인수입니다.  
  
## <a name="xaml-element-usage-nonparameterless-constructor"></a>XAML 요소 사용 (매개 변수가 없는 생성자)  
  
```xaml  
<object ...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-element-usage-factory-method"></a>XAML 요소 사용 (팩터리 메서드)  
  
```xaml  
<object x:FactoryMethod="methodName"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`oneOrMoreObjectElements`|매개 변수가 없는 지원 생성자 또는 팩터리 메서드에 전달할 인수를 지정 하는 하나 이상의 개체 요소입니다.<br /><br /> 일반적인 사용법은 개체 요소 내에서 초기화 텍스트를 사용 하 여 실제 인수 값을 지정 하는 것입니다. 예제 섹션을 참조 하세요.<br /><br /> 요소의 순서는 중요 합니다. 순서 대로 XAML 형식은 지원 생성자 또는 팩터리 메서드 오버 로드의 형식 및 형식 순서와 일치 해야 합니다.|  
|`methodName`|`x:Arguments` 인수를 처리 해야 하는 팩터리 메서드의 이름입니다.|  
  
## <a name="dependencies"></a>종속성  
 `x:FactoryMethod`에서 `x:Arguments` 적용 되는 범위 및 동작을 수정할 수 있습니다.  
  
 `x:FactoryMethod` 을`x:Arguments` 지정 하지 않으면은 지원 생성자의 대체 (기본값이 아닌) 서명에 적용 됩니다.  
  
 `x:FactoryMethod` 이`x:Arguments` 지정 된 경우는 명명 된 메서드의 오버 로드에 적용 됩니다.  
  
## <a name="remarks"></a>설명  
 XAML 2006은 초기화 텍스트를 통해 기본값이 아닌 초기화를 지원할 수 있습니다. 그러나 초기화 텍스트 생성 기술의 실용적인 응용 프로그램은 제한적입니다. 초기화 텍스트는 단일 텍스트 문자열로 처리 됩니다. 따라서 사용자 지정 정보 항목 및 사용자 지정 구분 기호를 문자열에서 구문 분석할 수 있는 생성 동작에 대해 형식 변환기가 정의 되어 있지 않으면 단일 매개 변수 초기화에 대 한 기능만 추가 합니다. 또한 개체 논리에 대 한 텍스트 문자열은 실제 문자열 이외의 기본 형식을 처리 하기 위해 지정 된 XAML 파서의 네이티브 기본 형식 변환기가 될 수 있습니다.  
  
 지시문 태그가 포함 하는 개체 요소의 형식을 참조 하지 않기 때문에 XAML사용은일반적인의미의속성요소사용이아닙니다.`x:Arguments` 요소에서 태그를 자식 내용에 대 한 `x:Code` 기본값 이외의 것으로 해석 해야 하는 범위를 표시 하는 것과 같은 다른 지시문과 더 유사 합니다. 이 경우 각 개체 요소의 xaml 형식은 인수 형식에 대 한 정보를 전달 합니다 .이는 xaml 파서에서 사용 되는 특정 생성자 팩터리 메서드 시그니처 `x:Arguments` 를 결정 하는 데 사용 됩니다.  
  
 `x:Arguments`생성 되는 개체 요소는 개체 요소의 다른 속성 요소, 콘텐츠, 내부 텍스트 또는 초기화 문자열 앞에와 야 합니다. 내의 `x:Arguments` 개체 요소에는 해당 XAML 형식 및 지원 생성자 또는 팩터리 메서드에서 허용 하는 특성과 초기화 문자열이 포함 될 수 있습니다. 개체 또는 인수 중 하나에 대해 설정 된 접두사 매핑을 참조 하 여 기본 XAML 네임 스페이스의 외부에 있는 사용자 지정 XAML 형식 또는 XAML 형식을 지정할 수 있습니다.  
  
 XAML 프로세서는에 `x:Arguments` 지정 된 인수를 사용 하 여 개체를 생성 하는 방법을 결정 하기 위해 다음 지침을 사용 합니다. 가 `x:FactoryMethod` 지정 된 경우 정보는 지정 `x:FactoryMethod` 된와 비교 됩니다 .의 `x:FactoryMethod` 값은 메서드 이름이 고 명명 된 메서드에는 오버 로드가 있을 수 있습니다. 을 `x:FactoryMethod` 지정 하지 않으면 정보를 개체의 모든 공용 생성자 오버 로드 집합과 비교 합니다. 그런 다음 XAML 처리 논리는 매개 변수 수를 비교 하 고 인자 수가 일치 하는 오버 로드를 선택 합니다. 일치 하는 항목이 두 개 이상 있는 경우 XAML 프로세서는 제공 된 개체 요소의 XAML 형식에 따라 매개 변수의 형식을 비교 해야 합니다. 일치 하는 항목이 두 개 이상 있으면 XAML 프로세서 동작이 정의 되어 있지 않습니다. 을 `x:FactoryMethod` 지정 했지만 메서드를 확인할 수 없는 경우 XAML 프로세서에서 예외를 throw 해야 합니다.  
  
 XAML 특성 사용 `<x:Arguments>string</x:Arguments>` 은 기술적으로 가능 합니다. 그러나이 경우 초기화 텍스트와 형식 변환기를 통해 수행할 수 있는 작업 외에 다른 기능을 제공 하지 않으며,이 구문을 사용 하는 것은 XAML 2009 팩터리 메서드 기능의 디자인 의도가 아닙니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 매개 변수가 없는 생성자 시그니처를 표시 한 다음 해당 서명에 액세스 하 `x:Arguments` 는의 XAML 사용을 보여 줍니다.  
  
```csharp  
public class Food {  
    private string _name;  
    private Int32 _calories;  
    public Food(string name, Int32 calories) {  
        _name=name;  
        _calories=calories;  
    }  
}  
```  
  
```xaml  
<my:Food>  
    <x:Arguments>  
        <x:String>Apple</x:String>  
        <x:Int32>150</x:Int32>  
    </x:Arguments>  
</my:Food>  
```  
  
 다음 예제에서는 대상 팩터리 메서드 시그니처와 해당 서명에 액세스 하는의 `x:Arguments` XAML 사용을 보여 줍니다.  
  
```csharp  
public Food TryLookupFood(string name)  
{  
  switch (name) {  
    case "Apple": return new Food("Apple",150);  
    case "Chocolate": return new Food("Chocolate",200);  
    case "Cheese": return new Food("Cheese", 450);  
    default: {return new Food(name,0);  
  }  
}  
```  
  
```xaml  
<my:Food x:FactoryMethod="TryLookupFood">  
    <x:Arguments>  
        <x:String>Apple</x:String>  
    </x:Arguments>  
</my:Food>  
```  
  
## <a name="see-also"></a>참고자료

- [.NET Framework XAML 서비스에서 사용할 사용자 지정 형식 정의](defining-custom-types-for-use-with-net-framework-xaml-services.md)
- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
