---
title: "'<structurename>' 구조체에는 'Custom'으로 표시되지 않은 적어도 하나의 인스턴스 멤버 변수 또는 이벤트 선언이 있어야 합니다."
ms.date: 07/20/2015
f1_keywords:
- bc30941
- vbc30941
helpviewer_keywords:
- BC30941
ms.assetid: 7054cc1e-bac3-4c3d-82f3-35772bd8dd3b
ms.openlocfilehash: 4ce24073896326bb5a68e563e2d34aafa09ef1c1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593213"
---
# <a name="structure-structurename-must-contain-at-least-one-instance-member-variable-or-at-least-one-instance-event-declaration-not-marked-custom"></a>구조 '\<structurename >' 하나 이상의 인스턴스 멤버 변수 또는 'Custom' 표시 되지 않은 인스턴스를 하나 이상 이벤트 선언이 있어야
구조체 정의 비공유 변수 또는 비공유 비 사용자 정의 이벤트 포함 되지 않습니다.  
  
 모든 구조체는 변수 또는 모든 인스턴스에 (비공유) 대신 특정 인스턴스의 전체적으로 적용 되는 이벤트 해야 합니다. ([공유](../../../visual-basic/language-reference/modifiers/shared.md)). 비공유 상수, 속성 및 절차가 요구이 사항을 충족 하지 않습니다. 또한 비공유 변수가 없고 하나의 비공유 이벤트가 없으면 이벤트 일 수 없습니다는 `Custom` 이벤트입니다.  
  
 **오류 ID:** BC30941  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 하나 이상의 변수 또는 없는 이벤트를 정의 `Shared`합니다. 하나의 이벤트를 정의 하는 경우 사용자와 공유 되지 않는 이어야 합니다.  
  
## <a name="see-also"></a>참고자료

- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [방법: 구조 선언](../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
