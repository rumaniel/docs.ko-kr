---
title: 기본 속성 '<propertyname1>'은(는) '<propertyname2>'의 기본 속성 '<classname>'과(와) 충돌하므로 'Shadows'로 선언해야 합니다.
ms.date: 07/20/2015
f1_keywords:
- vbc40007
- bc40007
helpviewer_keywords:
- BC40007
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
ms.openlocfilehash: c964003217e7b96cf25288e2ae6ae6a2fb07a6c3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651385"
---
# <a name="default-property-propertyname1-conflicts-with-default-property-propertyname2-in-classname-and-so-should-be-declared-shadows"></a>기본 속성 '\<propertyname1 >' 기본 속성과 충돌 '\<propertyname2 >'에서 '\<classname >' h'로 선언 해야 하므로
기본 클래스에 정의 된 속성과 동일한 이름을 가진 속성이 선언 됩니다. 이 이런 경우이 클래스의 속성이 기본 클래스 속성을 숨겨야 합니다.  
  
 이 메시지는 경고입니다. 기본적으로`Shadows` 로 간주됩니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC40007  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 추가 된 `Shadows` 속성의 이름을 선언 되는 선언 또는 변경 하는 키워드입니다.  
  
## <a name="see-also"></a>참고자료

- [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)
- [Visual Basic의 숨김 기능](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
