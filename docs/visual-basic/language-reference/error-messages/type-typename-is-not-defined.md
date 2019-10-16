---
title: "'<typename>' 형식이 정의되지 않았습니다."
ms.date: 07/20/2015
f1_keywords:
- vbc30002
- bc30002
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
ms.openlocfilehash: 1f66b86a61fb0344a449bf0aa46b7655813c7c30
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64664249"
---
# <a name="type-typename-is-not-defined"></a>형식 '\<typename >'가 정의 되지 않은
문에 정의 되지 않은 형식에 대 한 참조를 만들었습니다. 선언문의 형식 같은 정의 `Enum`, `Structure`를 `Class`, 또는 `Interface`합니다.  
  
 **오류 ID:** BC30002  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 형식 정 및 참조 모두 사용 하는 동일한 철자를 확인 합니다.  
  
- 형식 정의 참조에 액세스할 수 있는지 확인 합니다. 예를 들어, 형식이 다른 모듈에서 선언 된 경우 `Private`를 참조 하는 모듈로 형식 정의 이동 하거나 선언 `Public`합니다.  
  
- 형식의 네임 스페이스에 프로젝트 내에서 다시 정의 되지 않는지 확인 합니다. 인 경우 사용 된 `Global` 형식 이름을 정규화 하는 키워드입니다. 예를 들어 프로젝트 이름이 네임 스페이스를 정의 하는 경우 `System`는 <xref:System.Object?displayProperty=nameWithType> 사용 하 여 정규화 하지 않은 형식에 액세스할 수 없습니다는 `Global` 키워드: `Global.System.Object`합니다.  
  
- 형식 정의 되었지만 Visual Basic을 사용 하면 클릭에 정의 된 형식 라이브러리를 개체 라이브러리를 등록 하지 않은 경우 **참조 추가** 에 **프로젝트** 메뉴를 선택한 후 적절 한 개체 라이브러리 또는 형식 라이브러리입니다.  
  
- 대상된.NET 프레임 워크 프로필의 일부인 어셈블리의 형식 인지 확인 합니다. 자세한 내용은 [.NET Framework 대상 지정 오류 문제 해결](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
- [프로젝트의 참조 관리](/visualstudio/ide/managing-references-in-a-project)
