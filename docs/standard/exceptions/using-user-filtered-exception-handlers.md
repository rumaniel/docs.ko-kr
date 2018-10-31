---
title: 사용자 필터 예외 처리기 사용
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- user-filtered exceptions
- exceptions, user-filtered
ms.assetid: aa80d155-060d-41b4-a636-1ceb424afee8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d1e771a95542153dfad0981d3198e6b4c31cdeb9
ms.sourcegitcommit: 700b9003ea6bdd83a53458bbc436c9b5778344f1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48261422"
---
# <a name="using-user-filtered-exception-handlers"></a>사용자 필터 예외 처리기 사용
현재 Visual Basic에서는 사용자 필터 예외를 지원합니다. 사용자 필터 예외 처리기는 예외에 대해 정의한 요구 사항을 기반으로 하여 예외를 catch하고 처리합니다. 이러한 처리기는 **Catch** 문을 **When** 키워드와 함께 사용합니다.  
  
 이 기법은 특정 예외 개체가 여러 오류에 해당하는 경우에 유용합니다. 이 경우 개체는 일반적으로 오류와 관련된 특정 오류 코드를 포함하는 속성을 갖습니다. 식에서 해당 오류 코드 속성을 사용하여 **Catch** 절에서 처리하려는 특정 오류만 선택할 수 있습니다.  
  
 다음 Visual Basic 예제에서는 **Catch/When** 문을 보여 줍니다.  
  
```  
Try  
      'Try statements.  
   Catch When Err = VBErr_ClassLoadException  
      'Catch statements.  
End Try  
```  
  
 사용자 필터 절의 식에는 어떤 제한도 적용되지 않습니다. 사용자 필터 식을 실행하는 중에 예외가 발생하면 예외는 무시되고 필터 식이 false로 계산된 것으로 간주됩니다. 이 경우 공용 언어 런타임은 현재 예외에 대한 처리기를 계속 검색합니다.  
  
## <a name="combining-the-specific-exception-and-the-user-filtered-clauses"></a>특정 예외 및 사용자 필터 절 조합  
 Catch 문은 특정 예외와 사용자 필터 절을 모두 포함할 수 있습니다. 런타임은 특정 예외를 먼저 테스트합니다. 특정 예외가 성공하면 런타임은 사용자 필터를 실행합니다. 일반 필터에는 클래스 필터에 선언된 변수에 대한 참조가 포함될 수 있습니다. 두 필터 절의 순서는 바꿀 수 없습니다.  
  
 다음 Visual Basic 예제에서는 **When** 키워드를 사용하는 사용자 필터 절 뿐만 아니라 **Catch** 문의 특정 예외 `ClassLoadException`을 보여 줍니다.  
  
```  
Try  
      'Try statements.  
   Catch cle As ClassLoadException When cle.IsRecoverable()  
      'Catch statements.  
End Try  
```  

## <a name="see-also"></a>참고 항목

- [예외](index.md)
