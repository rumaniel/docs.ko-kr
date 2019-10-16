---
title: 기타 데이터 형식(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Object data type [Visual Basic], data types
- data types [Visual Basic], choosing
ms.assetid: 64c71a12-9057-4dbf-baca-7379c4aada69
ms.openlocfilehash: 4808d87322d5b21b70ec38e2eb31b2b204938745
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62008243"
---
# <a name="miscellaneous-data-types-visual-basic"></a>기타 데이터 형식(Visual Basic)
Visual Basic에는 숫자나 문자 분류 되지 않는 몇 가지 데이터 형식을 제공 합니다. 대신는 특수화 된 데이터 처리와 같은 예/아니요 값, 날짜/시간 값 및 개체 주소 합니다.  
  
 Side-by-side-Visual Basic 데이터 형식 비교를 보여 주는 표를 참조 하세요 [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)합니다.  
  
## <a name="boolean-type"></a>부울 형식  
 합니다 [Boolean 데이터 형식](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) 로 해석 되는 부호 없는 값인 `True` 또는 `False`합니다. 데이터 너비를 구현 하는 플랫폼에 따라 달라 집니다. 변수를 포함할 수 있으면 true/false와 같은 두 가지 상태 값만 예/아니요 또는 설정/해제로 선언 `Boolean`합니다.  
  
## <a name="date-type"></a>날짜 형식  
 합니다 [날짜 데이터 형식](../../../../visual-basic/language-reference/data-types/date-data-type.md) 날짜와 시간 정보를 포함 하는 64 비트 값입니다. 각 증분은 일반 달력에서 1 년 1 월 1 일의 (오전 12시)부터 경과 된 시간의 100 나노초를 나타냅니다. 변수 값을 날짜, 시간 값 또는 둘 다를 포함할 수 있으면로 선언 `Date`합니다.  
  
## <a name="object-type"></a>개체 유형  
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md) 다른 응용 프로그램 또는 응용 프로그램 내에서 개체 인스턴스를 가리키는 32 비트 주소입니다. `Object` 변수는 응용 프로그램에서 인식 하는 모든 개체 또는 모든 데이터 형식의 데이터를 참조할 수 있습니다. 여기에 둘 다 *값 형식*와 같은 `Integer`, `Boolean`, 및 구조체 인스턴스 및 *형식을 참조*를 와같은클래스에서생성된개체의인스턴스는`String`고 <xref:System.Windows.Forms.Form>, 및 인스턴스를 배열 합니다.  
  
 변수는 컴파일 타임에 모르는 클래스의 인스턴스에 대 한 포인터를 저장, 다양 한 데이터 형식의 데이터를 가리키는로 선언 `Object`합니다.  
  
 이점은 `Object` 는 모든 데이터 형식의 데이터를 저장 하는 데 사용할 수 있습니다 데이터 형식입니다. 단점은 실행 시간이 더 느리게 수행 하는 응용 프로그램에 추가 작업을 발생 하는 것입니다. 사용 하는 경우는 `Object` 발생 값 형식에 대 한 변수를 *boxing* 하 고 *unboxing*합니다. 참조 형식에 대해 사용 하는 경우 사용자가 발생 시킨 *런타임에 바인딩*합니다.  
  
## <a name="see-also"></a>참고자료

- [형식 문자](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
- [기본 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)
- [숫자 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)
- [문자 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [초기 바인딩 및 런타임에 바인딩](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
