---
title: 클래스, 구조체 및 공용 구조체 마샬링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data marshaling, classes
- marshaling, unions
- marshaling, structures
- marshaling, samples
- data marshaling, structures
- platform invoke, marshaling data
- marshaling, classes
- data marshaling, unions
- data marshaling, samples
- data marshaling, platform invoke
- marshaling, platform invoke
ms.assetid: 027832a2-9b43-4fd9-9b45-7f4196261a4e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6f3e67fe49fb6d8a4d56b3d36d78d86c6c517d2a
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50181607"
---
# <a name="marshaling-classes-structures-and-unions"></a>클래스, 구조체 및 공용 구조체 마샬링
.NET Framework에서는 클래스와 구조체가 서로 비슷합니다. 둘 다 필드, 속성 및 이벤트를 포함할 수 있습니다. 또한 정적 및 비정적 메서드를 포함할 수 있습니다. 한 가지 주목할 만한 차이점은 구조체는 값 형식이고 클래스는 참조 형식이라는 것입니다.  
  
 다음 표에서는 클래스, 구조체 및 공용 구조체에 대한 마샬링 옵션을 나열하고 용도를 설명하며 해당하는 플랫폼 호출 샘플에 대한 링크를 제공합니다.  
  
|형식|설명|샘플|  
|----------|-----------------|------------|  
|값 방식 클래스.|관리되는 사례와 같이 정수 멤버를 In/Out 매개 변수로 사용하여 클래스를 전달합니다.|SysTime 샘플|  
|값 방식 구조체.|구조체를 In 매개 변수로 전달합니다.|Structures 샘플|  
|참조 방식 구조체.|구조체를 In/Out 매개 변수로 전달합니다.|OSInfo 샘플|  
|중첩 구조체를 포함하는 구조체(결합).|관리되지 않는 함수에서 중첩 구조체를 포함하는 구조체를 나타내는 클래스를 전달합니다. 관리되는 프로토타입에서는 구조체가 하나의 큰 구조체로 결합됩니다.|FindFile 샘플|  
|다른 구조체에 대한 포인터를 포함하는 구조체.|두 번째 구조체에 대한 포인터를 멤버로 포함하는 구조체를 전달합니다.|구조체 샘플|  
|값 형식 정수를 포함하는 구조체 배열.|정수만 포함하는 구조체 배열을 In/Out 매개 변수로 전달합니다. 배열의 멤버를 변경할 수 있습니다.|배열 샘플|  
|참조 형식 정수 및 문자열을 포함하는 구조체 배열.|정수 및 문자열을 포함하는 구조체 배열을 Out 매개 변수로 전달합니다. 호출된 함수가 배열에 대한 메모리를 할당합니다.|OutArrayOfStructs 샘플|  
|값 형식을 포함하는 공용 구조체.|값 형식(정수 및 double)을 포함하는 공용 구조체를 전달합니다.|Unions 샘플|  
|혼합된 형식을 포함하는 공용 구조체.|혼합된 형식(정수 및 문자열)을 포함하는 공용 구조체를 전달합니다.|Unions 샘플|  
|구조체의 null 값.|값 형식에 대한 참조 대신 null 참조(Visual Basic에서는 **Nothing**)를 전달합니다.|HandleRef 샘플|  
  
## <a name="structures-sample"></a>Structures 샘플  
 이 샘플에서는 두 번째 구조체를 가리키는 구조체, 포함된 구조체가 있는 구조체 및 포함된 배열이 있는 구조체를 전달하는 방법을 보여 줍니다.  
  
 Structs 샘플에서는 원래 함수 선언과 함께 표시되는 다음과 같은 관리되지 않는 함수를 사용합니다.  
  
-   PinvokeLib.dll에서 내보낸 **TestStructInStruct**.  
  
    ```  
    int TestStructInStruct(MYPERSON2* pPerson2);  
    ```  
  
-   PinvokeLib.dll에서 내보낸 **TestStructInStruct3**.  
  
    ```  
    void TestStructInStruct3(MYPERSON3 person3);  
    ```  
  
-   PinvokeLib.dll에서 내보낸 **TestArrayInStruct**.  
  
    ```  
    void TestArrayInStruct( MYARRAYSTRUCT* pStruct );  
    ```  
  
 [PinvokeLib.dll](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as6wyhwt(v=vs.100))은 앞에 나열된 함수 및 4개의 구조체(**MYPERSON**, **MYPERSON2**, **MYPERSON3** 및 **MYARRAYSTRUCT**)에 대한 구현을 포함하는 관리되지 않는 사용자 지정 라이브러리입니다. 이러한 구조체에는 다음과 같은 요소가 포함됩니다.  
  
```  
typedef struct _MYPERSON  
{  
   char* first;   
   char* last;   
} MYPERSON, *LP_MYPERSON;  
  
typedef struct _MYPERSON2  
{  
   MYPERSON* person;  
   int age;   
} MYPERSON2, *LP_MYPERSON2;  
  
typedef struct _MYPERSON3  
{  
   MYPERSON person;  
   int age;   
} MYPERSON3;  
  
typedef struct _MYARRAYSTRUCT  
{  
   bool flag;  
   int vals[ 3 ];   
} MYARRAYSTRUCT;  
```  
  
 관리되는 `MyPerson`, `MyPerson2`, `MyPerson3` 및 `MyArrayStruct` 구조체는 다음과 같은 특성을 갖습니다.  
  
-   `MyPerson`에는 문자열 멤버만 포함됩니다. [CharSet](specifying-a-character-set.md) 필드는 관리되지 않는 함수에 전달되는 경우 문자열을 ANSI 형식으로 설정합니다.  
  
-   `MyPerson2`에는 `MyPerson` 구조체에 대한 **IntPtr**이 포함됩니다. .NET Framework 응용 프로그램은 코드가 **안전하지 않은** 것으로 표시된 경우가 아니면 포인터를 사용하지 않으므로 **IntPtr** 형식이 관리되지 않는 구조체에 대한 원래 포인터를 대체합니다.  
  
-   `MyPerson3`에는 `MyPerson`이 포함된 구조체로 포함됩니다. 포함된 구조체의 요소를 기본 구조에 직접 배치하여 다른 구조체 내에 포함된 구조체를 결합하거나 이 샘플과 같이 포함된 구조체로 그대로 둘 수 있습니다.  
  
-   `MyArrayStruct`에는 정수 배열이 포함됩니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성은 <xref:System.Runtime.InteropServices.UnmanagedType> 열거형 값을 배열의 요소 수를 나타내는 데 사용되는 **ByValArray**로 설정합니다.  
  
 이 샘플의 모든 구조체에는 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성이 적용되어 멤버가 표시되는 순서대로 순차적으로 메모리에 정렬되게 합니다.  
  
 `LibWrap` 클래스에는 `App` 클래스가 호출하는 `TestStructInStruct`, `TestStructInStruct3` 및 `TestArrayInStruct` 메서드에 대한 관리되는 프로토타입이 포함됩니다. 각 프로토타입은 다음과 같이 단일 매개 변수를 선언합니다.  
  
-   `TestStructInStruct`는 `MyPerson2` 형식에 대한 참조를 해당 매개 변수로 선언합니다.  
  
-   `TestStructInStruct3`은 `MyPerson3` 형식을 해당 매개 변수로 선언하고 매개 변수를 값으로 전달합니다.  
  
-   `TestArrayInStruct`는 `MyArrayStruct` 형식에 대한 참조를 해당 매개 변수로 선언합니다.  
  
 메서드에 대한 인수로서의 구조체는 매개 변수에 **ref**(Visual Basic에서는 **ByRef**) 키워드가 포함되지 않은 경우 값으로 전달됩니다. 예를 들어 `TestStructInStruct` 메서드는 `MyPerson2` 형식의 개체에 대한 참조(주소 값)를 비관리 코드에 전달합니다. `MyPerson2`가 가리키는 구조체를 조작하기 위해 샘플에서는 지정된 크기의 버퍼를 만들고 <xref:System.Runtime.InteropServices.Marshal.AllocCoTaskMem%2A?displayProperty=nameWithType> 및 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 메서드를 결합하여 해당 주소를 반환합니다. 그런 다음 관리되는 구조체의 콘텐츠를 관리되지 않는 버퍼로 복사합니다. 끝으로, <xref:System.Runtime.InteropServices.Marshal.PtrToStructure%2A?displayProperty=nameWithType> 메서드를 사용하여 관리되지 않는 버퍼의 데이터를 관리되는 개체로 마샬링하고 <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A?displayProperty=nameWithType> 메서드를 사용하여 관리되지 않는 메모리 블록을 해제합니다.  
  
### <a name="declaring-prototypes"></a>프로토타입 선언  
 [!code-cpp[Conceptual.Interop.Marshaling#23](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/structures.cpp#23)]
 [!code-csharp[Conceptual.Interop.Marshaling#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/structures.cs#23)]
 [!code-vb[Conceptual.Interop.Marshaling#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/structures.vb#23)]  
  
### <a name="calling-functions"></a>함수 호출  
 [!code-cpp[Conceptual.Interop.Marshaling#24](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/structures.cpp#24)]
 [!code-csharp[Conceptual.Interop.Marshaling#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/structures.cs#24)]
 [!code-vb[Conceptual.Interop.Marshaling#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/structures.vb#24)]  
  
## <a name="findfile-sample"></a>FindFile 샘플  
 이 샘플에서는 포함된 두 번째 구조체를 포함하는 구조체를 관리되지 않는 함수에 전달하는 방법을 보여 줍니다. 또한 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 사용하여 구조체 내에서 고정 길이 배열을 선언하는 방법을 보여 줍니다. 이 샘플에서는 포함된 구조체 요소가 부모 구조체에 추가됩니다. 결합되지 않는 포함된 구조체의 샘플은 [Structures 샘플](https://msdn.microsoft.com/library/96a62265-dcf9-4608-bc0a-1f762ab9f48e(v=vs.100))을 참조하세요.  
  
 FindFile 샘플에서는 원래 함수 선언과 함께 표시되는 다음과 같은 관리되지 않는 함수를 사용합니다.  
  
-   Kernel32.dll에서 내보낸 **FindFirstFile**.  
  
    ```  
    HANDLE FindFirstFile(LPCTSTR lpFileName, LPWIN32_FIND_DATA lpFindFileData);  
    ```  
  
 함수에 전달된 원래 구조체에는 다음과 같은 요소가 포함됩니다.  
  
```  
typedef struct _WIN32_FIND_DATA   
{  
  DWORD    dwFileAttributes;   
  FILETIME ftCreationTime;   
  FILETIME ftLastAccessTime;   
  FILETIME ftLastWriteTime;   
  DWORD    nFileSizeHigh;   
  DWORD    nFileSizeLow;   
  DWORD    dwReserved0;   
  DWORD    dwReserved1;   
  TCHAR    cFileName[ MAX_PATH ];   
  TCHAR    cAlternateFileName[ 14 ];   
} WIN32_FIND_DATA, *PWIN32_FIND_DATA;  
```  
  
 이 샘플에서 `FindData` 클래스에는 원래 구조체 및 포함된 구조체의 각 요소에 해당하는 데이터 멤버가 포함됩니다. 두 개의 원래 문자 버퍼 대신 이 클래스가 문자열을 대체합니다. **MarshalAsAttribute**는 <xref:System.Runtime.InteropServices.UnmanagedType> 열거형을 관리되지 않는 구조체 내에 표시되는 인라인 고정 길이 문자 배열을 식별하는 데 사용되는 **ByValTStr**로 설정합니다.  
  
 `LibWrap` 클래스에는 `FindData` 클래스를 매개 변수로 전달하는 `FindFirstFile` 메서드의 관리되는 프로토타입이 포함됩니다. 참조 형식인 클래스는 기본적으로 In 매개 변수로 전달되므로 <xref:System.Runtime.InteropServices.InAttribute> 및 <xref:System.Runtime.InteropServices.OutAttribute> 특성을 통해 매개 변수를 선언해야 합니다.  
  
### <a name="declaring-prototypes"></a>프로토타입 선언  
 [!code-cpp[Conceptual.Interop.Marshaling#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/findfile.cpp#17)]
 [!code-csharp[Conceptual.Interop.Marshaling#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/findfile.cs#17)]
 [!code-vb[Conceptual.Interop.Marshaling#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/findfile.vb#17)]  
  
### <a name="calling-functions"></a>함수 호출  
 [!code-cpp[Conceptual.Interop.Marshaling#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/findfile.cpp#18)]
 [!code-csharp[Conceptual.Interop.Marshaling#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/findfile.cs#18)]
 [!code-vb[Conceptual.Interop.Marshaling#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/findfile.vb#18)]  
  
## <a name="unions-sample"></a>Unions 샘플  
 이 샘플에서는 값 형식만 포함하는 구조체 및 값 형식과 문자열을 매개 변수로 포함하는 구조체를 공용 구조체가 필요한 관리되지 않는 함수에 전달하는 방법을 보여 줍니다. 공용 구조체는 둘 이상의 변수가 공유할 수 있는 메모리 위치를 나타냅니다.  
  
 Unions 샘플에서는 원래 함수 선언과 함께 표시되는 다음과 같은 관리되지 않는 함수를 사용합니다.  
  
-   PinvokeLib.dll에서 내보낸 **TestUnion**.  
  
    ```  
    void TestUnion(MYUNION u, int type);  
    ```  
  
 [PinvokeLib.dll](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as6wyhwt(v=vs.100))은 앞에 나열된 함수와 두 공용 구조체, **MYUNION** and **MYUNION2**에 대한 구현을 포함하는 관리되지 않는 사용자 지정 라이브러리입니다. 공용 구조체에는 다음과 같은 요소가 포함됩니다.  
  
```  
union MYUNION  
{  
    int number;  
    double d;  
}  
  
union MYUNION2  
{  
    int i;  
    char str[128];  
};  
```  
  
 관리 코드에서는 공용 구조체가 구조체로 정의됩니다. `MyUnion` 구조체에는 두 개의 값 형식(정수 및 double)이 해당 멤버로 포함됩니다. <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성은 각 데이터 멤버의 정확한 위치를 제어하기 위해 설정됩니다. <xref:System.Runtime.InteropServices.FieldOffsetAttribute> 특성은 공용 구조체의 관리되지 않는 표현 내에서 필드의 실제 위치를 제공합니다. 두 멤버는 오프셋 값이 같으므로 동일한 메모리 부분을 정의할 수 있습니다.  
  
 `MyUnion2_1` 및 `MyUnion2_2`에는 각각 값 형식(정수)과 문자열이 포함됩니다. 관리 코드에서는 값 형식과 참조 형식이 겹칠 수 없습니다. 이 샘플에서는 메서드 오버로드를 통해 호출자가 동일한 관리되지 않는 함수를 호출할 때 두 형식을 모두 사용할 수 있게 합니다. `MyUnion2_1`의 레이아웃은 명시적이며 정확한 오프셋 값을 가집니다. 반면, 명시적 레이아웃은 참조 형식에 사용할 수 없으므로 `MyUnion2_2`에는 순차적 레이아웃이 있습니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성은 <xref:System.Runtime.InteropServices.UnmanagedType> 열거형을 공용 구조체의 관리되지 않는 표현 내에 표시되는 인라인 고정 길이 문자 배열을 식별하는 데 사용되는 **ByValTStr**로 설정합니다.  
  
 `LibWrap` 클래스에는 `TestUnion` 및 `TestUnion2` 메서드에 대한 프로토타입이 포함됩니다. `TestUnion2`는 `MyUnion2_1` 또는 `MyUnion2_2`를 매개 변수로 선언하기 위해 오버로드됩니다.  
  
### <a name="declaring-prototypes"></a>프로토타입 선언  
 [!code-cpp[Conceptual.Interop.Marshaling#28](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/unions.cpp#28)]
 [!code-csharp[Conceptual.Interop.Marshaling#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/unions.cs#28)]
 [!code-vb[Conceptual.Interop.Marshaling#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/unions.vb#28)]  
  
### <a name="calling-functions"></a>함수 호출  
 [!code-cpp[Conceptual.Interop.Marshaling#29](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/unions.cpp#29)]
 [!code-csharp[Conceptual.Interop.Marshaling#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/unions.cs#29)]
 [!code-vb[Conceptual.Interop.Marshaling#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/unions.vb#29)]  
  
## <a name="systime-sample"></a>SysTime 샘플  
 이 샘플에서는 구조체에 대한 포인터가 필요한 관리되지 않는 함수에 클래스에 대한 포인터를 전달하는 방법을 보여 줍니다.  
  
 SysTime 샘플에서는 원래 함수 선언과 함께 표시되는 다음과 같은 관리되지 않는 함수를 사용합니다.  
  
-   Kernel32.dll에서 내보낸 **GetSystemTime**.  
  
    ```  
    VOID GetSystemTime(LPSYSTEMTIME lpSystemTime);  
    ```  
  
 함수에 전달된 원래 구조체에는 다음과 같은 요소가 포함됩니다.  
  
```  
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
  
 이 샘플에서 `SystemTime` 클래스에는 클래스 멤버로 표현된 원래 구조체의 요소가 포함됩니다. <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성이 설정되어 멤버가 표시되는 순서대로 순차적으로 메모리에 정렬되게 합니다.  
  
 `LibWrap` 클래스에는 기본적으로 `SystemTime` 클래스를 In/Out 매개 변수로 전달하는 `GetSystemTime` 메서드의 관리되는 프로토타입이 포함됩니다. 참조 형식인 클래스는 기본적으로 In 매개 변수로 전달되므로 <xref:System.Runtime.InteropServices.InAttribute> 및 <xref:System.Runtime.InteropServices.OutAttribute> 특성을 통해 매개 변수를 선언해야 합니다. 호출자가 결과를 받으려면 이러한 [방향 특성](https://msdn.microsoft.com/library/241ac5b5-928e-4969-8f58-1dbc048f9ea2(v=vs.100))을 명시적으로 적용해야 합니다. `App` 클래스는 `SystemTime` 클래스의 새 인스턴스를 만들고 해당 데이터 필드에 액세스합니다.  
  
### <a name="code-samples"></a>코드 샘플  
 [!code-cpp[Conceptual.Interop.Marshaling#25](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/systime.cpp#25)]
 [!code-csharp[Conceptual.Interop.Marshaling#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/systime.cs#25)]
 [!code-vb[Conceptual.Interop.Marshaling#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/systime.vb#25)]  
  
## <a name="outarrayofstructs-sample"></a>OutArrayOfStructs 샘플  
 이 샘플에서는 정수 및 문자열을 Out 매개 변수로 포함하는 구조체의 배열을 관리되지 않는 함수에 전달하는 방법을 보여 줍니다.  
  
 <xref:System.Runtime.InteropServices.Marshal> 클래스 및 안전하지 않은 코드를 사용하여 네이티브 함수를 호출하는 방법을 보여 줍니다.  
  
 이 샘플에서는 [PinvokeLib.dll](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as6wyhwt(v=vs.100))에서 정의된 래퍼 함수 및 플랫폼 호출을 사용합니다(소스 파일에도 제공됨). `TestOutArrayOfStructs` 함수 및 `MYSTRSTRUCT2` 구조체를 사용합니다. 이 구조체에는 다음과 같은 요소가 포함됩니다.  
  
```  
typedef struct _MYSTRSTRUCT2  
{  
   char* buffer;  
   UINT size;   
} MYSTRSTRUCT2;  
```  
  
 `MyStruct` 클래스에는 ANSI 문자의 문자열 개체가 포함됩니다. <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> 필드는 ANSI 형식을 지정합니다. `MyUnsafeStruct`는 문자열 대신 <xref:System.IntPtr> 형식을 포함하는 구조체입니다.  
  
 `LibWrap` 클래스에는 오버로드된 `TestOutArrayOfStructs` 프로토타입 메서드가 포함됩니다. 메서드가 포인터를 매개 변수로 선언하는 경우 클래스에 `unsafe` 키워드를 표시해야 합니다. [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)]는 안전하지 않은 코드를 사용할 수 없으므로 오버로드된 메서드, 안전하지 않은 한정자 및 `MyUnsafeStruct` 구조체는 필요하지 않습니다.  
  
 `App` 클래스는 배열을 전달하는 데 필요한 모든 작업을 수행하는 `UsingMarshaling` 메서드를 구현합니다. 배열에 `out`(Visual Basic에서는 `ByRef`) 키워드가 표시되어 데이터가 호출 수신자에서 호출자로 전달됨을 나타냅니다. 이 구현에서는 다음과 같은 <xref:System.Runtime.InteropServices.Marshal> 클래스 메서드를 사용합니다.  
  
-   <xref:System.Runtime.InteropServices.Marshal.PtrToStructure%2A> - 관리되지 않는 버퍼의 데이터를 관리되는 개체로 마샬링합니다.  
  
-   <xref:System.Runtime.InteropServices.Marshal.DestroyStructure%2A> - 구조체의 문자열에 예약된 메모리를 해제합니다.  
  
-   <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> - 배열에 예약된 메모리를 해제합니다.  
  
 앞서 설명한 것처럼, C#에서는 안전하지 않은 코드를 허용하고 [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)]에서는 허용하지 않습니다. C# 샘플에서 `UsingUnsafePointer`는 <xref:System.Runtime.InteropServices.Marshal> 클래스 대신 포인터를 사용하여 `MyUnsafeStruct` 구조체가 포함된 배열을 다시 전달하는 대체 구현입니다.  
  
### <a name="declaring-prototypes"></a>프로토타입 선언  
 [!code-cpp[Conceptual.Interop.Marshaling#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/outarrayofstructs.cpp#20)]
 [!code-csharp[Conceptual.Interop.Marshaling#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/outarrayofstructs.cs#20)]
 [!code-vb[Conceptual.Interop.Marshaling#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/outarrayofstructs.vb#20)]  
  
### <a name="calling-functions"></a>함수 호출  
 [!code-cpp[Conceptual.Interop.Marshaling#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/outarrayofstructs.cpp#21)]
 [!code-csharp[Conceptual.Interop.Marshaling#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/outarrayofstructs.cs#21)]
 [!code-vb[Conceptual.Interop.Marshaling#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/outarrayofstructs.vb#21)]  
  
## <a name="see-also"></a>참고 항목  
 [플랫폼 호출을 사용하여 데이터 마샬링](marshaling-data-with-platform-invoke.md)  
 [플랫폼 호출 데이터 형식](https://msdn.microsoft.com/library/16014d9f-d6bd-481e-83f0-df11377c550f(v=vs.100))  
 [문자열 마샬링](marshaling-strings.md)  
 [형식 배열 마샬링](https://msdn.microsoft.com/library/049b1c1b-228f-4445-88ec-91bc7fd4b1e8(v=vs.100))
