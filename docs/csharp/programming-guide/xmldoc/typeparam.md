---
title: '&lt;typeparam&gt;(C# 프로그래밍 가이드)'
ms.date: 07/20/2015
f1_keywords:
- typeparam
helpviewer_keywords:
- <typeparam> C# XML tag
- typeparam C# XML tag
ms.assetid: 9b99d400-e911-4e55-99c6-64367c96aa4f
ms.openlocfilehash: ec19060008c1c06c54c89dbddee7d24001bcdebc
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50187116"
---
# <a name="lttypeparamgt-c-programming-guide"></a>&lt;typeparam&gt;(C# 프로그래밍 가이드)
## <a name="syntax"></a>구문  
  
```xml  
<typeparam name="name">description</typeparam>  
```  
  
#### <a name="parameters"></a>매개 변수  
 `name`  
 형식 매개 변수의 이름입니다. 이름을 큰따옴표(“ ”)로 묶습니다.  
  
 `description`  
 형식 매개 변수에 대한 설명입니다.  
  
## <a name="remarks"></a>설명  
 `<typeparam>` 태그는 제네릭 형식 또는 메서드 선언의 주석에서 형식 매개 변수를 설명하는 데 사용해야 합니다. 제네릭 형식 또는 메서드의 각 형식 매개 변수에 대한 태그를 추가합니다.  
  
 자세한 내용은 [제네릭](../../../csharp/programming-guide/generics/index.md)을 참조하세요.  
  
 `<typeparam>` 태그에 대한 텍스트는 IntelliSense와 [개체 브라우저 창](https://msdn.microsoft.com/library/3c7f1673-1f0d-41b1-94ca-a3dcfcb82cda)의 코드 주석 웹 보고서에 표시됩니다.  
  
 [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)로 컴파일하여 문서 주석을 파일로 처리합니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csProgGuideDocComments#13](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/typeparam_1.cs)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [문서 주석에 대한 권장 태그](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
