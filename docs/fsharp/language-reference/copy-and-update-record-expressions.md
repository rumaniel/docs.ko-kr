---
title: 레코드 식 복사 및 업데이트
description: 기존 레코드나 익명 레코드를 복사 하 고, 지정 된 필드를 업데이트 하 고, 업데이트 된 레코드나 익명 레코드를 반환 하는 ' 복사 및 업데이트 식 '을 작성 하는 방법에 대해 알아봅니다.
author: ChrSteinert
ms.date: 06/12/2019
ms.openlocfilehash: dfb20a6ff8282ae5988772cc0f0841db23aad942
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630384"
---
# <a name="copy-and-update-record-expressions"></a>레코드 식 복사 및 업데이트

*복사 및 업데이트 레코드 식은* 기존 레코드를 복사 하 고, 지정 된 필드를 업데이트 하 고, 업데이트 된 레코드를 반환 하는 식입니다.

## <a name="syntax"></a>구문

```fsharp
{ record-name with
    updated-labels }

{| anonymous-record-name with
    updated-labels |}
```

## <a name="remarks"></a>설명

레코드와 익명 레코드는 기본적으로 변경할 수 없으므로 기존 레코드를 업데이트할 수 없습니다. 업데이트 된 레코드를 만들려면 레코드의 모든 필드를 다시 지정 해야 합니다. 이 작업을 단순화 하기 위해 *복사 및 업데이트 식을* 사용할 수 있습니다. 이 식은 기존 레코드를 사용 하 여 식에서 지정 된 필드를 사용 하 고 식에 지정 된 누락 필드를 사용 하 여 동일한 형식으로 새를 만듭니다.

이는 기존 레코드를 복사 하 고 일부 필드 값을 변경 해야 하는 경우에 유용할 수 있습니다.

새로 만든 레코드를 인스턴스로 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

해당 레코드의 필드만 업데이트 하는 경우 다음과 같이 *복사 및 업데이트 레코드 식을* 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

## <a name="see-also"></a>참고자료

- [레코드](records.md)
- [익명 레코드](anonymous-records.md)
- [F# 언어 참조](index.md)
