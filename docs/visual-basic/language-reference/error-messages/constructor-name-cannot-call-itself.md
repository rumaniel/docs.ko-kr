---
title: "'<name>' 생성자는 자신을 호출할 수 없습니다."
ms.date: 07/20/2015
f1_keywords:
- bc30298
- vbc30298
helpviewer_keywords:
- BC30298
ms.assetid: 2d77b7f4-0640-4f89-9c65-f101fd2847c0
ms.openlocfilehash: 8459ee7fec6d761161a721c88ccdc88e513fc95f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61936697"
---
# <a name="constructor-name-cannot-call-itself"></a>생성자 '\<이름 >' 자신을 호출할 수 없습니다.
`Sub New` 클래스 또는 구조체에서 프로시저가 자신을 호출 합니다.  
  
 생성자의 목적은 클래스의 인스턴스를 초기화 하는 것 또는 첫 번째 경우 구조체를 생성 합니다. 클래스 또는 구조체는 다른 매개 변수 목록을 모두 제공 된 몇 가지 생성자에 있을 수 있습니다. 생성자는 자체 외에도 해당 기능을 수행 하는 다른 생성자를 호출 하도록 허용 됩니다. 자신을 호출 하는 생성자에 대 한 의미가 없습니다 있고 실제로 결과가 무한 재귀가 허용 합니다.  
  
 **오류 ID:** BC30298  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 호출할 생성자의 매개 변수 목록을 확인 합니다. 호출을 수행 하는 생성자에서 달라 야 합니다.  
  
2. 다른 생성자를 호출 하지 않을 경우 제거 된 `Sub New` 전적으로 호출 합니다.  
  
## <a name="see-also"></a>참고자료

- [개체 수명: 개체가 만들어지고 제거 하는 방법](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
