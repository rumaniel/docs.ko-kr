---
title: "'<typename>'은(는) 대리자 형식입니다."
ms.date: 07/20/2015
f1_keywords:
- bc32008
- vbc32008
helpviewer_keywords:
- BC32008
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
ms.openlocfilehash: 45dc0403468fa40888a6c5e6bdfe6ca782e98325
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64664186"
---
# <a name="typename-is-a-delegate-type"></a>'\<typename >' 대리자 형식이
'\<typename >' 대리자 형식이 있습니다. 인수 목록으로 단일 AddressOf 식만 허용 하는 대리자 생성 합니다. 종종 AddressOf 식은 대리자 구문 대신 사용할 수 있습니다.  
  
 `New` 대리자 클래스의 인스턴스를 만들고 절 대리자 생성자에는 잘못 된 인수 목록을 제공 합니다.  
  
 하나만 제공할 수 있습니다 `AddressOf` 새 대리자 인스턴스를 만들 때 식입니다.  
  
 전달 하지 않으면 모든 인수 대리자 생성자에는 잘못 된 단일 인수를 전달 하는 경우 또는 둘 이상의 인수를 전달 하는 경우이 오류가 발생할 수 있습니다 `AddressOf` 식입니다.  
  
 **오류 ID:** BC32008  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 단일을 사용 하 여 `AddressOf` 대리자 클래스에 대 한 인수 목록에 있는 식의 `New` 절.  
  
## <a name="see-also"></a>참고자료

- [New 연산자](../../../visual-basic/language-reference/operators/new-operator.md)
- [AddressOf 연산자](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [대리자](../../../visual-basic/programming-guide/language-features/delegates/index.md)
- [방법: 대리자 메서드 호출](../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
