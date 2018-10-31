---
title: object(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- object_CSharpKeyword
- object
helpviewer_keywords:
- object keyword [C#]
ms.assetid: 93f60c0b-e17a-40a9-9362-cca5fb77b0e7
ms.openlocfilehash: b36703828e6027a89297ac88edaf2b55ec18f42e
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48849903"
---
# <a name="object-c-reference"></a>object(C# 참조)

`object` 형식은 .NET에서 <xref:System.Object>의 별칭입니다. C#의 통합 형식 시스템에서 사용자 정의 및 미리 정의된 참조 형식과 값 형식을 비롯한 모든 형식은 직접 또는 간접적으로 <xref:System.Object>에서 상속합니다. `object` 형식의 변수에 모든 형식의 값을 할당할 수 있습니다. 값 형식의 변수가 개체로 변환된 경우 *boxed*라고 합니다. 형식 개체의 변수가 값 형식으로 변환된 경우 *unboxed*라고 합니다. 자세한 내용은 [boxing 및 unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)을 참조하세요.

## <a name="example"></a>예

다음 샘플은 `object` 형식의 변수가 모든 데이터 형식의 값을 허용할 수 있는 방법 및 `object` 형식의 변수가 .NET Framework의 <xref:System.Object>에 대해 메서드를 사용할 수 있는 방법을 보여 줍니다.

[!code-csharp[csrefKeywordsTypes#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#16)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [참조 형식](reference-types.md)
- [값 형식](value-types.md)