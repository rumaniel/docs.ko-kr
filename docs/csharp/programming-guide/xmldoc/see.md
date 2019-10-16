---
title: <see> - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- <see>
- see
helpviewer_keywords:
- cref [C#], <see> tag
- <see> C# XML tag
- cross-references [C#]
- see C# XML tag
ms.assetid: 0200de01-7e2f-45c4-9094-829d61236383
ms.openlocfilehash: e292e116ac468246bfe81e1eb5d5c5819a506701
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69587691"
---
# <a name="see-c-programming-guide"></a>\<see>(C# 프로그래밍 가이드)
## <a name="syntax"></a>구문  
  
```xml  
<see cref="member"/>  
```  
  
## <a name="parameters"></a>매개 변수  
 cref = " `member`"  
 현재 컴파일 환경에서 호출할 수 있는 멤버 또는 필드에 대한 참조입니다. 컴파일러는 지정된 코드 요소가 있으며 `member`를 출력 XML의 요소 이름에 전달하는지 확인합니다. *멤버*는 큰따옴표(“ ”)로 묶으세요.  
  
## <a name="remarks"></a>설명  
 \<see> 태그를 사용하면 텍스트 내부에서 링크를 지정할 수 있습니다. 참고 항목 부분에 배치할 텍스트를 지정하려면 [\<seealso>](./seealso.md)를 사용합니다. 코드 요소의 문서 페이지에 대한 내부 하이퍼링크를 만들려면 [cref 특성](./cref-attribute.md)을 사용합니다.  
  
 [-doc](../../language-reference/compiler-options/doc-compiler-option.md)로 컴파일하여 문서 주석을 파일로 처리합니다.  
  
 다음 예제에서는 요약 섹션의 \<see> 태그를 보여 줍니다.  
  
 [!code-csharp[csProgGuideDocComments#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#12)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [문서 주석에 대한 권장 태그](./recommended-tags-for-documentation-comments.md)
