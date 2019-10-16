---
title: My.forms 개체 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- My.Forms
- My.MyProject.Forms
helpviewer_keywords:
- My.Forms object
ms.assetid: f6bff4e6-6769-4294-956b-037aa6106d2a
ms.openlocfilehash: 9fa5c77dd12c98100e3d17fc473a6802180d1e32
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965977"
---
# <a name="myforms-object"></a>My.Forms 개체
현재 프로젝트에 선언 된 각 Windows form의 인스턴스에 액세스 하기 위한 속성을 제공 합니다.  
  
## <a name="remarks"></a>설명  
 개체 `My.Forms` 는 현재 프로젝트에 있는 각 폼의 인스턴스를 제공 합니다. 속성의 이름은 속성이 액세스 하는 폼의 이름과 동일 합니다.   
  
 한정자를 사용 하지 않고 폼 이름을 사용 `My.Forms` 하 여 개체에서 제공 하는 폼에 액세스할 수 있습니다. 속성 이름이 폼의 형식 이름과 동일 하기 때문에 기본 인스턴스가 있는 것 처럼 폼에 액세스할 수 있습니다. 예를 들어 `My.Forms.Form1.Show`은 `Form1.Show`와 같습니다.  
  
 개체 `My.Forms` 는 현재 프로젝트와 연결 된 폼만 노출 합니다. 참조 된 Dll에 선언 된 폼에 대 한 액세스 권한은 제공 하지 않습니다. DLL이 제공 하는 폼에 액세스 하려면 *DllName*로 작성 된 양식의 정규화 된 이름을 사용 해야 합니다. *FormName*.  
  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A> 속성을 사용 하 여 모든 응용 프로그램의 열려 있는 폼의 컬렉션을 가져올 수 있습니다.  
  
 개체 및 해당 속성은 Windows 응용 프로그램에 대해서만 사용할 수 있습니다.  
  
## <a name="properties"></a>속성  
 `My.Forms` 개체의 각 속성은 현재 프로젝트에 있는 폼의 인스턴스에 대 한 액세스를 제공 합니다. 속성의 이름은 속성이 액세스 하는 폼의 이름과 동일 하며, 속성 형식은 폼의 형식과 동일 합니다.  
  
> [!NOTE]
> 이름 충돌이 있는 경우 폼에 액세스 하기 위한 속성 이름은 *RootNamespace*_*Namespace*\_*FormName*입니다. 예를 들어, 이러한 폼 중 `Form1.`하나가 루트 네임 스페이스 `WindowsApplication1` 및 네임 스페이스 `Namespace1`에 있는 경우 라는 두 개의 폼을 고려 하 여를 통해 `My.Forms.WindowsApplication1_Namespace1_Form1`해당 폼에 액세스 합니다.  
  
 개체 `My.Forms` 는 시작 시 만들어진 응용 프로그램 기본 폼의 인스턴스에 대 한 액세스를 제공 합니다. 다른 모든 폼의 경우 개체 `My.Forms` 는 액세스 될 때 폼의 새 인스턴스를 만들고 저장 합니다. 이후에 해당 속성에 액세스 하려고 하면 해당 폼의 인스턴스가 반환 됩니다.  
  
 폼의 속성에를 할당 `Nothing` 하 여 폼을 삭제할 수 있습니다. 속성 setter는 폼의 <xref:System.Windows.Forms.Form.Close%2A> 메서드를 호출한 다음 저장 된 값에 `Nothing` 할당 합니다. 속성 `Nothing` 에 이외의 값을 할당 하면 setter가 <xref:System.ArgumentException> 예외를 throw 합니다.  
  
 또는 `My.Forms` `Is` 연산자를 사용 하 여 개체의 속성이 폼의 인스턴스를 저장 하는지 여부를 테스트할 수 있습니다. `IsNot` 이러한 연산자를 사용 하 여 속성 값이 인지 `Nothing`확인할 수 있습니다.  
  
> [!NOTE]
> 일반적으로 또는 `Is` `IsNot` 연산자는 비교를 수행 하기 위해 속성의 값을 읽어야 합니다. 그러나 속성이 현재 저장 `Nothing`된 경우 속성은 폼의 새 인스턴스를 만든 다음 해당 인스턴스를 반환 합니다. 그러나 Visual Basic 컴파일러는 `My.Forms` 개체의 속성을 다르게 처리 하 고 `Is` 또는 `IsNot` 연산자가 해당 값을 변경 하지 않고 속성의 상태를 확인할 수 있도록 허용 합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 기본 `SidebarMenu` 폼의 제목을 변경 합니다.  
  
 [!code-vb[VbVbalrMyForms#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyForms/VB/Class1.vb#2)]  
  
 이 예제가 작동 하려면 프로젝트에 라는 `SidebarMenu`양식이 있어야 합니다.  
  
 이 코드는 Windows 응용 프로그램 프로젝트 에서만 작동 합니다.  
  
## <a name="requirements"></a>요구 사항  
  
### <a name="availability-by-project-type"></a>프로젝트 형식에 따라 가용성  
  
|프로젝트 형식|사용 가능|  
|---|---|  
|Windows 애플리케이션|**예**|  
|클래스 라이브러리|아니요|  
|콘솔 애플리케이션|아니요|  
|Windows 컨트롤 라이브러리|아니요|  
|웹 컨트롤 라이브러리|아니요|  
|Windows 서비스|아니요|  
|웹 사이트|아니요|  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>
- <xref:System.Windows.Forms.Form>
- <xref:System.Windows.Forms.Form.Close%2A>
- [개체](../../../visual-basic/language-reference/objects/index.md)
- [Is 연산자](../../../visual-basic/language-reference/operators/is-operator.md)
- [IsNot 연산자](../../../visual-basic/language-reference/operators/isnot-operator.md)
- [응용 프로그램 폼 액세스](../../../visual-basic/developing-apps/programming/accessing-application-forms.md)
