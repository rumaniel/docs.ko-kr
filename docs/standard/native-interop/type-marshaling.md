---
title: 형식 마샬링 - .NET
description: .NET에서 형식을 네이티브 표현으로 마샬링하는 방법을 알아봅니다.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: bc44a2c63dfa3fde3e3c4197e5d1fe79857ea717
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929060"
---
# <a name="type-marshaling"></a>형식 마샬링

**마샬링**은 관리 코드와 네이티브 코드 간에 변환해야 하는 경우 형식을 변환하는 프로세스입니다.

관리 코드와 비관리 코드의 형식이 서로 다르기 때문에 마샬링이 필요합니다. 예를 들어 관리 코드에서는 `String`을 사용하지만 관리되지 않는 환경에서는 문자열이 유니코드(“와이드”), 비유니코드, null 종료, ASCII 등일 수 있습니다. 기본적으로 P/Invoke 하위 시스템은 이 문서에 설명된 기본 동작에 따라 올바른 작업을 수행하려고 합니다. 그러나 추가 제어가 필요한 경우 [MarshalAs](xref:System.Runtime.InteropServices.MarshalAsAttribute) 특성을 사용하여 관리되지 않는 쪽에서 필요한 형식을 지정할 수 있습니다. 예를 들어 문자열을 null 종료 ANSI 문자열로 보내려는 경우 다음과 같이 할 수 있습니다.

```csharp
[DllImport("somenativelibrary.dll")]
static extern int MethodA([MarshalAs(UnmanagedType.LPStr)] string parameter);
```

## <a name="default-rules-for-marshaling-common-types"></a>일반 형식을 마샬링하기 위한 기본 규칙

일반적으로 런타임은 최소한의 사용자 작업이 필요하도록 마샬링할 때 “올바른 작업”을 수행하려고 합니다. 다음 표에서는 매개 변수 또는 필드에 사용할 때 각 형식이 기본적으로 마샬링되는 방식을 설명합니다. C99/C++11 고정 너비 정수 및 문자 형식은 다음 표의 내용이 모든 플랫폼에 적용되도록 하는 데 사용됩니다. 맞춤 및 크기 요구 사항이 이러한 형식과 동일한 모든 네이티브 형식을 사용할 수 있습니다.

이 첫 번째 표에서는 마샬링이 P/Invoke 및 필드 마샬링에 대해 동일한 다양한 형식의 매핑을 설명합니다.

| .NET 형식 | 네이티브 형식  |
|-----------|-------------------------|
| `byte`    | `uint8_t`               |
| `sbyte`   | `int8_t`                |
| `short`   | `int16_t`               |
| `ushort`  | `uint16_t`              |
| `int`     | `int32_t`               |
| `uint`    | `uint32_t`              |
| `long`    | `int64_t`               |
| `ulong`   | `uint64_t`              |
| `char`    | P/Invoke 또는 구조체의 `CharSet`에 따라 `char` 또는 `char16_t`입니다. [문자 집합 문서](charset.md)를 참조하세요. |
| `string`  | P/Invoke 또는 구조체의 `CharSet`에 따라 `char*` 또는 `char16_t*`입니다. [문자 집합 문서](charset.md)를 참조하세요. |
| `System.IntPtr` | `intptr_t`        |
| `System.UIntPtr` | `uintptr_t`      |
| .NET 포인터 형식(예: `void*`)  | `void*` |
| `System.Runtime.InteropServices.SafeHandle`에서 파생된 형식 | `void*` |
| `System.Runtime.InteropServices.CriticalHandle`에서 파생된 형식 | `void*`          |
| `bool`    | Win32 `BOOL` 형식       |
| `decimal` | COM `DECIMAL` 구조체 |
| .NET 대리자 | 네이티브 함수 포인터 |
| `System.DateTime` | Win32 `DATE` 형식 |
| `System.Guid` | Win32 `GUID` 형식 |

매개 변수 또는 구조체로 마샬링하는 경우 마샬링의 몇 가지 범주에 다른 기본값이 있습니다.

| .NET 형식 | 네이티브 형식(매개 변수) | 네이티브 형식(필드) |
|-----------|-------------------------|---------------------|
| .NET 배열 | 배열 요소의 네이티브 표현 배열 시작을 가리키는 포인터 | `[MarshalAs]` 특성이 없으면 허용되지 않음|
| `LayoutKind`가 `Sequential` 또는 `Explicit`인 클래스 | 클래스의 네이티브 표현을 가리키는 포인터 | 클래스의 네이티브 표현 |

다음 표에는 Windows 전용인 기본 마샬링 규칙이 나와 있습니다. 비 Windows 플랫폼에서는 다음 형식을 마샬링할 수 없습니다.

| .NET 형식 | 네이티브 형식(매개 변수) | 네이티브 형식(필드) |
|-----------|-------------------------|---------------------|
| `object`  | `VARIANT`               | `IUnknown*`         |
| `System.Array` | COM 인터페이스 | `[MarshalAs]` 특성이 없으면 허용되지 않음 |
| `System.ArgIterator` | `va_list` | 허용되지 않음 |
| `System.Collections.IEnumerator` | `IEnumVARIANT*` | 허용되지 않음 |
| `System.Collections.IEnumerable` | `IDispatch*` | 허용되지 않음 |
| `System.DateTimeOffset` | 1601년 1월 1일 자정 이후의 틱 수를 나타내는 `int64_t` || 1601년 1월 1일 자정 이후의 틱 수를 나타내는 `int64_t` |

일부 형식은 필드가 아닌 매개 변수로만 마샬링할 수 있습니다. 해당 형식은 다음 표에 나와 있습니다.

| .NET 형식 | 네이티브 형식(매개 변수만 해당) |
|-----------|------------------------------|
| `System.Text.StringBuilder` | P/Invoke의 `CharSet`에 따라 `char*` 또는 `char16_t*`입니다.  [문자 집합 문서](charset.md)를 참조하세요. |
| `System.ArgIterator` | `va_list`(Windows x86/x64/arm64만 해당) |
| `System.Runtime.InteropServices.ArrayWithOffset` | `void*` |
| `System.Runtime.InteropServices.HandleRef` | `void*` |

이러한 기본값이 원하는 동작을 정확히 수행하지 않는 경우 매개 변수의 마샬링 방식을 사용자 지정할 수 있습니다. [매개 변수 마샬링](customize-parameter-marshaling.md) 문서에서는 여러 매개 변수 형식의 마샬링 방식을 사용자 지정하는 방법을 안내합니다.

## <a name="default-marshaling-in-com-scenarios"></a>COM 시나리오의 기본 마샬링

.NET에서 COM 개체에 대한 메서드를 호출할 때 .NET 런타임은 일반적인 COM 의미 체계와 일치하도록 기본 마샬링 규칙을 변경합니다. 다음 표에서는 .NET 런타임이 COM 시나리오에서 사용하는 규칙을 나열합니다.

| .NET 형식 | 네이티브 형식(COM 메서드 호출) |
|-----------|--------------------------------|
| `bool`    | `VARIANT_BOOL`                 |
| `StringBuilder` | `LPWSTR`                 |
| `string`  | `BSTR`                         |
| 대리자 형식 | .NET Framework의 `_Delegate*`. .NET Core에서는 허용되지 않습니다. |
| `System.Drawing.Color` | `OLECOLOR`        |
| .NET 배열 | `SAFEARRAY`                   |
| `string[]` | `BSTR`의 `SAFEARRAY`        |

## <a name="marshaling-classes-and-structs"></a>클래스 및 구조체 마샬링

형식 마샬링의 또 다른 측면은 비관리형 메서드에 구조체를 전달하는 방법입니다. 예를 들어 관리되지 않는 일부 메서드의 경우 매개 변수로 구조체가 필요합니다. 이러한 경우 관리형 부분에서 해당 구조체 또는 클래스를 만들어 매개 변수로 사용해야 합니다. 그러나 클래스 정의만으로는 충분하지 않습니다. 클래스의 필드를 비관리형 구조체에 매핑하는 방법도 마샬러에 지정해야 합니다. 여기서 `StructLayout` 특성이 유용합니다.

```csharp
[DllImport("kernel32.dll")]
static extern void GetSystemTime(SystemTime systemTime);

[StructLayout(LayoutKind.Sequential)]
class SystemTime {
    public ushort Year;
    public ushort Month;
    public ushort DayOfWeek;
    public ushort Day;
    public ushort Hour;
    public ushort Minute;
    public ushort Second;
    public ushort Milsecond;
}

public static void Main(string[] args) {
    SystemTime st = new SystemTime();
    GetSystemTime(st);
    Console.WriteLine(st.Year);
}
```

앞의 코드는 `GetSystemTime()` 함수를 호출하는 간단한 예제를 보여 줍니다. 흥미로운 부분은 줄 4에 있습니다. 특성이 클래스의 필드를 다른 쪽(비관리)의 구조체에 순차적으로 매핑하도록 지정합니다. 즉, 다음 예제와 같이 비관리형 구조체에 대응해야 하므로 필드의 이름 지정은 중요하지 않고 해당 순서만 중요합니다.

```c
typedef struct _SYSTEMTIME {
  WORD wYear;
  WORD wMonth;
  WORD wDayOfWeek;
  WORD wDay;
  WORD wHour;
  WORD wMinute;
  WORD wSecond;
  WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME;
```

구조체에 대한 기본 마샬링이 필요한 것이 아닌 경우도 있습니다. [구조 마샬링 사용자 지정](./customize-struct-marshaling.md) 문서에서는 구조체의 마샬링 방식을 사용자 지정하는 방법을 설명합니다.
