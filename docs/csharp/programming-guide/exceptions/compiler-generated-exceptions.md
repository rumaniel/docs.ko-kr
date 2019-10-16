---
title: 컴파일러 생성 예외 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions [C#], compiler-generated
ms.assetid: 53b52f97-b366-4ed7-b05b-9eb78096b7f9
ms.openlocfilehash: d0e0a304c8f7d77e7ba5c89b643fc5658c458558
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590362"
---
# <a name="compiler-generated-exceptions-c-programming-guide"></a>컴파일러 생성 예외(C# 프로그래밍 가이드)
기본 작업이 실패하면 .NET Framework의 CLR(공용 언어 런타임)에 의해 자동으로 일부 예외가 throw됩니다. 이러한 예외와 관련 오류 조건이 다음 표에 나와 있습니다.  
  
|예외|설명|  
|---------------|-----------------|  
|<xref:System.ArithmeticException>|<xref:System.DivideByZeroException>, <xref:System.OverflowException> 등의 산술 연산 중에 발생하는 예외에 대한 기본 클래스입니다.|  
|<xref:System.ArrayTypeMismatchException>|제공된 요소의 실제 형식이 배열의 실제 형식과 호환되지 않아 배열이 요소를 저장할 수 없는 경우 throw됩니다.|  
|<xref:System.DivideByZeroException>|정수 값을 0으로 나누려고 시도할 경우 throw됩니다.|  
|<xref:System.IndexOutOfRangeException>|인덱스가 0보다 작거나 배열 경계를 벗어날 때 배열을 인덱싱하려고 시도할 경우 throw됩니다.|  
|<xref:System.InvalidCastException>|기본 형식에서 인터페이스 또는 파생 형식으로의 명시적 변환이 런타임에 실패할 경우 throw됩니다.|  
|<xref:System.NullReferenceException>|값이 [null](../../language-reference/keywords/null.md)인 개체를 참조하려고 시도할 경우 throw됩니다.|  
|<xref:System.OutOfMemoryException>|[new](../../language-reference/operators/new-operator.md) 연산자를 사용한 메모리 할당 시도가 실패할 경우 throw됩니다. 이 예외는 공용 언어 런타임에 사용할 수 있는 메모리가 모두 사용되었음을 나타냅니다.|  
|<xref:System.OverflowException>|`checked` 컨텍스트의 산술 연산이 오버플로될 경우 throw됩니다.|  
|<xref:System.StackOverflowException>|보류 중인 메서드 호출이 너무 많아 실행 스택이 모두 사용될 경우 throw됩니다. 대개 매우 깊은 재귀나 무한 재귀를 나타냅니다.|  
|<xref:System.TypeInitializationException>|정적 생성자가 예외를 throw하고 이 예외를 catch할 수 있는 호환되는 `catch` 절이 없는 경우 throw됩니다.|  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [예외 및 예외 처리](./index.md)
- [예외 처리](./exception-handling.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
