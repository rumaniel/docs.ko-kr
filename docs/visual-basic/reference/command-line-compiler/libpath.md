---
title: -libpath
ms.date: 03/10/2018
helpviewer_keywords:
- libpath compiler option [Visual Basic]
- /libpath compiler option [Visual Basic]
- -libpath compiler option [Visual Basic]
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
ms.openlocfilehash: d713a63c9503581f38048fe79c559883dc96efd2
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50202974"
---
# <a name="-libpath"></a>-libpath
참조 된 어셈블리의 위치를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-libpath:dirList  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`dirList`|필수. 컴파일러가 참조 된 어셈블리에서에서 찾는 대 한 디렉터리의 세미콜론으로 구분 된 목록에 없는 하나는 현재 작업 디렉터리 (컴파일러를 호출 하는 디렉터리) 또는 공용 언어 런타임의 시스템 디렉터리입니다. 디렉터리 이름에 공백이 있으면 이름을 따옴표로 묶습니다 ("").|  
  
## <a name="remarks"></a>설명  
 합니다 `-libpath` 옵션에서 참조 어셈블리의 위치를 지정 합니다 [-참조](../../../visual-basic/reference/command-line-compiler/reference.md) 옵션입니다.  
  
 컴파일러는 정규화되지 않은 어셈블리 참조를 다음 순서대로 검색합니다.  
  
1.  현재 작업 디렉터리입니다. 컴파일러가 호출되는 디렉터리입니다.  
  
2.  공용 언어 런타임 시스템 디렉터리입니다.  
  
3.  지정 된 디렉터리 `/libpath`합니다.  
  
4.  LIB 환경 변수로 지정된 디렉터리입니다.  
  
 `-libpath` 가산적; 지정 옵션은 이전 값에 추가 되 면 보다 더 많은 것입니다.  
  
 사용 하 여 `-reference` 어셈블리 참조를 지정 합니다.  
  
|Visual Studio에서 /libpath를 설정 하려면 통합 개발 환경|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **참조** 탭을 클릭합니다.<br />3.  클릭 된 **경로 참조 하는 중...**  단추입니다.<br />4.  에 **참조 경로** 대화 상자에서 디렉터리 이름을 입력 합니다 합니다 **폴더:** 상자입니다.<br />5.  클릭 **폴더 추가**합니다.|  
  
## <a name="example"></a>예제  
 다음 코드에서는 `T2.vb` .exe 파일을 만듭니다. 컴파일러는 어셈블리 참조에 대 한 작업 디렉터리, c: 드라이브의 루트 디렉터리 및 c: 드라이브의 새 어셈블리 디렉터리를 찾습니다.  
  
```console  
vbc -libpath:c:\;"c:\New Assemblies" -reference:t2.dll t2.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [어셈블리 및 전역 어셈블리 캐시](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
