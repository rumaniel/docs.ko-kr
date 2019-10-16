---
title: '방법: 만들기는 컬렉션 이니셜라이저 (Visual Basic)를 사용 하는 확장 메서드를 추가 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- collection initializers [Visual Basic]
ms.assetid: f64b52c7-8b11-4410-93a6-cb3aeebcc772
ms.openlocfilehash: a5af41e25b8f82aa173e2df28cc41b313c8d68dd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61907077"
---
# <a name="how-to-create-an-add-extension-method-used-by-a-collection-initializer-visual-basic"></a>방법: 만들기는 컬렉션 이니셜라이저 (Visual Basic)를 사용 하는 확장 메서드를 추가 합니다.
Visual Basic 컴파일러에 대 한 검색 컬렉션 이니셜라이저를 사용 하 여 컬렉션을 만드는 경우는 `Add` 는 컬렉션 형식의 메서드 매개 변수는 `Add` 컬렉션 이니셜라이저의 값의 형식과 일치 하는 메서드. 이 `Add` 메서드 컬렉션을 컬렉션 이니셜라이저의 값으로 채우는 데 사용 됩니다.  
  
 일치 하는 경우 `Add` 메서드 및 컬렉션에 대 한 코드를 수정할 수 없습니다, 확장 메서드를 추가할 수 있습니다 `Add` 컬렉션 이니셜라이저에 필요한 매개 변수를 사용 하는 합니다. 일반적으로 이것이 컬렉션 이니셜라이저를 사용 하 여 제네릭 컬렉션 용 때 수행할 작업을 해야 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 제네릭 확장 메서드를 추가 하는 방법을 보여 줍니다 <xref:System.Collections.Generic.List%601> 형식의 개체를 추가할 컬렉션 이니셜라이저를 사용할 수 있도록 입력 `Employee`합니다. 확장 메서드를 사용 하면 축약된 컬렉션 이니셜라이저 구문을 사용할 수 있습니다.  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo1/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo1/VB/Module1.vb#2)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo1/VB/Module1.vb#3)]  
  
## <a name="see-also"></a>참고자료

- [컬렉션 이니셜라이저](../../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)
- [방법: 컬렉션 이니셜라이저에서 사용 되는 컬렉션 만들기](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)
