---
title: 상호 운용성 문제 해결(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interop, deploying assemblies
- assemblies [Visual Basic]
- interop, installing assemblies that share components
- COM objects, troubleshooting
- interop, sharing components
- troubleshooting interoperability [Visual Basic]
- interoperability, troubleshooting
- COM interop [Visual Basic], troubleshooting
- assemblies [Visual Basic], deploying
- troubleshooting Visual Basic, interoperability
- interop assemblies
- interoperability, sharing components
- shared components, using with assemblies
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
ms.openlocfilehash: c04cd0928eb83aabcd1f0f4b1b43f8ae6d356d20
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969331"
---
# <a name="troubleshooting-interoperability-visual-basic"></a>상호 운용성 문제 해결(Visual Basic)
COM과 .NET Framework의 관리 코드 간에 상호 운용 하는 경우 다음과 같은 일반적인 문제 중 하나 이상이 발생할 수 있습니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor1"></a>Interop 마샬링  
 때때로 .NET Framework에 포함 되지 않은 데이터 형식을 사용 해야 할 수 있습니다. Interop 어셈블리는 대부분의 COM 개체 작업을 처리 하지만 관리 되는 개체를 COM에 노출할 때 사용 되는 데이터 형식을 제어 해야 할 수도 있습니다. 예를 들어 클래스 라이브러리의 구조체는 Visual Basic 6.0 `BStr` 이전 버전에서 만든 COM 개체로 전송 되는 문자열에 대해 관리 되지 않는 형식을 지정 해야 합니다. 이러한 경우 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 사용 하 여 관리 되는 형식을 관리 되지 않는 형식으로 노출 시킬 수 있습니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor2"></a>고정 길이 문자열을 비관리 코드로 내보내기  
 Visual Basic 6.0 이전 버전에서 문자열은 null 종결 문자가 없는 바이트 시퀀스로 COM 개체로 내보내집니다. 다른 언어와의 호환성을 위해 Visual Basic .NET은 문자열을 내보낼 때 종료 문자를 포함 합니다. 이러한 비 호환성 문제를 해결 하는 가장 좋은 방법은 종료 문자를 `Byte` 또는 `Char`배열로 하지 않는 문자열을 내보내는 것입니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor3"></a>상속 계층 구조 내보내기  
 관리 되는 클래스 계층 구조는 COM 개체로 노출 될 때 결합 됩니다. 예를 들어 멤버를 사용 하 여 기본 클래스를 정의한 다음 COM 개체로 노출 되는 파생 클래스에서 기본 클래스를 상속 하는 경우 COM 개체에서 파생 클래스를 사용 하는 클라이언트는 상속 된 멤버를 사용할 수 없습니다. 기본 클래스 멤버는 기본 클래스의 인스턴스로만 COM 개체에서 액세스할 수 있으며, 기본 클래스도 COM 개체로 생성 된 경우에만 사용할 수 있습니다.  
  
## <a name="overloaded-methods"></a>오버로드된 메서드  
 Visual Basic를 사용 하 여 오버 로드 된 메서드를 만들 수는 있지만 COM에서 지원 되지 않습니다. 오버 로드 된 메서드를 포함 하는 클래스가 COM 개체로 노출 되는 경우 오버 로드 된 메서드에 대 한 새 메서드 이름이 생성 됩니다.  
  
 예를 들어 `Synch` 메서드의 오버 로드가 두 개 있는 클래스를 생각해 보겠습니다. 클래스가 COM 개체로 노출 되는 경우 생성 되는 새 메서드 이름은 및 `Synch` `Synch_2`일 수 있습니다.  
  
 이름을 바꾸면 COM 개체의 소비자에 게 두 가지 문제가 발생할 수 있습니다.  
  
1. 클라이언트는 생성 된 메서드 이름을 필요로 하지 않을 수 있습니다.  
  
2. COM 개체로 노출 된 클래스에서 생성 된 메서드 이름은 새 오버 로드가 클래스 또는 해당 기본 클래스에 추가 될 때 변경 될 수 있습니다. 이로 인해 버전 관리 문제가 발생할 수 있습니다.  
  
 두 문제를 모두 해결 하려면 COM 개체로 노출 되는 개체를 개발할 때 오버 로드를 사용 하는 대신 각 메서드에 고유한 이름을 지정 합니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor4"></a>Interop 어셈블리를 통해 COM 개체 사용  
 Interop 어셈블리는 해당 어셈블리가 나타내는 COM 개체에 대 한 관리 코드 대체 인 경우와 거의 동일 하 게 사용 됩니다. 그러나 래퍼는 실제 COM 개체가 아니라 래퍼 이므로 interop 어셈블리와 표준 어셈블리를 사용 하는 것 사이에는 약간의 차이가 있습니다. 이러한 차이 영역에는 클래스의 노출, 매개 변수 및 반환 값에 대 한 데이터 형식이 포함 됩니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor5"></a>인터페이스와 클래스로 노출 되는 클래스  
 표준 어셈블리의 클래스와 달리 COM 클래스는 COM 클래스를 나타내는 인터페이스와 클래스로 interop 어셈블리에서 노출 됩니다. 인터페이스의 이름은 COM 클래스의 이름과 동일 합니다. Interop 클래스의 이름은 원래 COM 클래스의 이름과 같지만 "Class" 라는 단어가 추가 됩니다. 예를 들어 COM 개체에 대 한 interop 어셈블리에 대 한 참조가 포함 된 프로젝트가 있다고 가정 합니다. COM 클래스의 이름이 `MyComClass`인 경우 IntelliSense와 개체 브라우저는 이라는 `MyComClass` 인터페이스와 라는 `MyComClassClass`클래스를 표시 합니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor6"></a>.NET Framework 클래스의 인스턴스 만들기  
 일반적으로 클래스 이름으로 `New` 문을 사용 하 여 .NET Framework 클래스의 인스턴스를 만듭니다. Interop 어셈블리로 표시 되는 COM 클래스는 인터페이스와 함께 `New` 문을 사용할 수 있는 한 가지 경우입니다. `Inherits` 문을 사용 하 여 COM 클래스를 사용 하지 않는 경우 클래스와 동일한 방식으로 인터페이스를 사용할 수 있습니다. 다음 코드에서는 Microsoft ADO(ActiveX Data Objects) 2.8 Library COM `Command` 개체에 대 한 참조를 포함 하는 프로젝트에서 개체를 만드는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrInterop#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#20)]  
  
 그러나 COM 클래스를 파생 클래스의 기본으로 사용 하는 경우에는 다음 코드와 같이 COM 클래스를 나타내는 interop 클래스를 사용 해야 합니다.  
  
 [!code-vb[VbVbalrInterop#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#21)]  
  
> [!NOTE]
> Interop 어셈블리는 COM 클래스를 나타내는 인터페이스를 암시적으로 구현 합니다. 이러한 인터페이스를 구현 하는 `Implements` 데 문을 사용해 서는 안 됩니다. 그렇지 않으면 오류가 발생 합니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor7"></a>매개 변수 및 반환 값에 대 한 데이터 형식  
 표준 어셈블리의 멤버와 달리 interop 어셈블리 멤버는 원래 개체 선언에 사용 된 것과 다른 데이터 형식을 가질 수 있습니다. Interop 어셈블리는 암시적으로 COM 형식을 호환 되는 공용 언어 런타임 형식으로 변환 하지만 런타임 오류를 방지 하기 위해 양쪽에서 사용 되는 데이터 형식에 주의 해야 합니다. 예를 들어 Visual Basic 6.0 이전 버전에서 만든 COM 개체에서 형식의 `Integer` 값은 .NET Framework 해당 형식이 인 `Short`것으로 가정 합니다. 사용 하기 전에 개체 브라우저를 사용 하 여 가져온 멤버의 특성을 검사 하는 것이 좋습니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor8"></a>모듈 수준 COM 메서드  
 대부분의 com 개체는 키워드를 `New` 사용 하 여 com 클래스의 인스턴스를 만든 다음 개체의 메서드를 호출 하 여 사용 됩니다. 이 규칙의 한 가지 예외는 또는 `AppObj` `GlobalMultiUse` com 클래스를 포함 하는 com 개체와 관련이 있습니다. 이러한 클래스는 Visual Basic .NET 클래스의 모듈 수준 메서드와 유사 합니다. Visual Basic 6.0 이전 버전에서는 처음에 해당 메서드 중 하나를 호출할 때 이러한 개체의 인스턴스를 암시적으로 만듭니다. 예를 들어 Visual Basic 6.0에서는 Microsoft DAO 3.6 개체 라이브러리에 대 한 참조를 추가 하 고 먼저 인스턴스 `DBEngine` 를 만들지 않고 메서드를 호출할 수 있습니다.  
  
```vb  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 Visual Basic .NET을 사용 하려면 먼저 COM 개체의 인스턴스를 만든 후에 해당 메서드를 사용 해야 합니다. Visual Basic에서 이러한 메서드를 사용 하려면 원하는 클래스의 변수를 선언 하 고 new 키워드를 사용 하 여 개체를 개체 변수에 할당 합니다. 클래스 `Shared` 의 인스턴스를 하나만 만들도록 하려면 키워드를 사용할 수 있습니다.  
  
 [!code-vb[VbVbalrInterop#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#23)]  
  
## <a name="vbconinteroperabilitymarshalinganchor9"></a>이벤트 처리기에서 처리 되지 않은 오류  
 일반적인 interop 문제 중 하나에는 COM 개체에서 발생 한 이벤트를 처리 하는 이벤트 처리기의 오류가 포함 됩니다. `On Error` 또는`Try...Catch...Finally` 문을 사용 하 여 오류를 구체적으로 확인 하지 않으면 이러한 오류는 무시 됩니다. 예를 들어 다음 예제는 Microsoft ADO(ActiveX Data Objects) 2.8 Library COM 개체에 대 한 참조를 포함 하는 Visual Basic .NET 프로젝트에서 가져온 것입니다.  
  
 [!code-vb[VbVbalrInterop#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#24)]  
  
 이 예에서는 예상 대로 오류를 발생 시킵니다. 그러나 `Try...Catch...Finally` 블록 없이 동일한 예제를 시도 하는 경우에는 `OnError Resume Next` 문을 사용한 것 처럼 오류가 무시 됩니다. 오류 처리를 사용 하지 않으면 0으로 나누기가 자동으로 실패 합니다. 이러한 오류는 처리 되지 않은 예외 오류를 발생 시 키 지 않으므로 COM 개체의 이벤트를 처리 하는 이벤트 처리기에서 특정 형식의 예외 처리를 사용 하는 것이 중요 합니다.  
  
### <a name="understanding-com-interop-errors"></a>COM interop 오류 이해  
 오류 처리를 사용 하지 않으면 interop 호출은 종종 거의 정보를 제공 하지 않는 오류를 생성 합니다. 가능 하면 구조화 된 오류 처리를 사용 하 여 발생 하는 문제에 대 한 자세한 정보를 제공 합니다. 응용 프로그램을 디버그할 때 특히 유용할 수 있습니다. 예를 들어:  
  
 [!code-vb[VbVbalrInterop#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#25)]  
  
 예외 개체의 내용을 검사 하 여 오류 설명, HRESULT 및 COM 오류 소스와 같은 정보를 찾을 수 있습니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor10"></a>ActiveX 컨트롤 문제  
 Visual Basic 6.0에서 작동 하는 대부분의 ActiveX 컨트롤은 문제 없이 Visual Basic .NET과 함께 작동 합니다. 주요 예외는 컨테이너 컨트롤이 나 시각적으로 다른 컨트롤을 포함 하는 컨트롤입니다. Visual Studio에서 제대로 작동 하지 않는 이전 컨트롤의 몇 가지 예는 다음과 같습니다.  
  
- Microsoft Forms 2.0 프레임 컨트롤  
  
- Up-down 컨트롤 (spin 컨트롤이 라고도 함)  
  
- Sheridan 탭 컨트롤  
  
 지원 되지 않는 ActiveX 컨트롤 문제에 대 한 몇 가지 해결 방법이 있습니다. 원래 소스 코드를 소유 하 고 있는 경우 기존 컨트롤을 Visual Studio로 마이그레이션할 수 있습니다. 그렇지 않으면 소프트웨어 공급 업체와 함께 업데이트를 확인할 수 있습니다. 지원 되지 않는 ActiveX 컨트롤을 대체할 수 있는 .NET 호환 버전의 컨트롤입니다.  
  
## <a name="vbconinteroperabilitymarshalinganchor11"></a>컨트롤의 ReadOnly 속성 전달 ByRef  
 Visual Basic .net은 일부 이전 ActiveX 컨트롤의 속성을 다른 프로시저에 대 한 매개 변수로 `ReadOnly` `ByRef` 전달 하는 경우 "Error 0x800a017f CTL_E_SETNOTSUPPORTED"와 같은 COM 오류를 발생 시킬 수 있습니다. Visual Basic 6.0의 비슷한 프로시저 호출은 오류를 발생 시 키 지 않으며 매개 변수는 값으로 전달 된 것 처럼 처리 됩니다. Visual Basic .net 오류 메시지는 속성 `Set` 프로시저가 없는 속성을 변경 하려고 함을 나타냅니다.  
  
 호출 중인 프로시저에 대 한 액세스 권한이 있는 경우 `ByVal` 키워드를 사용 하 여 속성을 허용 `ReadOnly` 하는 매개 변수를 선언 하 여이 오류를 방지할 수 있습니다. 예를 들어:  
  
 [!code-vb[VbVbalrInterop#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#26)]  
  
 호출 되는 프로시저의 소스 코드에 액세스할 수 없는 경우 호출 하는 프로시저 주위에 추가 대괄호를 추가 하 여 속성을 값으로 전달할 수 있습니다. 예를 들어 Microsoft ADO(ActiveX Data Objects) 2.8 Library COM 개체에 대 한 참조를 포함 하는 프로젝트에서는 다음을 사용할 수 있습니다.  
  
 [!code-vb[VbVbalrInterop#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#27)]  
  
## <a name="vbconinteroperabilitymarshalinganchor12"></a>Interop를 노출 하는 어셈블리 배포  
 COM 인터페이스를 노출 하는 어셈블리를 배포 하면 몇 가지 고유한 과제가 제공 됩니다. 예를 들어 별도의 응용 프로그램이 동일한 COM 어셈블리를 참조 하는 경우 잠재적인 문제가 발생 합니다. 이 상황은 어셈블리의 새 버전이 설치 되 고 다른 응용 프로그램이 여전히 이전 버전의 어셈블리를 사용 하는 경우에 일반적입니다. DLL을 공유 하는 어셈블리를 제거 하는 경우 다른 어셈블리에서 실수로 사용할 수 없게 될 수 있습니다.  
  
 이 문제를 방지 하려면 공유 어셈블리를 GAC (전역 어셈블리 캐시)에 설치 하 고 구성 요소에 대 한 병합 모듈를 사용 해야 합니다. GAC에 응용 프로그램을 설치할 수 없는 경우 버전별 하위 디렉터리에 CommonFilesFolder에 설치 해야 합니다.  
  
 공유 되지 않은 어셈블리는 호출 하는 응용 프로그램과 함께 디렉터리에 나란히 배치 되어야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)
- [Tlbimp.exe(형식 라이브러리 가져오기)](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe(형식 라이브러리 내보내기)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [연습: COM 개체를 사용한 상속 구현](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)
- [Inherits 문](../../../visual-basic/language-reference/statements/inherits-statement.md)
- [전역 어셈블리 캐시](../../../framework/app-domains/gac.md)
