---
title: 런타임에 바인딩을 확인합니다. 런타임 오류가 발생할 수 있습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc42017
- BC42017
helpviewer_keywords:
- BC42017
ms.assetid: 45f552c8-57c6-44c0-97d3-e510119b257a
ms.openlocfilehash: 6b78dfed1d615ba865f136365eac1c9c131ed5a5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661945"
---
# <a name="late-bound-resolution-runtime-errors-could-occur"></a>런타임에 바인딩을 확인합니다. 런타임 오류가 발생할 수 있습니다.
개체가 되도록 선언 된 변수에 할당 되는 [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md)합니다.  
  
 변수를 선언 하는 경우 `Object`, 컴파일러에서 수행 해야 *런타임에 바인딩*, 런타임에 추가 작업이 필요 하면 합니다. 또한 애플리케이션이 잠재적인 런타임 오류에 노출됩니다. 예를 들어, 할당 하는 경우를 <xref:System.Windows.Forms.Form> 에 `Object` 변수 및 액세스를 <xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=nameWithType> 속성인 런타임에서 throw를 <xref:System.MemberAccessException> 때문에 <xref:System.Windows.Forms.Form> 클래스를 노출 하지 않습니다는 `NameTable` 속성.  
  
 특정 형식으로 변수를 선언할 경우 컴파일러 수행할 수 있습니다 *초기 바인딩* 컴파일 타임에 있습니다. 이 인해 성능 향상된, 코드의 가독성을 높이기 및 특정 형식의 멤버에 액세스를 제어 합니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42017  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 가능한 경우 특정 유형의 변수를 선언 합니다.  
  
## <a name="see-also"></a>참고자료

- [초기 바인딩 및 런타임에 바인딩](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
- [개체 변수 선언](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
