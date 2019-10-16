---
title: 변수
description: 명명 된 값 또는 F# 변수에 실제 값이 없을 수 있는 경우 옵션 유형을 사용 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 9326cf04f53adac7422c09a49a59c4eecd49486d
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627356"
---
# <a name="options"></a>변수

의 옵션 유형은 명명 F# 된 값 또는 변수에 대 한 실제 값이 없을 수 있는 경우에 사용 됩니다. 옵션에는 기본 형식이 있으며 해당 형식의 값을 포함 하거나 값이 없을 수 있습니다.

## <a name="remarks"></a>설명

다음 코드는 옵션 유형을 생성 하는 함수를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1404.fs)]

여기서 볼 수 있듯이 입력 `a` 이 `Some(a)` 0 보다 크면이 생성 됩니다.  그렇지 않으면 `None` 이 생성 됩니다.

값 `None` 은 옵션에 실제 값이 없을 때 사용 됩니다. 그렇지 않으면 식 `Some( ... )` 에서 옵션에 값을 제공 합니다. 및 `Some` `exists` `true` `false` 값은 다음 함수와 같이 패턴 일치에 유용 합니다 .이 함수는 옵션에 값이 있는 경우를 반환 하 고 그렇지 않으면를 반환 합니다. `None`

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1401.fs)]

## <a name="using-options"></a>옵션 사용

옵션은 다음 코드와 같이 검색에서 일치 하는 결과를 반환 하지 않는 경우에 일반적으로 사용 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1403.fs)]

위의 코드에서는 목록이 재귀적으로 검색 됩니다. 함수 `tryFindMatch` 는 부울 값을 반환 `pred` 하는 조건자 함수와 검색할 목록을 사용 합니다. 조건자를 만족 하는 요소가 발견 되 면 재귀가 종료 되 고 함수는 값을 식 `Some(head)`의 옵션으로 반환 합니다. 빈 목록이 일치 하면 재귀가 종료 됩니다. 이 시점에서 값 `head` 을 찾을 수 `None` 없으며이 반환 됩니다.

컬렉션 F# 에서 존재 하거나 존재 하지 않을 수 있는 값을 검색 하는 라이브러리 함수는 대부분 `option` 형식을 반환 합니다. 규칙에 따라 이러한 함수는 `try` 접두사로 시작 [`Seq.tryFindIndex`](https://msdn.microsoft.com/library/c357b221-edf6-4f68-bf40-82a3156d945a)합니다 (예:).

값을 생성 하려고 할 때 예외가 throw 될 수 있는 경우와 같이 값이 없는 경우에도 옵션이 유용할 수 있습니다. 다음 코드 예제에서는 그 구체적인 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1402.fs)]

이전 `openFile` 예제의 함수는 파일이 성공적으로 열리고 `string -> File option` 예외가 발생 하 `None` 는 `File` 경우 개체를 반환 하므로 형식이 있습니다. 상황에 따라 예외를 전파 하도록 허용 하는 것이 아니라 예외를 catch 하는 것이 적절 한 디자인이 아닐 수도 있습니다.

또한 옵션의 `Some` 경우 null 또는 null 값 `null` 을 전달할 수 있습니다. 일반적으로이를 방지 하는 것이 일반적 이며 일반적 F# 으로 루틴 프로그래밍에 있지만 .net의 참조 형식 특성 때문에 가능 합니다.

## <a name="option-properties-and-methods"></a>옵션 속성 및 메서드

옵션 형식은 다음 속성 및 메서드를 지원 합니다.

|속성 또는 메서드|형식|Description|
|------------------|----|-----------|
|[없음](https://msdn.microsoft.com/library/83ef260a-aa33-4e6f-aee6-b9bf0a461476)|`'T option`|`None` 값을 포함 하는 옵션 값을 만들 수 있도록 하는 정적 속성입니다.|
|[IsNone](https://msdn.microsoft.com/library/f08532ca-1716-4f60-ae59-8ef6256df234)|`bool`|옵션 `true` 값`None` 이 이면를 반환 합니다.|
|[IsSome](https://msdn.microsoft.com/library/c5088d51-c5d7-425f-a77f-12c379bb356f)|`bool`|옵션 `true` 에이 아닌 `None`값이 있으면를 반환 합니다.|
|[개](https://msdn.microsoft.com/library/12f048d2-e293-4596-accb-de036ecd63fc)|`'T option`|값이이 아닌 `None`옵션을 만드는 정적 멤버입니다.|
|[값](https://msdn.microsoft.com/library/c79f68e8-11fd-45b1-a053-e8fc38b56df7)|`'T`|내부 값을 반환 하거나, 값이 `System.NullReferenceException` 인 `None`경우을 throw 합니다.|

## <a name="option-module"></a>옵션 모듈

옵션에 대 한 작업을 수행 하는 유용한 함수를 포함 하는 모듈 ( [옵션](https://msdn.microsoft.com/library/e615e4d3-bbbb-49ba-addc-6061ea2e2f4c))이 있습니다. 일부 함수는 속성의 기능을 반복 하지만 함수가 필요한 컨텍스트에서는 유용 합니다. [옵션. isSome](https://msdn.microsoft.com/library/41ad0857-5672-4326-84b5-c33dc43dcf79) 및 [Option. issome](https://msdn.microsoft.com/library/73db6a53-15e7-40a6-94f9-a0049e5f4819) 은 옵션에 값이 포함 되어 있는지 여부를 테스트 하는 모듈 함수입니다. [Option. get](https://msdn.microsoft.com/library/803e9fcb-6edd-4910-808c-25f08cbc55ea) 값 (있는 경우)을 가져옵니다. 값이 없으면이 throw `System.ArgumentException`됩니다.

[옵션. bind](https://msdn.microsoft.com/library/c3406192-24ac-49b5-bc3b-8f805187f1c0) 함수는 값이 있는 경우 값에 대해 함수를 실행 합니다. 함수는 인수를 하나만 사용 해야 하 고 해당 매개 변수 형식이 옵션 형식 이어야 합니다. 함수의 반환 값은 또 다른 옵션 유형입니다.

옵션 모듈에는 목록, 배열, 시퀀스 및 기타 컬렉션 형식에 사용할 수 있는 함수에 해당 하는 함수도 포함 되어 있습니다. 이러한 함수에 [`Option.map`](https://msdn.microsoft.com/library/91a20385-7e73-40c2-9adc-635e86d6a622)는 [`Option.iter`](https://msdn.microsoft.com/library/83389eef-3dff-4074-b4cc-f69581c25191) [`Option.exists`](https://msdn.microsoft.com/library/a606d2d4-fddc-4eab-ab37-c6138fb7ad99),, [,,`Option.foldBack`](https://msdn.microsoft.com/library/a882fbaf-c019-46f0-b4f5-b8c2b8b90ffb) [,및`Option.count`](https://msdn.microsoft.com/library/2dac83a9-684e-4d0f-b50e-ff722a8bb876)가 포함 됩니다. [`Option.fold`](https://msdn.microsoft.com/library/af896794-3d53-406c-9411-316cd5c33ad8) [`Option.forall`](https://msdn.microsoft.com/library/ba884586-5eae-49c5-9e36-05481c1c3428) 이러한 함수를 사용 하면 0 개 또는 한 개의 요소 컬렉션과 같은 옵션을 사용할 수 있습니다. 자세한 내용 및 예제는 [목록](lists.md)에서 컬렉션 함수에 대 한 설명을 참조 하세요.

## <a name="converting-to-other-types"></a>다른 형식으로 변환

옵션은 목록 또는 배열로 변환할 수 있습니다. 옵션을 이러한 데이터 구조 중 하나로 변환 하는 경우 결과 데이터 구조에는 0 또는 1 개의 요소가 있습니다. 옵션을 배열로 변환 하려면를 사용 [`Option.toArray`](https://msdn.microsoft.com/library/c8044873-ba17-4b52-8231-eb1a28318c64)합니다. 옵션을 목록으로 변환 하려면를 사용 [`Option.toList`](https://msdn.microsoft.com/library/5f1af295-9fa9-40ad-b4a1-3578d94d44e1)합니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [F# 형식](fsharp-types.md)
