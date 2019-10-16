---
title: Visual Basic의 배열
ms.date: 12/06/2017
f1_keywords:
- vb.Array
helpviewer_keywords:
- arrays [Visual Basic]
- Visual Basic, arrays
ms.assetid: dbf29737-b589-4443-bee6-a27588d9c67e
ms.openlocfilehash: 12846b80f04e9fa6d1188485ad55b061cd2863fa
ms.sourcegitcommit: 904b98d8d706f0e2d5ceaa00ce17ffbd92adfb88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66758854"
---
# <a name="arrays-in-visual-basic"></a>Visual Basic의 배열

배열 라고 하는 값의 집합이 *요소*, 서로 논리적으로 관련이 있는 합니다. 예를 들어, 배열; 초등학교에서 각 학년의 학생 수가 구성 될 수 있습니다. 배열의 각 요소에는 단일 학년의 학생 수입니다. 마찬가지로, 클래스에 대 한 학생의 성적 배열을 구성 될 수 있습니다. 배열의 각 요소에는 단일 등급입니다.

각 데이터 항목이 저장 가능한 개별 변수 이며 예를 들어, 응용 프로그램 분석 학생 점수를 사용할 수 있습니다 별도 변수로 각 학생의 등급이 대 한 같은 `englishGrade1`, `englishGrade2`등입니다. 이 방법에는 세 가지 주요 제한 사항:

- 처리할 수 있다고 얼마나 많은 등급 정확 하 게 디자인 타임에 인식 해야 합니다.
- 많은 수의 등급을 신속 하 게 처리 하기 힘들어집니다. 이 응용 프로그램을에 심각한 버그가 있을 가능성이 훨씬 더를 수 있습니다.
- 유지 관리 하는 것이 어렵습니다. 추가 하는 각 새 엔터프라이즈급 응용 프로그램 수 수정, 다시 컴파일 및 다시 배포는 필요 합니다.

배열을 사용 하 여 동일한 이름으로 이러한 관련된 값을 참조할 고 라고 하는 숫자를 사용할 수 있습니다는 *인덱스* 하거나 *첨자* 배열에서 해당 위치에 따라 개별 요소를 식별 하기. 배열 범위를 0에서 1을 뺀 총 수가 배열의 요소의 인덱스입니다. Visual Basic 구문을 사용 하 여 배열의 크기를 정의 하는 경우 총 배열의 요소 수가 아니라 가장 높은 인덱스를 지정 합니다. 하나의 단위로 배열을 사용 하 여 작업할 수 및 해당 요소를 반복 하는 기능 디자인 타임에 포함 하는 정확 하 게 얼마나 많은 요소입니다. 알 필요가 없도록 해제 합니다.

설명하기 전에 몇 가지 빠른 예제는 다음과 같습니다.

```vb
' Declare a single-dimension array of 5 numbers.
Dim numbers(4) As Integer

' Declare a single-dimension array and set its 4 values.
Dim numbers = New Integer() {1, 2, 4, 8}

' Change the size of an existing array to 16 elements and retain the current values.
ReDim Preserve numbers(15)

' Redefine the size of an existing array and reset the values.
ReDim numbers(15)

' Declare a 6 x 6 multidimensional array.
Dim matrix(5, 5) As Double

' Declare a 4 x 3 multidimensional array and set array element values.
Dim matrix = New Integer(3, 2) {{1, 2, 3}, {2, 3, 4}, {3, 4, 5}, {4, 5, 6}}

' Declare a jagged array
Dim sales()() As Double = New Double(11)() {}
```

## <a name="array-elements-in-a-simple-array"></a>차원 배열의 배열 요소

라는 배열을 만들어 보겠습니다 `students` 초등학교 각 학년의 학생 수를 저장 합니다. 요소의 인덱스 범위는 0부터 6까지입니다. 이 배열을 사용 하 여 7 개의 변수를 선언 하는 보다 간단 합니다.

다음 그림에 표시 된 `students` 배열입니다. 각 배열 요소에서

- 요소의 인덱스는 학년을 나타냅니다(인덱스 0은 유치원을 나타냄).

- 요소에 포함된 값은 해당 학년의 학생 수를 나타냅니다.

![학생 수 배열을 보여 주는 다이어그램](./media/index/students-array-elements.gif)

다음 예제에서는 만들고 배열을 사용 하는 Visual Basic 코드를 포함 합니다.

[!code-vb[simple-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/simple-array.vb)]

이 예제에서는 세 가지를 수행합니다.

- 선언 된 `students` 개의 일곱 개의 요소로 이루어진 배열입니다. 수 `6` 배열 선언은 배열의 마지막 인덱스를 나타냅니다. 즉, 하나는 배열의 요소 수보다 작아야 합니다.
- 배열의 각 요소에 값을 할당합니다. 배열 요소는 배열 이름을 사용 하 여 괄호 안에 있는 개별 요소의 인덱스를 포함 하 여 액세스 됩니다.
- 배열의 각 값을 나열합니다. 이 예제에서는 사용을 [ `For` ](../../../language-reference/statements/for-next-statement.md) 인덱스 번호로 배열의 각 요소에 액세스 하는 문입니다.

`students` 앞의 예제에서 배열 하나의 인덱스를 사용 하기 때문에 1 차원 배열입니다. 둘 이상의 인덱스 또는 아래 첨자를 사용 하는 배열 이라고 *다차원*합니다. 자세한 내용은이 문서의 나머지 부분을 참조 하세요. 및 [Array Dimensions in Visual Basic](../../language-features/arrays/array-dimensions.md)합니다.

## <a name="creating-an-array"></a>배열 만들기

여러 가지 방법으로 배열의 크기를 정의할 수 있습니다.

- 배열 선언 되 면 크기를 지정할 수 있습니다.

  [!code-vb[creating1](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#1)]

- 사용할 수는 `New` 절을 만들 때 배열의 크기를 제공 합니다.

  [!code-vb[creating2](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#2)]

기존 배열에 있는 경우 사용 하 여 해당 크기를 재정의할 수 있습니다 합니다 [ `ReDim` ](../../../language-reference/statements/redim-statement.md) 문입니다. 지정할 수 있습니다는 `ReDim` 문이 배열에 있는 값을 유지 하거나 빈 배열을 만들도록 지정할 수 있습니다. 다음 예제에서는 `ReDim` 문을 사용하여 기존 배열의 크기를 수정하는 여러 가지 방법을 보여 줍니다.

[!code-vb[redimensioning](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#3)]

자세한 내용은 참조는 [ReDim 문](../../../language-reference/statements/redim-statement.md)합니다.

## <a name="storing-values-in-an-array"></a>배열에 값 저장

`Integer`형식의 인덱스를 사용하여 배열의 각 위치에 액세스할 수 있습니다. 괄호로 묶인 해당 인덱스를 통해 각 배열 위치를 참조하여 배열에 값을 저장하고 검색할 수 있습니다. 다차원 배열에 대 한 인덱스는 쉼표 (,)로 구분 됩니다. 각 배열 차원에 대해 하나의 인덱스가 필요합니다.

다음 예제에서는 배열에서 값을 검색 및 저장 하는 몇 가지 문을 보여 줍니다.

[!code-vb[store-and-retrieve](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/store-and-retrieve.vb)]

## <a name="populating-an-array-with-array-literals"></a>배열 리터럴 사용 하 여 배열 채우기

배열 리터럴을 사용 하 여 동시에 만들 배열 값의 초기 집합으로 채울 수 있습니다. 배열 리터럴은 중괄호(`{}`)로 묶인 쉼표로 구분된 값 목록으로 구성됩니다.

배열 리터럴을 사용하여 배열을 만드는 경우 배열 형식을 제공하거나 형식 유추를 사용하여 배열 형식을 결정할 수 있습니다. 다음 예제에서는 두 옵션을 보여 줍니다.

[!code-vb[create-with-literals](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#4)]

형식 유추를 사용 하는 경우는 배열 형식에 의해 결정 됩니다는 *기준 형식* 리터럴 값의 목록에서입니다. 기준 형식은 배열의 다른 모든 형식과 넓힐 수 있는 형식이입니다. 이 고유 형식을 확인할 수 없는 경우 기준 형식은 배열의 다른 모든 형식이 축소될 수 있는 고유 형식입니다. 이러한 고유 형식을 모두 확인할 수 없는 경우 기준 형식은 `Object`입니다. 예를 들어 배열 리터럴에 제공된 값 목록이 `Integer`, `Long`및 `Double`형식의 값을 포함하는 경우 결과 배열은 `Double`형식입니다. 때문에 `Integer` 하 고 `Long` 로 확장 `Double`, `Double` 기준 형식입니다. 자세한 내용은 [Widening and Narrowing Conversions](../../language-features/data-types/widening-and-narrowing-conversions.md)을 참조하세요.

> [!NOTE]
> 형식 유추에서 형식 멤버를 지역 변수로 정의 된 배열에만 사용할 수 있습니다. 클래스 수준에서 배열 리터럴을 사용 하 여 정의 하는 배열 형식의 명시적 형식 정의 없으면 `Object[]`합니다. 자세한 내용은 [지역 형식 유추](../variables/local-type-inference.md)합니다.

앞의 예제를 정의 하는 참고 `values` 형식의 배열로 `Double` 형식의 모든 배열 리터럴에 있더라도 `Integer`합니다. 배열 리터럴의 값을 변환할 수 있으므로이 배열을 만들 수 있습니다 `Double` 값입니다.

또한 만들기를 사용 하 여 다차원 배열을 채웁니다 *배열 리터럴을 중첩*합니다. 중첩 된 배열 리터럴 결과 배열을 사용 하 여 일치 하는 차원 수가 있어야 합니다. 다음 예제에서는 중첩 된 배열 리터럴을 사용 하 여 정수의 2 차원 배열을 만듭니다.

[!code-vb[nested-array-literals](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#5)]

중첩 된 배열 리터럴을 사용 하 여 만들고 채울 배열을 중첩 된 배열 리터럴의 요소 수가 일치 하지 않는 경우 오류가 발생 합니다. 배열 리터럴 보다 차원 수가 다른 배열 변수를 명시적으로 선언 하는 경우에 오류가 발생 합니다.

1 차원 배열에 대 한 가능한 것 처럼 중첩 된 배열 리터럴을 사용 하 여 다차원 배열을 만들 때 형식 유추를 사용할 수 있습니다. 유추 된 유형 모든 중첩 수준에 대 한 모든 배열 리터럴에 있는 모든 값에 대 한 기준 형식이입니다. 다음 예제에서는 형식의 2 차원 배열을 만듭니다 `Double[,]` 형식의 값에서 `Integer` 고 `Double`입니다.

[!code-vb[nested-type-inference](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#6)]

추가 예제를 보려면 [방법: Visual Basic에서 배열 변수 초기화](../../language-features/arrays/how-to-initialize-an-array-variable.md)합니다.

## <a name="iterating-through-an-array"></a>배열 반복

가장 높은 가장 낮은 인덱스 또는 높은 배열의 각 요소를 액세스 배열을 통해 반복 하는 경우 가장 낮은 합니다. 일반적으로 사용 하 여는 [에 대 한 중... 다음 문](../../../language-reference/statements/for-next-statement.md) 또는 [각각에 대 한 중... 다음 문을](../../../language-reference/statements/for-each-next-statement.md) 에 배열의 요소를 반복 합니다. 호출할 수는 배열의 상한이 모르는 경우는 <xref:System.Array.GetUpperBound%2A?displayProperty=nameWithType> 메서드를 가장 높은 인덱스 값을 가져옵니다. 가장 낮은 인덱스 값은 거의 항상 0을 호출할 수 있습니다는 <xref:System.Array.GetLowerBound%2A?displayProperty=nameWithType> 메서드를 가장 낮은 인덱스 값을 가져옵니다.

다음 예제에서는 사용 하 여 1 차원 배열을 반복 합니다 [ `For...Next` ](../../../language-reference/statements/for-next-statement.md) 문입니다.

[!code-vb[iterate-one-dimensional-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/iterate1d.vb)]

다음 예제에서는 사용 하 여 다차원 배열을 반복을 [ `For...Next` ](../../../language-reference/statements/for-next-statement.md) 문입니다. <xref:System.Array.GetUpperBound%2A> 메서드에는 차원을 지정하는 매개 변수가 있습니다. `GetUpperBound(0)` 첫 번째 차원의 가장 높은 인덱스를 반환 하 고 `GetUpperBound(1)` 가장 높은 두 번째 차원 인덱스를 반환 합니다.

[!code-vb[iterate-two-dimensional-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/iterate2d.vb)]

다음 예제에서는 [각각에 대 한 중... 다음 문을](../../../language-reference/statements/for-each-next-statement.md)1 차원 배열과 2 차원 배열을 반복 하 합니다.

[!code-vb[iterate-for-each-next](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/iterate-for-each-next.vb)]

## <a name="array-size"></a>배열 크기

배열 크기는 모든 차원의 길이 곱입니다. 현재 배열에 포함된 요소의 총 수를 나타냅니다.  예를 들어, 다음 예제에서는 각 차원에 4 개의 요소가 있는 2 차원 배열을 선언합니다. 배열의 크기는 16 예제의 출력에서 볼 수 있듯이 (또는 (3 + 1) * (3 + 1).

[!code-vb[array-size](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-size.vb)]

> [!NOTE]
> 이 설명은 배열 크기는 가변된 배열에는 적용 되지 않습니다. 가변된 배열 및 가변 배열의 크기를 결정에 대 한 내용은 참조는 [가변 배열](#jagged-arrays) 섹션입니다.

<xref:System.Array.Length%2A?displayProperty=nameWithType> 속성을 사용하여 배열의 크기를 찾을 수 있습니다. 사용 하 여 다차원 배열의 각 차원 길이 찾을 수는 <xref:System.Array.GetLength%2A?displayProperty=nameWithType> 메서드.

새 배열 개체를 할당 하 여 또는 사용 하 여 배열 변수의 크기를 조정할 수 있습니다 합니다 [ `ReDim` 문](../../../language-reference/statements/redim-statement.md) 문입니다. 다음 예제에서는 `ReDim` 51 요소 배열에는 100 개의 요소로 이루어진 배열을 변경 하려면.

[!code-vb[resize-an-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-size2.vb)]

배열의 크기를 처리할 때 유의해야 하는 여러 가지 사항이 있습니다.

|||
|---|---|
|차원 길이|각 차원의 인덱스는 0 기반, 즉,이 범위는 0부터 상한입니다. 따라서 지정 된 차원의 길이 해당 차원의 선언된 된 상한 보다 큰 하나입니다.|
|길이 제한|배열의 각 차원 길이 최대 값 제한 합니다 `Integer` 데이터 형식, 즉 <xref:System.Int32.MaxValue?displayProperty=nameWithType> 또는 (2 ^31)-1입니다. 그러나 배열의 총 크기는 시스템에서 사용 가능한 메모리에 의해서도 제한됩니다. 배열을 초기화 하려고 하면 사용 가능한 메모리 양을 초과 하는, 런타임에서 throw는 <xref:System.OutOfMemoryException>합니다.|
|크기 및 요소 크기|배열의 크기는 해당 요소의 데이터 형식과 독립적입니다. 크기는 항상 메모리에 사용 하는 바이트 수가 아니라 요소의 총 수를 나타냅니다.|
|메모리 소비|배열이 메모리에 저장되는 방법에 대해서는 어떠한 가정도 하지 않는 것이 좋습니다. 스토리지는 각 데이터 너비의 플랫폼마다 달라지므로 동일한 배열이 32비트 시스템보다 64비트 시스템에서 더 많은 메모리를 사용할 수 있습니다. 시스템 구성에 따라 배열을 초기화할 때 CLR(공용 언어 런타임)에서 스토리지를 할당하여 요소를 최대한 가깝게 압축하거나 모두 일반적인 하드웨어 경계에 맞출 수 있습니다. 또한 배열의 제어 정보로 인해 스토리지 오버헤드가 필요하며, 차원이 추가될 때마다 이 오버헤드가 증가합니다.|

## <a name="the-array-type"></a>배열 형식

각 배열에는 해당 요소의 데이터 형식을 다른 데이터 형식입니다. 모든 배열에 대한 단일 데이터 형식은 없습니다. 대신, 배열의 데이터 형식은 배열의 차원 수 또는 *차수*와 배열에 있는 요소의 데이터 형식에 의해 결정됩니다. 두 배열 변수는 동일한 차수 있는 경우에 입력 하 고 해당 요소는 동일한 데이터 형식이 동일한 데이터입니다. 배열의 차원 길이 배열 데이터 형식이 영향을 주지 않습니다.

모든 배열은 <xref:System.Array?displayProperty=nameWithType> 클래스에서 상속되며 `Array` 형식으로 변수를 선언할 수 있지만, `Array` 형식의 배열을 만들 수는 없습니다. 예를 들어, 다음 코드는 선언 되지만 `arr` 형식으로 변수를 `Array` 호출는 <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> Object 배열을, 배열의 형식을 인스턴스화하기 위한 메서드를 확인 합니다.

[!code-vb[array-class](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-class.vb)]

또한 [ReDim 문](../../../language-reference/statements/redim-statement.md)은 `Array` 형식으로 선언된 변수에 대해 작업할 수 없습니다. 이러한 이유로, 및 형식 안전성에 대 한 특정 형식으로 모든 배열을 선언 하는 것이 좋습니다.

배열이나 해당 요소의 데이터 형식을 여러 가지 방법으로 확인할 수 있습니다.

- 호출할 수 있습니다 합니다 <xref:System.Object.GetType%2A> 메서드를 가져올 변수의 <xref:System.Type> 변수의 런타임 형식을 나타내는 개체입니다. <xref:System.Type> 개체는 해당 속성과 메서드에 광범위한 정보를 보유합니다.
- 변수를 전달할 수 있습니다는 <xref:Microsoft.VisualBasic.Information.TypeName%2A> 함수를 한 `String` 런타임 형식의 이름을 사용 하 여 합니다.

다음 예제에서는 모두 호출 합니다 `GetType` 메서드 및 `TypeName` 배열의 형식을 결정 하는 함수입니다. 배열 형식은 `Byte(,)`합니다. 유의 합니다 <xref:System.Type.BaseType%2A?displayProperty=nameWithType> 속성 또한는 바이트 배열의 기본 형식임을 나타냅니다는 <xref:System.Array> 클래스입니다.

[!code-vb[array-type](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-type.vb)]

## <a name="arrays-as-return-values-and-parameters"></a>반환 값 및 매개 변수로 사용 되는 배열

`Function` 프로시저에서 배열을 반환하려면 배열 데이터 형식 및 차원 수를 [Function 문](../../../language-reference/statements/function-statement.md)의 반환 형식으로 지정합니다. 함수 내에서 동일한 데이터 형식 및 차원 수의 지역 배열 변수를 선언합니다. [Return 문](../../../language-reference/statements/return-statement.md)에 지역 배열 변수를 괄호 없이 포함합니다.

`Sub` 또는 `Function` 프로시저에 대한 매개 변수로 배열을 지정하려면 지정된 데이터 형식 및 차원 수의 배열로 매개 변수를 정의합니다. 프로시저 호출에서 동일한 데이터 형식 및 차원 수를 사용 하 여 배열 변수를 전달 합니다.

다음 예제에서는 `GetNumbers` 함수에서 반환을 `Integer()`, 형식의 1 차원 배열을 `Integer`합니다. `ShowNumbers` 프로시저는 `Integer()` 인수를 사용합니다.

[!code-vb[return-value-and-params](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/return-values-and-params.vb)]

다음 예제에서는 `GetNumbersMultiDim` 함수에서 반환을 `Integer(,)`, 형식의 2 차원 배열을 `Integer`합니다.  `ShowNumbersMultiDim` 프로시저는 `Integer(,)` 인수를 사용합니다.

[!code-vb[multidimensional-return-value](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/return-values-and-params-2d.vb)]

## <a name="jagged-arrays"></a>가변 배열

애플리케이션의 데이터 구조가 2차원 배열이지만 사각형이 아닌 경우도 있습니다. 예를 들어, 해당 월의 각 날짜의 최고 기온에 대 한 데이터를 저장할 배열을 사용할 수 있습니다. 배열의 첫 번째 차원에는 월을 나타내는 하지만 두 번째 차원의 일 수를 나타내는 아니며 그 달의 일 수가 균일 한 합니다. *가변된 배열을*는 라고는 *배열로 이루어진 배열*, 이러한 시나리오에 대 한 설계 되었습니다. 가변된 배열에 요소가 들어 있는 배열도 배열이입니다. 가변 배열 및 가변 배열의 각 요소에는 하나 이상의 차원이 있을 수 있습니다.

다음 예제는 각 요소가 일 배열인 월의 배열을 사용 합니다. 이 예제에서는 월에 다른 일 수 있으므로 가변된 배열을 사용 합니다.  이 예제에서는 가변된 배열을 만들고, 값을 할당, 검색 및 해당 값을 표시 하는 방법을 보여 줍니다.

[!code-vb[jagged-arrays](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/jagged.vb)]

앞의 예제를 사용 하 여 요소 별로 단위로 가변된 배열에 값을 할당 한 `For...Next` 루프입니다. 또한 가변 배열의 요소에 중첩 된 배열 리터럴을 사용 하 여 값을 할당할 수 있습니다. 그러나 사용 하려고 중첩 배열 리터럴 (예를 들어 `Dim valuesjagged = {{1, 2}, {2, 3, 4}}`) 컴파일러 오류가 [BC30568](../../../,,/../misc/bc30568.md)합니다. 오류를 해결 하려면 내부 배열 리터럴을 괄호로 묶어야 합니다. 괄호는 배열 리터럴 식이 평가 되 고, 강제 하 고 결과 값은 다음 예제와 같이 외부 배열 리터럴과 사용 하 여 사용 됩니다.

[!code-vb[jagged-array-initialization](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/jagged-assign.vb)]

가변된 배열에 요소가 배열을 포함할 1 차원 배열이입니다. 따라서 합니다 <xref:System.Array.Length%2A?displayProperty=nameWithType> 속성 및 `Array.GetLength(0)` 1 차원 배열에 있는 요소의 개수를 반환 하는 메서드 및 `Array.GetLength(1)` throw는 <xref:System.IndexOutOfRangeException> 가변된 배열을 다차원 없기 때문에 합니다. 각 하위 문자열의 값을 검색 하 여 각 하위 배열에 있는 요소의 수를 결정 <xref:System.Array.Length%2A?displayProperty=nameWithType> 속성입니다. 다음 예제에서는 가변된 배열의 요소 수를 결정 하는 방법을 보여 줍니다.

[!code-vb[jagged-array-size](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/jagged-length.vb)]

## <a name="zero-length-arrays"></a>길이가 0 인 배열

Visual Basic 초기화 되지 않은 배열 구별 (값이 배열을 `Nothing`) 및 *길이가 0 인 배열을* 이거나 빈 배열 (요소가 없는 배열입니다.) 초기화 되지 않은 배열이 차원이 구분 되지 않습니다는 하나 또는 모든 값을 할당 합니다. 예를 들어 다음과 같습니다.

```vb
Dim arr() As String
```

길이가 0 인 배열은 1 차원으로 선언 됩니다. 예를 들어 다음과 같습니다.

```vb
Dim arrZ(-1) As String
```

다음과 같은 경우 길이가 0인 배열을 만들어야 할 수도 있습니다.

- 위험 없이 <xref:System.NullReferenceException> 예외를 코드의 멤버에 액세스 해야 합니다는 <xref:System.Array> 클래스와 같이 <xref:System.Array.Length%2A> 또는 <xref:System.Array.Rank%2A>와 같은 Visual Basic 함수를 호출 하거나 <xref:Microsoft.VisualBasic.Information.UBound%2A>합니다.

- 확인 하지 않고 코드를 단순하게 유지 하려는 `Nothing` 특수 한 경우.

- 코드가 하나 이상의 프로시저에 길이가 0인 배열을 전달해야 하거나 하나 이상의 프로시저에서 길이가 0인 배열을 반환하는 API(애플리케이션 프로그래밍 인터페이스)와 상호 작용하는 경우

## <a name="splitting-an-array"></a>배열 분

경우에 따라 여러 배열을 단일 배열로 분할 해야 합니다. 분할할 배열 되는 점을 식별 하 고 다음 배열 두 개 이상의 별도 배열로 스 피팅이 포함 됩니다.

> [!NOTE]
> 이 섹션에서는 단일 문자열 구분 기호에 따라 문자열 배열로 분할 하는 것을 설명 하지 않습니다. 문자열 분할에 대 한 내용은 참조는 <xref:System.String.Split%2A?displayProperty=nameWithType> 메서드.

배열 분할에 대 한 가장 일반적인 기준은 다음과 같습니다.

- 배열의 요소 수입니다. 예를 들어 다음 배열의 지정 된 수의 요소를 보다 다양 한 약 균등 한 부분으로 분할 하는 것이 좋습니다. 이 작업을 위해 값을 반환 하거나 사용할 수는 <xref:System.Array.Length%2A?displayProperty=nameWithType> 또는 <xref:System.Array.GetLength%2A?displayProperty=nameWithType> 메서드.

- 배열의 위치를 나타내는 구분 기호로 사용 되는 요소의 값을 분할 해야 합니다. 호출 하 여 특정 값을 검색할 수 있습니다 합니다 <xref:System.Array.FindIndex%2A?displayProperty=nameWithType> 고 <xref:System.Array.FindLastIndex%2A?displayProperty=nameWithType> 메서드.

다음 호출 하 여 개별 배열 배열을 분할 해야 하는 인덱스를 결정 한 후 만들면는 <xref:System.Array.Copy%2A?displayProperty=nameWithType> 메서드.

다음 예제에서는 두 개의 배열로 대략 동일한 크기의 배열을 분할합니다. (배열 요소의 총 홀수 이면 첫 번째 배열에 두 번째 보다 더 많은 요소가 하나 있습니다.)

[!code-vb[splitting-an-array-by-length](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/split1.vb)]

다음 예제에서는 문자열 배열 값이 배열 구분 기호로 사용 되는 "zzz" 요소의 유무에 따라 두 개의 배열을 분할 합니다. 새 배열 구분 기호를 포함 하는 요소를 포함 하지 않습니다.

[!code-vb[splitting-an-array-by-delimiter](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/split2.vb)]

## <a name="joining-arrays"></a>배열에 가입

또한 단일 큰 배열을 배열의 수를 결합할 수 있습니다. 또한 사용이 작업을 수행 하는 <xref:System.Array.Copy%2A?displayProperty=nameWithType> 메서드.

> [!NOTE]
> 이 섹션에서는 문자열 배열을 단일 문자열로 조인 하는 것을 설명 하지 않습니다. 조인 하는 문자열 배열에 대 한 내용은 참조는 <xref:System.String.Join%2A?displayProperty=nameWithType> 메서드.

각 배열의 요소를 새 배열에 복사 하기 전에 먼저 새 배열에 맞게 충분히 큰 되도록 배열 초기화 확인 해야 합니다. 이 작업은 다음 두 가지 방법 중 하나로 수행할 수 있습니다.

- 사용 된 [ `ReDim Preserve` ](../../../language-reference/statements/redim-statement.md) 문을 동적으로 배열에 새 요소를 추가 하기 전에 확장. 이것이 가장 쉬운 방법 이지만 대형 배열을 복사 하는 경우 성능 저하 및 과도 한 메모리 소비에서 발생할 수 있습니다.
- 새 큰 배열에 대해 필요한 요소의 총 수를 계산 다음 원본 배열의 각 요소를 추가 합니다.

다음 예제에서는 10 개의 요소를 사용 하 여 4 개의 배열을 단일 배열로에 추가할 두 번째 방법을 사용 합니다.

[!code-vb[joining-an-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/join.vb)]

되므로 경우 원본 배열의 모든 작은, 각 새 배열의 요소를 추가 하는 대로 배열 동적으로 확장 수 있습니다. 다음 예제에서는 해당 작업을 수행합니다.

[!code-vb[joining-an-array-dynamically](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/join2.vb)]

## <a name="collections-as-an-alternative-to-arrays"></a>배열의 대 안으로 컬렉션

배열은 고정된 개수의 강력한 형식 개체를 만들고 작업하는 데 가장 유용합니다. 컬렉션은 개체 그룹에 대해 작업하는 보다 유연한 방법을 제공합니다. 배열과 달리,이 있는 배열의 크기를 명시적으로 변경 하는 필요 합니다 [ `ReDim` 문](../../../language-reference/statements/redim-statement.md), 컬렉션 증가 및는 응용 프로그램 변경이 필요에 따라 동적으로 축소 합니다.

사용 하는 경우 `ReDim` 배열 차원을, Visual Basic 새 배열을 만듭니다를 이전을 해제 합니다. 이 경우 실행 시간이 걸립니다. 따라서 자주 변경 되거나 사용 중인 항목 수가 필요한 항목의 최대 수를 예측할 수 없습니다, 하는 경우 일반적으로 얻을 수 더 나은 성능을 컬렉션을 사용 합니다.

일부 컬렉션의 경우 키를 사용하여 개체를 신속하게 검색할 수 있도록 컬렉션에 추가하는 모든 개체에 키를 할당할 수 있습니다.

컬렉션에 단일 데이터 형식의 요소만 포함된 경우 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임스페이스의 클래스 중 하나를 사용할 수 있습니다. 제네릭 컬렉션은 다른 데이터 형식을 추가할 수 없도록 형식 안전성을 적용합니다.

항목 컬렉션에 대한 자세한 내용은 [컬렉션](../../concepts/collections.md)을 참조하세요.

## <a name="related-topics"></a>관련 항목

|용어|정의|
|----------|----------------|
|[Array Dimensions in Visual Basic](../../language-features/arrays/array-dimensions.md)|배열의 차수 및 차원을 설명합니다.|
|[방법: Visual Basic에서 배열 변수 초기화](../../language-features/arrays/how-to-initialize-an-array-variable.md)|배열에 초기 값을 채우는 방법을 설명합니다.|
|[방법: Visual Basic에서 배열 정렬](../../language-features/arrays/how-to-sort-an-array.md)|배열의 요소를 사전순으로 정렬하는 방법을 보여 줍니다.|
|[방법: 하나의 배열에 다른 배열 할당](../../language-features/arrays/how-to-assign-one-array-to-another-array.md)|다른 배열 변수에 배열을 할당하는 규칙 및 단계를 설명합니다.|
|[배열 문제 해결](../../language-features/arrays/troubleshooting-arrays.md)|배열에서 작업할 때 발생할 수 있는 몇 가지 일반적인 문제를 설명합니다.|

## <a name="see-also"></a>참고 항목

- <xref:System.Array?displayProperty=nameWithType>
- [Dim 문](../../../language-reference/statements/dim-statement.md)
- [ReDim 문](../../../language-reference/statements/redim-statement.md)
