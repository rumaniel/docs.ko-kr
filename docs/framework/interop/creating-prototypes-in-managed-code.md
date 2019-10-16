---
title: 관리 코드에서 프로토타입 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- prototypes in managed code
- COM interop, DLL functions
- unmanaged functions
- platform invoke, creating prototypes
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, object fields
- DLL functions
- object fields in platform invoke
ms.assetid: ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f32924c8c104f37fdb98a2a9ff104b6f6c19e478
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70853840"
---
# <a name="creating-prototypes-in-managed-code"></a>관리 코드에서 프로토타입 만들기
이 항목에서는 관리되지 않는 함수에 액세스하는 방법을 설명하고 관리 코드에서 메서드 정의에 주석을 다는 여러 특성 필드를 소개합니다. 플랫폼 호출에서 사용되는 .NET 기반 선언을 생성하는 방법을 보여 주는 예제는 [플랫폼 호출을 사용하여 데이터 마샬링](marshaling-data-with-platform-invoke.md)을 참조하세요.  
  
 관리 코드에서 관리되지 않는 DLL 함수에 액세스하기 전에 함수 이름과 함수를 내보내는 DLL 이름을 알아야 합니다. 이 정보를 사용하여 DLL에서 구현되는 관리되지 않는 함수에 대한 관리되는 정의를 쓰기 시작할 수 있습니다. 또한 플랫폼 호출이 함수를 만들고 데이터를 함수로 또는 반대로 마샬링하는 방법을 조정할 수 있습니다.  
  
> [!NOTE]
> 문자열을 할당하는 Windows API 함수를 통해 `LocalFree`와 같은 메서드를 사용하여 문자열을 해제할 수 있습니다. 플랫폼 호출은 매개 변수를 다르게 처리합니다. 플랫폼 호출의 경우 매개 변수를 `String` 형식 대신 `IntPtr` 형식으로 설정합니다. <xref:System.Runtime.InteropServices.Marshal?displayProperty=nameWithType> 클래스에서 제공된 메서드를 사용하여 형식을 문자열로 수동으로 변환하고 해제합니다.  
  
## <a name="declaration-basics"></a>선언 기본 사항  
 관리되지 않는 함수에 대한 관리되는 정의는 다음 예제와 같이 언어 종속적입니다. 전체 코드 예제를 보려면 [플랫폼 호출 예제](platform-invoke-examples.md)를 참조하세요.  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
 <xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError?displayProperty=nameWithType> 또는 <xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar?displayProperty=nameWithType> 필드를 Visual Basic 선언에 적용하려면 `Declare` 문 대신 <xref:System.Runtime.InteropServices.DllImportAttribute> 특성을 사용해야 합니다.  
  
```vb
Imports System.Runtime.InteropServices

Friend Class NativeMethods
    <DllImport("user32.dll", CharSet:=CharSet.Auto)>
    Friend Shared Function MessageBox(
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
    End Function
End Class
```
  
```csharp
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll")]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```
  
```cpp
using namespace System;
using namespace System::Runtime::InteropServices;

[DllImport("user32.dll")]
extern "C" int MessageBox(
    IntPtr hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="adjusting-the-definition"></a>정의 조정  
 명시적으로 설정하는지와 관계없이 특성 필드는 관리 코드 동작을 정의합니다. 플랫폼 호출은 어셈블리에서 메타데이터로 있는 다양한 필드에 설정된 기본값에 따라 작동합니다. 필드 하나 이상의 값을 조정하여 이 기본 동작을 변경할 수 있습니다. 대부분 <xref:System.Runtime.InteropServices.DllImportAttribute>를 사용하여 값을 설정합니다.  
  
 다음 표에는 플랫폼 호출과 관련된 전체 특성 필드 집합이 나와 있습니다. 표에는 각 필드에 대한 기본값과 이들 필드를 사용하여 관리되지 않는 DLL 함수를 정의하는 방법에 대한 정보 링크가 포함됩니다.  
  
|필드|설명|  
|-----------|-----------------|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>|최적 매핑을 사용하거나 사용하지 않도록 설정합니다.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>|메서드 인수 전달 시 사용할 호출 규칙을 지정합니다. 기본값은 `WinAPI`로, 32비트 Intel 기반 플랫폼의 `__stdcall`에 해당합니다.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet>|이름 손상 및 문자열 인수가 함수로 마샬링되는 방법을 제어합니다. 기본값은 `CharSet.Ansi`입니다.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>|호출할 DLL 진입점을 지정합니다.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>|문자 집합과 일치하도록 진입점을 수정해야 하는지를 제어합니다. 기본값은 프로프래밍 언어에 따라 달라집니다.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>|HRESULT를 반환하고 반환 값에 대한 추가 [out, retval] 인수가 포함된 관리되지 않는 서명으로 관리되는 메서드 서명을 변환할지를 제어합니다.<br /><br /> 기본값은 `true`입니다(서명을 변형하지 않아야 함).|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError>|호출자가 `Marshal.GetLastWin32Error` API 함수를 사용하여 메서드를 실행하는 동안 오류가 발생했는지를 확인할 수 있도록 합니다. Visual Basic에서 기본값은 `true`이고, C# 및 C++에서 기본값은 `false`입니다.|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar>|ANSI "?" 문자로 변환되는 매핑할 수 없는 유니코드 문자에 대한 예외 throw를 제어합니다.|  
  
 자세한 참조 정보는 <xref:System.Runtime.InteropServices.DllImportAttribute>를 참조하세요.  
  
## <a name="platform-invoke-security-considerations"></a>플랫폼 호출 보안 고려 사항  
 <xref:System.Security.Permissions.SecurityAction> 열거형의 `Assert`, `Deny` 및 `PermitOnly` 멤버를 *스택 워크 한정자*라고 합니다. 이들 멤버는 플랫폼 호출 선언 및 COM IDL(Interface Definition Language) 문에서 선언 특성으로 사용될 경우 무시됩니다.  
  
### <a name="platform-invoke-examples"></a>플랫폼 호출 예제  
 이 섹션의 플랫폼 호출 샘플에서는 스택 워크 한정자와 함께 `RegistryPermission` 특성을 사용하는 방법을 보여 줍니다.  
  
 다음 예제에서는 <xref:System.Security.Permissions.SecurityAction>`Assert`, `Deny` 및 `PermitOnly` 한정자가 무시됩니다.  
  
```csharp  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionAssert();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 그러나 다음 예제에서 `Demand` 한정자는 허용됩니다.  
  
```csharp
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 <xref:System.Security.Permissions.SecurityAction> 한정자는 플랫폼 호출을 포함(래핑)하는 클래스에 배치될 경우 제대로 작동합니다.  
  
```cpp  
      [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
public ref class PInvokeWrapper  
{  
public:  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
};  
```  
  
```csharp  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
class PInvokeWrapper  
{  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
}  
```  
  
 <xref:System.Security.Permissions.SecurityAction> 한정자는 플랫폼 호출의 호출자에 배치되는 중첩된 시나리오에서도 제대로 작동합니다.  
  
```cpp  
      {  
public ref class PInvokeWrapper  
public:  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
  
    [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
};  
```  
  
```csharp  
class PInvokeScenario  
{  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionInternal();  
  
    [RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
}  
```  
  
#### <a name="com-interop-examples"></a>COM Interop 예제  
 이 섹션의 COM Interop 샘플에서는 스택 워크 한정자와 함께 `RegistryPermission` 특성을 사용하는 방법을 보여 줍니다.  
  
 이전 섹션의 플랫폼 호출 예제와 비슷하게 다음 COM interop 인터페이스 선언은 `Assert`, `Deny` 및 `PermitOnly` 한정자를 무시합니다.  
  
```csharp
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDenyStubsItf  
{  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
 또한 다음 예제와 같이 `Demand` 한정자는 COM interop 인터페이스 선언 시나리오에서 허용되지 않습니다.  
  
```csharp  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDemandStubsItf  
{  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [관리되지 않는 DLL 함수 사용](consuming-unmanaged-dll-functions.md)
- [진입점 지정](specifying-an-entry-point.md)
- [문자 집합 지정](specifying-a-character-set.md)
- [플랫폼 호출 예제](platform-invoke-examples.md)
- [플랫폼 호출 보안 고려 사항](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb397754(v=vs.100))
- [DLL 함수 식별](identifying-functions-in-dlls.md)
- [DLL 함수가 포함된 클래스 만들기](creating-a-class-to-hold-dll-functions.md)
- [DLL 함수 호출](calling-a-dll-function.md)
