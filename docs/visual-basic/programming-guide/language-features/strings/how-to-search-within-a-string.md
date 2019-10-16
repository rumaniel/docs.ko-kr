---
title: '방법: 문자열 내에서 검색-Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], finding
- strings [Visual Basic], searching
- examples [Visual Basic], strings
ms.assetid: ae4c79e0-08ea-489f-bdb2-5eb6d355f284
ms.openlocfilehash: fe9e50dc5458fdf8546094e5f41c2f001f1d2791
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700070"
---
# <a name="how-to-search-within-a-string-visual-basic"></a>방법: 문자열 내에서 검색 (Visual Basic)

이 문서에서는 Visual Basic 문자열 내에서 검색 하는 방법의 예를 보여 줍니다.

## <a name="example"></a>예제

이 예에서는 <xref:System.String> 개체의 <xref:System.String.IndexOf%2A> 메서드를 호출 하 여 첫 번째 부분 문자열의 인덱스를 보고 합니다.

 [!code-vb[VbVbalrStrings#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#71)]

## <a name="robust-programming"></a>강력한 프로그래밍

@No__t-0 메서드는 맨 처음 발견 되는 부분 문자열의 첫 번째 문자 위치를 반환 합니다. 인덱스는 0부터 시작 하며,이는 문자열의 첫 번째 문자에 인덱스가 0 인 것을 의미 합니다.

@No__t-0은 부분 문자열을 찾지 못하면-1을 반환 합니다.

@No__t-0 메서드는 대/소문자를 구분 하며 현재 문화권을 사용 합니다.

최적의 오류 제어를 위해 Try ...의 `Try` 블록에 문자열 검색을 포함 하는 것이 좋습니다. [ Catch ... Finally 문](../../../language-reference/statements/try-catch-finally-statement.md) 생성

## <a name="see-also"></a>참조

- <xref:System.String.IndexOf%2A>
- [Try...Catch...Finally 문](../../../language-reference/statements/try-catch-finally-statement.md)
- [Visual Basic의 문자열 소개](introduction-to-strings.md)
- [문자열](index.md)
