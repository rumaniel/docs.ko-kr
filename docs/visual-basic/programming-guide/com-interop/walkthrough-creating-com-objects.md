---
title: '연습: Visual Basic를 사용 하 여 COM 개체 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop [Visual Basic], creating COM objects
- COM objects, creating
- COM interop [Visual Basic], walkthroughs
- object creation [Visual Basic], COM objects
- COM objects, walkthroughs
ms.assetid: 7b07a463-bc72-4392-9ba0-9dfcb697a44f
ms.openlocfilehash: 39012ebdd8946f707fe459cb09bb2bbfc8e50088
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958274"
---
# <a name="walkthrough-creating-com-objects-with-visual-basic"></a>연습: Visual Basic를 사용 하 여 COM 개체 만들기
새 응용 프로그램 또는 구성 요소를 만들 때 .NET Framework 어셈블리를 만드는 것이 가장 좋습니다. 그러나 Visual Basic를 사용 하면 .NET Framework 구성 요소를 COM에 쉽게 노출할 수 있습니다. 이를 통해 COM 구성 요소가 필요한 이전 응용 프로그램 제품군에 대해 새로운 구성 요소를 제공할 수 있습니다. 이 연습에서는 Visual Basic를 사용 하 여 COM 클래스 템플릿을 사용 하거나 사용 하지 않고 .NET Framework 개체를 COM 개체로 노출 하는 방법을 보여 줍니다.  
  
 Com 개체를 노출 하는 가장 쉬운 방법은 COM 클래스 템플릿을 사용 하는 것입니다. COM 클래스 템플릿은 새 클래스를 만든 다음 클래스 및 상호 운용성 계층을 COM 개체로 생성 하 고 운영 체제에 등록 하도록 프로젝트를 구성 합니다.  
  
> [!NOTE]
> Visual Basic에서 만든 클래스를 비관리 코드에서 사용할 COM 개체로 노출할 수도 있지만,이 클래스는 진정한 COM 개체가 아니므로 Visual Basic 사용할 수 없습니다. 자세한 내용은 [.NET Framework 애플리케이션의 COM 상호 운용성](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)합니다.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-com-object-by-using-the-com-class-template"></a>COM 클래스 템플릿을 사용 하 여 COM 개체를 만들려면  
  
1. **파일** 메뉴에서 새 **프로젝트**를 클릭 하 여 새 Windows 응용 프로그램 프로젝트를 엽니다.  
  
2. **새 프로젝트** 대화 상자의 **프로젝트 형식** 필드에서 Windows가 선택 되어 있는지 확인 합니다. **템플릿** 목록에서 **클래스 라이브러리** 를 선택 하 고 **확인**을 클릭 합니다. 새 프로젝트가 표시 됩니다.  
  
3. **프로젝트** 메뉴에서 **새 항목 추가** 를 선택 합니다. **새 항목 추가** 대화 상자가 표시됩니다.  
  
4. **템플릿** 목록에서 **COM 클래스** 를 선택한 다음 **추가**를 클릭 합니다. Visual Basic 새 클래스를 추가 하 고 COM interop에 대 한 새 프로젝트를 구성 합니다.  
  
5. 속성, 메서드 및 이벤트와 같은 코드를 COM 클래스에 추가 합니다.  
  
6. **빌드** 메뉴에서 **classlibrary1.chainone 빌드** 를 선택 합니다. Visual Basic는 어셈블리를 빌드하고 운영 체제에 COM 개체를 등록 합니다.  
  
## <a name="creating-com-objects-without-the-com-class-template"></a>COM 클래스 템플릿을 사용 하지 않고 COM 개체 만들기  
 COM 클래스 템플릿을 사용 하는 대신 COM 클래스를 수동으로 만들 수도 있습니다. 이 절차는 명령줄에서 작업 하는 경우 나 COM 개체가 정의 되는 방법을 더 자세히 제어 하려는 경우에 유용 합니다.  
  
#### <a name="to-set-up-your-project-to-generate-a-com-object"></a>COM 개체를 생성 하도록 프로젝트를 설정 하려면  
  
1. **Newproject**를 클릭 하 여 **파일** 메뉴에서 새 Windows 응용 프로그램 프로젝트를 엽니다.  
  
2. **새 프로젝트** 대화 상자의 **프로젝트 형식** 필드에서 Windows가 선택 되어 있는지 확인 합니다. **템플릿** 목록에서 **클래스 라이브러리** 를 선택 하 고 **확인**을 클릭 합니다. 새 프로젝트가 표시 됩니다.  
  
3. **솔루션 탐색기**에서 프로젝트를 오른쪽 마우스 단추로 클릭하고 **속성**을 클릭합니다. **프로젝트 디자이너가** 표시 됩니다.  
  
4. **컴파일** 탭을 클릭합니다.  
  
5. **COM Interop 등록** 확인란을 선택 합니다.  
  
#### <a name="to-set-up-the-code-in-your-class-to-create-a-com-object"></a>COM 개체를 만들기 위해 클래스에 코드를 설정 하려면  
  
1. **솔루션 탐색기**에서 **Class1 .vb** 를 두 번 클릭 하 여 해당 코드를 표시 합니다.  
  
2. 클래스 이름을 `ComClass1`로 바꿉니다.  
  
3. 에 `ComClass1`다음 상수를 추가 합니다. COM 개체에 필요한 GUID (Globally Unique Identifier) 상수를 저장 합니다.  
  
     [!code-vb[VbVbalrInterop#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#2)]  
  
4. **도구** 메뉴에서 **GUID 만들기**를 클릭합니다. **GUID 만들기** 대화 상자에서 **레지스트리 형식**과 **복사**를 차례로 클릭합니다. **끝내기**를 클릭합니다.  
  
5. 에 대 한 `ClassId` 빈 문자열을 GUID로 바꾸고 선행 중괄호와 후행 중괄호를 제거 합니다. 예를 들어, guidgen.exe에서 제공 하는 GUID `"{2C8B0AEE-02C9-486e-B809-C780A11530FE}"` 가 이면 코드가 다음과 같이 표시 됩니다.  
  
     [!code-vb[VbVbalrInterop#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#3)]  
  
6. 다음 예제와 같이 `InterfaceId` 및 `EventsId` 상수에 대해 이전 단계를 반복 합니다.  
  
     [!code-vb[VbVbalrInterop#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#4)]  
  
    > [!NOTE]
    > Guid가 새롭고 고유한 지 확인 합니다. 그렇지 않으면 COM 구성 요소가 다른 COM 구성 요소와 충돌할 수 있습니다.  
  
7. 다음 예제와 같이 `ComClass1`클래스 id, 인터페이스 id 및 이벤트 id에 대 한 guid를 지정 하 여 특성을에추가합니다.`ComClass`  
  
     [!code-vb[VbVbalrInterop#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#5)]  
  
8. COM 클래스에는 매개 변수가 `Public Sub New()` 없는 생성자가 있어야 합니다. 그렇지 않으면 클래스가 올바르게 등록 되지 않습니다. 클래스에 매개 변수가 없는 생성자를 추가 합니다.  
  
     [!code-vb[VbVbalrInterop#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#6)]  
  
9. 클래스에 속성, 메서드 및 이벤트를 추가 하 여 `End Class` 문으로 종료 합니다. **빌드** 메뉴에서 **솔루션 빌드** 를 선택 합니다. Visual Basic는 어셈블리를 빌드하고 운영 체제에 COM 개체를 등록 합니다.  
  
    > [!NOTE]
    > Visual Basic를 사용 하 여 생성 하는 COM 개체는 진정한 COM 개체가 아니기 때문에 다른 Visual Basic 응용 프로그램에서 사용할 수 없습니다. 이러한 COM 개체에 대 한 참조를 추가 하려고 하면 오류가 발생 합니다. 자세한 내용은 참조 하세요 [.NET Framework 애플리케이션의 COM 상호 운용성](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ComClassAttribute>
- [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)
- [연습: COM 개체를 사용한 상속 구현](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)
- [#Region 지시문](../../../visual-basic/language-reference/directives/region-directive.md)
- [.NET Framework 응용 프로그램의 COM 상호 운용성](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)
- [상호 운용성 문제 해결](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)
