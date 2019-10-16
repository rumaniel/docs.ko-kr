---
title: .NET에서 I/O 오류 처리
ms.date: 08/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O, exception handling
- I/O, errors
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: d2ff4e69596e721f485d107317f261231615c5a6
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53126877"
---
# <a name="handling-io-errors-in-net"></a>.NET에서 I/O 오류 처리

메서드 호출에서 throw될 수 있는 예외(예: 시스템 부하가 큰 경우의 <xref:System.NullReferenceException> 또는 프로그래머 오류로 인한 <xref:System.OutOfMemoryException>) 외에도, .NET 파일 시스템 메서드는 다음과 같은 예외를 throw할 수 있습니다.

- <xref:System.IO.IOException?displayProperty=nameWithType> - 모든 <xref:System.IO> 예외 유형의 기본 클래스입니다. 운영 체제의 반환 코드가 다른 예외 유형에 직접 매핑되지 않는 오류에 대해 throw됩니다.
- <xref:System.IO.FileNotFoundException?displayProperty=nameWithType>.
- <xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType>.
- <xref:System.IO.DriveNotFoundException??displayProperty=nameWithType>.
- <xref:System.IO.PathTooLongException?displayProperty=nameWithType>.
- <xref:System.OperationCanceledException?displayProperty=nameWithType>.
- <xref:System.UnauthorizedAccessException?displayProperty=nameWithType>.
- <xref:System.ArgumentException?displayProperty=nameWithType> - .NET Framework와 .NET Core 2.0 및 이전 버전에서 잘못된 경로 문자에 대해 throw됩니다.
- <xref:System.NotSupportedException?displayProperty=nameWithType> - .NET Framework의 잘못된 콜론에 대해 throw됩니다.
- <xref:System.Security.SecurityException?displayProperty=nameWithType> - .NET Framework에서만 필요한 권한이 없는, 제한된 신뢰로 실행되는 응용 프로그램에 대해 throw됩니다. (.NET Framework의 기본값은 완전 신뢰입니다.)

## <a name="mapping-error-codes-to-exceptions"></a>예외에 오류 코드 매핑

파일 시스템은 운영 체제 리소스이므로 .NET Core와 .NET Framework의 I/O 메서드는 기본 운영 체제 호출을 래핑합니다. 운영 체제가 실행한 코드에서 I/O 오류가 발생할 경우 운영 체제는 .NET I/O 메서드에 오류 정보를 반환합니다. 그런 다음, 메서드가 일반적으로 오류 코드 형태인 오류 정보를 .NET 예외 유형으로 변환합니다. 대부분의 경우 이 작업을 위해 오류 코드를 해당 예외 유형으로 직접 변환하며, 메서드 호출 컨텍스트에 따라 오류의 특수 매핑을 수행하지 않습니다.

예를 들어 Windows 운영 체제에서 `ERROR_FILE_NOT_FOUND`의 오류 코드(또는 0x02)를 반환하는 메서드 호출은 <xref:System.IO.FileNotFoundException>에 매핑되고, `ERROR_PATH_NOT_FOUND`의 오류 코드(또는 0x03)를 반환하는 메서드 호출은 <xref:System.IO.DirectoryNotFoundException>에 매핑됩니다.

그러나 운영 체제가 특정 오류 코드를 반환하는 정확한 조건은 문서화되지 않거나 잘못 문서화된 경우가 많습니다. 따라서 예기치 않은 예외가 발생할 수 있습니다. 예를 들어 파일이 아닌 디렉터리로 작업하고 있기 때문에 <xref:System.IO.DirectoryInfo.%23ctor%2A?displayProperty=nameWithType> 생성자에 잘못된 디렉터리 경로를 제공하면 <xref:System.IO.DirectoryNotFoundException>이 throw됩니다. 그러나 <xref:System.IO.FileNotFoundException>이 throw될 수도 있습니다.

## <a name="exception-handling-in-io-operations"></a>I/O 작업의 예외 처리

이러한 운영 체제 사용 때문에 예제의 디렉터리를 찾을 수 없음 오류와 같은 동일한 예외 조건에서 I/O 메서드가 I/O 예외의 전체 클래스 중 하나를 임의로 throw할 수 있습니다. 따라서 I/O API를 호출할 때 다음 표와 같이 이러한 예외를 대부분 또는 모두 처리할 수 있도록 코드를 준비해야 합니다.

| 예외 형식 | .NET Core | .NET Framework |
|---|---|---|
| <xref:System.IO.IOException> | 예 | 예 |
| <xref:System.IO.FileNotFoundException> | 예 | 예 |
| <xref:System.IO.DirectoryNotFoundException> | 예 | 예 |
| <xref:System.IO.DriveNotFoundException?> | 예 | 예 |
| <xref:System.IO.PathTooLongException> | 예 | 예 |
| <xref:System.OperationCanceledException> | 예 | 예 |
| <xref:System.UnauthorizedAccessException> | 예 | 예 |
| <xref:System.ArgumentException> | .NET Core 2.0 및 이전| 예 |
| <xref:System.NotSupportedException> | 아니요 | 예 |
| <xref:System.Security.SecurityException> | 아니요 | 제한된 신뢰만 |

## <a name="handling-ioexception"></a>IOException 처리

<xref:System.IO> 네임스페이스에 있는 예외의 기본 클래스인 <xref:System.IO.IOException>은 미리 정의된 예외 유형에 매핑되지 않는 오류 코드에 대해서도 throw됩니다. 따라서 이 예외는 모든 I/O 작업에서 throw될 수 있습니다.

> [!IMPORTANT]
> <xref:System.IO.IOException>은 <xref:System.IO> 네임스페이스에 있는 다른 예외 유형의 기본 클래스이므로 다른 I/O 관련 예외를 처리한 후에 `catch` 블록에서 처리해야 합니다.

또한 .NET Core 2.1부터 경로 정확성에 대한 유효성 검사(예: 경로에 잘못된 문자가 없는지 확인)가 제거되었으며, 런타임 시 자체 유효성 검사 코드가 아닌 운영 체제 오류 코드에서 매핑된 예외가 throw됩니다. 이 경우에 throw될 가능성이 큰 예외는 <xref:System.IO.IOException>이지만 다른 예외 유형도 throw될 수 있습니다.

예외 처리 코드에서 <xref:System.IO.IOException>을 항상 마지막에 처리해야 합니다. 그러지 않으면 다른 모든 IO 예외의 기본 클래스이므로 파생 클래스의 catch 블록이 평가되지 않습니다.

<xref:System.IO.IOException>의 경우 [IOException.HResult](xref:System.Exception.HResult) 속성에서 추가 오류 정보를 얻을 수 있습니다. HResult 값을 Win32 오류 코드로 변환하려면 32비트 값의 상위 16비트를 제거합니다. 다음 표에는 <xref:System.IO.IOException>에 래핑될 수 있는 오류 코드가 나와 있습니다.

| HResult | 상수 | 설명 |
| --- | --- | --- |
| ERROR_SHARING_VIOLATION | 32 | 파일 이름이 없거나 파일 또는 디렉터리가 사용 중입니다. |
| ERROR_FILE_EXISTS | 80 | 파일이 이미 있습니다. |
| ERROR_INVALID_PARAMETER | 87 | 메서드에 제공된 인수가 잘못되었습니다. |
| ERROR_ALREADY_EXISTS | 183 | 파일 또는 디렉터리가 이미 있습니다. |

다음 예제와 같이 catch 문에서 `When` 절을 사용하여 이러한 예외를 처리할 수 있습니다.

[!code-csharp[io-exception-handling](~/samples/snippets/standard/io/io-exceptions/cs/io-exceptions.cs)]
[!code-vb[io-exception-handling](~/samples/snippets/standard/io/io-exceptions/vb/io-exceptions.vb)]

## <a name="see-also"></a>참고 항목

- [.NET의 예외 처리 및 Throw](../exceptions/index.md)
- [예외 처리(작업 병렬 라이브러리)](../parallel-programming/exception-handling-task-parallel-library.md)
- [예외에 대한 모범 사례](../exceptions/best-practices-for-exceptions.md)
- [catch 블록에서 특정 예외를 사용하는 방법](../exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)
