---
title: Visual Basic 제한 사항
ms.date: 07/20/2015
helpviewer_keywords:
- limits
- limitations [Visual Basic]
- limitations
- limits, Visual Basic code
- Visual Basic code, limitations
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
ms.openlocfilehash: 9fa0844f4508906ae30b936e41fb4392b74d1437
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648728"
---
# <a name="visual-basic-limitations"></a>Visual Basic 제한 사항
이전 버전의 Visual Basic 코드에서 변수 이름, 모듈 및 모듈 크기에 허용 되는 변수의 수의 길이 같은 경계를 적용 합니다. Visual Basic.net에서는 이러한 제한은 완화 되었습니다, 큰 자유롭게 쓰고 정렬 코드를 제공 합니다.  
  
 물리적 제한은 종속 런타임 메모리 보다 더 컴파일 시간 고려 사항입니다. 신중한 프로그래밍 사례를 사용 하 고 여러 클래스와 모듈 큰 응용 프로그램을 나누는 경우에 내부 Visual Basic 제한 사항이 발생할 확률이 거의 없습니다.  
  
 다음은 극단적인 경우에 발생할 수 있는 몇 가지 제한 사항입니다.  
  
- **이름 길이입니다.** 모든 선언 된 프로그래밍 요소의 이름에 대 한 문자의 최대 수가입니다. 이 최대 요소 이름이 정규화 된 경우 전체 한정 문자열에 적용 됩니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.  
  
- **Line Length.** 실제 소스 코드 줄에서 65535 자가 있습니다. 논리 소스 코드 줄은 줄 연속 문자를 사용 하는 경우에 길어질 수 있습니다. [방법: 코드에서 문 분리 및 결합](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)합니다.  
  
- **배열 차원이 있습니다.** 배열에 선언할 수 있는 차원의 최대 수가입니다. 이 배열 요소를 지정 하 여 인덱스 수를 제한 합니다. 참조 [Array Dimensions in Visual Basic](../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md)합니다.  
  
- **문자열 길이입니다.** 단일 문자열에 저장할 수 있습니다 하는 유니코드 문자의 최대 수가입니다. 참조 [문자열 데이터 형식](../../../visual-basic/language-reference/data-types/string-data-type.md)합니다.  
  
- **환경 문자열 길이입니다.** 명령줄 인수를 받았던 환경 문자열의 32768 자의 있습니다. 모든 플랫폼에서 제한 됩니다.  
  
## <a name="see-also"></a>참고자료

- [프로그램 구조 및 코드 규칙](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [Visual Basic 명명 규칙](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
