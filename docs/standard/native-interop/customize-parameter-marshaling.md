---
title: 매개 변수 마샬링 사용자 지정 - .NET
description: .NET에서 매개 변수를 네이티브 표현으로 마샬링하는 방식을 사용자 지정하는 방법을 알아봅니다.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: 877eb00c18c9108fe6bcfb50104ff5ed813e85f3
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065976"
---
# <a name="customizing-parameter-marshaling"></a>매개 변수 마샬링 사용자 지정

.NET 런타임의 기본 매개 변수 마샬링 동작이 원하는 대로 작동하지 않을 경우, <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> 특성을 사용하여 매개 변수가 마샬링되는 방식을 사용자 지정할 수 있습니다.

## <a name="customizing-string-parameters"></a>문자열 매개 변수 사용자 지정

.NET에는 문자열을 마샬링하기 위한 다양한 형식이 있습니다. 이러한 메서드는 C 스타일 문자열 및 Windows 중심 문자열 형식에 대한 개별 섹션으로 나누어져 있습니다.

### <a name="c-style-strings"></a>C 스타일 문자열

이러한 형식은 각각 Null 종료 문자열을 네이티브 코드에 전달하며, 네이티브 문자열의 인코딩에 따라 다릅니다.

| `System.Runtime.InteropServices.UnmanagedType` 값 | 인코딩 |
|------------------------------------------------------|----------|
| LPStr | ANSI |
| LPUTF8Str | UTF-8 | 
| LPWStr | UTF-16 |
| LPTStr | UTF-16 |

<xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=nameWithType> 형식은 약간 다릅니다. `LPWStr`과 마찬가지로, 이 형식은 문자열을 UTF-16으로 인코드된 네이티브 C 스타일 문자열로 마샬링합니다. 그러나 관리형 시그니처는 문자열을 참조로 전달하게 하고, 일치하는 네이티브 시그니처는 문자열을 값으로 사용합니다. 이러한 차이를 통해 `StringBuilder`를 사용하지 않고도 문자열을 값으로 사용하고 현재 위치에서 수정하는 네이티브 API를 사용할 수 있습니다. 네이티브 시그니처와 관리형 시그니처의 불일치와 혼동되는 경향이 있으므로 이 형식을 수동으로 사용하지 않는 것이 좋습니다.

### <a name="windows-centric-string-formats"></a>Windows 중심 문자열 형식

COM 또는 OLE 인터페이스를 조작하는 경우 네이티브 함수가 문자열을 `BSTR` 인수로 사용하는 것을 보게 될 가능성이 큽니다. <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> 비관리형 형식을 사용하여 문자열을 `BSTR`로 마샬링할 수 있습니다.

WinRT API를 조작하는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> 형식을 사용하여 문자열을 `HSTRING`로 마샬링할 수 있습니다.

## <a name="customizing-array-parameters"></a>배열 매개 변수 사용자 지정

.NET에서는 배열 매개 변수를 마샬링하는 몇 가지 방법도 제공합니다. C 스타일 배열을 사용하는 API를 호출하는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.LPArray?displayProperty=nameWithType> 비관리형 형식을 사용합니다. 배열의 값에 사용자 지정 마샬링이 필요한 경우 해당 배열의 `[MarshalAs]` 특성에 있는 <xref:System.Runtime.InteropServices.MarshalAsAttribute.ArraySubType> 필드를 사용할 수 있습니다.

COM API를 사용하는 경우 배열 매개 변수를 `SAFEARRAY*`로 마샬링해야 할 가능성이 큽니다. 이렇게 하려면 <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> 비관리형 형식을 사용할 수 있습니다. `SAFEARRAY` 요소의 기본 형식은 [`object` 필드 사용자 지정](./customize-struct-marshaling.md#marshaling-systemobjects)에 대한 표에서 확인할 수 있습니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> 및 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> 필드를 사용하여 `SAFEARRAY`의 정확한 요소 형식을 사용자 지정할 수 있습니다.

## <a name="customizing-boolean-or-decimal-parameters"></a>부울 또는 10진 매개 변수 사용자 지정

부울 또는 10진 매개 변수 마샬링에 대한 자세한 내용은 [구조체 마샬링 사용자 지정](customize-struct-marshaling.md)을 참조하세요.

## <a name="customizing-object-parameters-windows-only"></a>개체 매개 변수 사용자 지정(Windows에만 해당)

Windows에서 .NET 런타임은 개체 매개 변수를 네이티브 코드로 마샬링하는 몇 가지 방법을 제공합니다.

### <a name="marshaling-as-specific-com-interfaces"></a>특정 COM 인터페이스로 마샬링

API에서 COM 개체에 대한 포인터를 사용하는 경우 `object` 형식 매개 변수에 다음과 같은 `UnmanagedType` 형식 중 하나를 사용하여 이러한 특정 인터페이스로 마샬링하도록 .NET에 지정할 수 있습니다.

- `IUnknown`
- `IDispatch`
- `IInspectable`

또한 형식이 `[ComVisible(true)]`로 표시되거나 `object` 형식을 마샬링하는 경우 <xref:System.Runtime.InteropServices.UnmanagedType.Interface?displayProperty=nameWithType> 형식을 사용하여 해당 형식의 COM 보기에 대한 COM 호출 가능 래퍼로 개체를 마샬링할 수 있습니다.

### <a name="marshaling-to-a-variant"></a>`VARIANT`로 마샬링

네이티브 API에서 Win32 `VARIANT`를 사용하는 경우 `object` 매개 변수의 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> 형식을 사용하여 개체를 `VARIANT`로 마샬링할 수 있습니다. .NET 형식과 `VARIANT` 형식 간의 매핑에 대해서는 [`object` 필드 사용자 지정](customize-struct-marshaling.md#marshaling-systemobjects) 문서를 참조하세요.

### <a name="custom-marshalers"></a>사용자 설정 마샬러

네이티브 COM 인터페이스를 다른 관리형 형식으로 프로젝트하려는 경우 `UnmanagedType.CustomMarshaler` 형식과 <xref:System.Runtime.InteropServices.ICustomMarshaler> 구현을 사용하여 사용자 고유의 사용자 지정 마샬링 코드를 제공할 수 있습니다.
