---
title: 구조체 전달
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- platform invoke, calling unmanaged functions
ms.assetid: 9b92ac73-32b7-4e1b-862e-6d8d950cf169
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eef52827bfe36977c9c4c844f4f431e7404adc97
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051672"
---
# <a name="passing-structures"></a>구조체 전달
관리되지 않는 여러 함수에서는 함수, 구조체 멤버(Visual Basic의 사용자 정의 형식) 또는 관리 코드에 정의된 클래스 멤버에 매개 변수로 전달해야 합니다. 플랫폼 호출을 사용하여 구조체 또는 클래스를 비관리 코드에 전달할 때 원래 레이아웃과 맞춤을 유지하기 위해 추가 정보를 제공해야 합니다. 이 항목에서는 형식이 지정된 유형을 정의하는 데 사용하는 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성을 소개합니다. 관리되는 구조체와 클래스의 경우 **LayoutKind** 열거형에서 제공하는 예측 가능한 여러 레이아웃 동작 중에서 선택할 수 있습니다.  
  
 이 항목에 제시된 개념의 핵심은 구조체와 클래스 형식 사이에 중요한 차이점이 있다는 것입니다. 구조체는 값 형식이고 클래스는 참조 형식입니다. 클래스는 항상 한 수준 이상의 메모리 간접 참조(값에 대한 포인터)를 제공합니다. 다음 표의 첫 번째 열에 있는 시그니처를 통해 표시된 대로 관리되지 않는 함수는 간접 참조를 요구하는 경우가 많으므로 이 차이점은 중요합니다. 나머지 열에 있는 클래스 선언과 관리된 구조체는 선언에서 간접 참조의 수준을 조정할 수 있는 정도를 보여 줍니다. 선언은 Visual Basic과 Visual C# 모두용으로 제공됩니다.  
  
|관리되지 않는 서명|관리되는 선언: <br />간접 참조가 아님<br />`Structure MyType`<br />`struct MyType;`|관리되는 선언: <br />한 수준의 간접 참조<br />`Class MyType`<br />`class MyType;`|  
|-------------------------|---------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|  
|`DoWork(MyType x);`<br /><br /> 0 수준의 간접 참조를 요구합니다.|`DoWork(ByVal x As MyType)` <br /> `DoWork(MyType x)`<br /><br /> 0 수준의 간접 참조를 추가합니다.|이미 한 수준의 간접 참조가 있으므로 가능하지 않습니다.|  
|`DoWork(MyType* x);`<br /><br /> 한 수준의 간접 참조를 요구합니다.|`DoWork(ByRef x As MyType)` <br /> `DoWork(ref MyType x)`<br /><br /> 한 수준의 간접 참조를 추가합니다.|`DoWork(ByVal x As MyType)` <br /> `DoWork(MyType x)`<br /><br /> 0 수준의 간접 참조를 추가합니다.|  
|`DoWork(MyType** x);`<br /><br /> 두 수준의 간접 참조를 요구합니다.|**ByRef** **ByRef** 또는 `ref` `ref`는 사용할 수 없기 때문에 불가능합니다.|`DoWork(ByRef x As MyType)` <br /> `DoWork(ref MyType x)`<br /><br /> 한 수준의 간접 참조를 추가합니다.|  
  
 이 표에서는 플랫폼 호출 선언에 대한 다음과 같은 지침을 설명합니다.  
  
- 관리되지 않는 함수에서 간접 참조를 요구하지 않는 경우 값 형식으로 전달된 구조체를 사용합니다.  
  
- 관리되지 않는 함수에서 한 수준의 간접 참조를 요구하는 경우 참조 형식으로 전달된 구조체 또는 값 형식으로 전달된 클래스를 사용합니다.  
  
- 관리되지 않는 함수에서 두 수준의 간접 참조를 요구하는 경우 참조 형식으로 전달된 클래스를 사용합니다.  
  
## <a name="declaring-and-passing-structures"></a>구조체 선언 및 전달  
 다음 예제에서는 관리 코드에서 `Point` 및 `Rect` 구조체를 정의하고, User32.dll 파일의 **PtInRect** 함수에 매개 변수로 형식을 전달하는 방법을 보여 줍니다. **PtInRect**에는 다음과 같은 관리되지 않은 시그니처가 있습니다.  
  
```cpp
BOOL PtInRect(const RECT *lprc, POINT pt);  
```  
  
 함수에는 RECT 형식에 대한 포인터가 있어야 하므로 참조 형식으로 Rect 구조체를 전달해야 합니다.  
  
```vb  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> Public Structure Point  
    Public x As Integer  
    Public y As Integer  
End Structure  
  
Public Structure <StructLayout(LayoutKind.Explicit)> Rect  
    <FieldOffset(0)> Public left As Integer  
    <FieldOffset(4)> Public top As Integer  
    <FieldOffset(8)> Public right As Integer  
    <FieldOffset(12)> Public bottom As Integer  
End Structure  
  
Friend Class NativeMethods      
    Friend Declare Auto Function PtInRect Lib "user32.dll" (
        ByRef r As Rect, p As Point) As Boolean  
End Class  
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
  
internal static class NativeMethods
{  
    [DllImport("User32.dll")]  
    internal static extern bool PtInRect(ref Rect r, Point p);  
}  
```  
  
## <a name="declaring-and-passing-classes"></a>클래스 선언 및 전달  
 클래스에 고정 멤버 레이아웃이 있는 한 관리되지 않은 DLL 함수에 클래스 멤버를 전달할 수 있습니다. 다음 예제에서는 `MySystemTime` 클래스의 멤버를 전달하는 방법을 설명합니다. 이 멤버는 User32.dll 파일의 **GetSystemTime**에 순차적으로 정의됩니다. **GetSystemTime**에는 관리되지 않는 다음과 같은 시그니처가 있습니다.  
  
```cpp
void GetSystemTime(SYSTEMTIME* SystemTime);  
```  
  
 값 형식과 달리 클래스에는 항상 한 수준의 간접 참조가 하나 이상 있습니다.  
  
```vb  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> Public Class MySystemTime  
    Public wYear As Short  
    Public wMonth As Short  
    Public wDayOfWeek As Short   
    Public wDay As Short  
    Public wHour As Short  
    Public wMinute As Short  
    Public wSecond As Short  
    Public wMiliseconds As Short  
End Class  
  
Friend Class NativeMethods  
    Friend Declare Auto Sub GetSystemTime Lib "Kernel32.dll" (
        sysTime As MySystemTime)  
    Friend Declare Auto Function MessageBox Lib "User32.dll" (
        hWnd As IntPtr, lpText As String, lpCaption As String, uType As UInteger) As Integer  
End Class  
  
Public Class TestPlatformInvoke      
    Public Shared Sub Main()  
        Dim sysTime As New MySystemTime()  
        NativeMethods.GetSystemTime(sysTime)  
  
        Dim dt As String  
        dt = "System time is:" & ControlChars.CrLf & _  
              "Year: " & sysTime.wYear & _  
              ControlChars.CrLf & "Month: " & sysTime.wMonth & _  
              ControlChars.CrLf & "DayOfWeek: " & sysTime.wDayOfWeek & _  
              ControlChars.CrLf & "Day: " & sysTime.wDay  
        NativeMethods.MessageBox(IntPtr.Zero, dt, "Platform Invoke Sample", 0)        
    End Sub  
End Class  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public class MySystemTime {  
    public ushort wYear;   
    public ushort wMonth;  
    public ushort wDayOfWeek;   
    public ushort wDay;   
    public ushort wHour;   
    public ushort wMinute;   
    public ushort wSecond;   
    public ushort wMilliseconds;   
}  
internal static class NativeMethods
{  
    [DllImport("Kernel32.dll")]  
    internal static extern void GetSystemTime(MySystemTime st);  
  
    [DllImport("user32.dll", CharSet = CharSet.Auto)]  
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);  
}  
  
public class TestPlatformInvoke  
{  
    public static void Main()  
    {  
        MySystemTime sysTime = new MySystemTime();  
        NativeMethods.GetSystemTime(sysTime);  
  
        string dt;  
        dt = "System time is: \n" +  
              "Year: " + sysTime.wYear + "\n" +  
              "Month: " + sysTime.wMonth + "\n" +  
              "DayOfWeek: " + sysTime.wDayOfWeek + "\n" +  
              "Day: " + sysTime.wDay;  
        NativeMethods.MessageBox(IntPtr.Zero, dt, "Platform Invoke Sample", 0);  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [DLL 함수 호출](calling-a-dll-function.md)
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- <xref:System.Runtime.InteropServices.FieldOffsetAttribute>
