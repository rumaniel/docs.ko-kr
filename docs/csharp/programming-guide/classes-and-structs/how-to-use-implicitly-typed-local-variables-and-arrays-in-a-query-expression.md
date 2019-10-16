---
title: '방법: 쿼리 식에서 암시적으로 형식화된 지역 변수 및 배열 사용 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- implicitly-typed local variables [C#], how to use
ms.assetid: 6b7354d2-af79-427a-b6a8-f74eb8fd0b91
ms.openlocfilehash: 5003e03b488a16d53e4e3d20a0b0b0e09630b46f
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596711"
---
# <a name="how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression-c-programming-guide"></a>방법: 쿼리 식에서 암시적으로 형식화된 지역 변수 및 배열 사용(C# 프로그래밍 가이드)
컴파일러에서 지역 변수의 형식을 확인하려는 경우 항상 암시적으로 형식화된 지역 변수를 사용할 수 있습니다. 쿼리 식에 자주 사용되는 무명 형식을 저장하려면 암시적으로 형식화된 지역 변수를 사용해야 합니다. 다음 예제에서는 쿼리에서 암시적으로 형식화된 지역 변수의 선택적 및 필수 사용을 보여 줍니다.  
  
 암시적으로 형식화된 지역 변수는 [var](../../language-reference/keywords/var.md) 상황별 키워드를 사용하여 선언됩니다. 자세한 내용은 [암시적으로 형식화된 지역 변수](./implicitly-typed-local-variables.md) 및 [암시적으로 형식화된 배열](../arrays/implicitly-typed-arrays.md)을 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서는 `var` 키워드가 필요한 일반적인 시나리오로, 무명 형식의 시퀀스를 생성하는 쿼리 식을 보여 줍니다. 이 시나리오에서는 무명 형식의 형식 이름에 대한 액세스 권한이 없기 때문에 `foreach` 문의 쿼리 변수와 반복 변수가 모두 `var`을 사용하여 암시적으로 형식화되어야 합니다. 무명 형식에 대한 자세한 내용은 [무명 형식](./anonymous-types.md)을 참조하세요.  
  
 [!code-csharp[csProgGuideLINQ#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#32)]  
  
## <a name="example"></a>예  
 다음 예제에서는 유사하지만 `var` 사용이 선택 사항인 상황에서 `var` 키워드를 사용합니다. `student.LastName`이 문자열이기 때문에 쿼리를 실행하면 문자열 시퀀스가 반환됩니다. 따라서 `queryID`의 형식을 `var` 대신 `System.Collections.Generic.IEnumerable<string>`로 선언할 수 있습니다. `var` 키워드는 편의상 사용됩니다. 예제에서 `foreach` 문의 반복 변수는 명시적으로 문자열로 형식화되었지만, 대신 `var`을 사용하여 선언할 수도 있습니다. 반복 변수의 형식이 무명 형식이 아니기 때문에 `var` 사용은 요구 사항이 아니라 옵션입니다. `var` 자체는 형식이 아니라 형식을 유추하고 할당하도록 컴파일러에 지시하는 명령입니다.  
  
 [!code-csharp[csProgGuideLINQ#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#33)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [확장명 메서드](./extension-methods.md)
- [LINQ(Language-Integrated Query)](../../linq/index.md)
- [var](../../language-reference/keywords/var.md)
- [LINQ 쿼리 식](../linq-query-expressions/index.md)
