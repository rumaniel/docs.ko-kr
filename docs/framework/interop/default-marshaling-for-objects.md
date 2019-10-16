---
title: 개체에 대한 마샬링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- objects, interop marshaling
- interop marshaling, objects
ms.assetid: c2ef0284-b061-4e12-b6d3-6a502b9cc558
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b2c6e8a013d6486ec55723b91d6bfb6b838c9be5
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044175"
---
# <a name="default-marshaling-for-objects"></a>개체에 대한 마샬링

<xref:System.Object?displayProperty=nameWithType>로 형식화된 매개 변수와 필드는 비관리 코드에 다음 형식 하나로 표시할 수 있습니다.

- 개체가 매개 변수인 경우 변형.

- 개체가 구조체 필드인 경우 인터페이스.

COM interop만 개체 형식에 대한 마샬링을 지원합니다. 기본 동작은 개체를 COM 변형으로 마샬링하는 것입니다. 이러한 규칙은 **개체**에만 적용되고 **Object** 클래스에서 파생되는 강력한 형식의 개체에는 적용되지 않습니다.

## <a name="marshaling-options"></a>마샬링 옵션

다음 표에서는 **Object** 데이터 형식에 대한 마샬링 옵션을 보여 줍니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성은 개체를 마샬링하기 위한 여러 <xref:System.Runtime.InteropServices.UnmanagedType> 열거형 값을 제공합니다.

|열거형 형식|관리되지 않는 형식에 대한 설명|
|----------------------|-------------------------------------|
|**UnmanagedType.Struct**<br /><br /> (매개 변수 기본값)|COM 스타일 변형.|
|**UnmanagedType.Interface**|**IDispatch** 인터페이스(가능한 경우), 이외에는 **IUnknown** 인터페이스.|
|**UnmanagedType.IUnknown**<br /><br /> (필드 기본값)|**IUnknown** 인터페이스.|
|**UnmanagedType.IDispatch**|**IDispatch** 인터페이스.|

다음 예제에서는 `MarshalObject`에 대한 관리되는 인터페이스 정의를 보여 줍니다.

```vb
Interface MarshalObject
   Sub SetVariant(o As Object)
   Sub SetVariantRef(ByRef o As Object)
   Function GetVariant() As Object

   Sub SetIDispatch( <MarshalAs(UnmanagedType.IDispatch)> o As Object)
   Sub SetIDispatchRef(ByRef <MarshalAs(UnmanagedType.IDispatch)> o _
      As Object)
   Function GetIDispatch() As <MarshalAs(UnmanagedType.IDispatch)> Object
   Sub SetIUnknown( <MarshalAs(UnmanagedType.IUnknown)> o As Object)
   Sub SetIUnknownRef(ByRef <MarshalAs(UnmanagedType.IUnknown)> o _
      As Object)
   Function GetIUnknown() As <MarshalAs(UnmanagedType.IUnknown)> Object
End Interface
```

```csharp
interface MarshalObject {
   void SetVariant(Object o);
   void SetVariantRef(ref Object o);
   Object GetVariant();

   void SetIDispatch ([MarshalAs(UnmanagedType.IDispatch)]Object o);
   void SetIDispatchRef([MarshalAs(UnmanagedType.IDispatch)]ref Object o);
   [MarshalAs(UnmanagedType.IDispatch)] Object GetIDispatch();
   void SetIUnknown ([MarshalAs(UnmanagedType.IUnknown)]Object o);
   void SetIUnknownRef([MarshalAs(UnmanagedType.IUnknown)]ref Object o);
   [MarshalAs(UnmanagedType.IUnknown)] Object GetIUnknown();
}
```

다음 코드는 `MarshalObject` 인터페이스를 형식 라이브러리에 내보냅니다.

```cpp
interface MarshalObject {
   HRESULT SetVariant([in] VARIANT o);
   HRESULT SetVariantRef([in,out] VARIANT *o);
   HRESULT GetVariant([out,retval] VARIANT *o)
   HRESULT SetIDispatch([in] IDispatch *o);
   HRESULT SetIDispatchRef([in,out] IDispatch **o);
   HRESULT GetIDispatch([out,retval] IDispatch **o)
   HRESULT SetIUnknown([in] IUnknown *o);
   HRESULT SetIUnknownRef([in,out] IUnknown **o);
   HRESULT GetIUnknown([out,retval] IUnknown **o)
}
```

> [!NOTE]
> Interop 마샬러는 호출한 후 변형 내부에서 할당된 메모리를 자동으로 해제합니다.

다음 예제에서는 서식 있는 값 형식을 보여 줍니다.

```vb
Public Structure ObjectHolder
   Dim o1 As Object
   <MarshalAs(UnmanagedType.IDispatch)> Public o2 As Object
End Structure
```

```csharp
public struct ObjectHolder {
   Object o1;
   [MarshalAs(UnmanagedType.IDispatch)]public Object o2;
}
```

다음 코드는 서식 있는 형식을 형식 라이브러리에 내보냅니다.

```cpp
struct ObjectHolder {
   VARIANT o1;
   IDispatch *o2;
}
```

## <a name="marshaling-object-to-interface"></a>인터페이스에 개체 마샬링

개체가 COM에 인터페이스로 노출되면 해당 인터페이스는 관리되는 형식 <xref:System.Object>에 대한 클래스 인터페이스입니다( **_Object** 인터페이스). 이 인터페이스는 결과 형식 라이브러리에서 **IDispatch**(<xref:System.Runtime.InteropServices.UnmanagedType>) 또는 **IUnknown**(**UnmanagedType.IUnknown**)으로 형식화됩니다. COM 클라이언트는 **_Object** 인터페이스를 통해 관리되는 클래스 또는 파생 클래스에 의해 구현된 모든 멤버를 동적으로 호출할 수 있습니다. 클라이언트는 **QueryInterface**를 호출하여 관리되는 형식에 의해 명시적으로 구현된 다른 인터페이스를 가져올 수도 있습니다.

## <a name="marshaling-object-to-variant"></a>변형에 개체 마샬링

개체가 변형에 마샬링되면 내부 변형 형식은 런타임에 다음 규칙에 따라 결정됩니다.

- 개체 참조가 null(Visual Basic의 경우 **Nothing**)이면 개체는 **VT_EMPTY** 형식 변형에 마샬링됩니다.

- 개체가 다음 표에 나열된 형식의 인스턴스이면 결과 변형 형식은 표에 나와 있는 대로 마샬러에 기본 제공된 규칙에 따라 결정됩니다.

- 마샬링 동작을 명시적으로 제어해야 하는 기타 개체는 <xref:System.IConvertible> 인터페이스를 구현합니다. 이 경우 변형 형식은 <xref:System.IConvertible.GetTypeCode%2A?displayProperty=nameWithType> 메서드에서 반환된 형식 코드에 의해 결정됩니다. 이외의 경우에는 개체가 **VT_UNKNOWN** 형식 변형으로 마샬링됩니다.

### <a name="marshaling-system-types-to-variant"></a>변형에 시스템 형식 마샬링

다음 표에서는 관리 개체 형식 및 해당 COM 변형 형식을 보여 줍니다. 이러한 형식은 호출되는 메서드의 시그니처가 <xref:System.Object?displayProperty=nameWithType> 형식인 경우에만 변환됩니다.

|개체 유형|COM 변형 형식|
|-----------------|----------------------|
|Null 개체 참조(Visual Basic의 경우 **Nothing**).|**VT_EMPTY**|
|<xref:System.DBNull?displayProperty=nameWithType>|**VT_NULL**|
|<xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=nameWithType>|**VT_ERROR**|
|<xref:System.Reflection.Missing?displayProperty=nameWithType>|**VT_ERROR**(**E_PARAMNOTFOUND** 포함)|
|<xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=nameWithType>|**VT_DISPATCH**|
|<xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=nameWithType>|**VT_UNKNOWN**|
|<xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=nameWithType>|**VT_CY**|
|<xref:System.Boolean?displayProperty=nameWithType>|**VT_BOOL**|
|<xref:System.SByte?displayProperty=nameWithType>|**VT_I1**|
|<xref:System.Byte?displayProperty=nameWithType>|**VT_UI1**|
|<xref:System.Int16?displayProperty=nameWithType>|**VT_I2**|
|<xref:System.UInt16?displayProperty=nameWithType>|**VT_UI2**|
|<xref:System.Int32?displayProperty=nameWithType>|**VT_I4**|
|<xref:System.UInt32?displayProperty=nameWithType>|**VT_UI4**|
|<xref:System.Int64?displayProperty=nameWithType>|**VT_I8**|
|<xref:System.UInt64?displayProperty=nameWithType>|**VT_UI8**|
|<xref:System.Single?displayProperty=nameWithType>|**VT_R4**|
|<xref:System.Double?displayProperty=nameWithType>|**VT_R8**|
|<xref:System.Decimal?displayProperty=nameWithType>|**VT_DECIMAL**|
|<xref:System.DateTime?displayProperty=nameWithType>|**VT_DATE**|
|<xref:System.String?displayProperty=nameWithType>|**VT_BSTR**|
|<xref:System.IntPtr?displayProperty=nameWithType>|**VT_INT**|
|<xref:System.UIntPtr?displayProperty=nameWithType>|**VT_UINT**|
|<xref:System.Array?displayProperty=nameWithType>|**VT_ARRAY**|

다음 코드 예제에서는 이전 예제에서 정의된 `MarshalObject` 인터페이스를 사용하여 다양한 변형 형식을 COM 서버에 전달하는 방법을 보여 줍니다.

```vb
Dim mo As New MarshalObject()
mo.SetVariant(Nothing)         ' Marshal as variant of type VT_EMPTY.
mo.SetVariant(System.DBNull.Value) ' Marshal as variant of type VT_NULL.
mo.SetVariant(CInt(27))        ' Marshal as variant of type VT_I2.
mo.SetVariant(CLng(27))        ' Marshal as variant of type VT_I4.
mo.SetVariant(CSng(27.0))      ' Marshal as variant of type VT_R4.
mo.SetVariant(CDbl(27.0))      ' Marshal as variant of type VT_R8.
```

```csharp
MarshalObject mo = new MarshalObject();
mo.SetVariant(null);            // Marshal as variant of type VT_EMPTY.
mo.SetVariant(System.DBNull.Value); // Marshal as variant of type VT_NULL.
mo.SetVariant((int)27);          // Marshal as variant of type VT_I2.
mo.SetVariant((long)27);          // Marshal as variant of type VT_I4.
mo.SetVariant((single)27.0);   // Marshal as variant of type VT_R4.
mo.SetVariant((double)27.0);   // Marshal as variant of type VT_R8.
```

일치하는 관리되는 형식이 없는 COM 형식은 <xref:System.Runtime.InteropServices.ErrorWrapper>, <xref:System.Runtime.InteropServices.DispatchWrapper>, <xref:System.Runtime.InteropServices.UnknownWrapper>, <xref:System.Runtime.InteropServices.CurrencyWrapper> 등의 래퍼 클래스를 사용하여 마샬링할 수 있습니다. 다음 코드 예제에서는 이러한 래퍼를 사용하여 다양한 변형 형식을 COM 서버에 전달하는 방법을 보여 줍니다.

```vb
Imports System.Runtime.InteropServices
' Pass inew as a variant of type VT_UNKNOWN interface.
mo.SetVariant(New UnknownWrapper(inew))
' Pass inew as a variant of type VT_DISPATCH interface.
mo.SetVariant(New DispatchWrapper(inew))
' Pass a value as a variant of type VT_ERROR interface.
mo.SetVariant(New ErrorWrapper(&H80054002))
' Pass a value as a variant of type VT_CURRENCY interface.
mo.SetVariant(New CurrencyWrapper(New Decimal(5.25)))
```

```csharp
using System.Runtime.InteropServices;
// Pass inew as a variant of type VT_UNKNOWN interface.
mo.SetVariant(new UnknownWrapper(inew));
// Pass inew as a variant of type VT_DISPATCH interface.
mo.SetVariant(new DispatchWrapper(inew));
// Pass a value as a variant of type VT_ERROR interface.
mo.SetVariant(new ErrorWrapper(0x80054002));
// Pass a value as a variant of type VT_CURRENCY interface.
mo.SetVariant(new CurrencyWrapper(new Decimal(5.25)));
```

래퍼 클래스는 <xref:System.Runtime.InteropServices> 네임스페이스에서 정의됩니다.

### <a name="marshaling-the-iconvertible-interface-to-variant"></a>변형에 IConvertible 인터페이스 마샬링

이전 섹션에 나와 있지 않은 형식의 경우 <xref:System.IConvertible> 인터페이스를 구현하여 형식을 마샬링하는 방법을 제어할 수 있습니다. 개체가 **IConvertible** 인터페이스를 구현할 경우 COM 변형 형식은 런타임에 <xref:System.IConvertible.GetTypeCode%2A?displayProperty=nameWithType> 메서드에서 반환된 <xref:System.TypeCode> 열거형 값에 따라 결정됩니다.

다음 표에서는 **TypeCode** 열거형의 가능한 값과 각 값에 대한 일치하는 COM 변형 형식을 보여 줍니다.

|TypeCode|COM 변형 형식|
|--------------|----------------------|
|**TypeCode.Empty**|**VT_EMPTY**|
|**TypeCode.Object**|**VT_UNKNOWN**|
|**TypeCode.DBNull**|**VT_NULL**|
|**TypeCode.Boolean**|**VT_BOOL**|
|**TypeCode.Char**|**VT_UI2**|
|**TypeCode.Sbyte**|**VT_I1**|
|**TypeCode.Byte**|**VT_UI1**|
|**TypeCode.Int16**|**VT_I2**|
|**TypeCode.UInt16**|**VT_UI2**|
|**TypeCode.Int32**|**VT_I4**|
|**TypeCode.UInt32**|**VT_UI4**|
|**TypeCode.Int64**|**VT_I8**|
|**TypeCode.UInt64**|**VT_UI8**|
|**TypeCode.Single**|**VT_R4**|
|**TypeCode.Double**|**VT_R8**|
|**TypeCode.Decimal**|**VT_DECIMAL**|
|**TypeCode.DateTime**|**VT_DATE**|
|**TypeCode.String**|**VT_BSTR**|
|지원되지 않습니다.|**VT_INT**|
|지원되지 않습니다.|**VT_UINT**|
|지원되지 않습니다.|**VT_ARRAY**|
|지원되지 않습니다.|**VT_RECORD**|
|지원되지 않습니다.|**VT_CY**|
|지원되지 않습니다.|**VT_VARIANT**|

COM 변형 값은 **IConvertible.To** *Type* 인터페이스를 호출하여 결정됩니다. 여기서 **To** *Type*은 **IConvertible.GetTypeCode**에서 반환된 형식에 해당하는 변환 루틴입니다. 예를 들어 **IConvertible.GetTypeCode**에서 **TypeCode.Double**을 반환하는 개체는 **VT_R8** 형식의 COM 변형으로 마샬링됩니다. **IConvertible** 인터페이스를 캐스팅하고 <xref:System.IConvertible.ToDouble%2A> 메서드를 호출하여 COM 변형의 **dblVal** 필드에 저장된 변형 값을 가져올 수 있습니다.

## <a name="marshaling-variant-to-object"></a>개체에 변형 마샬링

변형을 개체에 마샬링하면 마샬링된 변형의 형식 및 때때로 값에 따라 생성된 개체 형식이 결정됩니다. 다음 표에서는 각 변형 형식 및 변형이 COM에서 .NET Framework로 전달될 때 마샬러가 만드는 일치하는 개체 형식을 나타냅니다.

|COM 변형 형식|개체 유형|
|----------------------|-----------------|
|**VT_EMPTY**|Null 개체 참조(Visual Basic의 경우 **Nothing**).|
|**VT_NULL**|<xref:System.DBNull?displayProperty=nameWithType>|
|**VT_DISPATCH**|**System.__ComObject** 또는 null((pdispVal == null)인 경우)|
|**VT_UNKNOWN**|**System.__ComObject** 또는 null((punkVal == null)인 경우)|
|**VT_ERROR**|<xref:System.UInt32?displayProperty=nameWithType>|
|**VT_BOOL**|<xref:System.Boolean?displayProperty=nameWithType>|
|**VT_I1**|<xref:System.SByte?displayProperty=nameWithType>|
|**VT_UI1**|<xref:System.Byte?displayProperty=nameWithType>|
|**VT_I2**|<xref:System.Int16?displayProperty=nameWithType>|
|**VT_UI2**|<xref:System.UInt16?displayProperty=nameWithType>|
|**VT_I4**|<xref:System.Int32?displayProperty=nameWithType>|
|**VT_UI4**|<xref:System.UInt32?displayProperty=nameWithType>|
|**VT_I8**|<xref:System.Int64?displayProperty=nameWithType>|
|**VT_UI8**|<xref:System.UInt64?displayProperty=nameWithType>|
|**VT_R4**|<xref:System.Single?displayProperty=nameWithType>|
|**VT_R8**|<xref:System.Double?displayProperty=nameWithType>|
|**VT_DECIMAL**|<xref:System.Decimal?displayProperty=nameWithType>|
|**VT_DATE**|<xref:System.DateTime?displayProperty=nameWithType>|
|**VT_BSTR**|<xref:System.String?displayProperty=nameWithType>|
|**VT_INT**|<xref:System.Int32?displayProperty=nameWithType>|
|**VT_UINT**|<xref:System.UInt32?displayProperty=nameWithType>|
|**VT_ARRAY** &#124; **VT_** \*|<xref:System.Array?displayProperty=nameWithType>|
|**VT_CY**|<xref:System.Decimal?displayProperty=nameWithType>|
|**VT_RECORD**|일치하는 boxed 값 형식.|
|**VT_VARIANT**|지원되지 않습니다.|

COM에서 관리 코드에 전달된 다음 다시 COM에 전달되는 변형 형식은 호출하는 동안 동일한 변형 형식을 유지할 수 없습니다. **VT_DISPATCH** 형식 변형이 COM에서 .NET Framework에 전달될 경우 어떤 일이 나타나는지 살펴봅니다. 마샬링하는 동안 변형은 <xref:System.Object?displayProperty=nameWithType>로 변환됩니다. **Object**가 다시 COM에 전달되면 다시 **VT_UNKNOWN** 형식 변형에 마샬링됩니다. 개체가 관리 코드에서 COM에 마샬링될 때 생성된 변형이 처음에 개체를 생성하는 데 사용되는 변형과 같은 형식이라는 보장은 없습니다.

## <a name="marshaling-byref-variants"></a>ByRef 변형 마샬링

변형 자체는 값 또는 참조로 전달될 수 있지만 **VT_BYREF** 플래그를 변형 형식과 함께 사용하여 변형의 콘텐츠가 값 대신 참조로 전달되고 있음을 나타낼 수도 있습니다. 참조를 통한 변형 마샬링과 **VT_BYREF** 플래그를 통한 변형 마샬링의 차이점은 혼동될 수 있습니다. 다음 그림에서는 차이점을 분명히 설명합니다.

![스택에 전달된 변형을 보여 주는 다이어그램](./media/default-marshaling-for-objects/interop-variant-passed-value-reference.gif)
값 및 참조로 전달되는 변형

**값을 통한 개체 및 변형 마샬링의 기본 동작**

- 관리 코드에서 COM에 개체를 전달할 경우 [변형에 개체 마샬링](#marshaling-object-to-variant)에 정의된 규칙에 따라 개체의 콘텐츠가 마샬러에서 생성된 새 변형에 복사됩니다. 비관리 쪽에서 변형에 적용된 변경 내용은 호출에서 반환 시 다시 원래 개체에 전파되지 않습니다.

- COM에서 관리 코드에 변형을 전달할 경우 [개체에 변형 마샬링](#marshaling-variant-to-object)에 정의된 규칙에 따라 변형의 콘텐츠가 새로 생성된 개체에 복사됩니다. 관리 쪽에서 개체에 적용된 변경 내용은 호출에서 반환 시 다시 원래 변형에 전파되지 않습니다.

**참조를 통한 개체 및 변형 마샬링의 기본 동작**

변경 내용을 다시 호출자에게 전파하려면 매개 변수를 참조로 전달해야 합니다. 예를 들어 C#에서 **ref**키워드(또는 Visual Basic 관리 코드의 경우 **ByRef**)를 사용하여 매개 변수를 참조로 전달합니다. COM에서 참조 매개 변수는 **변형\*** 같은 포인터를 통해 전달됩니다.

- 개체를 COM에 참조로 전달하면 마샬러는 새 변형을 만들고 호출이 수행되기 전에 개체 참조의 콘텐츠를 변형에 복사합니다. 사용자가 변형 콘텐츠를 자유롭게 변경할 수 있는 관리되지 않는 함수에 변형이 전달됩니다. 호출에서 반환 시 비관리 쪽에서 변형에 적용된 변경 내용이 다시 원래 개체에 전파됩니다. 변형 형식이 호출에 전달된 변형 형식과 다를 경우 변경 내용이 다른 형식의 개체에 다시 전파됩니다. 즉, 호출에 전달된 개체 형식이 호출에서 반환된 개체 형식과 다를 수 있습니다.

- 변형을 관리 코드에 참조로 전달하면 마샬러가 새 개체를 만들고 호출을 수행하기 전에 변형 콘텐츠를 개체에 복사합니다. 사용자가 개체를 자유롭게 변경할 수 있는 관리되는 함수에 개체 참조가 전달됩니다. 호출에서 반환 시 참조된 개체의 변경 내용이 다시 원래 변형에 전파됩니다. 개체 형식이 호출에 전달된 개체 형식과 다를 경우 원래 변형의 형식이 변경되고 값이 다시 변형에 전파됩니다. 즉, 호출에 전달된 변형 형식이 호출에서 반환된 변형 형식과 다를 수 있습니다.

 **VT_BYREF 플래그가 설정된 변형 마샬링의 기본 동작**

- 값으로 관리 코드에 전달되는 변형에는 변형에 값 대신 참조가 포함됨을 나타내도록 **VT_BYREF** 플래그가 설정되어 있을 수 있습니다. 이 경우 변형은 값으로 전달되므로 개체에 계속 마샬링됩니다. 마샬러는 변형 콘텐츠를 자동으로 역참조하고 호출을 수행하기 전에 변형을 새로 생성된 개체에 복사합니다. 그런 다음 개체가 관리되는 함수에 전달되지만 호출에서 반환 시 개체는 다시 원래 변형으로 전파되지 않습니다. 관리 개체의 변경 내용이 손실됩니다.

  > [!CAUTION]
  > 변형에 **VT_BYREF** 플래그가 설정된 경우에도 값으로 전달된 변형 값을 변경할 수 없습니다.

- 참조로 관리 코드에 전달되는 변형에는 변형에 또 다른 참조가 포함됨을 나타내도록 **VT_BYREF** 플래그가 설정되어 있을 수도 있습니다. 이 경우 변형은 참조로 전달되므로 **ref** 개체에 마샬링됩니다. 마샬러는 변형 콘텐츠를 자동으로 역참조하고 호출을 수행하기 전에 변형을 새로 생성된 개체에 복사합니다. 호출에서 반환 시 개체의 형식이 전달된 개체와 동일한 경우에만 개체 값이 다시 원래 변형 내의 참조에 전파됩니다. 즉, 전파를 통해 **VT_BYREF** 플래그가 설정된 변형의 형식이 변경되지 않습니다. 호출하는 동안 개체 형식이 변경되면 호출에서 반환 시 <xref:System.InvalidCastException>이 발생합니다.

다음 표에서는 변형 및 개체에 대한 전파 규칙을 간략하게 설명합니다.

|시작|대상|변경 내용이 다시 전파됨|
|----------|--------|-----------------------------|
|**변형**  *v*|**개체**  *o*|Never|
|**개체**  *o*|**변형**  *v*|Never|
|**변형**   ***\****  *pv*|**Ref 개체**  *o*|항상|
|**Ref 개체**  *o*|**변형**   ***\****  *pv*|항상|
|**변형**  *v* **(VT_BYREF** *&#124;* **VT_\*)**|**개체**  *o*|Never|
|**변형**  *v* **(VT_BYREF** *&#124;* **VT_)**|**Ref 개체**  *o*|형식이 변경되지 않은 경우에만.|

## <a name="see-also"></a>참고 항목

- [기본 마샬링 동작](default-marshaling-behavior.md)
- [Blittable 형식 및 비 Blittable 형식](blittable-and-non-blittable-types.md)
- [방향 특성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100))
- [복사 및 고정](copying-and-pinning.md)
