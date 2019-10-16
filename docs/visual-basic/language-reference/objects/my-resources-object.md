---
title: My.Resources 개체 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- My.Resources
- My.Resources.MyResources.ResourceManager
- My.Resources.MyResources.Culture
helpviewer_keywords:
- My.Resources object
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
ms.openlocfilehash: 02e29b17404da0e868973364b0b17b5c4ca418c6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647623"
---
# <a name="myresources-object"></a>My.Resources 개체
응용 프로그램의 리소스에 액세스 하기 위한 속성 및 클래스를 제공 합니다.  
  
## <a name="remarks"></a>설명  
 `My.Resources` 개체 응용 프로그램의 리소스에 대 한 액세스를 제공 하 고 사용 하면 동적으로 응용 프로그램에 대 한 리소스를 검색 합니다. 자세한 내용은 [응용 프로그램 리소스 관리 (.NET)](/visualstudio/ide/managing-application-resources-dotnet)합니다.  
  
 `My.Resources` 개체는 전역 리소스만 노출 합니다. 폼과 관련 된 리소스 파일에 대 한 액세스를 제공 하지 않습니다. 폼에서 폼 리소스에 액세스 해야 합니다.  
  
 응용 프로그램의 문화권 관련 리소스 파일에서 액세스할 수는 `My.Resources` 개체입니다. 기본적으로 `My.Resources` 개체의 culture와 일치 하는 리소스 파일에서 리소스 조회는 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> 속성입니다. 그러나이 동작을 재정의 하 고 리소스에 사용할 특정 문화권을 지정할 수 있습니다. 자세한 내용은 [데스크톱 앱의 리소스](../../../framework/resources/index.md)를 참조하세요.  
  
## <a name="properties"></a>속성  
 속성을 `My.Resources` 개체 응용 프로그램의 리소스에 대 한 읽기 전용 액세스를 제공 합니다. 리소스 추가 또는 제거를 사용 합니다 **프로젝트 디자이너**합니다. 통해 추가 리소스에 액세스할 수 합니다 **프로젝트 디자이너** 사용 하 여 `My.Resources.` *resourceName*합니다.  
  
 추가 하거나에서 프로젝트를 선택 하 여 리소스 파일을 제거할 수도 **솔루션 탐색기** 를 클릭 하 고 **새 항목 추가** 하거나 **기존 항목 추가** 에서  **프로젝트** 메뉴. 이 방식으로 사용 하 여 추가 리소스에 액세스할 수 있습니다 `My.Resources.` *resourceFileName*`.`*resourceName*합니다.  
  
 각 리소스에 이름, 범주 및 값 및 이러한 리소스 설정에 따라 리소스를 액세스 하는 속성에 표시 되는 방식을 결정 합니다 `My.Resources` 개체입니다. 리소스에 추가 합니다 **프로젝트 디자이너**:  
  
- 속성의 이름이 확인 하는 이름  
  
- 리소스 데이터는 속성의 값  
  
- 범주에는 속성의 형식을 결정합니다.  
  
|범주|속성 데이터 형식|  
|---|---|  
|**문자열**|[String](../../../visual-basic/language-reference/data-types/string-data-type.md)|  
|**이미지**|<xref:System.Drawing.Bitmap>|  
|**아이콘**|<xref:System.Drawing.Icon>|  
|**오디오**|<xref:System.IO.UnmanagedMemoryStream><br /><br /> <xref:System.IO.UnmanagedMemoryStream> 클래스에서 파생 되는 <xref:System.IO.Stream> 같은 스트림을 사용 하는 메서드를 사용 하 여 사용할 수 있도록 클래스를 <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> 메서드.|  
|**파일**|-   [문자열](../../../visual-basic/language-reference/data-types/string-data-type.md) 텍스트 파일에 대 한 합니다.<br />-   <xref:System.Drawing.Bitmap> 이미지 파일입니다.<br />-   <xref:System.Drawing.Icon> 아이콘 파일입니다.<br />-   <xref:System.IO.UnmanagedMemoryStream> 사운드 파일입니다.|  
|**기타**|디자이너에 있는 정보에 따른 **형식** 열입니다.|  
  
## <a name="classes"></a>클래스  
 `My.Resources` 개체 공유 속성을 사용 하 여 클래스와 각 리소스 파일을 노출 합니다. 클래스 이름은 리소스 파일의 이름과 동일 합니다. 이전 섹션에서 설명한 대로, 리소스 파일의 리소스 클래스의 속성으로 노출 됩니다.  
  
## <a name="example"></a>예제  
 라는 문자열 리소스에는 폼의 제목을 설정 하는이 예제 `Form1Title` 응용 프로그램 리소스 파일에서입니다. 예제가 작동 하려면 응용 프로그램 이라는 문자열로 있어야 `Form1Title` 해당 리소스 파일에 있습니다.  
  
 [!code-vb[VbVbalrMyResources#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#1)]  
  
## <a name="example"></a>예제  
 이 예제에서는 명명 된 아이콘을 폼의 아이콘 설정 `Form1Icon` 는 응용 프로그램의 리소스 파일에 저장 됩니다. 예제가 작동 하려면 응용 프로그램 이라는 아이콘이 있어야 `Form1Icon` 해당 리소스 파일에 있습니다.  
  
 [!code-vb[VbVbalrMyResources#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#2)]  
  
## <a name="example"></a>예제  
 명명 된 이미지 리소스에는 폼의 배경 이미지를 설정 하는이 예제 `Form1Background`, 응용 프로그램 리소스 파일에 있습니다. 이 예제가 작동 하려면 응용 프로그램 명명 된 이미지 리소스 있어야 `Form1Background` 해당 리소스 파일에 있습니다.  
  
 [!code-vb[VbVbalrMyResources#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#3)]  
  
## <a name="example"></a>예제  
 이 예제에서는 명명 된 오디오 리소스로 저장 되는 소리를 재생 `Form1Greeting` 응용 프로그램의 리소스 파일입니다. 이 예제에서 응용 프로그램 이라는 오디오 리소스가 있어야 `Form1Greeting` 해당 리소스 파일에 있습니다. `My.Computer.Audio.Play` 방법은 Windows Forms 응용 프로그램에 대해서만 사용할 수 있습니다.  
  
 [!code-vb[VbVbalrMyResources#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#4)]  
  
## <a name="example"></a>예제  
 이 예제에서는 프랑스어 문화권 버전의 응용 프로그램의 문자열 리소스를 검색합니다. 리소스 이름은 `Message`합니다. 문화권을 변경 하는 합니다 `My.Resources` 개체를 사용 하 여 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>입니다.  
  
 이 예제가 작동 하려면 응용 프로그램 이라는 문자열로 있어야 `Message` 리소스 파일 및 응용 프로그램 있어야 Resources.fr-FR.resx, 해당 리소스 파일의 프랑스어 문화권 버전입니다. 응용 프로그램 리소스 파일의 프랑스어 문화권 버전이 없는 경우는 `My.Resource` 개체는 기본 문화권 리소스 파일에서 리소스를 검색 합니다.  
  
 [!code-vb[VbVbalrMyResources#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#10)]  
  
## <a name="see-also"></a>참고자료

- [애플리케이션 리소스 관리(.NET)](/visualstudio/ide/managing-application-resources-dotnet)
- [데스크톱 앱의 리소스](../../../framework/resources/index.md)
