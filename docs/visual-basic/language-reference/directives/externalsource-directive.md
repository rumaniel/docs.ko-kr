---
title: '#ExternalSource 지시문 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- '#Externalsource'
- '#ExternalSource'
- vb.ExternalSource
- Externalsource
- vb.#ExternalSource
- ExternalSource
helpviewer_keywords:
- ExternalSource directive (#ExternalSource)
- '#ExternalSource directive'
ms.assetid: 243bc6a2-34c3-4eeb-a776-9fd2bf988149
ms.openlocfilehash: ac7096e998dd8d2a416dc739e1d7625e1abff7a6
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696832"
---
# <a name="externalsource-directive"></a>#ExternalSource 지시문
소스 코드의 특정 줄과 소스 외부의 텍스트 간 매핑을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
#ExternalSource( StringLiteral , IntLiteral )  
    [ LogicalLine+ ]  
#End ExternalSource  
```  
  
## <a name="parts"></a>요소  
 `StringLiteral`  
 외부 소스에 대 한 경로입니다.  
  
 `IntLiteral`  
 외부 소스 첫째 줄의 줄 번호입니다.  
  
 `LogicalLine`  
 외부 소스에서 오류가 발생 하는 줄입니다.  
  
 `#End ExternalSource`  
 `#ExternalSource` 블록을 종료합니다.  
  
## <a name="remarks"></a>설명  
 이 지시문은 컴파일러와 디버거에서만 사용 됩니다.  
  
 소스 파일에는 소스 파일의 특정 코드 줄과 소스 외부의 텍스트 (예: .aspx 파일) 간의 매핑을 나타내는 외부 소스 지시문이 포함 될 수 있습니다. 컴파일 중에 지정 된 소스 코드에서 오류가 발생 하면 외부 소스에서 가져온 것으로 식별 됩니다.  
  
 외부 소스 지시문은 컴파일에 영향을 주지 않으며 중첩할 수 없습니다. 응용 프로그램에서 내부용으로 사용 됩니다.  
  
## <a name="see-also"></a>참조

- [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
