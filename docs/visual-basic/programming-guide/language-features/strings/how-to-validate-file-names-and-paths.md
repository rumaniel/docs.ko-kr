---
title: '방법: 파일 이름 및 Visual Basic에서 경로 확인'
ms.date: 07/20/2015
helpviewer_keywords:
- file names [Visual Basic], validating
- strings [Visual Basic], validating
- Boolean values [Visual Basic]
- paths [Visual Basic], validating
ms.assetid: f673462d-57b7-4120-b13a-6a7592f7ab2c
ms.openlocfilehash: c8e01a0f5a3f99fdbc424d6cd7d224367c7bad08
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032177"
---
# <a name="how-to-validate-file-names-and-paths-in-visual-basic"></a>방법: 파일 이름 및 Visual Basic에서 경로 확인
이 예는 `Boolean` 문자열로 파일 이름이 나 경로 나타내는지 여부를 나타내는 값입니다. 유효성 검사 이름을 파일 시스템에서 허용 되지 않는 문자를 포함 하는 경우를 확인 합니다.  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbcnRegEx#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#4)]  
  
 이 예제는 콜론 또는 디렉터리 이름이 없는 이름을 올바르게 배치가 아니면 이름의 길이 시스템 정의 최대 길이 초과 하는 경우를 확인 하지 않습니다. 또한 확인 하지 않습니다 응용 프로그램은 지정 된 이름의 파일 시스템 리소스에 액세스 하는 경우.  
  
## <a name="see-also"></a>참고자료

- <xref:System.IO.Path.GetInvalidPathChars%2A>
- [Visual Basic의 문자열 유효성 검사](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)
