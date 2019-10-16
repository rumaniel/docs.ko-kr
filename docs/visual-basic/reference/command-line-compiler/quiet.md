---
title: -quiet
ms.date: 07/20/2015
f1_keywords:
- -quiet
- quiet
helpviewer_keywords:
- -quiet compiler option [Visual Basic]
- /quiet compiler option [Visual Basic]
- quiet compiler option [Visual Basic]
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
ms.openlocfilehash: 6e773c60469e8426956c92a5aa377741ba5af4d3
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005288"
---
# <a name="-quiet"></a>-quiet

컴파일러에서 구문 관련 오류 및 경고에 대한 코드를 표시하지 않도록 합니다.

## <a name="syntax"></a>구문

```console
-quiet
```

## <a name="remarks"></a>설명

기본적으로 `-quiet`은 적용되지 않습니다. 컴파일러가 구문 관련 오류 또는 경고를 보고 하면 소스 코드의 줄도 출력 합니다. 컴파일러 출력을 구문 분석 하는 응용 프로그램의 경우 컴파일러에서 진단 텍스트만 출력 하는 것이 더 편리할 수 있습니다.

다음 예제에서 `Module1`은 `-quiet` 없이 컴파일할 때 소스 코드를 포함 하는 오류를 출력 합니다.

```vb
Module Module1
    Sub Main()
        x()
    End Sub
End Module
```

출력:

```console
C:\projects\vb2.vb(3) : error BC30451: 'x' is not declared. It may be inaccessible due to its protection level.

        x()
        ~
```

@No__t-0을 사용 하 여 컴파일하면 컴파일러는 다음만 출력 합니다.

```console
E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.
```

> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.

## <a name="example"></a>예제

다음 코드는 @no__t를 컴파일하고 구문 관련 컴파일러 진단에 대 한 코드를 표시 하지 않습니다.

```console
vbc -quiet t2.vb
```

## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
