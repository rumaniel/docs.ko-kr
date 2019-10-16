---
title: 기본 마샬링 동작
ms.date: 06/26/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interop marshaling, default
- interoperation with unmanaged code, marshaling
- marshaling behavior
ms.assetid: c0a9bcdf-3df8-4db3-b1b6-abbdb2af809a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c6de6091b8970fde4a958148acf32dcefe1a6726
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946552"
---
# <a name="default-marshaling-behavior"></a>기본 마샬링 동작
Interop 마샬링은 메서드 매개 변수와 연결된 데이터가 관리되는 메모리와 관리되지 않는 메모리 간에 전달될 때 동작하는 방식을 제어하는 규칙에 따라 작동합니다. 이러한 기본 제공 규칙은 데이터 형식 변형, 호출 수신자가 전달된 데이터를 변경하고 해당 변경 내용을 호출자에게 반환할 수 있는지 여부 및 마샬러가 성능 최적화를 제공하는 상황과 같은 마샬링 작업을 제어합니다.  
  
 이 섹션에서는 interop 마샬링 서비스의 기본 동작 특성을 식별합니다. 배열, 부울 형식, char 형식, 대리자, 클래스, 개체, 문자열 및 구조체 마샬링에 대한 자세한 정보를 표시됩니다.  
  
> [!NOTE]
> 제네릭 형식의 마샬링은 지원되지 않습니다. 자세한 내용은 [제네릭 형식을 통한 상호 운용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229590(v=vs.100))을 참조하세요.  
  
## <a name="memory-management-with-the-interop-marshaler"></a>Interop 마샬러를 사용한 메모리 관리  
 Interop 마샬러는 항상 비관리 코드에 의해 할당된 메모리를 해제하려고 합니다. 이 동작은 COM 메모리 관리 규칙을 준수하지만 네이티브 C++를 제어하는 규칙과는 다릅니다.  
  
 포인터에 대한 메모리를 자동으로 해제하는 플랫폼 호출을 사용하는 경우 네이티브 C++ 동작(메모리 해제 안 함)을 예상하면 혼란이 발생할 수 있습니다. 예를 들어 C++ DLL에서 다음 관리되지 않는 메서드를 호출하는 경우 메모리가 자동으로 해제되지 않습니다.  
  
### <a name="unmanaged-signature"></a>관리되지 않는 서명  
  
```cpp  
BSTR MethodOne (BSTR b) {  
     return b;  
}  
```  
  
 그러나 메서드를 플랫폼 호출 프로토타입으로 정의하고, 각 **BSTR** 형식을 <xref:System.String> 형식으로 바꾼 다음 `MethodOne`을 호출하는 경우 공용 언어 런타임에서 `b`를 해제하려고 두 번 시도합니다. **String** 형식보다 <xref:System.IntPtr> 형식을 사용하여 마샬링 동작을 변경할 수 있습니다.  
  
 런타임은 항상 **CoTaskMemFree** 메서드를 사용하여 메모리를 해제합니다. 사용하는 메모리가 **CoTaskMemAlloc** 메서드를 통해 할당되지 않은 경우 **IntPtr**을 사용하고 적절한 메서드를 통해 수동으로 메모리를 해제해야 합니다. 마찬가지로, 커널 메모리에 대한 포인터를 반환하는 Kernel32.dll의 **GetCommandLine** 함수를 사용하는 경우와 같이 메모리가 해제되지 않아야 하는 상황에서는 자동 메모리 해제를 방지할 수 있습니다. 수동으로 메모리를 해제하는 방법에 대한 자세한 내용은 [Buffers 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/x3txb6xc(v=vs.100))을 참조하세요.  
  
## <a name="default-marshaling-for-classes"></a>클래스에 대한 기본 마샬링  
 클래스는 COM interop에 의해서만 마샬링될 수 있으며 항상 인터페이스로 마샬링됩니다. 클래스를 마샬링하는 데 사용되는 인터페이스를 클래스 인터페이스라고 하는 경우도 있습니다. 선택한 인터페이스로 클래스 인터페이스를 재정의하는 방법에 대한 자세한 내용은 [클래스 인터페이스 소개](../../standard/native-interop/com-callable-wrapper.md#introducing-the-class-interface)를 참조하세요.  
  
### <a name="passing-classes-to-com"></a>COM에 클래스 전달  
 관리되는 클래스를 COM에 전달하면 interop 마샬러가 자동으로 클래스를 COM 프록시로 래핑하고 프록시에 의해 생성된 클래스 인터페이스를 COM 메서드 호출에 전달합니다. 그런 다음 프록시는 클래스 인터페이스에 대한 모든 호출을 관리되는 개체에 다시 위임합니다. 또한 프록시는 클래스에 의해 명시적으로 구현되지 않은 다른 인터페이스를 노출합니다. 프록시는 클래스를 대신하여 **IUnknown** 및 **IDispatch**와 같은 인터페이스를 자동으로 구현합니다.  
  
### <a name="passing-classes-to-net-code"></a>.NET 코드에 클래스 전달  
 Coclass는 대개 COM에서 메서드 인수로 사용되지 않습니다. 대신, 일반적으로 기본 인터페이스가 coclass 대신 전달됩니다.  
  
 인터페이스가 관리 코드에 전달되는 경우 interop 마샬러가 인터페이스를 적절한 래퍼로 래핑하고 관리되는 메서드에 래퍼를 전달해야 합니다. 사용할 래퍼를 결정하기 어려울 수 있습니다. COM 개체의 모든 인스턴스에는 개체가 구현하는 인터페이스 수에 관계없이 하나의 고유한 래퍼가 있습니다. 예를 들어 서로 다른 인터페이스 5개를 구현하는 단일 COM 개체에는 하나의 래퍼만 있습니다. 동일한 래퍼가 5개 인터페이스를 모두 노출합니다. COM 개체 인스턴스를 2개 만들면 래퍼 인스턴스도 2개 만들어집니다.  
  
 래퍼가 전체 수명 동안 동일한 형식을 유지하려면 개체에 의해 노출된 인터페이스가 마샬러를 통해 처음 전달될 때 interop 마샬러가 올바른 래퍼를 식별해야 합니다. 마샬러는 개체가 구현하는 인터페이스 중 하나를 확인하여 개체를 식별합니다.  
  
 예를 들어 마샬러는 클래스 래퍼를 사용하여 관리 코드에 전달된 인터페이스를 래핑해야 한다고 결정합니다. 인터페이스는 마샬러를 통해 처음 전달될 때 마샬러는 인터페이스가 알려진 개체에서 제공되는지 여부를 확인합니다. 이 검사는 다음 두 가지 상황에서 발생합니다.  
  
- 다른 곳에서 COM에 전달된 다른 관리되는 개체에 의해 인터페이스가 구현되는 경우. 마샬러는 관리되는 개체에 의해 노출된 인터페이스를 쉽게 식별할 수 있으며, 구현을 제공하는 관리되는 개체와 인터페이스를 일치시킬 수 있습니다. 그런 다음 관리되는 개체가 메서드에 전달되며 래퍼는 필요하지 않습니다.  
  
- 이미 래핑된 개체가 인터페이스를 구현하는 경우. 이러한 경우인지 확인하기 위해 마샬러는 해당 **IUnknown** 인터페이스에 대해 개체를 쿼리하고 반환된 인터페이스를 이미 래핑된 다른 개체의 인터페이스와 비교합니다. 인터페이스가 다른 래퍼의 인터페이스와 같으면 개체 ID가 동일하고 기존 래퍼가 메서드에 전달됩니다.  
  
 알려진 개체의 인터페이스가 아닌 경우 마샬러는 다음을 수행합니다.  
  
1. 마샬러가 **IProvideClassInfo2** 인터페이스에 대해 개체를 쿼리합니다. 제공되면 마샬러가 **IProvideClassInfo2.GetGUID**에서 반환된 CLSID를 사용하여 인터페이스를 제공하는 coclass를 식별합니다. CLSID를 통해 마샬러는 어셈블리가 이전에 등록된 경우 레지스트리에서 래퍼를 찾을 수 있습니다.  
  
2. 마샬러가 **IProvideClassInfo** 인터페이스에 대해 인터페이스를 쿼리합니다. 제공되면 마샬러가 **IProvideClassInfo.GetClassinfo**에서 반환된 **ITypeInfo**를 사용하여 인터페이스를 노출하는 클래스의 CLSID를 확인합니다. 마샬러는 CLSID를 사용하여 래퍼에 대한 메타데이터를 찾을 수 있습니다.  
  
3. 마샬러가 여전히 클래스를 식별할 수 없는 경우 **System.__ComObject**라는 제네릭 래퍼 클래스로 인터페이스를 래핑합니다.  
  
## <a name="default-marshaling-for-delegates"></a>대리자에 대한 기본 마샬링  
 관리되는 대리자는 호출 메커니즘에 따라 COM 인터페이스 또는 함수 포인터로 마샬링됩니다.  
  
- 플랫폼 호출의 경우 대리자는 기본적으로 관리되지 않는 함수 포인터로 마샬링됩니다.  
  
- COM interop의 경우 대리자는 기본적으로 **_Delegate** 형식의 COM 인터페이스로 마샬링됩니다. **_Delegate** 인터페이스는 Mscorlib.tlb 형식 라이브러리에서 정의되며 대리자가 참조하는 메서드를 호출할 수 있게 해주는 <xref:System.Delegate.DynamicInvoke%2A?displayProperty=nameWithType> 메서드를 포함합니다.  
  
 다음 표에서는 관리되는 대리자 데이터 형식에 대한 마샬링 옵션을 보여 줍니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성은 대리자를 마샬링하기 위한 여러 <xref:System.Runtime.InteropServices.UnmanagedType> 열거형 값을 제공합니다.  
  
|열거형 형식|관리되지 않는 형식에 대한 설명|  
|----------------------|-------------------------------------|  
|**UnmanagedType.FunctionPtr**|관리되지 않는 함수 포인터입니다.|  
|**UnmanagedType.Interface**|Mscorlib.tlb에서 정의된 **_Delegate** 형식의 인터페이스입니다.|  
  
 `DelegateTestInterface`의 메서드를 COM 형식 라이브러리로 내보내는 다음 예제 코드를 살펴보세요. **ref**(또는 **ByRef**) 키워드로 표시된 대리자만 In/Out 매개 변수로 전달됩니다.  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
public interface DelegateTest {  
void m1(Delegate d);  
void m2([MarshalAs(UnmanagedType.Interface)] Delegate d);     
void m3([MarshalAs(UnmanagedType.Interface)] ref Delegate d);    
void m4([MarshalAs(UnmanagedType.FunctionPtr)] Delegate d);   
void m5([MarshalAs(UnmanagedType.FunctionPtr)] ref Delegate d);     
}  
```  
  
### <a name="type-library-representation"></a>형식 라이브러리 표현  
  
```cpp  
importlib("mscorlib.tlb");  
interface DelegateTest : IDispatch {  
[id(…)] HRESULT m1([in] _Delegate* d);  
[id(…)] HRESULT m2([in] _Delegate* d);  
[id(…)] HRESULT m3([in, out] _Delegate** d);  
[id()] HRESULT m4([in] int d);  
[id()] HRESULT m5([in, out] int *d);  
   };  
```  
  
 다른 모든 관리되지 않는 함수 포인터를 역참조할 수 있는 것과 마찬가지로 함수 포인터도 역참조할 수 있습니다.  

이 예제에서 두 개의 대리자가 <xref:System.Runtime.InteropServices.UnmanagedType.FunctionPtr?displayProperty=nameWithType>으로 마샬링되면 결과는 `int` 및 `int`에 대한 포인터입니다. 대리자 형식이 마샬링되기 때문에 여기에서 `int`는 void(`void*`)에 대한 포인터를 나타냅니다. 이 항목은 메모리에서 대리자의 주소입니다. 즉, 여기서 `int`가 함수 포인터의 크기를 나타내므로 이 결과는 32비트 Windows 시스템에 해당됩니다.

> [!NOTE]
> 비관리 코드에서 보유한 관리되는 대리자에 대한 함수 포인터 참조는 공용 언어 런타임이 관리되는 개체에서 가비지 컬렉션을 수행할 수 없도록 차단하지 않습니다.  
  
 예를 들어 다음 코드는 `SetChangeHandler` 메서드에 전달된 `cb` 개체 참조가 `Test` 메서드의 수명을 초과하여 `cb` 연결을 유지하지 않으므로 잘못된 것입니다. `cb` 개체가 가비지 수집되고 나면 `SetChangeHandler`에 전달된 함수 포인터가 더이상 유효하지 않습니다.  
  
```csharp  
public class ExternalAPI {  
   [DllImport("External.dll")]  
   public static extern void SetChangeHandler(  
      [MarshalAs(UnmanagedType.FunctionPtr)]ChangeDelegate d);  
}  
public delegate bool ChangeDelegate([MarshalAs(UnmanagedType.LPWStr) string S);  
public class CallBackClass {  
   public bool OnChange(string S){ return true;}  
}  
internal class DelegateTest {  
   public static void Test() {  
      CallBackClass cb = new CallBackClass();  
      // Caution: The following reference on the cb object does not keep the   
      // object from being garbage collected after the Main method   
      // executes.  
      ExternalAPI.SetChangeHandler(new ChangeDelegate(cb.OnChange));     
   }  
}  
```  
  
 예기치 않은 가비지 수집을 보완하기 위해 호출자는 관리되지 않는 함수 포인터가 사용되는 한 `cb` 개체 연결이 유지되도록 해야 합니다. 필요에 따라 다음 예제와 같이 함수 포인터가 더 이상 필요하지 않을 때 비관리 코드에서 관리 코드에 알리도록 할 수 있습니다.  
  
```csharp  
internal class DelegateTest {  
   CallBackClass cb;  
   // Called before ever using the callback function.  
   public static void SetChangeHandler() {  
      cb = new CallBackClass();  
      ExternalAPI.SetChangeHandler(new ChangeDelegate(cb.OnChange));  
   }  
   // Called after using the callback function for the last time.  
   public static void RemoveChangeHandler() {  
      // The cb object can be collected now. The unmanaged code is   
      // finished with the callback function.  
      cb = null;  
   }  
}  
```  
  
## <a name="default-marshaling-for-value-types"></a>값 형식에 대한 기본 마샬링  
 정수 및 부동 소수점 숫자와 같은 대부분의 값 형식은 [blittable](blittable-and-non-blittable-types.md)이며 마샬링할 필요가 없습니다. 다른 [비 blittable](blittable-and-non-blittable-types.md) 형식은 관리되는 메모리와 관리되지 않는 메모리에서 서로 다르게 표현되므로 마샬링해야 합니다. 다른 형식은 상호 운용 경계 간에 명시적 형식 지정도 필요합니다.  
  
 이 섹션에서는 다음과 같은 서식이 지정된 값 형식에 대한 정보를 제공합니다.  
  
- [플랫폼 호출에서 사용되는 값 형식](#value-types-used-in-platform-invoke)  
  
- [COM Interop에서 사용되는 값 형식](#value-types-used-in-com-interop)  
  
 이 항목에서는 형식이 지정된 형식을 설명할 뿐 아니라 특별한 마샬링 동작이 있는 [시스템 값 형식](#system-value-types)을 식별합니다.  
  
 형식이 지정된 형식은 메모리에서 해당 멤버의 레이아웃을 명시적으로 제어하는 정보가 포함된 복합 형식입니다. 멤버 레이아웃 정보는 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성을 사용하여 제공됩니다. 레이아웃은 다음 <xref:System.Runtime.InteropServices.LayoutKind> 열거형 값 중 하나일 수 있습니다.  
  
- **LayoutKind.Automatic**  
  
     공용 언어 런타임이 효율성을 위해 형식의 멤버 순서를 자유롭게 조정할 수 있음을 나타냅니다. 그러나 값 형식이 비관리 코드에 전달될 때는 멤버의 레이아웃을 예측할 수 있습니다. 이러한 구조체를 자동으로 마샬링하려고 하면 예외가 발생합니다.  
  
- **LayoutKind.Sequential**  
  
     형식의 멤버가 관리되는 형식 정의에 나타나는 순서대로 관리되지 않는 메모리에 배치됨을 나타냅니다.  
  
- **LayoutKind.Explicit**  
  
     각 필드에 제공된 <xref:System.Runtime.InteropServices.FieldOffsetAttribute>에 따라 멤버가 배치됨을 나타냅니다.  
  
### <a name="value-types-used-in-platform-invoke"></a>플랫폼 호출에서 사용되는 값 형식  
 다음 예제에서 `Point` 및 `Rect` 형식은 **StructLayoutAttribute**를 사용하여 멤버 레이아웃 정보를 제공합니다.  
  
```vb  
Imports System.Runtime.InteropServices  
<StructLayout(LayoutKind.Sequential)> Public Structure Point  
   Public x As Integer  
   Public y As Integer  
End Structure  
<StructLayout(LayoutKind.Explicit)> Public Structure Rect  
   <FieldOffset(0)> Public left As Integer  
   <FieldOffset(4)> Public top As Integer  
   <FieldOffset(8)> Public right As Integer  
   <FieldOffset(12)> Public bottom As Integer  
End Structure  
```  
  
```csharp  
using System.Runtime.InteropServices;  
[StructLayout(LayoutKind.Sequential)]  
public struct Point {  
   public int x;  
   public int y;  
}     
  
[StructLayout(LayoutKind.Explicit)]  
public struct Rect {  
   [FieldOffset(0)] public int left;  
   [FieldOffset(4)] public int top;  
   [FieldOffset(8)] public int right;  
   [FieldOffset(12)] public int bottom;  
}  
```  
  
 비관리 코드로 마샬링된 경우 이러한 형식이 지정된 형식은 C 스타일 구조체로 마샬링됩니다. 이렇게 하면 구조체 인수가 있는 관리되지 않는 API를 쉽게 호출할 수 있습니다. 예를 들어 다음과 같이 Microsoft Windows API **PtInRect** 함수에 `POINT` 및 `RECT` 구조체를 전달할 수 있습니다.  
  
```cpp  
BOOL PtInRect(const RECT *lprc, POINT pt);  
```  
  
 다음과 같은 플랫폼 호출 정의를 사용하여 구조체를 전달할 수 있습니다.  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function PtInRect Lib "User32.dll" (
        ByRef r As Rect, p As Point) As Boolean
End Class
```
  
```csharp
internal static class NativeMethods
{
   [DllImport("User32.dll")]
   internal static extern bool PtInRect(ref Rect r, Point p);
}
```
  
 관리되지 않는 API는 `RECT`에 대한 포인터가 함수에 전달될 것으로 예상하기 때문에 `Rect` 값 형식은 참조로 전달되어야 합니다. 관리되지 않는 API는 `POINT`가 스택에서 전달될 것으로 예상하기 때문에 `Point` 값 형식은 값으로 전달되어야 합니다. 이러한 미묘한 차이가 매우 중요합니다. 참조는 비관리 코드에 포인터로 전달됩니다. 값은 스택에서 비관리 코드에 전달됩니다.  
  
> [!NOTE]
> 형식이 지정된 형식이 구조체로 마샬링된 경우 형식 내의 필드에만 액세스할 수 있습니다. 형식에 메서드, 속성 또는 이벤트가 있는 경우 비관리 코드에서 액세스할 수 없습니다.  
  
 고정된 멤버 레이아웃이 있는 경우 클래스를 비관리 코드에 C 스타일 구조체로 마샬링할 수도 있습니다. 클래스에 대한 멤버 레이아웃 정보도 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성을 통해 제공됩니다. 고정 레이아웃의 값 형식과 고정 레이아웃의 클래스 간에 주요 차이점은 비관리 코드로 마샬링되는 방법입니다. 값 형식은 스택에서 값으로 전달되므로 호출 수신자가 형식의 멤버를 변경해도 변경 내용이 호출자에게 표시되지 않습니다. 참조 형식은 참조로 전달되므로(스택에서 형식에 대한 참조가 전달됨) 호출 수신자가 형식의 blittable 형식 멤버를 변경할 경우 모든 변경 내용이 호출자에게 표시됩니다.  
  
> [!NOTE]
> 참조 형식에 non-blittable 형식 멤버가 있을 경우 변환이 두 번 필요합니다. 첫 번째는 인수가 관리되지 않는 쪽에 전달될 때이고 두 번째는 호출에서 반환될 때입니다. 이러한 추가 오버헤드로 인해 호출자가 호출 수신자에 의한 변경 내용을 보려는 경우 In/Out 매개 변수를 인수에 명시적으로 적용해야 합니다.  
  
 다음 예제에서 `SystemTime` 클래스는 순차적 멤버 레이아웃을 사용하며 Windows API **GetSystemTime** 함수에 전달될 수 있습니다.  
  
```vb  
<StructLayout(LayoutKind.Sequential)> Public Class SystemTime  
   Public wYear As System.UInt16  
   Public wMonth As System.UInt16  
   Public wDayOfWeek As System.UInt16  
   Public wDay As System.UInt16  
   Public wHour As System.UInt16  
   Public wMinute As System.UInt16  
   Public wSecond As System.UInt16  
   Public wMilliseconds As System.UInt16  
End Class  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
   public class SystemTime {  
   public ushort wYear;   
   public ushort wMonth;  
   public ushort wDayOfWeek;   
   public ushort wDay;   
   public ushort wHour;   
   public ushort wMinute;   
   public ushort wSecond;   
   public ushort wMilliseconds;   
}  
```  
  
 **GetSystemTime** 함수는 다음과 같이 정의됩니다.  
  
```cpp  
void GetSystemTime(SYSTEMTIME* SystemTime);  
```  
  
 **GetSystemTime**에 해당하는 플랫폼 호출 정의는 다음과 같습니다.  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Sub GetSystemTime Lib "Kernel32.dll" (
        ByVal sysTime As SystemTime)
End Class
```
  
```csharp
internal static class NativeMethods
{
   [DllImport("Kernel32.dll", CharSet = CharSet.Auto)]
   internal static extern void GetSystemTime(SystemTime st);
}
```
  
 `SystemTime`이 값 형식이 아니라 클래스이기 때문에 `SystemTime` 인수는 참조 인수로 형식화되지 않습니다. 값 형식과 달리 클래스는 항상 참조로 전달됩니다.  
  
 다음 코드 예제에서는 `SetXY`라는 메서드가 있는 다른 `Point` 클래스를 보여 줍니다. 형식이 순차적 레이아웃을 사용하므로 비관리 코드에 전달되고 구조체로 마샬링될 수 있습니다. 그러나 개체가 참조로 전달되는 경우에도 `SetXY` 멤버는 비관리 코드에서 호출할 수 없습니다.  
  
```vb  
<StructLayout(LayoutKind.Sequential)> Public Class Point  
   Private x, y As Integer  
   Public Sub SetXY(x As Integer, y As Integer)  
      Me.x = x  
      Me.y = y  
   End Sub  
End Class  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public class Point {  
   int x, y;  
   public void SetXY(int x, int y){   
      this.x = x;  
      this.y = y;  
   }  
}  
```  
  
### <a name="value-types-used-in-com-interop"></a>COM Interop에서 사용되는 값 형식  
 형식이 지정된 형식을 COM interop 메서드 호출에 전달할 수도 있습니다. 실제로 형식 라이브러리로 내보내는 경우 값 형식이 자동으로 구조체로 변환됩니다. 다음 예제에서 볼 수 있듯이, `Point` 값 형식은 이름이 `Point`인 형식 정의(typedef)가 됩니다. 형식 라이브러리의 다른 위치에 있는 `Point` 값 형식에 대한 모든 참조가 `Point` typedef로 대체됩니다.  
  
 **형식 라이브러리 표현**  
  
```cpp  
typedef struct tagPoint {  
   int x;  
   int y;  
} Point;  
interface _Graphics {  
   …  
   HRESULT SetPoint ([in] Point p)  
   HRESULT SetPointRef ([in,out] Point *p)  
   HRESULT GetPoint ([out,retval] Point *p)  
}  
```  
  
 값과 참조를 플랫폼 호출로 마샬링하는 데 사용되는 것과 동일한 규칙이 COM 인터페이스를 통해 마샬링할 때도 사용됩니다. 예를 들어 `Point` 값 형식의 인스턴스가 .NET Framework에서 COM으로 전달되는 경우 `Point`가 값으로 전달됩니다. `Point` 값 형식이 참조로 전달되는 경우에는 `Point`에 대한 포인터가 스택에서 전달됩니다. interop 마샬러는 두 방향에서 모두 더 높은 수준의 간접 참조(**Point** \*\*)를 지원하지 않습니다.  
  
> [!NOTE]
> 내보낸 형식 라이브러리에서 명시적 레이아웃을 표현할 수 없기 때문에 <xref:System.Runtime.InteropServices.LayoutKind> 열거형 값이 **Explicit**로 설정된 구조체는 COM interop에서 사용할 수 없습니다.  
  
### <a name="system-value-types"></a>시스템 값 형식  
 <xref:System> 네임스페이스에는 런타임 기본 형식의 boxed 형식을 나타내는 여러 개의 값 형식이 있습니다. 예를 들어 값 형식 <xref:System.Int32?displayProperty=nameWithType> 구조체는 **ELEMENT_TYPE_I4**의 boxed 형식을 나타냅니다. 다른 형식이 지정된 형식처럼 이러한 형식을 구조체로 마샬링하는 대신 boxing하는 기본 형식과 동일한 방식으로 마샬링합니다. 따라서 **System.Int32**는 **long** 형식의 단일 멤버를 포함하는 구조체가 아니라 **ELEMENT_TYPE_I4**로 마샬링됩니다. 다음 표에는 기본 형식의 boxed 표현인 **System** 네임스페이스의 값 형식 목록이 포함되어 있습니다.  
  
|시스템 값 형식|요소 형식|  
|-----------------------|------------------|  
|<xref:System.Boolean?displayProperty=nameWithType>|**ELEMENT_TYPE_BOOLEAN**|  
|<xref:System.SByte?displayProperty=nameWithType>|**ELEMENT_TYPE_I1**|  
|<xref:System.Byte?displayProperty=nameWithType>|**ELEMENT_TYPE_UI1**|  
|<xref:System.Char?displayProperty=nameWithType>|**ELEMENT_TYPE_CHAR**|  
|<xref:System.Int16?displayProperty=nameWithType>|**ELEMENT_TYPE_I2**|  
|<xref:System.UInt16?displayProperty=nameWithType>|**ELEMENT_TYPE_U2**|  
|<xref:System.Int32?displayProperty=nameWithType>|**ELEMENT_TYPE_I4**|  
|<xref:System.UInt32?displayProperty=nameWithType>|**ELEMENT_TYPE_U4**|  
|<xref:System.Int64?displayProperty=nameWithType>|**ELEMENT_TYPE_I8**|  
|<xref:System.UInt64?displayProperty=nameWithType>|**ELEMENT_TYPE_U8**|  
|<xref:System.Single?displayProperty=nameWithType>|**ELEMENT_TYPE_R4**|  
|<xref:System.Double?displayProperty=nameWithType>|**ELEMENT_TYPE_R8**|  
|<xref:System.String?displayProperty=nameWithType>|**ELEMENT_TYPE_STRING**|  
|<xref:System.IntPtr?displayProperty=nameWithType>|**ELEMENT_TYPE_I**|  
|<xref:System.UIntPtr?displayProperty=nameWithType>|**ELEMENT_TYPE_U**|  
  
 **System** 네임스페이스의 다른 값 형식은 다르게 처리됩니다. 비관리 코드에는 이러한 형식에 대해 잘 설정된 형식이 이미 있으므로 마샬러에 특수 마샬링 규칙이 있습니다. 다음 표에서는 **System** 네임스페이스의 특수 값 형식과 마샬링되는 관리되지 않는 형식을 보여 줍니다.  
  
|시스템 값 형식|IDL 형식|  
|-----------------------|--------------|  
|<xref:System.DateTime?displayProperty=nameWithType>|**DATE**|  
|<xref:System.Decimal?displayProperty=nameWithType>|**DECIMAL**|  
|<xref:System.Guid?displayProperty=nameWithType>|**GUID**|  
|<xref:System.Drawing.Color?displayProperty=nameWithType>|**OLE_COLOR**|  
  
 다음 코드에서는 Stdole2 형식 라이브러리에 있는 관리되지 않는 형식 **DATE**, **GUID**, **DECIMAL** 및 **OLE_COLOR**의 정의를 보여 줍니다.  
  
#### <a name="type-library-representation"></a>형식 라이브러리 표현  
  
```cpp  
typedef double DATE;  
typedef DWORD OLE_COLOR;  
  
typedef struct tagDEC {  
    USHORT    wReserved;  
    BYTE      scale;  
    BYTE      sign;  
    ULONG     Hi32;  
    ULONGLONG Lo64;  
} DECIMAL;  
  
typedef struct tagGUID {  
    DWORD Data1;  
    WORD  Data2;  
    WORD  Data3;  
    BYTE  Data4[ 8 ];  
} GUID;  
```  
  
 다음 코드에서는 관리되는 `IValueTypes` 인터페이스의 해당 정의를 보여 줍니다.  
  
```vb  
Public Interface IValueTypes  
   Sub M1(d As System.DateTime)  
   Sub M2(d As System.Guid)  
   Sub M3(d As System.Decimal)  
   Sub M4(d As System.Drawing.Color)  
End Interface  
```  
  
```csharp  
public interface IValueTypes {  
   void M1(System.DateTime d);  
   void M2(System.Guid d);  
   void M3(System.Decimal d);  
   void M4(System.Drawing.Color d);  
}  
```  
  
#### <a name="type-library-representation"></a>형식 라이브러리 표현  
  
```cpp  
[…]  
interface IValueTypes : IDispatch {  
   HRESULT M1([in] DATE d);  
   HRESULT M2([in] GUID d);  
   HRESULT M3([in] DECIMAL d);  
   HRESULT M4([in] OLE_COLOR d);  
};  
```  
  
## <a name="see-also"></a>참고 항목

- [Blittable 형식 및 비 Blittable 형식](blittable-and-non-blittable-types.md)
- [복사 및 고정](copying-and-pinning.md)
- [배열에 대한 기본 마샬링](default-marshaling-for-arrays.md)
- [개체에 대한 마샬링](default-marshaling-for-objects.md)
- [문자열에 대한 기본 마샬링](default-marshaling-for-strings.md)
