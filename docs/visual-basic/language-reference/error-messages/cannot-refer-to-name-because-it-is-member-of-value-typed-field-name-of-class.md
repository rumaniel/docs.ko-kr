---
title: "'<name>'은(는) 'System.MarshalByRefObject'를 기본 클래스로 사용하는 '<name>' 클래스의 값 형식 필드 '<classname>'의 멤버이므로 참조할 수 없습니다."
ms.date: 07/20/2015
f1_keywords:
- vbc30310
- bc30310
helpviewer_keywords:
- BC30310
ms.assetid: 2aeb8872-7c87-4f01-98ef-9714ba3eebbe
ms.openlocfilehash: 78b0a3131b6e77ed257f200523ecebd4dfce3691
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61649935"
---
# <a name="cannot-refer-to-name-because-it-is-a-member-of-the-value-typed-field-name-of-class-classname-which-has-systemmarshalbyrefobject-as-a-base-class"></a>참조할 수 없습니다. '\<이름 >' 값 형식 필드의 멤버 이기 때문에 '\<이름 >' 클래스의\<classname >'를 기본 클래스로 사용 되는 ' System.MarshalByRefObject'가
`System.MarshalByRefObject` 클래스를 사용 하면 응용 프로그램 도메인 경계를 넘어 개체에 대 한 원격 액세스를 지 원하는 응용 프로그램입니다. 형식에서 상속 해야 합니다는 `MarshalByRejectObject` 클래스 유형이 응용 프로그램 도메인 경계에 걸쳐 사용 됩니다. 개체의 멤버는 만든 응용 프로그램 도메인 외부에서 사용할 수 없기 때문에 개체의 상태는 복사 해야 합니다.  
  
 **오류 ID:** BC30310  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 에 참조 되는 멤버가 올바른지 확인에 대 한 참조를 확인 합니다.  
  
2. 멤버를 명시적으로 한정 된 `Me` 키워드입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.MarshalByRefObject>
- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
