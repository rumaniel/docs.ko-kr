---
title: 구조체 마샬링 사용자 지정 - .NET
description: .NET에서 구조체를 네이티브 표현으로 마샬링하는 방식을 사용자 지정하는 방법을 알아봅니다.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
dev_langs:
- csharp
- cpp
ms.openlocfilehash: b174a817e82f9a9f123c79581656cc8e7179b435
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929032"
---
# <a name="customizing-structure-marshaling"></a>구조체 마샬링 사용자 지정

구조체의 기본 마샬링 규칙이 필요한 것과 정확히 일치하지 않는 경우가 있습니다. .NET 런타임에서는 구조체 레이아웃과 필드 마샬링 방식을 사용자 지정할 수 있는 몇 가지 확장점을 제공합니다.

## <a name="customizing-structure-layout"></a>구조체 레이아웃 사용자 지정

.NET에서는 메모리에 필드가 배치되는 방식을 사용자 지정할 수 있도록 <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> 특성과 <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=nameWithType> 열거형을 제공합니다. 다음 지침은 일반적인 문제를 방지하는 데 도움이 됩니다.

**✔️** 가능한 경우 항상 `LayoutKind.Sequential`을 사용하는 것이 좋습니다.

**✔️** 네이티브 구조체에 공용 구조체 등의 명시적인 레이아웃도 있는 경우에만 마샬링할 때 `LayoutKind.Explicit`를 사용합니다.

**❌** 비 Windows 플랫폼에서 구조체를 마샬링하는 경우 `LayoutKind.Explicit`를 사용하지 않습니다. .NET Core 런타임을 통해 Intel 또는 AMD 64비트 비 Windows 시스템에서 명시적 구조체를 네이티브 함수에 값으로 전달할 수 없습니다. 그러나 런타임은 모든 플랫폼에서 명시적 구조체를 참조로 전달하는 기능을 지원합니다.

## <a name="customizing-boolean-field-marshaling"></a>부울 필드 마샬링 사용자 지정

네이티브 코드에는 여러 부울 표현이 있습니다. Windows만 해도 부울 값을 나타내는 세 가지 방법이 있습니다. 런타임은 구조체의 네이티브 정의를 알 수 없으므로, 부울 값을 나타내는 최상의 방법은 부울 값을 마샬링하는 방식을 추측하는 것입니다. .NET 런타임에서 부울 필드를 마샬링하는 방식을 나타내는 방법을 제공합니다. 다음 예제에서는 .NET `bool`을 여러 네이티브 부울 형식으로 마샬링하는 방법을 보여 줍니다.

다음 예제와 같이 부울 값은 기본적으로 네이티브 4바이트 Win32 [`BOOL`](/windows/desktop/winprog/windows-data-types#BOOL) 값으로 마샬링되도록 설정됩니다.

```csharp
public struct WinBool
{
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

명시적으로 설정하려는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.Bool?displayProperty=nameWithType> 값을 사용하여 위와 동일한 동작을 얻을 수 있습니다.

```csharp
public struct WinBool
{
    [MarshalAs(UnmanagedType.Bool)]
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

아래의 `UnmanagedType.U1` 또는 `UnmanagedType.I1` 값을 사용하여 `b` 필드를 1바이트 네이티브 `bool` 형식으로 마샬링하도록 런타임에 지정할 수 있습니다.

```csharp
public struct CBool
{
    [MarshalAs(UnmanagedType.U1)]
    public bool b;
}
```

```cpp
struct CBool
{
    public bool b;
};
```

Windows에서는 <xref:System.Runtime.InteropServices.UnmanagedType.VariantBool?displayProperty=nameWithType> 값을 사용하여 부울 값을 2바이트 `VARIANT_BOOL` 값으로 마샬링하도록 런타임에 지정할 수 있습니다.

```csharp
public struct VariantBool
{
    [MarshalAs(UnmanagedType.VariantBool)]
    public bool b;
}
```

```cpp
struct VariantBool
{
    public VARIANT_BOOL b;
};
```

> [!NOTE]
> `VARIANT_BOOL`은 `VARIANT_TRUE = -1` 및 `VARIANT_FALSE = 0`인 점에서 대부분의 bool 형식과는 다릅니다. 또한 `VARIANT_TRUE`와 같지 않은 모든 값은 false로 간주됩니다.

## <a name="customizing-array-field-marshaling"></a>배열 필드 마샬링 사용자 지정

.NET에는 배열 마샬링을 사용자 지정하는 몇 가지 방법도 있습니다.

기본적으로 .NET에서는 배열을 인접한 요소 목록에 대한 포인터로 마샬링합니다.

```csharp
public struct DefaultArray
{
    public int[] values;
}
```

```cpp
struct DefaultArray
{
    int* values;
};
```

COM API와 인터페이스하는 경우 배열을 `SAFEARRAY*` 개체로 마샬링해야 할 수도 있습니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> 및 <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> 값을 사용하여 배열을 `SAFEARRAY*`로 마샬링하도록 런타임에 지정할 수 있습니다.

```csharp
public struct SafeArrayExample
{
    [MarshalAs(UnmanagedType.SafeArray)]
    public int[] values;
}
```

```cpp
struct SafeArrayExample
{
    SAFEARRAY* values;
};
```

`SAFEARRAY`에 포함되는 요소 형식을 사용자 지정해야 하는 경우 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> 및 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> 필드를 사용하여 `SAFEARRAY`의 정확한 요소 형식을 사용자 지정할 수 있습니다.

현재 위치에서 배열을 마샬링해야 하는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> 값을 사용하여 현재 위치에서 배열을 마샬링하도록 마샬러에 지정할 수 있습니다. 이 마샬링을 사용하는 경우, 런타임에서 구조체의 공간을 올바르게 할당할 수 있도록 배열의 요소 수에 대한 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> 필드에도 값을 제공해야 합니다.

```csharp
public struct InPlaceArray
{
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public int[] values;
}
```

```cpp
struct InPlaceArray
{
    int values[4];
};
```

> [!NOTE]
> .NET에서는 가변 길이 배열 필드를 C99 유연한 배열 멤버로 마샬링할 수 없습니다.

## <a name="customizing-string-field-marshaling"></a>문자열 필드 마샬링 사용자 지정

.NET에서는 문자열 필드를 마샬링하기 위한 다양한 사용자 지정도 제공합니다.

기본적으로 .NET은 문자열을 Null 종료 문자열에 대한 포인터로 마샬링합니다. 인코딩은 <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType>의 <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> 필드 값에 따라 다릅니다. 특성을 지정하지 않으면 인코딩은 기본적으로 ANSI 인코딩으로 설정됩니다.

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char* str;
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

다른 필드에 다른 인코딩을 사용해야 하거나 구조체 정의를 좀 더 명시적으로 설정하려는 경우 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> 특성에 <xref:System.Runtime.InteropServices.UnmanagedType.LPStr?displayProperty=nameWithType> 또는 <xref:System.Runtime.InteropServices.UnmanagedType.LPWStr?displayProperty=nameWithType> 값을 사용할 수 있습니다.

```csharp
public struct AnsiString
{
    [MarshalAs(UnmanagedType.LPStr)]
    public string str;
}
```

```cpp
struct AnsiString
{
    char* str;
};
```

```csharp
public struct UnicodeString
{
    [MarshalAs(UnmanagedType.LPWStr)]
    public string str;
}
```

```cpp
struct UnicodeString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

UTF-8 인코딩을 사용하여 문자열을 마샬링하려는 경우 <xref:System.Runtime.InteropServices.MarshalAsAttribute>의 <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> 값을 사용할 수 있습니다.

```csharp
public struct UTF8String
{
    [MarshalAs(UnmanagedType.LPUTF8Str)]
    public string str;
}
```

```cpp
struct UTF8String
{
    char* str;
};
```

> [!NOTE]
> <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType>을 사용하려면 .NET Framework 4.7 이상 버전이나 .NET Core 1.1 이상 버전이 필요합니다. .NET Standard 2.0에서는 사용할 수 없습니다.

COM API로 작업하는 경우 문자열을 `BSTR`로 마샬링해야 할 수도 있습니다. <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> 값을 사용하여 문자열을 `BSTR`로 마샬링할 수 있습니다.

```csharp
public struct BString
{
    [MarshalAs(UnmanagedType.BStr)]
    public string str;
}
```

```cpp
struct BString
{
    BSTR str;
};
```

WinRT 기반 API를 사용하는 경우 문자열을 `HSTRING`로 마샬링해야 할 수도 있습니다.  <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> 값을 사용하여 문자열을 `HSTRING`로 마샬링할 수 있습니다.

```csharp
public struct HString
{
    [MarshalAs(UnmanagedType.HString)]
    public string str;
}
```

```cpp
struct BString
{
    HSTRING str;
};
```

API에서 구조체의 현재 위치에 문자열을 전달해야 하는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.ByValTStr?displayProperty=nameWithType> 값을 사용할 수 있습니다. `ByValTStr`에 의해 마샬링된 문자열의 인코딩은 `CharSet` 특성으로 결정됩니다. 또한 문자열 길이가 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> 필드에 의해 전달되어야 합니다.

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char str[4];
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t str[4]; // Could also be wchar_t[4] on Windows.
};
```

## <a name="customizing-decimal-field-marshaling"></a>10진 필드 마샬링 사용자 지정

Windows에서 작업하는 경우 네이티브 [`CY` 또는 `CURRENCY`](/windows/win32/api/wtypes/ns-wtypes-cy~r1) 구조체를 사용하는 일부 API를 발견할 수 있습니다. 기본적으로 .NET `decimal` 형식은 네이티브 [ `DECIMAL`](/windows/win32/api/wtypes/ns-wtypes-decimal~r1) 구조체로 마샬링됩니다. 그러나 <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=nameWithType> 값과 함께 <xref:System.Runtime.InteropServices.MarshalAsAttribute>를 사용하여 `decimal` 값을 네이티브 `CY` 값으로 변환하도록 마샬러에 지정할 수 있습니다.

```csharp
public struct Currency
{
    [MarshalAs(UnmanagedType.Currency)]
    public decimal dec;
}
```

```cpp
struct Currency
{
    CY dec;
};
```

## <a name="marshaling-systemobjects"></a>`System.Object` 마샬링

Windows에서 `object` 형식 필드를 네이티브 코드로 마샬링할 수 있습니다. 이러한 필드는 다음 세 가지 형식 중 하나로 마샬링할 수 있습니다.

- [`VARIANT`](/windows/win32/api/oaidl/ns-oaidl-variant)
- [`IUnknown*`](/windows/desktop/api/unknwn/nn-unknwn-iunknown)
- [`IDispatch*`](/windows/desktop/api/oaidl/nn-oaidl-idispatch)

기본적으로 `object` 형식 필드는 개체를 래핑하는 `IUnknown*`으로 마샬링됩니다.

```csharp
public struct ObjectDefault
{
    public object obj;
}
```

```cpp
struct ObjectDefault
{
    IUnknown* obj;
};
```

개체 필드를 `IDispatch*`로 마샬링하려는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType> 값과 함께 <xref:System.Runtime.InteropServices.MarshalAsAttribute>를 추가합니다.

```csharp
public struct ObjectDispatch
{
    [MarshalAs(UnmanagedType.IDispatch)]
    public object obj;
}
```

```cpp
struct ObjectDispatch
{
    IDispatch* obj;
};
```

`VARIANT`로 마샬링하려는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> 값과 함께 <xref:System.Runtime.InteropServices.MarshalAsAttribute>를 추가합니다.

```csharp
public struct ObjectVariant
{
    [MarshalAs(UnmanagedType.Struct)]
    public object obj;
}
```

```cpp
struct ObjectVariant
{
    VARIANT obj;
};
```

다음 표에서는 `obj` 필드의 여러 런타임 형식이 `VARIANT`에 저장된 다양한 형식에 매핑되는 방식을 설명합니다.

| .NET 형식 | VARIANT 형식 | | .NET 형식 | VARIANT 형식 |
|------------|--------------|-|----------|--------------|
|  `byte`  | `VT_UI1` |     | `System.Runtime.InteropServices.BStrWrapper` | `VT_BSTR` |
| `sbyte`  | `VT_I1`  |     | `object`  | `VT_DISPATCH` |
| `short`  | `VT_I2`  |     | `System.Runtime.InteropServices.UnknownWrapper` | `VT_UNKNOWN` |
| `ushort` | `VT_UI2` |     | `System.Runtime.InteropServices.DispatchWrapper` | `VT_DISPATCH` |
| `int`    | `VT_I4`  |     | `System.Reflection.Missing` | `VT_ERROR` |
| `uint`   | `VT_UI4` |     | `(object)null` | `VT_EMPTY` |
| `long`   | `VT_I8`  |     | `bool` | `VT_BOOL` |
| `ulong`  | `VT_UI8` |     | `System.DateTime` | `VT_DATE` |
| `float`  | `VT_R4`  |     | `decimal` | `VT_DECIMAL` |
| `double` | `VT_R8`  |     | `System.Runtime.InteropServices.CurrencyWrapper` | `VT_CURRENCY` |
| `char`   | `VT_UI2` |     | `System.DBNull` | `VT_NULL` |
| `string` | `VT_BSTR`|
