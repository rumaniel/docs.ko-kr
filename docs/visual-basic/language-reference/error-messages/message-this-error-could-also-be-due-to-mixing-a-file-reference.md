---
title: <message> 이 오류는 어셈블리에 대 한 프로젝트 참조를 사용 하는 파일 참조가 섞여 수도 있습니다 '<assemblyname>'
ms.date: 07/20/2015
f1_keywords:
- bc30971
- vbc30971
helpviewer_keywords:
- BC30971
ms.assetid: 75d2e8b5-2fdc-4623-8b32-cba805dab7db
ms.openlocfilehash: 951f90a9209ff31896f4426ceb75f05b012897a6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921019"
---
# <a name="message-this-error-could-also-be-due-to-mixing-a-file-reference-with-a-project-reference-to-assembly-assemblyname"></a>\<메시지 > 참조 어셈블리에 대 한 프로젝트 참조를 사용 하 여 파일 참조가 섞여 있기 때문에이 오류도 수 '\<assemblyname >'
\<메시지 > 참조 어셈블리에 대 한 프로젝트 참조를 사용 하 여 파일 참조가 섞여 있기 때문에이 오류도 수 '\<assemblyname >. 이 경우에 대 한 파일 참조를 교체를 시도 '\<assemblyfilename >' 프로젝트에서 '\<projectname1 >'에 대 한 프로젝트 참조를 사용 하 여 '\<projectname2 >'입니다.  
  
 코드 프로젝트에서 다른 프로젝트의 멤버에 액세스할 수 있지만 솔루션의 구성 참조를 해결 하려면 Visual Basic 컴파일러를 허용 하지 않습니다.  
  
 다른 어셈블리에 정의 된 형식에 액세스 하려면 해당 어셈블리에 대 한 참조를 Visual Basic 컴파일러에 있어야 합니다. 이 참조는 프로젝트 간의 순환 참조를 발생시키지 않는 명확한 단일 참조여야 합니다.  
  
 **오류 ID:** BC30971  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 참조할 프로젝트에 가장 적합한 어셈블리를 생성하는 프로젝트를 결정합니다. 이러한 결정을 위해 파일 접근성 및 업데이트 빈도 등의 조건을 사용할 수 있습니다.  
  
2. 프로젝트 속성에서 사용 중인 형식을 정의하는 어셈블리가 포함된 프로젝트에 대한 참조를 추가합니다.  
  
## <a name="see-also"></a>참고자료

- [프로젝트의 참조 관리](/visualstudio/ide/managing-references-in-a-project)
- [선언된 요소 참조](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)

- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
- [끊어진 참조 문제 해결](/visualstudio/ide/troubleshooting-broken-references)
