---
title: x:FactoryMethod 지시문
ms.date: 03/30/2017
helpviewer_keywords:
- XAML. x:FactoryMethod directive [XAML Services]
- FactoryMethod directive in XAML [XAML Services]
- x:FactoryMethod directive [XAML Services]
ms.assetid: 829bcbdf-5318-4afb-9a03-c310e0d2f23d
ms.openlocfilehash: 586965dd4094e81fd830a09b64604cf33f195630
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053785"
---
# <a name="xfactorymethod-directive"></a>x:FactoryMethod 지시문
지원 형식을 확인 한 후 XAML 프로세서에서 개체를 초기화 하는 데 사용 해야 하는 생성자 이외의 메서드를 지정 합니다.  
  
## <a name="xaml-attribute-usage-no-xarguments"></a>XAML 특성 사용, x:Arguments 안 함  
  
```xaml  
<object x:FactoryMethod="methodname"...>  
  ...  
</object>  
```  
  
## <a name="xaml-attribute-usage-xarguments-as-elements"></a>XAML 특성 사용, x:Arguments as 요소  
  
```xaml  
<object x:FactoryMethod="methodname"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`methodname`|로 `object`지정 된 인스턴스를 초기화 하기 위해 XAML 프로세서에서 호출 하는 메서드의 문자열 메서드 이름입니다. 설명 부분을 참조하세요.|  
|`oneOrMoreObjectElements`|팩터리 메서드 매개 변수를 지정 하는 개체에 대 한 하나 이상의 개체 요소입니다. 순서가 중요 합니다. 인수가 팩터리 메서드에 전달 되어야 하는 순서를 나타냅니다.|  
  
## <a name="remarks"></a>설명  
 가 `methodname` 인스턴스 메서드인 경우 정규화 할 수 없습니다.  
  
 팩터리 메서드인 정적 메서드가 지원 됩니다. 가 `methodname` 정적 `methodname` 메서드인 경우는 *typeName*으로 제공 됩니다. *methodName* 조합. 여기서 *typeName* 은 정적 팩터리 메서드를 정의 하는 클래스의 이름을로 합니다. *typeName* 은 매핑된 xmlns의 형식을 참조 하는 경우 접두사를 한정할 수 있습니다. *typeName* 은와 다른 형식일 `typeof(object)`수 있습니다.  
  
 팩터리 메서드는 관련 개체 요소를 지 원하는 형식의 선언 된 공용 메서드 여야 합니다.  
  
 팩터리 메서드는 관련 개체에 할당할 수 있는 인스턴스를 반환 해야 합니다. 팩터리 메서드는 null을 반환 하지 않아야 합니다.  
  
 `x:Arguments`팩터리 메서드의 시그니처와 가장 일치 하는 원칙에 대해 작동 합니다. 일치는 먼저 매개 변수 개수를 계산 합니다. 매개 변수 개수에 대해 일치 하는 항목이 두 개 이상 있는 경우 매개 변수 형식이 평가 되 고 가장 일치 하는 항목이 결정 됩니다. 이 평가 단계 후에도 모호성이 여전히 발생 하면 XAML 프로세서 동작이 정의 되지 않습니다.  
  
 지시문 태그가 포함 하는 개체 요소의 형식을 참조 하지 않기 때문에 요소사용은일반적인의미에서속성요소사용이아닙니다.`x:FactoryMethod` 요소 사용이 특성 사용 보다 일반적이 지 않은 것으로 예상 됩니다. `x:Arguments`(특성 또는 요소 사용)은 `x:FactoryMethod` 요소 사용량과 함께 사용할 수 있지만 사용 섹션에는 구체적으로 표시 되지 않습니다.  
  
 `x:FactoryMethod`요소는 다른 속성 요소 앞에와 야 하며, 요소로 제공 `x:Arguments` 되는 항목 앞에와 야 하며 모든 내용/내부 텍스트/초기화 텍스트 앞에와 야 합니다.  
  
## <a name="see-also"></a>참고자료

- [x:Arguments 지시문](x-arguments-directive.md)
