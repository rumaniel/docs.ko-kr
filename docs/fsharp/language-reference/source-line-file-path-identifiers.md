---
title: 소스 줄, 파일 및 경로 식별자
description: 코드의 소스 줄 번호, 디렉터리 F# 및 파일 이름에 액세스할 수 있는 기본 제공 식별자 값을 사용 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: f22c3dfb3cb106fbe45883ffd7de01feac30db00
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216750"
---
# <a name="source-line-file-and-path-identifiers"></a>소스 줄, 파일 및 경로 식별자

`__SOURCE_DIRECTORY__` 및 `__LINE__` 식별자는코드의소스줄번호,디렉터리및파일이름에액세스할수있는기본`__SOURCE_FILE__` 제공 값입니다.

## <a name="syntax"></a>구문

```fsharp
__LINE__
__SOURCE_DIRECTORY__
__SOURCE_FILE__
```

## <a name="remarks"></a>설명

이러한 각 값에는 형식이 `string`있습니다.

다음 표에서는에서 F#사용할 수 있는 소스 줄, 파일 및 경로 식별자를 요약 하 여 보여 줍니다. 이러한 식별자는 전처리기 매크로가 아닙니다. 이러한 값은 컴파일러에서 인식 하는 기본 제공 값입니다.

|미리 정의 된 식별자|설명|
|---------------------|-----------|
|`__LINE__`|지시문을 고려 `#line` 하 여 현재 줄 번호로 계산 합니다.|
|`__SOURCE_DIRECTORY__`|지시문을 고려 `#line` 하 여 원본 디렉터리의 현재 전체 경로를 확인 합니다.|
|`__SOURCE_FILE__`|는 지시문을 고려 `#line` 하 여 경로 없이 현재 소스 파일 이름으로 평가 됩니다.|

`#line` 지시문에 대 한 자세한 내용은 [컴파일러 지시문](compiler-directives.md)을 참조 하십시오.

## <a name="example"></a>예제

다음 코드 예제에서는 이러한 값을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet7401.fs)]

출력:

```console
Line: 4
Source Directory: C:\Users\username\Documents\Visual Studio 2017\Projects\SourceInfo\SourceInfo
Source File: Program.fs
```

## <a name="see-also"></a>참고 항목

- [컴파일러 지시문](compiler-directives.md)
- [F# 언어 참조](index.md)
