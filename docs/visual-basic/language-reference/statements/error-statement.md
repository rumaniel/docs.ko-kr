---
title: Error 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.error
helpviewer_keywords:
- Error statement [Visual Basic], syntax
- Error statement [Visual Basic]
- Error keyword [Visual Basic]
- run-time errors [Visual Basic], codes
- errors [Visual Basic], simulating
ms.assetid: 85cd5c59-5224-4f02-aaf5-fcfefab17a29
ms.openlocfilehash: 7b926214d3be7f5f57783a8599acf1bb1042f956
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69944452"
---
# <a name="error-statement"></a>Error 문
오류가 발생 한 경우를 시뮬레이션 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Error errornumber  
```  
  
## <a name="parts"></a>요소  
 `errornumber`  
 필수 요소. 모든 유효한 오류 번호가 될 수 있습니다.  
  
## <a name="remarks"></a>설명  
 `Error` 문은 이전 버전과의 호환성을 위해 지원 됩니다. 새 코드에서 특히 개체를 만들 때 `Err` 개체의 `Raise` 메서드를 사용 하 여 런타임 오류를 생성 합니다.  
  
 를 `errornumber` 정의 하면개체`Err` 의 속성에 다음 기본값이 할당 된 후에 문이오류처리기를호출합니다.`Error`  
  
|속성|값|  
|--------------|-----------|  
|`Number`|문에 대 한 `Error` 인수로 지정 된 값입니다. 모든 유효한 오류 번호가 될 수 있습니다.|  
|`Source`|현재 Visual Basic 프로젝트의 이름입니다.|  
|`Description`|`Error` 지정`Number`된에 대 한 함수의 반환 값에 해당 하는 문자열 식 (있는 경우)입니다. 문자열이 없으면에 `Description` 길이가 0 인 문자열 ("")이 포함 됩니다.|  
|`HelpFile`|적절 한 Visual Basic 도움말 파일의 정규화 된 드라이브, 경로 및 파일 이름입니다.|  
|`HelpContext`|`Number` 속성에 해당 하는 오류에 대 한 적절 한 Visual Basic 도움말 파일 컨텍스트 ID입니다.|  
|`LastDLLError`|0입니다.|  
  
 오류 처리기가 없거나 사용할 수 없는 경우 오류 메시지가 생성 되 고 `Err` 개체 속성에서 표시 됩니다.  
  
> [!NOTE]
> 일부 Visual Basic 호스트 응용 프로그램에서 개체를 만들 수 없습니다. 클래스 및 개체를 만들 수 있는지 여부를 확인 하려면 호스트 응용 프로그램의 설명서를 참조 하세요.  
  
## <a name="example"></a>예제  
 이 예에서는 `Error` 문을 사용 하 여 오류 번호 11을 생성 합니다.  
  
```  
On Error Resume Next   ' Defer error handling.  
Error 11   ' Simulate the "Division by zero" error.  
```  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **어셈블리** Visual Basic 런타임 라이브러리(Microsoft.VisualBasic.dll)  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ErrObject.Clear%2A>
- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Raise%2A>
- [On Error 문](../../../visual-basic/language-reference/statements/on-error-statement.md)
- [Resume 문](../../../visual-basic/language-reference/statements/resume-statement.md)
- [오류 메시지](../../../visual-basic/language-reference/error-messages/index.md)
