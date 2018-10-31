---
title: '&lt;include&gt;(C# 프로그래밍 가이드)'
ms.date: 07/20/2015
f1_keywords:
- include
- <include>
helpviewer_keywords:
- <include> C# XML tag
- include C# XML tag
ms.assetid: a8a70302-6196-4643-bd09-ef33f411f18f
ms.openlocfilehash: 854c8b61fa8164bccfc9451f2f163dab4a56388f
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48035190"
---
# <a name="ltincludegt-c-programming-guide"></a>&lt;include&gt;(C# 프로그래밍 가이드)
## <a name="syntax"></a>구문  
  
```xml  
<include file='filename' path='tagpath[@name="id"]' />  
```  
  
#### <a name="parameters"></a>매개 변수  
 `filename`  
 문서가 포함된 XML 파일의 이름입니다. 파일 이름은 소스 코드 파일에 상대 경로로 한정될 수 있습니다. `filename`을 작은따옴표(‘ ’)로 묶습니다.  
  
 `tagpath`  
 `filename`의 태그 경로로, `name` 태그에 연결됩니다. 경로를 작은따옴표(‘ ’)로 묶습니다.  
  
 `name`  
 주석 앞에 오는 태그의 이름 지정자입니다. `name`에는 `id`가 있습니다.  
  
 `id`  
 주석 앞에 오는 태그의 ID입니다. ID를 큰따옴표(“ ”)로 묶습니다.  
  
## <a name="remarks"></a>설명  
 \<include> 태그를 사용하면 소스 코드의 형식과 멤버를 설명하는 다른 파일의 주석을 참조할 수 있습니다. 소스 코드 파일에 직접 문서 주석을 포함하는 대신 사용되는 대안입니다. 별도 파일에 문서를 배치하면 소스 코드와 별도로 문서에 소스 제어를 적용할 수 있습니다. 한 사람은 소스 코드 파일을 체크 아웃하고 다른 사람은 문서 파일을 체크 아웃할 수 있습니다.  
  
 \<include> 태그는 XML XPath 구문을 사용합니다. \<include> 사용을 사용자 지정하는 방법은 XPath 설명서를 참조하세요.  
  
## <a name="example"></a>예  
 다중 파일 예제입니다. 아래에는 \<include>를 사용하는 첫 번째 파일이 나와 있습니다.  
  
 [!code-csharp[csProgGuideDocComments#5](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/include_1.cs)]  
  
 두 번째 파일인 xml_include_tag.doc에는 다음과 같은 문서 주석이 포함되어 있습니다.  
  
```xml  
<MyDocs>  
  
<MyMembers name="test">  
<summary>  
The summary for this type.  
</summary>  
</MyMembers>  
  
<MyMembers name="test2">  
<summary>  
The summary for this other type.  
</summary>  
</MyMembers>  
  
</MyDocs>  
```  
  
## <a name="program-output"></a>프로그램 출력  
 `/doc:DocFileName.xml.` 명령줄을 사용하여 Test 및 Test2 클래스를 컴파일하면 다음 출력이 생성됩니다. Visual Studio에서 프로젝트 디자이너의 빌드 창에 있는 XML 문서 주석 옵션을 지정합니다. C# 컴파일러는 \<inclue> 태그를 발견할 경우 현재 소스 파일 대신 xml_include_tag.doc에서 문서 주석을 검색합니다. 그런 다음 컴파일러는 DocFileName.xml을 생성합니다. 이 파일은 [Sandcastle](https://github.com/EWSoftware/SHFB) 등의 문서 도구에서 최종 문서를 생성하는 데 사용하는 파일입니다.  
  
```xml  
<?xml version="1.0"?>   
<doc>   
    <assembly>   
        <name>xml_include_tag</name>   
    </assembly>   
    <members>   
        <member name="T:Test">   
            <summary>   
The summary for this type.   
</summary>   
        </member>   
        <member name="T:Test2">   
            <summary>   
The summary for this other type.   
</summary>   
        </member>   
    </members>   
</doc>   
```  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [문서 주석에 대한 권장 태그](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
