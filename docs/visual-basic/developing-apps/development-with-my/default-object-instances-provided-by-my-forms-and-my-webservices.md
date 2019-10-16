---
title: My.Forms 및 My.WebServices에서 제공하는 기본 개체 인스턴스(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My.WebServices object [Visual Basic], developing applications
- My.Forms object [Visual Basic], developing applications
- rapid application development (RAD), My.Forms
- rapid application development (RAD), My.WebServices
ms.assetid: de930027-9108-4f0c-b97c-5e7db4d6ef79
ms.openlocfilehash: ca31e1c40c77bf7f42d246019d81f4ffaed646e8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62014455"
---
# <a name="default-object-instances-provided-by-myforms-and-mywebservices-visual-basic"></a>My.Forms 및 My.WebServices에서 제공하는 기본 개체 인스턴스(Visual Basic)
합니다 [My.Forms](../../../visual-basic/language-reference/objects/my-forms-object.md) 하 고 [My.WebServices](../../../visual-basic/language-reference/objects/my-webservices-object.md) 개체 폼, 데이터 원본 및 응용 프로그램에서 사용 하는 XML Web services에 대 한 액세스를 제공 합니다. 컬렉션을 제공 하 여 이렇게 *인스턴스를 기본* 이러한 각 개체의 합니다.  
  
## <a name="default-instances"></a>기본 인스턴스  
 기본 인스턴스가 될 필요가 없습니다 런타임에서 제공 하는 클래스의 인스턴스를 선언 하 고 사용 하 여 인스턴스화할 합니다 `Dim` 및 `New` 문. 다음 예제에서는 어떻게 하면 선언 하 고 인스턴스를 인스턴스화할를 <xref:System.Windows.Forms.Form> 라는 클래스 `Form1`, 어떻게 되 고 이제 수의 기본 인스턴스를 가져오는 <xref:System.Windows.Forms.Form> 클래스를 통해 `My.Forms`합니다.  
  
 [!code-vb[VbVbcnMy#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#5)]  
  
 [!code-vb[VbVbcnMy#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#6)]  
  
 합니다 `My.Forms` 개체에 대 한 기본 인스턴스의 컬렉션을 반환 합니다. 모든 `Form` 프로젝트에 있는 클래스입니다. 마찬가지로, `My.WebServices` 만들었다고에 대 한 참조 응용 프로그램에서 모든 웹 서비스에 대 한 프록시 클래스의 기본 인스턴스를 제공 합니다.  
  
## <a name="see-also"></a>참고자료

- [My.Forms 개체](../../../visual-basic/language-reference/objects/my-forms-object.md)
- [My.WebServices 개체](../../../visual-basic/language-reference/objects/my-webservices-object.md)
- [My가 프로젝트 형식에 의존하는 방식](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)
