---
title: 암호 복잡성 (Visual Basic) 유효성 검사
ms.date: 07/20/2015
helpviewer_keywords:
- String data type [Visual Basic], validation
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
ms.openlocfilehash: ff0ac933be917b5604966240ff1fbd331a34ba77
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64663622"
---
# <a name="walkthrough-validating-that-passwords-are-complex-visual-basic"></a>연습: 암호의 복합성 검사 (Visual Basic)
이 메서드는 몇 가지 강력한 암호 특성에 대 한 확인 하 고 실패에 대 한 암호를 확인 하는 정보를 사용 하 여 문자열 매개 변수를 업데이트 합니다.  
  
 사용자 권한을 부여 하는 보안 시스템에서 암호를 사용할 수 있습니다. 그러나 암호는 권한이 없는 사용자가 추측 하기 어려운 여야 합니다. 공격자가 사용할 수는 *사전 공격* 프로그램을 사전 (또는 다른 언어로 여러 사전)에 있는 단어의 모든 반복 하 고 사용자의 암호로 사용 된 단어 중 하나라도 있는지 여부를 테스트 합니다. "양키스" 또는 "Mustang"와 같은 취약 한 암호를 신속 하 게 추측할 수 있습니다. 강력한 암호와 같은 "? 있습니다 'L1N3vaFiNdMeyeP@sSWerd! "를 추측할 수 될 가능성이 훨씬 적습니다. 암호로 보호 된 시스템 사용자는 강력한 암호를 선택 해야 합니다.  
  
 강력한 암호 (대문자, 소문자, 숫자 및 특수 문자의 혼합 포함) 복잡 하며 단어 아닙니다. 이 예제에서는 복잡성을 확인 하는 방법에 설명 합니다.  
  
## <a name="example"></a>예제  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbcnRegEx#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 해당 암호가 들어 있는 문자열을 전달 하 여이 메서드를 호출 합니다.  
  
 이 예제에는 다음 사항이 필요합니다.  
  
- <xref:System.Text.RegularExpressions> 네임스페이스의 멤버에 대한 액세스 권한. 코드에서 멤버 이름을 정규화하지 않는 경우 `Imports` 문을 추가합니다. 자세한 내용은 [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)을 참조하세요.  
  
## <a name="security"></a>보안  
 를 사용 하는 네트워크를 통해 암호를 이동 하는 경우 데이터 전송에 안전한 방법을 사용 해야 합니다. 자세한 내용은 [ASP.NET 웹 응용 프로그램 보안](https://docs.microsoft.com/previous-versions/aspnet/330a99hc(v=vs.100))합니다.
  
 정확도 향상 시킬 수 있습니다는 `ValidatePassword` 복잡성 검사를 추가 하 여 함수:  
  
- 암호 및 사용자의 이름과 사용자 id는 응용 프로그램 정의 사전 해당 부분 문자열을 비교 합니다. 또한 비교를 수행할 때 동일한 것으로 시각적으로 유사한 문자를 처리 합니다. 예를 들어 문자 "l" 및 "e" 숫자 "1" 및 "3"으로 처리 합니다.  
  
- 대문자 하나만 있으면 암호의 첫 번째 문자 아닌지 확인 합니다.  
  
- 마지막 두 문자 암호의 문자 인지 확인 합니다.  
  
- 모든 기호는 키보드의 맨 위 행에서 입력 한 암호를 허용 하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Text.RegularExpressions.Regex>
- [ASP.NET 웹 응용 프로그램 보안](https://docs.microsoft.com/previous-versions/aspnet/330a99hc(v=vs.100))
