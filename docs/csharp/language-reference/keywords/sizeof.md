---
title: sizeof(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
ms.openlocfilehash: 37eb9345edc31a8d318540fd528f311059225de4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50184207"
---
# <a name="sizeof-c-reference"></a>sizeof(C# 참조)

관리되지 않는 형식의 크기(바이트)를 가져오는 데 사용됩니다.

관리되지 않는 형식은 다음과 같습니다.

- 다음 표에서는 간단한 형식을 보여 줍니다.

   |식|상수 값|
   |----------------|--------------------|
   |`sizeof(sbyte)`|1|
   |`sizeof(byte)`|1|
   |`sizeof(short)`|2|
   |`sizeof(ushort)`|2|
   |`sizeof(int)`|4|
   |`sizeof(uint)`|4|
   |`sizeof(long)`|8|
   |`sizeof(ulong)`|8|
   |`sizeof(char)`|2(유니코드)|
   |`sizeof(float)`|4|
   |`sizeof(double)`|8|
   |`sizeof(decimal)`|16|
   |`sizeof(bool)`|1|

- 열거형 형식.

- 포인터 형식.

- 참조 형식 또는 구성된 형식인 모든 인스턴스 필드 또는 자동 구현 인스턴스 속성을 포함하지 않는 사용자 정의 구조체입니다.

다음 예제에서는 `int`의 크기를 검색하는 방법을 보여 줍니다.

```csharp
// Constant value 4:
int intSize = sizeof(int);
```

## <a name="remarks"></a>설명

C# 버전 2.0부터 단순 형식 또는 열거형 형식에 `sizeof`를 적용하면 [안전하지 않은](unsafe.md) 컨텍스트에서 코드를 더 이상 컴파일할 필요가 없습니다.

`sizeof` 연산자를 오버로드할 수 없습니다. `sizeof` 연산자에서 반환되는 값은 `int` 형식입니다. 이전 표에서는 특정 단순 형식이 피연산자로 포함된 `sizeof` 식을 대체하는 상수 값을 보여 줍니다.

구조체를 비롯한 다른 모든 형식의 경우 `sizeof` 연산자는 안전하지 않은 코드 블록에서만 사용할 수 있습니다. <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 메서드를 사용할 수 있지만 이 메서드에서 반환된 값이 `sizeof`에서 반환된 값과 항상 같지는 않습니다. <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType>는 형식이 마샬링된 후의 크기를 반환하는 반면, `sizeof`는 안쪽 여백을 포함하여 공용 언어 런타임에 의해 할당된 크기를 반환합니다.

## <a name="example"></a>예

[!code-csharp[csrefKeywordsOperator#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#11)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [연산자 키워드](operator-keywords.md)
- [enum](enum.md)
- [안전하지 않은 코드 및 포인터](../../programming-guide/unsafe-code-pointers/index.md)
- [구조체](../../programming-guide/classes-and-structs/structs.md)
- [상수](../../programming-guide/classes-and-structs/constants.md)