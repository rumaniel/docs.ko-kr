---
title: "'#Region' 및 ' #End Region' 문은 메서드 본문-여러 줄 람다 식 내에서 유효 하지 않습니다."
ms.date: 07/20/2015
f1_keywords:
- bc32025
- vbc32025
helpviewer_keywords:
- BC32025
ms.assetid: 43707bf1-1c6b-4d82-b081-e5a17dca51c1
ms.openlocfilehash: c41b95da7e3565ae7aaf332fe49361336e79f7c7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013766"
---
# <a name="region-and-end-region-statements-are-not-valid-within-method-bodiesmultiline-lambdas"></a>메서드 본문에서는 '#Region' 및 '#End Region' 문을 사용할 수 없습니다./multiline lambdas
`#Region` 블록 클래스, 모듈 또는 네임 스페이스 수준에서 선언 해야 합니다. 축소 가능한 영역에는 하나 이상의 프로시저 포함할 수 있지만 시작 하거나 프로시저 내부에서 끝날 수 없습니다.  
  
 **오류 ID:** BC32025  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 앞의 절차와 올바르게 종료 확인을 `End Function` 또는 `End Sub` 문입니다.  
  
2. 있는지 확인 합니다 `#Region` 및 `#End Region` 지시문은 같은 코드 블록에 있습니다.  
  
## <a name="see-also"></a>참고자료

- [#Region 지시문](../../../visual-basic/language-reference/directives/region-directive.md)
