---
title: Checked 및 Unchecked - C# 참조
ms.custom: seodec18
ms.date: 05/15/2018
helpviewer_keywords:
- operators [C#], checked and unchecked
- exceptions [C#], overflow checking
- checked statement [C#]
- overflow checking [C#]
- unchecked statement [C#]
- statements [C#], checked and unchecked
ms.assetid: a84bc877-2c7f-4396-8735-1ce97c42f35e
ms.openlocfilehash: 3378cffc1dcee7bb12705704e66b7fdd287105fb
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592979"
---
# <a name="checked-and-unchecked-c-reference"></a>Checked 및 Unchecked(C# 참조)
checked 컨텍스트 또는 unchecked 컨텍스트에서 C# 문을 실행할 수 있습니다. checked 컨텍스트에서는 산술 오버플로가 있으면 예외가 발생합니다. unchecked 컨텍스트에서는 산술 오버플로가 무시되고 대상 형식에 맞지 않는 상위 비트가 삭제되어 해당 결과가 잘립니다.  
  
- [checked](checked.md) checked 컨텍스트를 지정합니다.  
  
- [unchecked](unchecked.md) unchecked 컨텍스트를 지정합니다.  
  
 오버플로 검사의 영향을 받는 작업은 다음과 같습니다.  
  
- 정수 계열 형식에 다음의 미리 정의된 연산자를 사용하는 식  
  
     `++`, `--`, `-`(단항), `+`, `-`, `*`, `/`  
  
- 정수 형식 간이나 `float` 또는 `double`에서 정수 형식으로의 명시적 숫자 변환  
  
 `checked`도 `unchecked`도 지정하지 않으면 상수가 아닌 식(런타임에 계산되는 식)의 기본 컨텍스트는 [-checked](../compiler-options/checked-compiler-option.md) 컴파일러 옵션의 값으로 정의됩니다. 기본적으로 이 옵션의 값은 설정되지 않으며 unchecked 컨텍스트에서 산술 연산이 실행됩니다.
 
 상수 식(컴파일 시간에 완전히 계산될 수 있는 식)의 경우 기본 컨텍스트는 항상 checked입니다. 상수 식이 unchecked 컨텍스트에 명시적으로 배치되지 않는 경우 식에 대한 컴파일 시간 계산 중 발생하는 오버플로로 인해 컴파일 시간 오류가 발생합니다.
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [문 키워드](statement-keywords.md)
