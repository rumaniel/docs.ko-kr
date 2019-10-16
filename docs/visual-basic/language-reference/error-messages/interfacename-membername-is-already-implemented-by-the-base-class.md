---
title: "'<interfacename>. <membername>'은 이미 구현 된 기본 클래스에 의해'<baseclassname>'. 다시 구현 <type> 가정"
ms.date: 07/20/2015
f1_keywords:
- vbc42015
- bc42015
helpviewer_keywords:
- BC42015
ms.assetid: 658c070a-113e-4bd8-b294-12c243191160
ms.openlocfilehash: 5943eff5fa7e68da9905e3e589eea264c06943c1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593312"
---
# <a name="interfacenamemembername-is-already-implemented-by-the-base-class-baseclassname-re-implementation-of-type-assumed"></a>'\<interfacename >. \<membername >'는 기본 클래스 의해 이미 구현\<baseclassname >'입니다. 다시 구현 \<유형 > 가정
속성, 프로시저 또는 파생된 클래스에서 이벤트를 사용 하는 `Implements` 절을 이미 기본 클래스에서 구현 된 인터페이스 멤버를 지정 합니다.  
  
 파생 클래스는 기본 클래스에 의해 구현된 인터페이스 멤버를 다시 구현할 수 있습니다. 이는 기본 클래스 구현 재정의와 다릅니다. 자세한 내용은 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md)을 참조하세요.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42015  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 인터페이스 멤버를 다시 구현하려는 경우 어떤 조치도 취할 필요가 없습니다. 사용 하지 않는 경우 파생된 클래스의 코드가 다시 구현 된 멤버에 액세스 합니다 `MyBase` 키워드를 기본 클래스 구현에 액세스 합니다.  
  
- 인터페이스 멤버를 다시 구현하지 않으려는 경우 속성, 프로시저 또는 이벤트 선언에서 `Implements` 절을 제거합니다.  
  
## <a name="see-also"></a>참고자료

- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
