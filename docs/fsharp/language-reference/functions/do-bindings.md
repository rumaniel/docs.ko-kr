---
title: do 바인딩
description: 함수 또는 값 F# 을 정의 하지 않고 ' do ' 바인딩을 사용 하 여 코드를 실행 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: f98f523296bfaceeda35d4861eafbfeaa5a60c32
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630536"
---
# <a name="do-bindings"></a>do 바인딩

`do` 바인딩은 함수나 값을 정의 하지 않고 코드를 실행 하는 데 사용 됩니다. 또한 클래스에서 바인딩 사용은 [ `do` 클래스의 바인딩](../members/do-bindings-in-classes.md)을 참조 하세요.

## <a name="syntax"></a>구문

```fsharp
[ attributes ]
[ do ]expression
```

## <a name="remarks"></a>설명

함수 또는 값 정의와 별개로 코드를 실행 하려는 경우 바인딩을사용합니다.`do` `do` 바인딩의 식은를 반환 `unit`해야 합니다. 최상위 `do` 바인딩의 코드는 모듈이 초기화 될 때 실행 됩니다. 키워드 `do` 는 선택 사항입니다.

최상위 `do` 바인딩에 특성을 적용할 수 있습니다. 예를 들어 프로그램에서 COM interop 사용 하는 경우 프로그램에 특성을 적용 `STAThread` 하는 것이 좋습니다. 다음 코드와 같이 `do` 바인딩에 특성을 사용 하 여이 작업을 수행할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet201.fs)]

## <a name="see-also"></a>참고자료

- [F# 언어 참조](../index.md)
- [함수](index.md)
