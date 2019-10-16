---
title: 이니셜라이저가 필요합니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30996
- bc30996
helpviewer_keywords:
- BC30996
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
ms.openlocfilehash: 0795fdc1c4b177e13979d7555cd7588217b8cb4c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013805"
---
# <a name="initializer-expected"></a>이니셜라이저가 필요합니다.
초기화 목록의 비어 있는 경우 다음 예제에서와 같이 개체 이니셜라이저를 사용 하 여 클래스의 인스턴스를 선언 하려고 했습니다.  
  
 `' Not valid.`  
  
 `' Dim aStudent As New Student With {}`  
  
 다음 예제에서와 같이 이니셜라이저 목록에서 하나 이상의 필드 또는 속성 초기화 되어야 합니다.  
  
 `Dim aStudent As New Student With {.year = "Senior"}`  
  
 **오류 ID:** BC30996  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 하나 이상의 필드 또는 속성 이니셜라이저에서을 초기화 하 하거나 개체 이니셜라이저를 사용 하지 마십시오.  
  
## <a name="see-also"></a>참고자료

- [개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [방법: 개체 이니셜라이저를 사용 하 여 개체 선언](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
