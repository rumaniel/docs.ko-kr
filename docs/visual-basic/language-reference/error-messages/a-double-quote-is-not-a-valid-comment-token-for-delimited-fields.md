---
title: EscapeQuote가 True로 설정되어 있으면 큰따옴표가 구분된 필드의 올바른 주석 토큰이 아닙니다.
ms.date: 07/20/2015
f1_keywords:
- vbrTextFieldParser_InvalidComment
ms.assetid: 636d4b81-00ba-4cfd-98f7-4d57036f494d
ms.openlocfilehash: b49a3223c6638adff757d7d82aee549cb1fee473
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64646918"
---
# <a name="a-double-quote-is-not-a-valid-comment-token-for-delimited-fields-where-escapequote-is-set-to-true"></a>EscapeQuote가 True로 설정되어 있으면 큰따옴표가 구분된 필드의 올바른 주석 토큰이 아닙니다.
`TextFieldParser`에 대한 구분 기호로 따옴표가 제공되었지만 `EscapeQuotes` 가 `True`로 설정되어 있습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- `EscapeQuotes`를 `False`로 설정합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.SetDelimiters%2A>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.Delimiters%2A>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser>
- [방법: 쉼표로 구분된 텍스트 파일에서 읽기](../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)
