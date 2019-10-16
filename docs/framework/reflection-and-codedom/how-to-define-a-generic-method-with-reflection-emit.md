---
title: '방법: 리플렉션 내보내기를 사용하여 제네릭 메서드 정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics [.NET Framework], reflection emit
- reflection emit, generic methods
- generics [.NET Framework], dynamic types
ms.assetid: 93892fa4-90b3-4ec4-b147-4bec9880de2b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 857bad224d1a88c7011a42d0595b17b1810381aa
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046052"
---
# <a name="how-to-define-a-generic-method-with-reflection-emit"></a>방법: 리플렉션 내보내기를 사용하여 제네릭 메서드 정의

첫 번째 절차에서는 두 개의 형식 매개 변수가 있는 간단한 제네릭 메서드를 만드는 방법 및 형식 매개 변수에 클래스 제약 조건, 인터페이스 제약 조건 및 특수 제약 조건을 적용하는 방법을 보여 줍니다.

두 번째 절차에서는 메서드 본문을 내보내는 방법 및 제네릭 메서드의 형식 매개 변수를 사용하여 제네릭 형식 인스턴스를 만들고 해당 메서드를 호출하는 방법을 보여 줍니다.

세 번째 절차에서는 제네릭 메서드를 호출하는 방법을 보여 줍니다.

> [!IMPORTANT]
> 제네릭 형식에 속하고 해당 형식의 형식 매개 변수를 사용한다고 해서 제네릭 메서드가 되는 것은 아닙니다. 고유한 형식 매개 변수 목록을 포함하는 경우에만 제네릭 메서드입니다. 제네릭 메서드는 이 예제와 같이 제네릭이 아닌 형식에 나타날 수 있습니다. 제네릭 형식의 제네릭이 아닌 메서드에 대한 예제는 [방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의](how-to-define-a-generic-type-with-reflection-emit.md)를 참조하세요.

### <a name="to-define-a-generic-method"></a>제네릭 메서드를 정의하려면

1. 시작하기 전에, 상위 수준 언어를 사용하여 작성할 경우 제네릭 메서드가 표시되는 방식을 확인하는 것이 좋습니다. 이 항목에 대한 예제 코드에는 제네릭 메서드를 호출하는 코드와 함께 다음 코드가 포함되어 있습니다. 메서드에는 두 개의 형식 매개 변수 `TInput` 및 `TOutput`이 있습니다. 두 번째 매개 변수는 참조 형식(`class`)이어야 하고, 매개 변수가 없는 생성자(`new`)를 포함해야 하며, `ICollection(Of TInput)`(C#에서는 `ICollection<TInput>`)을 구현해야 합니다. 이 인터페이스 제약 조건은 <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> 메서드를 사용하여 이 메서드가 만드는 `TOutput` 컬렉션에 요소를 추가할 수 있도록 합니다. 메서드에는 `TInput` 배열인 하나의 형식 매개 변수 `input`이 있습니다. 메서드는 `TOutput` 형식의 컬렉션을 만들고 `input`의 요소를 컬렉션에 복사합니다.

    [!code-csharp[GenericMethodHowTo#20](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#20)]
    [!code-vb[GenericMethodHowTo#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#20)]

2. 제네릭 메서드가 속하는 형식을 포함할 동적 모듈 및 동적 어셈블리를 정의합니다. 이 경우 어셈블리에는 `DemoMethodBuilder1`이라는 모듈 하나만 포함되며, 모듈 이름은 어셈블리 이름에 확장명을 추가한 이름과 같습니다. 이 예제에서는 어셈블리가 디스크에 저장되고 실행되므로 <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndSave?displayProperty=nameWithType>이 지정됩니다. [Ildasm.exe(IL 디스어셈블러)](../tools/ildasm-exe-il-disassembler.md)를 사용하여 DemoMethodBuilder1.dll를 검사하고 1단계에 표시된 메서드에 대한 MSIL(Microsoft Intermediate Language)과 비교합니다.

    [!code-csharp[GenericMethodHowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#2)]
    [!code-vb[GenericMethodHowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#2)]

3. 제네릭 메서드가 속하는 형식을 정의합니다. 제네릭 형식일 필요는 없습니다. 제네릭 메서드는 제네릭 형식 또는 제네릭이 아닌 형식에 속할 수 있습니다. 이 예제에서 형식은 클래스이고, 제네릭이 아니며, 이름이 `DemoType`입니다.

    [!code-csharp[GenericMethodHowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#3)]
    [!code-vb[GenericMethodHowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#3)]

4. 제네릭 메서드를 정의합니다. 제네릭 메서드의 공식 매개 변수 형식이 제네릭 메서드의 제네릭 형식 매개 변수로 지정된 경우 <xref:System.Reflection.Emit.TypeBuilder.DefineMethod%28System.String%2CSystem.Reflection.MethodAttributes%29> 메서드 오버로드를 사용하여 메서드를 정의합니다. 메서드의 제네릭 형식 매개 변수는 아직 정의되지 않았으므로 <xref:System.Reflection.Emit.TypeBuilder.DefineMethod%2A> 호출에서 메서드의 공식 매개 변수 형식을 지정할 수 없습니다. 이 예제에서 메서드 이름은 `Factory`입니다. 메서드가 public이고 `static`(Visual Basic에서는 `Shared`)입니다.

    [!code-csharp[GenericMethodHowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#4)]
    [!code-vb[GenericMethodHowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#4)]

5. 매개 변수 이름이 포함된 문자열 배열을 <xref:System.Reflection.Emit.MethodBuilder.DefineGenericParameters%2A?displayProperty=nameWithType> 메서드에 전달하여 `DemoMethod`의 제네릭 형식 매개 변수를 정의합니다. 이렇게 하면 메서드가 제네릭 메서드가 됩니다. 다음 코드에서는 형식 매개 변수 `TInput` 및 `TOutput`을 사용하여 `Factory`를 제네릭 메서드로 만듭니다. 코드를 읽기 쉽도록 두 개의 형식 매개 변수를 나타내는 <xref:System.Reflection.Emit.GenericTypeParameterBuilder> 개체를 포함하기 위해 이러한 이름을 가진 변수가 생성되었습니다.

    [!code-csharp[GenericMethodHowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#5)]
    [!code-vb[GenericMethodHowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#5)]

6. 필요에 따라 형식 매개 변수에 특수 제약 조건을 추가합니다. 특수 제약 조건은 <xref:System.Reflection.Emit.GenericTypeParameterBuilder.SetGenericParameterAttributes%2A> 메서드를 사용하여 추가됩니다. 이 예제에서 `TOutput`은 참조 형식으로, 매개 변수가 없는 생성자를 갖도록 제한됩니다.

    [!code-csharp[GenericMethodHowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#6)]
    [!code-vb[GenericMethodHowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#6)]

7. 필요에 따라 형식 매개 변수에 클래스 및 인터페이스 제약 조건을 추가합니다. 이 예제에서 형식 매개 변수 `TOutput`은 `ICollection(Of TInput)`(C#에서는 `ICollection<TInput>`) 인터페이스를 구현하는 형식으로 제한됩니다. 이렇게 하면 <xref:System.Collections.Generic.ICollection%601.Add%2A> 메서드를 사용하여 요소를 추가할 수 있습니다.

    [!code-csharp[GenericMethodHowTo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#7)]
    [!code-vb[GenericMethodHowTo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#7)]

8. <xref:System.Reflection.Emit.MethodBuilder.SetParameters%2A> 메서드를 사용하여 메서드의 공식 매개 변수를 정의합니다. 이 예제에서 `Factory` 메서드에는 `TInput` 배열인 매개 변수 하나가 있습니다. `TInput`을 나타내는 <xref:System.Reflection.Emit.GenericTypeParameterBuilder>에서 <xref:System.Type.MakeArrayType%2A> 메서드를 호출하면 이 형식이 생성됩니다. <xref:System.Reflection.Emit.MethodBuilder.SetParameters%2A>의 인수는 <xref:System.Type> 개체 배열입니다.

    [!code-csharp[GenericMethodHowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#8)]
    [!code-vb[GenericMethodHowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#8)]

9. <xref:System.Reflection.Emit.MethodBuilder.SetReturnType%2A> 메서드를 사용하여 메서드의 반환 형식을 정의합니다. 이 예제에서는 `TOutput` 인스턴스가 반환됩니다.

    [!code-csharp[GenericMethodHowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#9)]
    [!code-vb[GenericMethodHowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#9)]

10. <xref:System.Reflection.Emit.ILGenerator>를 사용하여 메서드 본문을 내보냅니다. 자세한 내용은 다음에 나오는 메서드 본문을 내보내기 위한 절차를 참조하십시오.

    > [!IMPORTANT]
    > 제네릭 형식의 메서드 호출을 내보내고 이러한 형식의 형식 인수가 제네릭 메서드의 형식 매개 변수인 경우 <xref:System.Reflection.Emit.TypeBuilder> 클래스의 `static`<xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29>, <xref:System.Reflection.Emit.TypeBuilder.GetMethod%28System.Type%2CSystem.Reflection.MethodInfo%29> 및 <xref:System.Reflection.Emit.TypeBuilder.GetField%28System.Type%2CSystem.Reflection.FieldInfo%29> 메서드 오버로드를 사용하여 생성된 형식의 메서드를 가져옵니다. 자세한 내용은 다음에 나오는 메서드 본문을 내보내는 절차를 참조하세요.

11. 메서드를 포함하는 형식을 완성하고 어셈블리를 저장합니다. 다음에 나오는 제네릭 메서드 호출에 대한 절차에서는 완성된 메서드를 호출하는 두 가지 방법을 보여 줍니다.

    [!code-csharp[GenericMethodHowTo#14](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#14)]
    [!code-vb[GenericMethodHowTo#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#14)]

<a name="procedureSection1"></a>

### <a name="to-emit-the-method-body"></a>메서드 본문을 내보내려면

1. 코드 생성기를 가져오고 지역 변수와 레이블을 선언합니다. <xref:System.Reflection.Emit.ILGenerator.DeclareLocal%2A> 메서드는 지역 변수를 선언하는 데 사용됩니다. `Factory` 메서드에는 4개의 지역 변수가 있습니다. `retVal`은 메서드에서 반환되는 새 `TOutput`을 포함하고, `ic`는 `ICollection(Of TInput)`(C#에서는 `ICollection<TInput>`)으로 캐스팅된 `TOutput`을 포함하고, `input`은 `TInput` 개체의 입력 배열을 포함하고, `index`는 배열을 반복합니다. 메서드에는 루프를 시작하는 레이블(`enterLoop`)과 <xref:System.Reflection.Emit.ILGenerator.DefineLabel%2A> 메서드를 사용하여 정의된 루프 맨 위 레이블(`loopAgain`)이 있습니다.

    메서드에서 수행하는 첫 번째 작업은 <xref:System.Reflection.Emit.OpCodes.Ldarg_0> opcode를 사용하여 해당 인수를 로드하고 <xref:System.Reflection.Emit.OpCodes.Stloc_S> opcode를 사용하여 지역 변수 `input`에 저장하는 것입니다.

    [!code-csharp[GenericMethodHowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#10)]
    [!code-vb[GenericMethodHowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#10)]

2. <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> 메서드의 제네릭 메서드 오버로드를 사용하여 `TOutput` 인스턴스를 만드는 코드를 내보냅니다. 이 오버로드를 사용하려면 지정된 형식이 매개 변수가 없는 생성자를 포함해야 하며, 이런 이유로 해당 제약 조건을 `TOutput`에 추가합니다. `TOutput`을 <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A>에 전달하여 생성된 제네릭 메서드를 만듭니다. 메서드를 호출하는 코드를 내보낸 후 <xref:System.Reflection.Emit.OpCodes.Stloc_S>를 사용하여 지역 변수 `retVal`에 저장하는 코드를 내보냅니다.

    [!code-csharp[GenericMethodHowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#11)]
    [!code-vb[GenericMethodHowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#11)]

3. 새 `TOutput` 개체를 `ICollection(Of TInput)`으로 캐스팅하고 지역 변수 `ic`에 저장하는 코드를 내보냅니다.

    [!code-csharp[GenericMethodHowTo#31](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#31)]
    [!code-vb[GenericMethodHowTo#31](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#31)]

4. <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> 메서드를 나타내는 <xref:System.Reflection.MethodInfo>를 가져옵니다. 메서드는 `ICollection(Of TInput)`(C#에서는 `ICollection<TInput>`)에 대해 작동하므로 생성된 해당 형식과 관련된 `Add` 메서드를 가져와야 합니다. <xref:System.Type.GetMethod%2A>는 <xref:System.Reflection.Emit.GenericTypeParameterBuilder>로 생성된 형식에서 지원되지 않으므로 <xref:System.Type.GetMethod%2A> 메서드를 사용하여 이 <xref:System.Reflection.MethodInfo>를 `icollOfTInput`에서 직접 가져올 수 없습니다. 대신, <xref:System.Collections.Generic.ICollection%601> 제네릭 인터페이스에 대한 제네릭 형식 정의를 포함하는 `icoll`에서 <xref:System.Type.GetMethod%2A>를 호출합니다. 그런 다음 <xref:System.Reflection.Emit.TypeBuilder.GetMethod%28System.Type%2CSystem.Reflection.MethodInfo%29>`static` 메서드를 사용하여 생성된 형식에 대한 <xref:System.Reflection.MethodInfo>를 생성합니다. 다음 코드에서는 이 작업을 보여 줍니다.

    [!code-csharp[GenericMethodHowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#12)]
    [!code-vb[GenericMethodHowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#12)]

5. 32비트 정수 0을 로드하고 변수에 저장하여 `index` 변수를 초기화하는 코드를 내보냅니다. `enterLoop` 레이블로 분기하는 코드를 내보냅니다. 이 레이블은 루프 내에 있기 때문에 아직 표시되지 않았습니다. 다음 단계에서는 루프에 대한 코드를 내보냅니다.

    [!code-csharp[GenericMethodHowTo#32](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#32)]
    [!code-vb[GenericMethodHowTo#32](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#32)]

6. 루프에 대한 코드를 내보냅니다. 첫 번째 단계는 `loopAgain` 레이블로 <xref:System.Reflection.Emit.ILGenerator.MarkLabel%2A>을 호출하여 루프 맨 위를 표시하는 것입니다. 이제 레이블을 사용하는 분기 문이 코드의 이 지점으로 분기됩니다. 다음 단계는 `ICollection(Of TInput)`으로 캐스팅된 `TOutput` 개체를 스택에 푸시하는 것입니다. 즉시 필요하지는 않지만 `Add` 메서드를 호출하려면 제자리에 있어야 합니다. 그다음 입력 배열이 스택에 푸시되고 현재 인덱스를 포함하는 `index` 변수가 배열에 푸시됩니다. <xref:System.Reflection.Emit.OpCodes.Ldelem> opcode는 스택에서 인덱스 및 배열을 팝하고 인덱싱된 배열 요소를 스택에 푸시합니다. 이제 스택이 <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> 메서드를 호출할 준비가 되었습니다. 컬렉션과 새 요소가 스택에서 팝되고 컬렉션에 요소가 추가됩니다.

    루프의 나머지 코드는 인덱스 및 테스트를 증가시켜 루프가 완료되었는지 여부를 확인합니다. 인덱스와 32비트 정수 1이 스택에 푸시되고 추가되어 스택에 합계가 남습니다. 합계는 `index`에 저장됩니다. <xref:System.Reflection.Emit.ILGenerator.MarkLabel%2A>이 호출되어 이 지점을 루프에 대한 진입점으로 설정합니다. 인덱스가 다시 로드됩니다. 입력 배열이 스택에 푸시되고 해당 길이를 가져오기 위해 <xref:System.Reflection.Emit.OpCodes.Ldlen>이 내보내집니다. 이제 인덱스 및 길이가 스택에 있으며 비교를 위해 <xref:System.Reflection.Emit.OpCodes.Clt>가 내보내집니다. 인덱스가 길이보다 작으면 <xref:System.Reflection.Emit.OpCodes.Brtrue_S>가 루프의 시작 부분으로 다시 분기됩니다.

    [!code-csharp[GenericMethodHowTo#13](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#13)]
    [!code-vb[GenericMethodHowTo#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#13)]

7. `TOutput` 개체를 스택에 푸시하는 코드를 내보내고 메서드에서 반환합니다. 지역 변수 `retVal` 및 `ic` 둘 다에 새 `TOutput`에 대한 참조가 포함되어 있습니다. `ic`는 <xref:System.Collections.Generic.ICollection%601.Add%2A?displayProperty=nameWithType> 메서드에 액세스하는 데만 사용됩니다.

    [!code-csharp[GenericMethodHowTo#33](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#33)]
    [!code-vb[GenericMethodHowTo#33](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#33)]

<a name="procedureSection2"></a>

### <a name="to-invoke-the-generic-method"></a>제네릭 메서드를 호출하려면

1. `Factory`는 제네릭 메서드 정의입니다. 호출하려면 해당 제네릭 형식 매개 변수에 형식을 할당해야 합니다. 이렇게 하려면 <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A> 메서드를 사용합니다. 다음 코드에서는 `TInput`에 대해 <xref:System.String>을 지정하고 `TOutput`에 대해 `List(Of String)`(C#에서는 `List<string>`)을 지정하여 생성된 제네릭 메서드를 만들고 메서드의 문자열 표현을 표시합니다.

    [!code-csharp[GenericMethodHowTo#21](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#21)]
    [!code-vb[GenericMethodHowTo#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#21)]

2. 런타임에 바인딩된 메서드를 호출하려면 <xref:System.Reflection.MethodBase.Invoke%2A> 메서드를 사용합니다. 다음 코드는 유일한 요소로 문자열 배열을 포함하여 <xref:System.Object> 배열을 만들고 제네릭 메서드의 인수 목록으로 전달합니다. <xref:System.Reflection.MethodBase.Invoke%2A>의 첫 번째 매개 변수는 메서드가 `static`이므로 null 참조입니다. 반환 값은 `List(Of String)`로 캐스팅되며 첫 번째 요소가 표시됩니다.

    [!code-csharp[GenericMethodHowTo#22](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#22)]
    [!code-vb[GenericMethodHowTo#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#22)]

3. 대리자를 사용하여 메서드를 호출하려면 생성된 제네릭 메서드의 시그니처와 일치하는 대리자가 있어야 합니다. 이 작업을 수행하는 편리한 방법은 제네릭 대리자를 만드는 것입니다. 다음 코드는 <xref:System.Delegate.CreateDelegate%28System.Type%2CSystem.Reflection.MethodInfo%29?displayProperty=nameWithType> 메서드 오버로드를 사용하여 예제 코드에서 정의된 제네릭 대리자 `D`의 인스턴스를 만들고 대리자를 호출합니다. 대리자는 런타임에 바인딩된 호출보다 성능이 우수합니다.

    [!code-csharp[GenericMethodHowTo#23](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#23)]
    [!code-vb[GenericMethodHowTo#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#23)]

4. 저장된 어셈블리를 참조하는 프로그램에서 내보낸 메서드를 호출할 수도 있습니다.

## <a name="example"></a>예제

다음 코드 예제에서는 제네릭 메서드 `Factory`를 사용하여 제네릭이 아닌 형식 `DemoType`을 만듭니다. 이 메서드에는 두 개의 제네릭 형식 매개 변수가 있습니다. `TInput`은 입력 형식을 지정하고 `TOutput`은 출력 형식을 지정합니다. `TOutput` 형식 매개 변수는 `ICollection<TInput>`(Visual Basic에서는 `ICollection(Of TInput)`)을 매개 변수가 없는 생성자를 갖는 참조 형식으로 구현하도록 제한됩니다.

메서드에는 `TInput` 배열인 하나의 공식 매개 변수가 있습니다. 메서드는 입력 배열의 모든 요소를 포함하는 `TOutput` 인스턴스를 반환합니다. `TOutput`은 <xref:System.Collections.Generic.ICollection%601> 제네릭 인터페이스를 구현하는 제네릭 컬렉션 형식일 수 있습니다.

코드를 실행하면 동적 어셈블리가 DemoGenericMethod1.dll로 저장되며 [Ildasm.exe(IL 디스어셈블러)](../tools/ildasm-exe-il-disassembler.md)를 사용하여 검사할 수 있습니다.

> [!NOTE]
> 코드를 내보내는 방법을 알아보려면 내보내려는 작업을 수행하는 Visual Basic, C# 또는 Visual C++ 프로그램을 작성하고 디스어셈블러를 사용하여 컴파일러에 의해 생성된 MSIL을 검사하는 것이 좋습니다.

코드 예제에는 내보낸 메서드에 해당하는 소스 코드가 포함되어 있습니다. 내보낸 메서드는 런타임에 바인딩되고 코드 예제에서 선언된 제네릭 대리자를 사용하여 호출됩니다.

[!code-csharp[GenericMethodHowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/GenericMethodHowTo/CS/source.cs#1)]
[!code-vb[GenericMethodHowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GenericMethodHowTo/VB/source.vb#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.Emit.MethodBuilder>
- [방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의](how-to-define-a-generic-type-with-reflection-emit.md)
