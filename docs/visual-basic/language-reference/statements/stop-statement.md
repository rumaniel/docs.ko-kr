---
title: Stop 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Stop
helpviewer_keywords:
- breakpoints, Stop statements
- Stop statements [Visual Basic], syntax
- Stop statements [Visual Basic]
- execution [Visual Basic], suspending
- processing, interrupting
- processes, interrupting
- execution [Visual Basic], stopping
ms.assetid: c9a9fde0-d649-4662-9bef-bd0146ebc2a7
ms.openlocfilehash: a617038ec51d98c62b6cf7e3c124c8af01305bac
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957616"
---
# <a name="stop-statement-visual-basic"></a>Stop 문(Visual Basic)
실행을 일시 중단 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Stop  
```  
  
## <a name="remarks"></a>설명  
 프로시저에 문을 `Stop` 추가 하 여 실행을 일시 중단할 수 있습니다. `Stop` 문을 사용 하는 것은 코드에서 중단점을 설정 하는 것과 비슷합니다.  
  
 문은 실행을 일시 중단 하지만, `End`와는 달리 컴파일된 실행 파일 (.exe)에서 발생 한 경우를 제외 하 고는 파일을 닫지 않거나 모든 변수를 지우지 않습니다. `Stop`  
  
> [!NOTE]
> IDE (통합 개발 환경) 외부에서 실행 되는 코드에 문이있으면디버거가호출됩니다.`Stop` 이는 코드가 디버그 모드에서 컴파일 되었는지 아니면 소매 모드에서 컴파일 되었는지에 관계 없이 적용 됩니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 `Stop` 문을 사용 하 여 `For...Next` 루프를 통해 반복할 때마다 실행을 일시 중단 합니다.  
  
 [!code-vb[VbVbalrStatements#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#56)]  
  
## <a name="see-also"></a>참고자료

- [End 문](../../../visual-basic/language-reference/statements/end-statement.md)
