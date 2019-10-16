---
title: "'<typename1>' 형식의 값을 '<typename2>'(으)로 변환할 수 없습니다.(여러 파일 참조)"
ms.date: 07/20/2015
f1_keywords:
- vbc30961
- bc30961
helpviewer_keywords:
- BC30961
ms.assetid: 8be5aa0d-d236-4ac3-aa9c-5044f9f6562b
ms.openlocfilehash: 7371cbd4fef4abced95744071ff222b40e160e3e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64620318"
---
# <a name="value-of-type-typename1-cannot-be-converted-to-typename2-multiple-file-references"></a>형식의 값 '\<typename1 >'로 변환할 수 없습니다 '\<typename2 >' (여러 파일 참조)
형식의 값 '\<typename1 >'로 변환할 수 없습니다 '\<typename2 >'입니다. 형식 불일치에 대 한 파일 참조가 섞여 때문일 수 있습니다 '\<filepath1 >' 프로젝트에서 '\<projectname1 >'에 대 한 파일 참조를 사용 하 여 '\<filepath2 >' 프로젝트에서 '\<projectname2 >'입니다. 두 어셈블리가 동일하면 동일한 대상을 참조하도록 두 참조를 바꿔 보세요.  
  
 프로젝트의 어셈블리에 둘 이상의 파일 참조는 있는 경우에서 컴파일러는 형식 간에 변환할 수는 보장할 수 없습니다.  
  
 각 파일 참조 (일반적으로 DLL 파일) 프로젝트의 출력 파일 이름과 파일 경로 지정합니다. 컴파일러는 동일한 소스에서 출력 파일 지거나 동일한 어셈블리의 동일한 버전을 표시 하는 보장할 수 없습니다. 따라서 다른 참조의 형식은 동일한 형식 또는 다른 하나의 변환할 수는 보장할 수 없습니다.  
  
 참조 된 어셈블리는 동일한 어셈블리 id를 알고 있는 경우 단일 파일 참조를 사용할 수 있습니다. *어셈블리 ID* 에는 어셈블리 이름, 버전, 공개 키(있는 경우) 및 문화권이 포함됩니다. 이 정보는 어셈블리를 고유하게 식별합니다.  
  
 **오류 ID:** BC30961  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 참조 된 어셈블리에서 동일한 어셈블리 id에 있는 경우 제거 하거나 단일 파일 참조만 되도록 파일 참조 중 하나를 대체 합니다.  
  
- 참조 된 어셈블리는 동일한 어셈블리 id에 없는 경우 형식에서 다른 형식으로 변환 하려고 하지 않도록 코드를 변경 합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 형식 변환](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [프로젝트의 참조 관리](/visualstudio/ide/managing-references-in-a-project)
