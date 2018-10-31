---
title: '| 연산자(C# 참조)'
ms.date: 07/20/2015
f1_keywords:
- '|_CSharpKeyword'
helpviewer_keywords:
- bitwise OR operator [C#]
- '| operator [C#]'
- binary operator (|) [C#]
ms.assetid: 82d6bb78-54c8-40bf-b679-531180ddaf70
ms.openlocfilehash: 999df9db0819a5f33e21a29b892de0a8854dd5d8
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48028180"
---
# <a name="-operator-c-reference"></a>| 연산자(C# 참조)
이항 `|` 연산자는 정수 형식 및 `bool`에 대해 미리 정의되어 있습니다. 정수 형식의 경우 `|` 연산자는 해당 피연산자의 비트 OR 연산자를 계산합니다. `bool` 피연산자의 경우 `|` 연산자는 해당 피연산자의 논리적 OR 연산을 계산합니다. 즉, 피연산자가 둘 다 `false`일 경우에만 결과가 `false`입니다.  
  
## <a name="remarks"></a>설명  
 이진 `|` 연산자는 [기존 OR 연산자](conditional-or-operator.md) `||`와 달리 첫 번째 연산자의 값에 상관없이 두 피연산자를 모두 계산합니다.
 
 사용자 정의 형식은 `|` 연산자를 오버로드할 수 있습니다([operator](../../../csharp/language-reference/keywords/operator.md) 참조).  
  
## <a name="example"></a>예  
 [!code-csharp[csRefOperators#31](../../../csharp/language-reference/operators/codesnippet/CSharp/or-operator_1.cs)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [C# 연산자](../../../csharp/language-reference/operators/index.md)
