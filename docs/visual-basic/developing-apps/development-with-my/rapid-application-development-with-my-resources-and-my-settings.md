---
title: My.Resources 및 My.Settings를 사용한 신속한 애플리케이션 개발(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My.Settings object [Visual Basic], developing applications
- rapid application development (RAD), My.Resources
- rapid application development (RAD), My.Settings
- My.Resources object [Visual Basic], developing applications
ms.assetid: 68284ab1-b685-4814-a2a4-01ae40445ff8
ms.openlocfilehash: 4a9021af23200323397cc49fa1a44a0cc48b5a1d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62014442"
---
# <a name="rapid-application-development-with-myresources-and-mysettings-visual-basic"></a>My.Resources 및 My.Settings를 사용한 신속한 애플리케이션 개발(Visual Basic)
`My.Resources` 개체 응용 프로그램의 리소스에 대 한 액세스를 제공 하며, 응용 프로그램에 대 한 리소스를 동적으로 검색할 수 있습니다.  
  
## <a name="retrieving-resources"></a>리소스 검색  
 다양 한 오디오 파일, 아이콘, 이미지 및 문자열 같은 리소스를 통해 검색할 수 있습니다는 `My.Resources` 개체입니다. 예를 들어, 응용 프로그램의 문화권 관련 리소스 파일을 액세스할 수 있습니다. 다음 예제에서는 명명 된 아이콘을 폼의 아이콘 설정 `Form1Icon` 응용 프로그램의 리소스 파일에 저장 합니다.  
  
 [!code-vb[VbVbcnMy#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#7)]  
  
 `My.Resources` 개체는 전역 리소스만 노출 합니다. 폼과 관련 된 리소스 파일에 대 한 액세스를 제공 하지 않습니다. 폼에서 폼 리소스에 액세스 해야 합니다.  
  
 마찬가지로,는 `My.Settings` 개체 응용 프로그램의 설정에 대 한 액세스를 제공 하 고 동적으로 저장 하 고 속성 설정 및 응용 프로그램에 대 한 다른 정보를 검색할 수 있습니다. 자세한 내용은 [My.Resources 개체](../../../visual-basic/language-reference/objects/my-resources-object.md) 하 고 [My.Settings 개체](../../../visual-basic/language-reference/objects/my-settings-object.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [My.Resources 개체](../../../visual-basic/language-reference/objects/my-resources-object.md)
- [My.Settings 개체](../../../visual-basic/language-reference/objects/my-settings-object.md)
- [응용 프로그램 설정 액세스](../../../visual-basic/developing-apps/programming/app-settings/index.md)
