---
title: 진입점 지정
ms.date: 03/30/2017
helpviewer_keywords:
- EntryPoint field
- platform invoke, attribute fields
- attribute fields in platform invoke, EntryPoint
ms.assetid: d1247f08-0965-416a-b978-e0b50652dfe3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2a5449b4fa77ba99a18595077081089e80bd32df
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833612"
---
# <a name="specifying-an-entry-point"></a>진입점 지정

진입점은 DLL에서 함수의 위치를 식별합니다. 관리되는 프로젝트 내에서 대상 함수의 원래 이름이나 서수 진입점은 상호 운용 경계 간에 해당 함수를 식별합니다. 또한 진입점을 다른 이름에 매핑하여 효과적으로 함수 이름을 바꿀 수 있습니다.  
  
 다음은 DLL 함수의 이름을 바꾸는 가능한 원인 목록입니다.  
  
- 대/소문자를 구분하는 API 함수 이름을 사용하지 않도록 하기 위해  
  
- 기존 명명 표준을 준수하기 위해  
  
- 동일한 DLL 함수의 여러 버전을 선언하여 다른 데이터 형식을 사용하는 함수를 수용하기 위해  
  
- ANSI 및 유니코드 버전을 포함하는 API 사용을 간소화하기 위해  
  
 이 항목에는 관리 코드에서 DLL 함수 이름을 바꾸는 방법을 보여 줍니다.  
  
## <a name="renaming-a-function-in-visual-basic"></a>Visual Basic에서 함수 이름 바꾸기  
 
Visual Basic에서는 **Declare** 문에 **Function** 키워드를 사용하여 <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=nameWithType> 필드를 설정합니다. 다음 예제에서는 기본 선언을 보여 줍니다.  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
다음 예제와 같이 정의에 **Alias** 키워드를 포함하여 **MessageBox** 진입점을 **MsgBox**로 바꿀 수 있습니다. 두 예제에서 모두 **Auto** 키워드를 사용하면 진입점의 문자 집합 버전을 지정할 필요가 없습니다. 문자 집합을 선택하는 방법에 대한 자세한 내용은 [문자 집합 지정](specifying-a-character-set.md)을 참조하세요.  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MsgBox _
        Lib "user32.dll" Alias "MessageBox" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
## <a name="renaming-a-function-in-c-and-c"></a>C# 및 C++에서 함수 이름 바꾸기  
 <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=nameWithType> 필드를 사용하여 DLL 함수를 이름 또는 서수로 지정할 수 있습니다. 메서드 정의의 함수 이름이 DLL의 진입점과 같으면 **EntryPoint** 필드를 사용하여 함수를 명시적으로 식별할 필요가 없습니다. 그러지 않으면 다음 특성 형식 중 하나를 사용하여 이름 또는 서수를 나타냅니다.  
  
```csharp
[DllImport("DllName", EntryPoint = "Functionname")]
[DllImport("DllName", EntryPoint = "#123")]
```
  
 서수 앞에 파운드 기호(#)를 추가해야 합니다.  
  
 다음 예제에서는 **EntryPoint** 필드를 사용하여 코드에서 **MessageBoxA**를 **MsgBox**로 바꾸는 방법을 보여 줍니다.  
  
```csharp
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll", EntryPoint = "MessageBoxA")]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```
  
```cpp
using namespace System;
using namespace System::Runtime::InteropServices;

typedef void* HWND;
[DllImport("user32", EntryPoint = "MessageBoxA")]
extern "C" int MsgBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="see-also"></a>참조

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [관리 코드에서 프로토타입 만들기](creating-prototypes-in-managed-code.md)
- [플랫폼 호출 예제](platform-invoke-examples.md)
- [플랫폼 호출을 사용하여 데이터 마샬링](marshaling-data-with-platform-invoke.md)
