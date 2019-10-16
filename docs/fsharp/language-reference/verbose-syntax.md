---
title: 자세한 구문
description: F# 프로그래밍 언어의 자세한 정보 표시와 간단한 구문 간의 차이점을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: d2459da60bba5d88bd23615c8bf09ba64f7c22c4
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214041"
---
# <a name="verbose-syntax"></a>자세한 구문

F# 언어의 여러 구문에 사용할 수 있는 구문에는 *자세한 구문* 및 *간단한*구문 이라는 두 가지 형식이 있습니다. 자세한 구문은 일반적으로 사용 되지 않지만 들여쓰기에 대 한 덜 중요 한 이점이 있습니다. 간단한 구문은 더 짧고 들여쓰기를 사용 하 여 `begin` `in`, `end`, 등의 추가 키워드가 아닌 구문의 시작과 끝을 알립니다. 기본 구문은 간단한 구문입니다. 이 항목에서는 간단한 구문을 사용 F# 하지 않는 경우의 구문에 대해 설명 합니다. Verbose 구문은 항상 사용 하도록 설정 되어 있으므로 간단한 구문을 사용 하는 경우에도 일부 구문에 대해 자세한 구문을 사용할 수 있습니다. 지시문을 `#light "off"` 사용 하 여 간단한 구문을 사용 하지 않도록 설정할 수 있습니다.

## <a name="table-of-constructs"></a>구문 테이블

다음 표에서는 두 형식 간에 차이가 있는 컨텍스트에서 F# 언어 구문의 간단한 구문 및 자세한 구문을 보여 줍니다. 이 표에서 꺾쇠 괄호 (&lt;&gt;)는 사용자가 제공 하는 구문 요소를 둘러쌉니다. 이러한 구문 내에서 사용 되는 구문에 대 한 자세한 내용은 각 언어 구문에 대 한 설명서를 참조 하세요.

<table>
<tr>
<th>언어 구문</th>
<th>간단한 구문</th>
<th>자세한 구문</th>
</tr>
<tr>
<td>
복합 식
</td>
<td>

```xml
<expression1>
<expression2>
```

</td><td>

```fsharp
<expression1>; <expression2>
```

</td>
</tr>
<tr><td>

중첩 `let` 바인딩

</td><td>

```fsharp
let f x =
    let a = 1
    let b = 2
    x + a + b
```

</td><td>

```fsharp
let f x =
    let a = 1 in
    let b = 2 in
    x + a + b
```

</td>
</tr>
<tr><td>
코드 블록
</td><td>

```fsharp
(
    <expression1>
    <expression2>
)
```

</td><td>

```fsharp
begin
    <expression1>;
    <expression2>;
end
```

</td>
</tr>
<tr><td>
`for...do`
</td><td>

```fsharp
for counter = start to finish do
    ...
```

</td><td>

```fsharp
for counter = start to finish do
    ...
done
```

</td>
</tr>
<tr><td>
`while...do`
</td><td>

```fsharp
while <condition> do
    ...
```

</td><td>

```fsharp
while <condition> do
    ...
done
```

</td>
</tr>
<tr><td>
`for...in`
</td><td>

```fsharp
for var in start .. finish do
    ...
```

</td><td>

```fsharp
for var in start .. finish do
    ...
done
```

</td>
</tr>
<tr><td>
`do`
</td><td>

```fsharp
do
    ...
```

</td><td>

```fsharp
do
    ...
in
```

</td>
</tr>
<tr><td>레코드(record)
</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    <value-or-member-definitions>
```

</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>클래스
</td><td>

```fsharp
type <class-name>(<params>) =
    ...
```

</td><td>

```fsharp
type <class-name>(<params>) =
    class
        ...
    end
```

</td>
</tr>
<tr><td>구조체(structure)</td><td>

```fsharp
[<StructAttribute>]
type <structure-name> =
    ...
```

</td><td>

```fsharp
type <structure-name> =
    struct
        ...
    end
```

</td>
</tr>
<tr><td>구별 된 공용 구조체</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    <value-or-member definitions>
```

</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>interface(인터페이스)</td><td>

```fsharp
type <interface-name> =
    ...
```

</td><td>

```fsharp
type <interface-name> =
    interface
        ...
    end
```

</td>
</tr>
<tr><td>개체 식</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
        <interface-implementations>
}
```

</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
    end
    <interface-implementations>
}
```

</td>
</tr>
<tr><td>인터페이스 구현</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>형식 확장</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>모듈(module)</td><td>

```fsharp
module <module-name> =
    ...
```

</td><td>

```fsharp
module <module-name> =
    begin
        ...
    end
```

</td>
</tr>
</table>

## <a name="see-also"></a>참고 항목

- [F# 언어 참조](index.md)
- [컴파일러 지시문](compiler-directives.md)
- [코드 서식 지정 지침](code-formatting-guidelines.md)
