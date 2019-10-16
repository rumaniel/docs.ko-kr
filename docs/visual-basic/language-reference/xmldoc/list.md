---
title: <list> (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- listheader XML tag
- <item> XML tag
- <list> XML tag
- <listheader> XML tag
- term XML tag
- list XML tag
- <description> XML tag
- description XML tag
- item XML tag
- <term> XML tag
ms.assetid: ec35fced-d58e-4520-a764-0691256e014b
ms.openlocfilehash: 7d7b85867f4c701322c5e6c31f2d89ab38fad05d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61940882"
---
# <a name="list-visual-basic"></a>\<목록 > (Visual Basic)
목록 또는 테이블을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<list type="type">  
   <listheader>  
      <term>term</term>  
      <description>description</description>  
   </listheader>  
   <item>  
      <term>term</term>  
      <description>description</description>  
   </item>  
</list>  
```  
  
## <a name="parameters"></a>매개 변수  
 `type`  
 형식 목록입니다. 글머리 기호 목록, 번호 매기기 목록 또는 "table" 2 열 테이블에 대 한 "number"에 대 한 "bullet" 여야 합니다.  
  
 `term`  
 경우에 사용 `type` "table"은 설명 태그에 정의 된 용어를 정의 하려면입니다.  
  
 `description`  
 때 `type` "bullet" 또는 "숫자" `description` 목록의 항목은 때 `type` "table"은 `description` 의 정의 `term`합니다.  
  
## <a name="remarks"></a>설명  
 `<listheader>` 블록은 테이블 또는 정의 목록의 머리글을 정의 합니다. 에 대 한 진입점을 제공할 수만 있는 테이블을 정의할 때 `term` 제목에서입니다.  
  
 지정 된 목록의 각 항목을 `<item>` 블록입니다. 둘 다 지정 해야 정의 목록을 만들 때는 `term` 고 `description`입니다. 그러나 테이블, 글머리 기호 목록 또는 번호 매기기 목록만 제공 해야 항목이 `description`합니다.  
  
 목록 또는 테이블 만큼 있습니다 `<item>` 필요에 따라 차단 합니다.  
  
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)로 컴파일하여 문서 주석을 파일로 처리합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 `<list>` 주의 섹션의 글머리 기호 목록을 정의 하는 태그입니다.  
  
 [!code-vb[VbVbcnXmlDocComments#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#5)]  
  
## <a name="see-also"></a>참고자료

- [XML 주석 태그](../../../visual-basic/language-reference/xmldoc/index.md)
