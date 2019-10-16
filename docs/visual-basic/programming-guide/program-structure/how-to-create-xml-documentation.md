---
title: '방법: Visual Basic에서 XML 문서 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- XML comments
- XML documentation [Visual Basic], creating
ms.assetid: 27b5b06c-09b9-496a-8245-f9542d846230
ms.openlocfilehash: ff93a7bb2d8fdef68fc956d4c569ca5ad37afb2c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054110"
---
# <a name="how-to-create-xml-documentation-in-visual-basic"></a>방법: Visual Basic에서 XML 문서 만들기

이 예제에서는 코드에 XML 문서 주석을 추가 하는 방법을 보여 줍니다.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-xml-documentation-for-a-type-or-member"></a>형식 또는 멤버에 대 한 XML 문서를 만들려면

1. **코드 편집기**에서 문서를 만들 형식 또는 멤버 위의 줄에 커서를 놓습니다.

2. ( `'''` 세 개의 작은 따옴표)를 입력 합니다.

    형식 또는 멤버에 대 한 XML 뼈대가 **코드 편집기**에 추가 됩니다.

3. 적절 한 태그 사이에 설명 정보를 추가 합니다.

    > [!NOTE]
    > XML 문서 블록 내에 줄을 추가 하는 경우 각 줄은로 `'''`시작 해야 합니다.

4. 형식 또는 멤버를 사용 하는 코드를 새 XML 문서 주석과 함께 추가 합니다.

    IntelliSense는 형식 또는 멤버에 \<대 한 요약 > 태그의 텍스트를 표시 합니다.

5. 코드를 컴파일하여 문서 주석을 포함 하는 XML 파일을 생성 합니다. 자세한 내용은 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)를 참조하세요.

## <a name="see-also"></a>참고자료

- [코드를 XML로 문서화](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
- [XML 주석 태그](../../../visual-basic/language-reference/xmldoc/index.md)
- [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)
