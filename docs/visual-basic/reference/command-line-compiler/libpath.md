---
title: -libpath
ms.date: 03/10/2018
helpviewer_keywords:
- libpath compiler option [Visual Basic]
- /libpath compiler option [Visual Basic]
- -libpath compiler option [Visual Basic]
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
ms.openlocfilehash: 8f4e415576562885c9edbd3d2dddbe2a271e9923
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005459"
---
# <a name="-libpath"></a>-libpath
참조 된 어셈블리의 위치를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-libpath:dirList  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`dirList`|필수. 컴파일러가 참조 된 어셈블리를 현재 작업 디렉터리 (컴파일러를 호출 하 고 있는 디렉터리) 또는 공용 언어 런타임의 시스템 디렉터리에서 찾을 수 없는 경우 조회할 세미콜론으로 구분 된 디렉터리 목록입니다. 디렉터리 이름에 공백이 포함 된 경우 이름을 큰따옴표 ("")로 묶습니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 옵션은 [-reference](../../../visual-basic/reference/command-line-compiler/reference.md) 옵션에서 참조 하는 어셈블리의 위치를 지정 합니다.  
  
 컴파일러는 정규화되지 않은 어셈블리 참조를 다음 순서대로 검색합니다.  
  
1. 현재 작업 디렉터리입니다. 컴파일러가 호출되는 디렉터리입니다.  
  
2. 공용 언어 런타임 시스템 디렉터리입니다.  
  
3. @No__t로 지정 된 디렉터리-0.  
  
4. LIB 환경 변수로 지정된 디렉터리입니다.  
  
 @No__t-0 옵션은 가감 연산자입니다. 두 번 이상 지정 하면 이전 값에 추가 됩니다.  
  
 @No__t-0을 사용 하 여 어셈블리 참조를 지정 합니다.  
  
|Visual Studio 통합 개발 환경에서/libpath를 설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **참조** 탭을 클릭합니다.<br />3.  **참조 경로 ...** 단추를 클릭 합니다.<br />4.  **참조 경로** 대화 상자에서 **폴더:** 상자에 디렉터리 이름을 입력 합니다.<br />5.  **폴더 추가**를 클릭 합니다.|  
  
## <a name="example"></a>예제  
 다음 코드는 `T2.vb`을 컴파일하여 .exe 파일을 만듭니다. 컴파일러는 C: 드라이브의 루트 디렉터리와 어셈블리 참조를 위한 C: 드라이브의 새 어셈블리 디렉터리에서 작업 디렉터리를 찾습니다.  
  
```console  
vbc -libpath:c:\;"c:\New Assemblies" -reference:t2.dll t2.vb  
```  
  
## <a name="see-also"></a>참조

- [.NET 어셈블리](../../../standard/assembly/index.md)
- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
