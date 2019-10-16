---
title: C# 키워드
ms.date: 03/07/2017
f1_keywords:
- cs.keywords
helpviewer_keywords:
- keywords [C#]
- C# language, keywords
- Visual C#, keywords
- '@ keyword'
ms.assetid: e929b0f2-4b92-4d37-8060-23d323b098ad
ms.openlocfilehash: 2bdaa2f4cdb19d01948effd599177f68859cb82c
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291063"
---
# <a name="c-keywords"></a>C# 키워드

키워드는 컴파일러에 대해 특별한 의미를 갖는, 미리 정의되어 있는 예약된 식별자입니다. 키워드는 프로그램에서 식별자로 사용되려면 접두어로 `@`을 포함해야 합니다. 예를 들어 `@if`는 올바른 식별자이지만 `if`는 `if`가 키워드이므로 식별자로 적절하지 않습니다.  
  
 이 항목의 첫 번째 표에는 C# 프로그램의 모든 부분에서 예약된 식별자로 사용되는 키워드가 나와 있습니다. 이 항목의 두 번째 표에는 C#의 상황별 키워드가 나와 있습니다. 상황별 키워드는 제한된 프로그램 컨텍스트에서만 특별한 의미를 가지며 해당 컨텍스트 외부에서는 식별자로 사용될 수 있습니다. 일반적으로 새 키워드는 C# 언어에 추가될 때 이전 버전에서 작성된 프로그램을 중단하지 않도록 하기 위해 상황별 키워드로 추가됩니다.  
  
|||||  
|---|---|---|---|  
|[abstract](abstract.md)|[as](../operators/type-testing-and-cast.md#as-operator)|[base](base.md)|[bool](bool.md)|  
|[break](break.md)|[byte](../builtin-types/integral-numeric-types.md)|[case](switch.md)|[catch](try-catch.md)|  
|[char](char.md)|[checked](checked.md)|[class](class.md)|[const](const.md)|  
|[continue](continue.md)|[decimal](../builtin-types/floating-point-numeric-types.md)|[default](default.md)|[delegate](delegate.md)|  
|[do](do.md)|[double](../builtin-types/floating-point-numeric-types.md)|[else](if-else.md)|[enum](enum.md)|  
|[event](event.md)|[explicit](../operators/user-defined-conversion-operators.md)|[extern](extern.md)|[false](false-literal.md)|  
|[finally](try-finally.md)|[fixed](fixed-statement.md)|[float](../builtin-types/floating-point-numeric-types.md)|[for](for.md)|  
|[foreach](foreach-in.md)|[goto](goto.md)|[if](if-else.md)|[implicit](../operators/user-defined-conversion-operators.md)|  
|[in](in.md)|[int](../builtin-types/integral-numeric-types.md)|[interface](interface.md)|[internal](internal.md)|
|[is](is.md)|[lock](lock-statement.md)|[long](../builtin-types/integral-numeric-types.md)|[namespace](namespace.md)|
|[new](../operators/new-operator.md)|[null](null.md)|[object](object.md)|[operator](../operators/operator-overloading.md)|
|[out](out.md)|[override](override.md)|[params](params.md)|[private](private.md)|
|[protected](protected.md)|[public](public.md)|[readonly](readonly.md)|[ref](ref.md)|
|[return](return.md)|[sbyte](../builtin-types/integral-numeric-types.md)|[sealed](sealed.md)|[short](../builtin-types/integral-numeric-types.md)||
[sizeof](../operators/sizeof.md)|[stackalloc](../operators/stackalloc.md)|[static](static.md)|[string](string.md)|
|[struct](struct.md)|[switch](switch.md)|[this](this.md)|[throw](throw.md)|
|[true](true-literal.md)|[try](try-catch.md)|[typeof](../operators/type-testing-and-cast.md#typeof-operator)|[uint](../builtin-types/integral-numeric-types.md)|
|[ulong](../builtin-types/integral-numeric-types.md)|[unchecked](unchecked.md)|[unsafe](unsafe.md)|[ushort](../builtin-types/integral-numeric-types.md)|
|[using](using.md)|[Static 사용](using-static.md)|[virtual](virtual.md)|[void](void.md)|
|[volatile](volatile.md)|[while](while.md)|

## <a name="contextual-keywords"></a>상황별 키워드

 상황별 키워드는 코드에서 특정 의미를 제공하는 데 사용되지만 C#의 예약어입니다. `partial` 및 `where`과 같은 일부 상황별 키워드는 두 개 이상의 컨텍스트에서 특별한 의미를 갖습니다.  
  
||||  
|---|---|---|  
|[add](add.md)|[alias](extern-alias.md)|[ascending](ascending.md)|
|[async](async.md)|[await](../operators/await.md)|[by](by.md)|
|[descending](descending.md)|[dynamic](dynamic.md)|[equals](equals.md)|
|[from](from-clause.md)|[get](get.md)|[global](../operators/namespace-alias-qualifier.md)|
|[group](group-clause.md)|[into](into.md)|[join](join-clause.md)|
|[let](let-clause.md)|[nameof](../operators/nameof.md)|[on](on.md)|
|[orderby](orderby-clause.md)|[partial(형식)](partial-type.md)|[partial(메서드)](partial-method.md)|
|[remove](remove.md)|[select](select-clause.md)|[set](set.md)|
|[비관리형 제네릭 형식 제약 조건](where-generic-type-constraint.md)|[value](value.md)|[var](var.md)|
|[when(필터 조건)](when.md)|[where(제네릭 형식 제약 조건)](where-generic-type-constraint.md)|[where(쿼리 절)](where-clause.md)|
|[yield](yield.md)| | |
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
