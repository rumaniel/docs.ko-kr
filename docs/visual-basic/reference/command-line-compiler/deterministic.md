---
title: -deterministic
ms.date: 04/11/2018
helpviewer_keywords:
- deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
ms.openlocfilehash: 6a83b636dd83534788f3a38971e0fef2919314f5
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005638"
---
# <a name="-deterministic"></a>-deterministic

컴파일러에서 동일한 입력에 대한 컴파일 간에 바이트 단위(byte-for-byte) 출력이 동일한 어셈블리를 생성합니다.

## <a name="syntax"></a>구문

```console
-deterministic
```

## <a name="remarks"></a>설명

기본적으로 컴파일러에서 타임스탬프 및 난수에서 생성된 GUID를 추가하기 때문에 지정된 입력 집합의 컴파일러 출력은 고유합니다. `-deterministic` 옵션을 사용하여 *결정적 어셈블리*를 생성하고, 입력이 동일하게 유지되는 한 해당 이진 콘텐츠가 컴파일 간에 동일합니다.

결정성의 목적을 위해 컴파일러에서 고려하는 입력은 다음과 같습니다.

- 명령줄 매개 변수의 순서
- 컴파일러의 .rsp 지시 파일의 내용
- 사용된 컴파일러의 정확한 버전 및 참조되는 어셈블리
- 현재 디렉터리 경로
- 다음을 포함하여 직접 또는 간접적으로 컴파일러에 명시적으로 전달된 모든 파일의 이진 콘텐츠
  - 소스 파일
  - 참조된 어셈블리
  - 참조된 모듈
  - 리소스
  - 강력한 이름 키 파일
  - @ 지시 파일
  - 분석기
  - 규칙 집합
  - 분석기에서 사용할 수 있는 추가 파일
- 현재 문화권(진단 및 예외 메시지가 생성되는 언어)
- 인코딩이 지정되지 않은 경우 기본 인코딩(또는 현재 코드 페이지)
- 컴파일러의 검색 경로(예: `/lib` 또는 `/recurse`로 지정)에 있는 파일의 존재 여부 및 내용
- 컴파일러가 실행되는 CLR 플랫폼
- `%LIBPATH%` 값(분석기 종속성 로드에 영향을 줄 수 있음)

원본을 공개적으로 사용할 수 있는 경우 결정적 컴파일을 사용하여 이진 파일이 신뢰할 수 있는 원본에서 컴파일되는지 여부를 설정할 수 있습니다. 또한 연속 빌드 시스템에서 이진 파일 변경에 종속된 빌드 단계를 실행해야 하는지 여부를 확인하는 데 유용할 수도 있습니다.

## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
