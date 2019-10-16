---
title: '연습: Windows Api 호출 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- DLLs, calling
- Windows API, walkthroughs
- platform invoke, walkthroughs
- API calls [Visual Basic], walkthroughs [Visual Basic]
- Windows API, calling
- walkthroughs [Visual Basic], API calls
- DllImport attribute, calling Windows API
- Declare statement [Visual Basic], declaring DLL functions
ms.assetid: 9280ca96-7a93-47a3-8d01-6d01be0657cb
ms.openlocfilehash: 8e6d3e7f84c96d145a48daa27918cbb2cb3b61ac
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958307"
---
# <a name="walkthrough-calling-windows-apis-visual-basic"></a>연습: Windows Api 호출 (Visual Basic)
Windows Api는 Windows 운영 체제의 일부인 Dll (동적 연결 라이브러리)입니다. 이러한 작업을 사용 하 여 고유한 프로시저를 작성 하기가 어려울 때 작업을 수행할 수 있습니다. 예를 들어 Windows는 응용 프로그램에 `FlashWindowEx` 대 한 제목 표시줄을 밝은 색과 어두운 음영 사이에서 교대로 수행할 수 있는 라는 함수를 제공 합니다.  
  
 코드에서 Windows Api를 사용 하는 이점은 이미 작성 되어 사용 대기 중인 수십 개의 유용한 함수를 포함 하기 때문에 개발 시간을 절약할 수 있다는 점입니다. 단점은 Windows Api를 사용 하는 것이 어려울 수 있습니다.  
  
 Windows Api는 특별 한 종류의 상호 운용성을 나타냅니다. Windows Api는 관리 코드를 사용 하지 않고, 기본 제공 형식 라이브러리를 사용 하지 않으며, Visual Studio에서 사용 되는 것과 다른 데이터 형식을 사용 합니다. 이러한 차이로 인해 Windows Api는 COM 개체가 아니기 때문에 Windows Api와의 상호 운용성 및 .NET Framework는 플랫폼 호출 또는 PInvoke를 사용 하 여 수행 됩니다. 플랫폼 호출은 관리 코드에서 Dll에 구현 된 관리 되지 않는 함수를 호출할 수 있도록 하는 서비스입니다. 자세한 내용은 [관리 되지 않는 DLL 함수](../../../framework/interop/consuming-unmanaged-dll-functions.md)사용을 참조 하세요. `Declare` 문을 사용 하거나 빈 프로시저에 `DllImport` 특성을 적용 하 여 Visual Basic에서 PInvoke를 사용할 수 있습니다.  
  
 Windows API 호출은 과거에 Visual Basic 프로그래밍의 중요 한 부분 이지만 Visual Basic .NET에서는 거의 필요 하지 않습니다. 가능 하면 Windows API 호출 대신 .NET Framework에서 관리 코드를 사용 하 여 작업을 수행 해야 합니다. 이 연습에서는 Windows Api를 사용 해야 하는 상황에 대 한 정보를 제공 합니다.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="api-calls-using-declare"></a>선언을 사용 하 여 API 호출  
 Windows api를 호출 하는 가장 일반적인 방법은 `Declare` 문을 사용 하는 것입니다.  
  
### <a name="to-declare-a-dll-procedure"></a>DLL 프로시저를 선언 하려면  
  
1. 호출 하려는 함수의 이름과 인수, 인수 형식 및 반환 값을 확인 하 고이를 포함 하는 DLL의 이름과 위치를 확인 합니다.  
  
    > [!NOTE]
    > Windows Api에 대 한 전체 정보는 Platform SDK Windows API에서 Win32 SDK 설명서를 참조 하세요. Windows Api에서 사용 하는 상수에 대 한 자세한 내용은 Platform SDK에 포함 된 Windows 등의 헤더 파일을 검사 합니다.  
  
2. **파일** 메뉴에서 **새로 만들기** 를 클릭 한 다음 **프로젝트**를 클릭 하 여 새 Windows 응용 프로그램 프로젝트를 엽니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
3. Visual Basic 프로젝트 템플릿 목록에서 **Windows 응용 프로그램** 을 선택 합니다. 새 프로젝트가 표시 됩니다.  
  
4. DLL을 사용 `Declare` 하려는 클래스나 모듈에 다음 함수를 추가 합니다.  
  
     [!code-vb[VbVbalrInterop#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#9)]  
  
### <a name="parts-of-the-declare-statement"></a>Declare 문의 일부  
 `Declare` 문에는 다음과 같은 요소가 포함 됩니다.  
  
#### <a name="auto-modifier"></a>Auto 한정자  
 한정자 `Auto` 는 공용 언어 런타임 규칙 또는 별칭 이름 (지정 된 경우)에 따라 메서드 이름에 따라 문자열을 변환 하도록 런타임에 지시 합니다.  
  
#### <a name="lib-and-alias-keywords"></a>Lib 및 Alias 키워드  
 `Function` 키워드 뒤의 이름은 프로그램에서 가져온 함수에 액세스 하는 데 사용 하는 이름입니다. 호출 하는 함수의 실제 이름과 같을 수도 있고, 유효한 프로시저 이름을 사용 하 고 `Alias` 키워드를 사용 하 여 호출 하는 함수의 실제 이름을 지정할 수도 있습니다.  
  
 `Lib` 키워드를 지정 하 고 그 뒤에 호출 하는 함수가 포함 된 DLL의 이름과 위치를 지정 합니다. Windows 시스템 디렉터리에 있는 파일에 대 한 경로를 지정할 필요가 없습니다.  
  
 호출 하 `Alias` 는 함수 이름이 올바른 Visual Basic 프로시저 이름이 아니거나 응용 프로그램의 다른 항목 이름과 충돌 하는 경우 키워드를 사용 합니다. `Alias`호출 되는 함수의 실제 이름을 나타냅니다.  
  
#### <a name="argument-and-data-type-declarations"></a>인수 및 데이터 형식 선언  
 인수와 해당 데이터 형식을 선언 합니다. 이 부분은 Windows에서 사용 하는 데이터 형식이 Visual Studio 데이터 형식과 일치 하지 않기 때문에 어려울 수 있습니다. Visual Basic는 인수를 호환 되는 데이터 형식으로 변환 하 여 *마샬링*이라는 프로세스를 수행 하는 데 많은 작업을 수행 합니다. 네임<xref:System.Runtime.InteropServices> 스페이스에 정의 된 특성을 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 사용 하 여 인수가 마샬링되는 방식을 명시적으로 제어할 수 있습니다.  
  
> [!NOTE]
> 이전 버전의 Visual Basic을 사용 하 여 매개 `As Any`변수를 선언할 수 있습니다. 즉, 모든 데이터 형식의 데이터를 사용할 수 있습니다. Visual Basic를 사용 하려면 모든 `Declare` 문에 특정 데이터 형식을 사용 해야 합니다.  
  
#### <a name="windows-api-constants"></a>Windows API 상수  
 일부 인수는 상수의 조합입니다. 예를 들어이 `MessageBox` 연습에 표시 된 API는 메시지 상자가 표시 되 `Typ` 는 방식을 제어 하는 라는 정수 인수를 허용 합니다. 이 상수는 winuser.h 파일의 `#define` 문을 검사 하 여 숫자 값을 확인할 수 있습니다. 숫자 값은 일반적으로 16 진수로 표시 되므로 계산기를 사용 하 여 숫자 값을 추가 하 고 decimal로 변환 하는 것이 좋습니다. 예를 들어 느낌표 `MB_ICONEXCLAMATION` 및 예/아니요 스타일 `MB_YESNO` 0x00000004에 대 한 상수를 결합 하려는 경우 숫자를 추가 하 고 0x00000030 또는 52 진수의 결과를 가져올 수 있습니다. Decimal 결과를 직접 사용할 수 있지만 이러한 값을 응용 프로그램에서 상수로 선언 하 고 `Or` 연산자를 사용 하 여 결합 하는 것이 좋습니다.  
  
##### <a name="to-declare-constants-for-windows-api-calls"></a>Windows API 호출에 대 한 상수를 선언 하려면  
  
1. 호출 하는 Windows 함수에 대 한 설명서를 참조 하세요. 이 상수에 사용 되는 상수의 이름과 이러한 상수에 대 한 숫자 값을 포함 하는 .h 파일의 이름을 결정 합니다.  
  
2. 메모장과 같은 텍스트 편집기를 사용 하 여 헤더 (.h) 파일의 내용을 보고 사용 중인 상수와 연결 된 값을 찾습니다. 예를 들어 API `MessageBox` 는 상수 `MB_ICONQUESTION` 를 사용 하 여 메시지 상자에 물음표를 표시 합니다. 에 대 한 `MB_ICONQUESTION` 정의는 winuser.h에 있으며 다음과 같이 표시 됩니다.  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3. 이러한 상수 `Const` 를 응용 프로그램에서 사용할 수 있도록 클래스 또는 모듈에 해당 하는 문을 추가 합니다. 예를 들어:  
  
     [!code-vb[VbVbalrInterop#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#11)]  
  
###### <a name="to-call-the-dll-procedure"></a>DLL 프로시저를 호출 하려면  
  
1. 이라는 `Button1` 단추를 프로젝트의 시작 폼에 추가한 다음 두 번 클릭 하 여 해당 코드를 확인 합니다. 단추에 대 한 이벤트 처리기가 표시 됩니다.  
  
2. 추가 된 단추에 `Click` 대 한 이벤트 처리기에 코드를 추가 하 여 프로시저를 호출 하 고 적절 한 인수를 제공 합니다.  
  
     [!code-vb[VbVbalrInterop#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#12)]  
  
3. F5 키를 눌러 프로젝트를 실행 합니다. 메시지 상자에 **예** 및 응답 **없음** 단추가 모두 표시 됩니다. 하나를 클릭 합니다.  
  
#### <a name="data-marshaling"></a>데이터 마샬링  
 Visual Basic는 Windows api 호출에 대 한 매개 변수 및 반환 값의 데이터 형식을 자동으로 변환 하지만, `MarshalAs` 특성을 사용 하 여 API에 필요한 관리 되지 않는 데이터 형식을 명시적으로 지정할 수 있습니다. Interop 마샬링에 대 한 자세한 내용은 [Interop 마샬링](../../../framework/interop/interop-marshaling.md)을 참조 하세요.  
  
##### <a name="to-use-declare-and-marshalas-in-an-api-call"></a>API 호출에서 Declare 및 MarshalAs를 사용 하려면  
  
1. 호출 하려는 함수의 이름 및 해당 인수, 데이터 형식 및 반환 값을 결정 합니다.  
  
2. `MarshalAs` 특성에 대 한 액세스를 간소화 하려면 다음 `Imports` 예제와 같이 클래스 또는 모듈에 대 한 코드의 맨 위에 문을 추가 합니다.  
  
     [!code-vb[VbVbalrInterop#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#13)]  
  
3. 가져온 함수의 함수 프로토타입을 사용 하는 클래스 또는 모듈에 추가 하 고 `MarshalAs` 특성을 매개 변수 또는 반환 값에 적용 합니다. 다음 예제에서는 형식을 `void*` 예상 하는 API 호출이 다음과 같이 `AsAny`마샬링됩니다.  
  
     [!code-vb[VbVbalrInterop#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#14)]  
  
## <a name="api-calls-using-dllimport"></a>DllImport를 사용 하 여 API 호출  
 특성 `DllImport` 은 형식 라이브러리 없이 dll에서 함수를 호출 하는 두 번째 방법을 제공 합니다. `DllImport`는 `Declare` 문을 사용 하는 것과 거의 동일 하지만 함수가 호출 되는 방법을 보다 세밀 하 게 제어할 수 있습니다.  
  
 호출이 shared ( `DllImport` *static*이 라고도 함) 메서드를 참조 하는 한 대부분의 Windows API 호출에서을 사용할 수 있습니다. 클래스의 인스턴스를 필요로 하는 메서드는 사용할 수 없습니다. `Declare` `MarshalAs` 문과 달리 호출은특성을사용할수없습니다.`DllImport`  
  
### <a name="to-call-a-windows-api-using-the-dllimport-attribute"></a>DllImport 특성을 사용 하 여 Windows API를 호출 하려면  
  
1. **파일** 메뉴에서 **새로 만들기** 를 클릭 한 다음 **프로젝트**를 클릭 하 여 새 Windows 응용 프로그램 프로젝트를 엽니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
2. Visual Basic 프로젝트 템플릿 목록에서 **Windows 응용 프로그램** 을 선택 합니다. 새 프로젝트가 표시 됩니다.  
  
3. 이라는 `Button2` 단추를 시작 폼에 추가 합니다.  
  
4. 폼의 코드 `Button2` 보기를 두 번 클릭 하 여 엽니다.  
  
5. 에 `DllImport`대 한 액세스를 간소화 하려면 `Imports` 시작 폼 클래스에 대 한 코드의 맨 위에 문을 추가 합니다.  
  
     [!code-vb[VbVbalrInterop#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#13)]  
  
6. 폼에 대 한 `End Class` 문 앞에 빈 함수를 선언 하 고 함수 `MoveFile`이름을로 합니다.  
  
7. 및 한정자를 함수 선언에 적용 하 고 Windows API 함수 `MoveFile` 에서 사용 하는 인수에 따라에 대 한 매개 변수를 설정 합니다. `Shared` `Public`  
  
     [!code-vb[VbVbalrInterop#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#16)]  
  
     함수에는 유효한 프로시저 이름이 있을 수 있습니다. 특성 `DllImport` 은 DLL의 이름을 지정 합니다. 또한 매개 변수 및 반환 값에 대 한 상호 운용성 마샬링을 처리 하므로 API에서 사용 하는 데이터 형식과 비슷한 Visual Studio 데이터 형식을 선택할 수 있습니다.  
  
8. 빈 함수에 특성을 적용 합니다. `DllImport` 첫 번째 매개 변수는 호출 하는 함수를 포함 하는 DLL의 이름과 위치입니다. Windows 시스템 디렉터리에 있는 파일에 대 한 경로를 지정할 필요가 없습니다. 두 번째 매개 변수는 Windows API에서 함수 이름을 지정 하는 명명 된 인수입니다. 이 예제에서 특성은 `DllImport` 에 대 `MoveFile` 한 호출이 kernel32.dll에서로 `MoveFileW` 전달 되도록 합니다. GDIPLUS.DLL. 메서드 `MoveFileW` 는 경로에서 `src` 경로 `dst`에 파일을 복사 합니다.  
  
     [!code-vb[VbVbalrInterop#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#17)]  
  
9. 함수를 호출 하 `Button2_Click` 는 코드를 이벤트 처리기에 추가 합니다.  
  
     [!code-vb[VbVbalrInterop#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#18)]  
  
10. Test.txt 라는 파일을 만들고 하드 드라이브의 C:\Tmp 디렉터리에 넣습니다. 필요한 경우 Tmp 디렉터리를 만듭니다.  
  
11. F5 키를 눌러 애플리케이션을 시작합니다. 기본 폼이 나타납니다.  
  
12. **Button2**를 클릭 합니다. 파일을 이동할 수 있는 경우 "파일이 성공적으로 이동 되었습니다." 라는 메시지가 표시 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
- [자동](../../../visual-basic/language-reference/modifiers/auto.md)
- [Alias](../../../visual-basic/language-reference/statements/alias-clause.md)
- [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)
- [관리 코드에서 프로토타입 만들기](../../../framework/interop/creating-prototypes-in-managed-code.md)
- [콜백 메서드로 대리자 마샬링](../../../framework/interop/marshaling-a-delegate-as-a-callback-method.md)
