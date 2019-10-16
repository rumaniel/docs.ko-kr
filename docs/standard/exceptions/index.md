---
title: .NET의 예외 처리 및 Throw
ms.date: 06/19/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- exceptions [.NET], handling
- runtime, exceptions
- filtering exceptions
- errors [.NET], exceptions
- exceptions [.NET], throwing
- exceptions [.NET]
- common language runtime, exceptions
ms.assetid: f99a1d29-a2a8-47af-9707-9909f9010735
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a417e964c2f44c291892f9ddec6e32438fbff9a1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945433"
---
# <a name="handling-and-throwing-exceptions-in-net"></a>.NET의 예외 처리 및 Throw

애플리케이션은 실행 중에 발생하는 오류를 일관된 방식으로 처리할 수 있어야 합니다. .NET에서는 일관된 방식으로 애플리케이션에 오류를 알리기 위한 모델을 제공합니다. .NET 작업은 예외를 throw하여 오류를 나타냅니다.

## <a name="exceptions"></a>예외

예외란 프로그램 실행 중 발생한 모든 오류 상태 또는 예기치 못한 동작입니다. 예외는 사용 중인 코드 또는 호출한 코드(예: 공유 라이브러리)의 오류, 사용 불가능한 운영 체제 리소스, 런타임에서 발생한 예기치 못한 상황(예: 확인할 수 없는 코드) 등에 의해 throw될 수 있습니다. 사용 중인 애플리케이션이 이러한 일부 상황으로부터 복구될 수 있지만 복구될 수 없는 경우도 있습니다. 대부분의 애플리케이션 예외로부터는 복구할 수 있지만 대부분의 런타임 예외로부터는 복구할 수 없습니다.

.NET에서 예외는 <xref:System.Exception?displayProperty=nameWithType> 클래스에서 상속되는 개체입니다. 예외는 문제가 발생한 코드 영역에서 throw됩니다. 예외는 애플리케이션에서 해당 예외를 처리하거나 프로그램이 종료될 때까지 스택으로 전달됩니다.

## <a name="exceptions-vs-traditional-error-handling-methods"></a>예외 대 일반적인 오류 처리 방법

일반적으로 언어 오류 처리 모델은 오류를 감지하고 해당 오류 처리기를 찾는 언어 고유의 방식에 의존하거나 운영 체제에서 제공하는 오류 처리 메커니즘에 의존했습니다. .NET에서 예외 처리를 구현하는 방법에는 다음과 같은 이점이 있습니다.

- 예외 throw 및 처리는 .NET 프로그래밍 언어에서 동일하게 작동합니다.

- 예외 처리에 특정한 언어 구문이 필요하지는 않지만, 각 언어에서 고유한 구문을 정의할 수 있도록 허용합니다.

- 프로세스 및 컴퓨터 경계 간에도 예외가 throw될 수 있습니다.

- 예외 처리 코드를 애플리케이션에 추가하여 프로그램 안정성을 높일 수 있습니다.

예외는 반환 코드 등의 다른 오류 알림 방법에 비해 이점을 제공합니다. 예외가 throw되고 사용자가 처리하지 않을 경우 런타임에서 애플리케이션을 종료하기 때문에 오류가 발견되지 않습니다. 오류 반환 코드를 검사하지 못한 코드의 결과로 잘못된 값이 시스템 전체에 계속 전파되지 않습니다.

## <a name="common-exceptions"></a>일반적인 예외

다음 표에서는 몇 가지 일반적인 예외 및 예외가 발생할 수 있는 경우의 예를 보여 줍니다.

| 예외 형식 | 설명 | 예제 |
| -------------- | ----------- | ------- |
| <xref:System.Exception> | 모든 예외의 기본 클래스. | 없음(이 예외의 파생된 클래스 사용). |
| <xref:System.IndexOutOfRangeException> | 배열이 올바르지 않게 인덱싱된 경우에만 런타임에서 발생됩니다. | 유효 범위를 벗어난 배열 인덱싱: <br /> `arr[arr.Length+1]` |
| <xref:System.NullReferenceException> | null 개체가 참조되는 경우에만 런타임에서 발생됩니다. | `object o = null;` <br /> `o.ToString();` |
| <xref:System.InvalidOperationException> | 잘못된 상태에 있는 경우에 메서드에서 발생됩니다. | 기본 컬렉션에서 항목을 제거한 후 `Enumerator.MoveNext()` 호출. |
| <xref:System.ArgumentException> | 모든 인수 예외에 대한 기본 클래스. | 없음(이 예외의 파생된 클래스 사용). |
| <xref:System.ArgumentNullException> | 인수에 Null을 허용하지 않는 메서드에서 발생됩니다. | `String s = null;` <br /> `"Calculate".IndexOf(s);`|
| <xref:System.ArgumentOutOfRangeException> | 인수가 지정된 범위에 있는지 확인하는 메서드에서 발생됩니다. | `String s = "string";` <br /> `s.Substring(s.Length+1);` |

## <a name="see-also"></a>참고 항목

- [Exception 클래스 및 속성](exception-class-and-properties.md)
- [방법: Try-Catch 블록을 사용하여 예외 catch](how-to-use-the-try-catch-block-to-catch-exceptions.md)
- [방법: catch 블록에서 특정 예외 사용](how-to-use-specific-exceptions-in-a-catch-block.md)
- [방법: 명시적으로 예외 Throw](how-to-explicitly-throw-exceptions.md)
- [방법: 사용자 정의 예외 만들기](how-to-create-user-defined-exceptions.md)
- [사용자 필터 예외 처리기 사용](using-user-filtered-exception-handlers.md)
- [방법: Finally 블록 사용](how-to-use-finally-blocks.md)
- [COM Interop 예외 처리](handling-com-interop-exceptions.md)
- [예외에 대한 모범 사례](best-practices-for-exceptions.md)
- [모든 개발자가 런타임 예외에 대해 알아야 할 사항](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/exceptions.md)
