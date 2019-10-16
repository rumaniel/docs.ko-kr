---
title: '방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET Framework], reflection emit
- generics [.NET Framework], dynamic types
- reflection emit, generic types
ms.assetid: 07d5f01a-7b5b-40ea-9b15-f21561098fe4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b9781e7ef8edde182a13779a01e042cb44c92881
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045991"
---
# <a name="how-to-define-a-generic-type-with-reflection-emit"></a>방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의
이 항목에서는 두 개의 형식 매개 변수가 있는 간단한 제네릭 형식을 만드는 방법, 형식 매개 변수에 클래스 제약 조건, 인터페이스 제약 조건, 특수 제약 조건을 적용하는 방법, 클래스의 형식 매개 변수를 매개 변수 형식 및 반환 형식으로 사용하는 멤버를 만드는 방법을 보여 줍니다.  
  
> [!IMPORTANT]
> 제네릭 형식에 속하고 해당 형식의 형식 매개 변수를 사용한다고 해서 제네릭 메서드가 되는 것은 아닙니다. 고유한 형식 매개 변수 목록을 포함하는 경우에만 제네릭 메서드입니다. 제네릭 형식의 메서드는 대부분 이 예제와 같이 제네릭 메서드가 아닙니다. 제네릭 메서드를 내보내는 예제는 [방법: 리플렉션 내보내기를 사용하여 제네릭 메서드 정의](how-to-define-a-generic-method-with-reflection-emit.md)를 참조하세요.  
  
### <a name="to-define-a-generic-type"></a>제네릭 형식을 정의하려면  
  
1. `GenericEmitExample1`이라는 동적 어셈블리를 정의합니다. 이 예제에서는 어셈블리가 실행되고 디스크에 저장되므로 <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndSave?displayProperty=nameWithType>이 지정됩니다.  
  
     [!code-cpp[EmitGenericType#2](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#2)]
     [!code-csharp[EmitGenericType#2](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#2)]
     [!code-vb[EmitGenericType#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#2)]  
  
2. 동적 모듈을 정의합니다. 어셈블리는 실행 모듈로 구성됩니다. 단일 모듈 어셈블리의 경우 모듈 이름은 어셈블리 이름과 같고, 파일 이름은 모듈 이름에 확장명을 추가한 이름입니다.  
  
     [!code-cpp[EmitGenericType#3](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#3)]
     [!code-csharp[EmitGenericType#3](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#3)]
     [!code-vb[EmitGenericType#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#3)]  
  
3. 클래스를 정의합니다. 이 예제에서 클래스 이름은 `Sample`입니다.  
  
     [!code-cpp[EmitGenericType#4](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#4)]
     [!code-csharp[EmitGenericType#4](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#4)]
     [!code-vb[EmitGenericType#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#4)]  
  
4. 매개 변수 이름이 포함된 문자열 배열을 <xref:System.Reflection.Emit.TypeBuilder.DefineGenericParameters%2A?displayProperty=nameWithType> 메서드에 전달하여 `Sample`의 제네릭 형식 매개 변수를 정의합니다. 이렇게 하면 클래스가 제네릭 형식이 됩니다. 반환 값은 내보낸 코드에서 사용할 수 있는 형식 매개 변수를 나타내는 <xref:System.Reflection.Emit.GenericTypeParameterBuilder> 개체 배열입니다.  
  
     다음 코드에서 `Sample`은 형식 매개 변수 `TFirst` 및 `TSecond`가 있는 제네릭 형식이 됩니다. 코드를 읽기 쉽도록 각 <xref:System.Reflection.Emit.GenericTypeParameterBuilder>는 형식 매개 변수와 동일한 이름을 가진 변수에 배치됩니다.  
  
     [!code-cpp[EmitGenericType#5](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#5)]
     [!code-csharp[EmitGenericType#5](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#5)]
     [!code-vb[EmitGenericType#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#5)]  
  
5. 형식 매개 변수에 특수 제약 조건을 추가합니다. 이 예제에서 형식 매개 변수 `TFirst`는 매개 변수가 없는 생성자를 가진 형식과 참조 형식으로 제한됩니다.  
  
     [!code-cpp[EmitGenericType#6](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#6)]
     [!code-csharp[EmitGenericType#6](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#6)]
     [!code-vb[EmitGenericType#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#6)]  
  
6. 필요에 따라 형식 매개 변수에 클래스 및 인터페이스 제약 조건을 추가합니다. 이 예제에서 형식 매개 변수 `TFirst`는 `baseType` 변수에 포함된 <xref:System.Type> 개체가 나타내는 기본 클래스에서 파생되고 `interfaceA` 및 `interfaceB` 변수에 포함된 형식의 인터페이스를 구현하는 형식으로 제한됩니다. 이러한 변수의 선언 및 할당은 코드 예제를 참조하세요.  
  
     [!code-cpp[EmitGenericType#7](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#7)]
     [!code-csharp[EmitGenericType#7](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#7)]
     [!code-vb[EmitGenericType#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#7)]  
  
7. 필드를 정의합니다. 이 예제에서 필드 형식은 형식 매개 변수 `TFirst`로 지정됩니다. <xref:System.Reflection.Emit.GenericTypeParameterBuilder>는 <xref:System.Type>에서 파생되므로 형식을 사용할 수 있는 어디에서든 제네릭 형식 매개 변수를 사용할 수 있습니다.  
  
     [!code-cpp[EmitGenericType#21](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#21)]
     [!code-csharp[EmitGenericType#21](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#21)]
     [!code-vb[EmitGenericType#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#21)]  
  
8. 제네릭 형식의 형식 매개 변수를 사용하는 메서드를 정의합니다. 이러한 메서드는 고유한 형식 매개 변수 목록이 없을 경우 제네릭 메서드가 아닙니다. 다음 코드는 `TFirst` 배열을 사용하고배열의 모든 요소가 포함된 `List<TFirst>`(Visual Basic에서는 `List(Of TFirst)`)를 반환하는 `static` 메서드(Visual Basic에서는 `Shared`)를 정의합니다. 이 메서드를 정의하려면 제네릭 형식 정의 `List<T>`에 대해 <xref:System.Type.MakeGenericType%2A>을 호출하여 `List<TFirst>` 형식을 만들어야 합니다. `typeof` 연산자(Visual Basic에서는 `GetType`)를 사용하여 제네릭 형식 정의를 가져오는 경우 `T`가 생략됩니다. 매개 변수 형식은 <xref:System.Type.MakeArrayType%2A> 메서드를 사용하여 생성됩니다.  
  
     [!code-cpp[EmitGenericType#22](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#22)]
     [!code-csharp[EmitGenericType#22](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#22)]
     [!code-vb[EmitGenericType#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#22)]  
  
9. 메서드 본문을 내보냅니다. 메서드 본문은 입력 배열을 스택에 로드하고 `IEnumerable<TFirst>`(입력 요소를 목록에 넣는 모든 작업 수행)를 사용하는 `List<TFirst>` 생성자를 호출하고 반환하는 세 개의 opcode로 구성됩니다(스택에 새 <xref:System.Collections.Generic.List%601> 개체를 남김). 이 코드를 내보내는 작업의 어려운 부분은 생성자를 가져오는 것입니다.  
  
     <xref:System.Type.GetConstructor%2A> 메서드는 <xref:System.Reflection.Emit.GenericTypeParameterBuilder>에서 지원되지 않으므로 `List<TFirst>`의 생성자를 직접 가져올 수 없습니다. 먼저 제네릭 형식 정의 `List<T>`의 생성자를 가져온 다음 해당하는 `List<TFirst>`의 생성자로 변환하는 메서드를 호출해야 합니다.  
  
     이 코드 예제에 사용되는 생성자는 `IEnumerable<T>`을 사용합니다. 그러나 <xref:System.Collections.Generic.IEnumerable%601> 제네릭 인터페이스의 제네릭 형식 정의는 아니며, `List<T>`의 형식 매개 변수 `T`를 `IEnumerable<T>`의 형식 매개 변수 `T` 대신 사용해야 합니다. 이는 두 형식에 모두 `T`라는 형식 매개 변수가 있기 때문에 혼동을 주는 것 같습니다. 이 때문에 이 코드 예제에서는 `TFirst` 및 `TSecond`라는 이름을 사용합니다. 생성자 인수의 형식의 가져오려면 제네릭 형식 정의 `IEnumerable<T>`로 시작하고 `List<T>`의 첫 번째 제네릭 형식 매개 변수를 사용하여 <xref:System.Type.MakeGenericType%2A>을 호출합니다. 생성자 인수 목록은 배열로 전달되어야 합니다. 여기서는 하나의 인수만 전달됩니다.  
  
    > [!NOTE]
    > 제네릭 형식 정의는 C#에서 `typeof` 연산자를 사용하는 경우 `IEnumerable<>`로 표현되고, Visual Basic에서 `IEnumerable(Of )` 연산자를 사용하는 경우 `GetType`로 표현됩니다.  
  
     이제 제네릭 형식 정의에서 <xref:System.Type.GetConstructor%2A>를 호출하여 `List<T>`의 생성자를 가져올 수 있습니다. 이 생성자를 해당하는 `List<TFirst>`의 생성자로 변환하려면 `List<TFirst>` 및 `List<T>`의 생성자를 static <xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29?displayProperty=nameWithType> 메서드에 전달합니다.  
  
     [!code-cpp[EmitGenericType#23](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#23)]
     [!code-csharp[EmitGenericType#23](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#23)]
     [!code-vb[EmitGenericType#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#23)]  
  
10. 형식을 만들고 파일을 저장합니다.  
  
     [!code-cpp[EmitGenericType#8](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#8)]
     [!code-csharp[EmitGenericType#8](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#8)]
     [!code-vb[EmitGenericType#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#8)]  
  
11. 메서드를 호출합니다. `ExampleMethod`는 제네릭이 아니지만 이 메서드가 속하는 형식이 제네릭이므로 호출할 수 있는 <xref:System.Reflection.MethodInfo>를 가져오려면 `Sample`에 대한 형식 정의에서 생성된 형식을 만들어야 합니다. 생성된 형식은 매개 변수가 없는 기본 생성자를 가진 참조 형식이므로 `Example`의 제약 조건을 충족하는 `TFirst` 클래스 및 `TSecond`의 제약 조건을 충족하는 `ExampleDerived` 클래스를 사용합니다. `ExampleDerived`에 대한 코드는 예제 코드 섹션에서 확인할 수 있습니다. 이러한 두 형식이 <xref:System.Type.MakeGenericType%2A>에 전달되어 생성된 형식을 만듭니다. 그런 다음 <xref:System.Type.GetMethod%2A> 메서드를 사용하여 <xref:System.Reflection.MethodInfo>를 가져옵니다.  
  
     [!code-cpp[EmitGenericType#9](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#9)]
     [!code-csharp[EmitGenericType#9](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#9)]
     [!code-vb[EmitGenericType#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#9)]  
  
12. 다음 코드는 `Example` 개체 배열을 만들고 호출할 메서드의 인수를 나타내는 <xref:System.Object> 형식의 배열에 해당 배열을 배치한 다음 <xref:System.Reflection.MethodBase.Invoke%28System.Object%2CSystem.Object%5B%5D%29> 메서드에 전달합니다. <xref:System.Reflection.MethodBase.Invoke%2A> 메서드가 `static`이기 때문에 해당 메서드의 첫 번째 인수는 null 참조입니다.  
  
     [!code-cpp[EmitGenericType#10](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#10)]
     [!code-csharp[EmitGenericType#10](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#10)]
     [!code-vb[EmitGenericType#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#10)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 기본 클래스 및 두 개의 인터페이스와 함께 `Sample`이라는 클래스를 정의합니다. 프로그램은 `Sample`에 대한 두 개의 제네릭 형식 매개 변수를 정의하고 제네릭 형식으로 변환합니다. 형식 매개 변수를 통해서만 제네릭 형식을 만들 수 있습니다. 프로그램은 형식 매개 변수 정의 앞과 뒤에 테스트 메시지를 표시하여 이를 보여 줍니다.  
  
 형식 매개 변수 `TSecond`는 기본 클래스 및 인터페이스를 통해 클래스 및 인터페이스 제약 조건을 보여 주는 데 사용되고, 형식 매개 변수 `TFirst`는 특수 제약 조건을 보여 주는 데 사용됩니다.  
  
 코드 예제에서는 필드 형식과 메서드의 매개 변수 및 반환 형식에 대해 클래스의 형식 매개 변수를 사용하여 필드와 메서드를 정의합니다.  
  
 `Sample` 클래스를 만든 후 메서드가 호출됩니다.  
  
 프로그램에는 제네릭 형식에 대한 정보를 나열하는 메서드 및 형식 매개 변수에 대한 특수 제약 조건을 나열하는 메서드가 포함되어 있습니다. 이러한 메서드는 완성된 `Sample` 클래스에 대한 정보를 표시하는 데 사용됩니다.  
  
 프로그램은 완성된 모듈을 디스크에 `GenericEmitExample1.dll`로 저장하므로 [Ildasm.exe(IL 디스어셈블러)](../tools/ildasm-exe-il-disassembler.md)를 사용하여 열고 `Sample` 클래스에 대한 MSIL을 검사할 수 있습니다.  
  
 [!code-cpp[EmitGenericType#1](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#1)]
 [!code-csharp[EmitGenericType#1](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#1)]
 [!code-vb[EmitGenericType#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.Emit.GenericTypeParameterBuilder>
- [리플렉션 내보내기 사용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y322t50(v=vs.100))
- [리플렉션 내보내기 동적 어셈블리 시나리오](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/tt9483fk(v=vs.100))
