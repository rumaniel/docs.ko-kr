---
title: 선언된 XML 요소 및 특성의 이름(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [XML in Visual Basic]
- element names [XML in Visual Basic]
- names in XML literals [Visual Basic]
- attribute names [XML in Visual Basic]
- XML literals [Visual Basic], element names
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
ms.openlocfilehash: dbe85b456f46c40c9cc9a703b38e11992edd24cf
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64598274"
---
# <a name="names-of-declared-xml-elements-and-attributes-visual-basic"></a>선언된 XML 요소 및 특성의 이름(Visual Basic)
이 항목에서는 XML 요소 및 XML 리터럴의 특성 이름을 지정 하는 것에 대 한 Visual Basic 지침을 제공 합니다.  Xml 리터럴, 로컬 이름 또는 정규화 된 이름을 지정할 수 있습니다. 정규화 된 이름은 XML 네임 스페이스 접두사, 콜론 및 로컬 이름으로 구성 됩니다. XML 네임 스페이스 접두사에 대 한 자세한 내용은 참조 하세요. [XML 요소 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)합니다.  
  
## <a name="rules"></a>규칙  
 요소 또는 Visual Basic의 특성의 로컬 이름은 다음 규칙을 준수 해야 합니다.  
  
- 네임 스페이스를 사용 하 여 시작할 수 있습니다. 알파벳 문자 또는 밑줄로 시작 해야 합니다 (`_`).  
  
- 영문자, 10 진수 숫자, 밑줄, 마침표 (.) 및 하이픈만 포함 해야 합니다 (-).  
  
- 1,024 자 아니어야 합니다.  
  
- 이름에 표시 되는 콜론 네임 스페이스 구분을 나타냅니다. 따라서 특정 이름에 대 한 XML 네임 스페이스를 지정 하기 위해서만 콜론을 사용할 수 있습니다.  
  
 또한 다음 지침을 준수 해야 합니다.  
  
- XML 1.0 사양에는 문자열의 대/소문자 변형 "xml"로 시작 하는 모든 이름을 예약 합니다. 따라서 이러한 요소에 대 한 이름 및 특성 이름을 사용 하지 마십시오.  
  
### <a name="name-length-guidelines"></a>이름 길이 지침  
 실제 문제로 명확히 요소의 특성을 식별 하는 동안는 이름은 가능한 한 짧은 것 이어야 합니다. 이 코드의 가독성을 향상 시키고 줄 길이 및 소스 파일 크기를 줄입니다.  
  
 그러나 프로그램 이름은 너무 짧아서는 설명 하지는 않습니다 적절 하 게 요소 또는 코드 방식을 사용 해야 합니다. 이 코드의 가독성을 위해 중요 합니다. 이해를 시도 하는 다른 사람에 게, 직접 살펴보면이 작성 한 후 오랫동안 적절 한 요소 이름을 시간을 절약할 수 있습니다.  
  
## <a name="case-sensitivity-in-names"></a>이름에서 대/소문자 구분  
 XML 요소 이름은 대/소문자를 구분 합니다. 이 Visual Basic 컴파일러는 알파벳 소문자만 다른 두 이름을 비교, 해석 다른 이름으로 의미 합니다. 예를 들어, 해석 `ABC` 및 `abc` 으로 요소를 구분 합니다.  
  
## <a name="xml-namespaces"></a>XML 네임스페이스  
 XML 요소 리터럴를 만들 때 요소 이름에 대 한 XML 네임 스페이스 접두사를 지정할 수 있습니다. 자세한 내용은 [XML 요소 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic에서 XML 만들기](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [XML 요소 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
