---
title: DLL을 로드하는 동안 오류가 발생했습니다(Visual Basic).
ms.date: 07/20/2015
f1_keywords:
- vbrID48
ms.assetid: 4226cd1f-028c-477d-88a5-cb57f7e0cdc8
ms.openlocfilehash: 5a26443a49b0b853f2f2188fb58d7ed907d671b4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64659611"
---
# <a name="error-in-loading-dll-visual-basic"></a>DLL을 로드하는 동안 오류가 발생했습니다(Visual Basic).
동적 연결 라이브러리 (DLL)는에 지정 된 라이브러리는 `Lib` 절을 `Declare` 문입니다. 이 오류의 가능한 원인은 다음과 같습니다.  
  
- 파일을 실행 하는 DLL 아닙니다.  
  
- Microsoft Windows DLL 파일이 아닙니다.  
  
- DLL에 들어 있지 않은 다른 DLL 참조 합니다.  
  
- DLL 또는 참조 된 DLL의 경로에 지정 된 디렉터리 아닙니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 파일 소스 텍스트 파일 및 따라서 이면 컴파일 및 DLL 실행 폼에 연결 수 해야 합니다.  
  
- Microsoft Windows DLL 파일이 없는 경우 해당 하는 Microsoft Windows를 가져옵니다.  
  
- DLL이 존재 하지 않는 다른 DLL을 참조 하는 경우 참조 된 DLL 가져오고 사용할 수 있도록 합니다.  
  
- DLL 또는 참조 된 DLL의 경로 지정 된 디렉터리에 없으면 DLL 참조 된 디렉터리로 이동 합니다.  
  
## <a name="see-also"></a>참고자료

- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
