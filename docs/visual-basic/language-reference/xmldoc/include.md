---
title: <include> (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- include XML tag
- <include> XML tag
ms.assetid: ba8e9173-82cd-460b-8938-a075a2dfb36d
ms.openlocfilehash: d9c1c1a50f0e3530c842a6058e288b8d2be15f95
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61940909"
---
# <a name="include-visual-basic"></a>\<포함 > (Visual Basic)
형식 및 소스 코드에서 멤버를 설명 하는 다른 파일을 가리킵니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<include file="filename" path="tagpath[@name='id']" />  
```  
  
## <a name="parameters"></a>매개 변수  
 `filename`  
 필수 요소. 문서가 포함된 파일의 이름입니다. 경로를 사용하여 파일 이름을 정규화할 수 있습니다. 묶습니다 `filename` 큰따옴표에서 ("").  
  
 `tagpath`  
 필수 요소. `filename`의 태그 경로로, `name` 태그에 연결됩니다. 경로를 큰따옴표로 묶습니다 ("").  
  
 `name`  
 필수 요소. 주석 앞에 오는 태그의 이름 지정자입니다. `Name` 갖습니다는 `id`합니다.  
  
 `id`  
 필수 요소. 주석 앞에 오는 태그의 ID입니다. ID는 작은따옴표로 묶습니다 (' ').  
  
## <a name="remarks"></a>설명  
 사용 된 `<include>` 태그를 다른 파일의 형식을 설명 하는 주석 및 소스 코드에서 멤버를 참조 하십시오. 소스 코드 파일에 직접 문서 주석을 포함하는 대신 사용되는 대안입니다.  
  
 `<include>` 태그 W3C XML Path Language (XPath) Version 1.0 권장 사항에 사용 합니다. 사용자 지정 하는 방법에 대 한 자세한 내용은 하 `<include>` 를 참조 하십시오 <https://www.w3.org/TR/xpath>합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 `<include>` 멤버 문서 주석 이라는 파일에서 가져오려는 태그 `commentFile.xml`합니다.  
  
 [!code-vb[VbVbcnXmlDocComments#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#4)]  
  
 형식의 여 `commentFile.xml` 는 다음과 같습니다.  
  
```xml  
<Docs>  
<Members name="Open">  
<summary>Opens a file.</summary>  
<param name="filename">File name to open.</param>  
</Members>  
<Members name="Close">  
<summary>Closes a file.</summary>  
<param name="filename">File name to close.</param>  
</Members>  
</Docs>  
```  
  
## <a name="see-also"></a>참고자료

- [XML 주석 태그](../../../visual-basic/language-reference/xmldoc/index.md)
