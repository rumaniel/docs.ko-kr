---
title: 이 'Sub New'의 첫째 문은 'MyBase.New' 또는 'MyClass.New'에 대한 호출이어야 합니다(매개 변수가 없는 액세스할 수 있는 생성자가 없음).
ms.date: 07/20/2015
f1_keywords:
- bc30148
- vbc30148
helpviewer_keywords:
- BC30148
ms.assetid: 4426e8fc-cb39-4eb8-ba95-503cd32fcc89
ms.openlocfilehash: 160e4d512a1533b3c89a1af50b47600ca6df51c2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592051"
---
# <a name="first-statement-of-this-sub-new-must-be-a-call-to-mybasenew-or-myclassnew-no-accessible-constructor-without-parameters"></a>이 'Sub New'의 첫째 문은 'MyBase.New' 또는 'MyClass.New'에 대한 호출이어야 합니다(매개 변수가 없는 액세스할 수 있는 생성자가 없음).
때문에이 ' Sub n e '의 첫째 문은 'MyBase.New' 또는 'm y'에 대 한 호출 이어야 합니다 기본 클래스\<basename >'의 '\<derivedname >' 인수 없이 호출할 수 있는 액세스 가능한 ' Sub n이 없습니다.  
  
 모든 생성자는 파생된 클래스에서 기본 클래스 생성자를 호출 해야 합니다 (`MyBase.New`). 기본 클래스에 파생된 클래스에 액세스할 수 있는 매개 변수가 없는 생성자가 하는 경우 `MyBase.New` 자동으로 호출할 수 있습니다. 그렇지 않은 경우 매개 변수를 사용 하 여 기본 클래스 생성자를 호출 해야 하 고 자동으로 수행할 수 없습니다. 이 경우 모든 파생된 클래스 생성자의 첫 번째 문 기본 클래스에서 매개 변수화 된 생성자를 호출 하거나 기본 클래스 생성자를 호출 하는 파생된 클래스의 다른 생성자를 호출 해야 합니다.  
  
 **오류 ID:** BC30148  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 호출 `MyBase.New` 필수 매개 변수를 제공 하거나 이러한 호출 피어 생성자를 호출 합니다.  
  
     예를 들어, 기본 클래스에 생성자로 선언 된 경우 `Public Sub New(ByVal index as Integer)`, 파생의 첫째 문은 클래스 생성자 않을 `MyBase.New(100)`합니다.  
  
## <a name="see-also"></a>참고자료

- [상속 기본 사항](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
