---
title: '방법: 콜백 함수 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- callback function, implementing
ms.assetid: e55b3712-b9ea-4453-bd9a-ad5cfa2f6bfa
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6eba8202f0284b7b1054585039f12da9364ca1e9
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051761"
---
# <a name="how-to-implement-callback-functions"></a>방법: 콜백 함수 구현
다음 절차 및 예제에서는 관리되는 애플리케이션이 플랫폼 호출을 사용하여 로컬 컴퓨터에서 각 창에 대한 핸들 값을 인쇄하는 방법을 보여 줍니다. 특히 프로시저 및 예제에서는 **EnumWindows** 함수를 사용하여 창 목록을 단계별로 실행하고 관리되는 콜백 함수(CallBack)를 사용하여 창 핸들 값을 인쇄합니다.  
  
### <a name="to-implement-a-callback-function"></a>콜백 함수를 구현하려면  
  
1. 구현을 계속 진행하기 전에 **EnumWindows** 함수에 대한 시그니처를 확인합니다. **EnumWindows**에는 다음 시그니처가 있습니다.  
  
    ```cpp
    BOOL EnumWindows(WNDENUMPROC lpEnumFunc, LPARAM lParam)
    ```
  
     이 함수에 콜백이 필요한 한 가지 단서는 **lpEnumFunc** 인수가 있다는 것입니다. 일반적으로 포인터를 콜백 함수로 이동하는 인수의 이름에서 **Func** 접미사와 결합된 **lp**(long pointer) 접두사를 확인합니다. Win32 함수에 대한 설명서는 Microsoft Platform SDK를 참조하세요.  
  
2. 관리되는 콜백 함수를 만듭니다. 예제에서는 두 인수(**hwnd** 및 **lparam**)를 사용하는 `CallBack`이라는 대리자 형식을 선언합니다. 첫 번째 인수는 창에 대한 핸들이고 두 번째 인수는 애플리케이션에서 정의됩니다. 이 릴리스에서 두 인수는 모두 정수여야 합니다.  
  
     일반적으로 콜백 함수는 성공을 나타내는 0이 아닌 값 및 실패를 나타내는 0을 반환합니다. 이 예제에서는 반환 값을 **true**로 명시적으로 설정하여 열거를 계속합니다.  
  
3. 대리자를 만들고 **EnumWindows** 함수에 인수로 전달합니다. 플랫폼 호출은 대리자를 친숙한 콜백 형식으로 자동으로 변환합니다.  
  
4. 콜백 함수가 작업을 완료하기 전에 가비지 수집기가 대리자를 회수하지 않는지 확인합니다. 대리자를 매개 변수로 전달하거나 구조체에 필드로 포함된 대리자를 전달하면 호출 중에 대리자가 수집되지 않습니다. 따라서 다음 열거 예제처럼 콜백 함수는 호출이 반환되기 전에 작업을 완료하고 관리되는 호출자의 추가적인 작업이 필요하지 않습니다.  
  
     그러나 호출이 반환된 후에 콜백 함수를 호출할 수 있으면 관리되는 호출자는 단계에 따라 콜백 함수가 완료될 때까지 대리자가 수집되지 않는지 확인해야 합니다. 가비지 수집을 방지하는 방법에 대한 자세한 내용은 플랫폼 호출을 사용한 [Interop 마샬링](interop-marshaling.md)을 참조하세요.  
  
## <a name="example"></a>예제  
  
```vb  
Imports System  
Imports System.Runtime.InteropServices  
  
Public Delegate Function CallBack( _  
hwnd As Integer, lParam As Integer) As Boolean  
  
Public Class EnumReportApp  
  
    Declare Function EnumWindows Lib "user32" ( _  
       x As CallBack, y As Integer) As Integer  
  
    Public Shared Sub Main()  
        EnumWindows(AddressOf EnumReportApp.Report, 0)  
    End Sub 'Main  
  
    Public Shared Function Report(hwnd As Integer, lParam As Integer) _  
    As Boolean  
        Console.Write("Window handle is ")  
        Console.WriteLine(hwnd)  
        Return True  
    End Function 'Report  
End Class 'EnumReportApp  
```  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
public delegate bool CallBack(int hwnd, int lParam);  
  
public class EnumReportApp  
{  
    [DllImport("user32")]  
    public static extern int EnumWindows(CallBack x, int y);   
  
    public static void Main()   
    {  
        CallBack myCallBack = new CallBack(EnumReportApp.Report);  
        EnumWindows(myCallBack, 0);  
    }  
  
    public static bool Report(int hwnd, int lParam)  
    {   
        Console.Write("Window handle is ");  
        Console.WriteLine(hwnd);  
        return true;  
    }  
}  
```  
  
```cpp  
using namespace System;  
using namespace System::Runtime::InteropServices;  
  
// A delegate type.  
delegate bool CallBack(int hwnd, int lParam);  
  
// Managed type with the method to call.  
ref class EnumReport  
{  
// Report the window handle.  
public:  
    [DllImport("user32")]  
    static int EnumWindows(CallBack^ x, int y);  
  
    static void Main()  
    {  
        EnumReport^ er = gcnew EnumReport;  
        CallBack^ myCallBack = gcnew CallBack(&EnumReport::Report);  
        EnumWindows(myCallBack, 0);  
    }  
  
    static bool Report(int hwnd, int lParam)  
    {  
       Console::Write(L"Window handle is ");  
       Console::WriteLine(hwnd);  
       return true;  
    }  
};  
  
int main()  
{  
    EnumReport::Main();  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [콜백 함수](callback-functions.md)
- [DLL 함수 호출](calling-a-dll-function.md)
