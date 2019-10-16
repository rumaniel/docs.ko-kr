---
title: '방법: 동적 메서드 정의 및 실행'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reflection emit, dynamic methods
- dynamic methods
ms.assetid: 07d08a99-62c5-4254-bce2-2a75e55a18ab
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b5c6de2bde111ae459dbcfa1c0a7363d406f5f80
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928252"
---
# <a name="how-to-define-and-execute-dynamic-methods"></a>방법: 동적 메서드 정의 및 실행
다음 절차에서는 간단한 동적 메서드 및 클래스 인스턴스에 바인딩된 동적 메서드를 정의하고 실행하는 방법을 보여 줍니다. 동적 메서드에 대한 자세한 내용은 <xref:System.Reflection.Emit.DynamicMethod> 클래스 및 [리플렉션 내보내기 동적 메서드 시나리오](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sfk2s47t(v=vs.100))를 참조하세요.  
  
### <a name="to-define-and-execute-a-dynamic-method"></a>동적 메서드를 정의하고 실행하려면  
  
1. 메서드를 실행할 대리자 형식을 선언합니다. 제네릭 대리자를 사용하여 선언해야 하는 대리자 형식 수를 최소화하는 것이 좋습니다. 다음 코드는 `SquareIt` 메서드에 사용할 수 있는 두 개의 대리자 형식을 선언하며, 둘 중 하나는 제네릭입니다.  
  
     [!code-cpp[DynamicMethodHowTo#2](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#2)]
     [!code-csharp[DynamicMethodHowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#2)]
     [!code-vb[DynamicMethodHowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#2)]  
  
2. 동적 메서드에 대한 매개 변수 형식을 지정하는 배열을 만듭니다. 이 예제에서 유일한 매개 변수는 `int`(Visual Basic에서는 `Integer`)이므로 배열에 요소가 하나만 있습니다.  
  
     [!code-cpp[DynamicMethodHowTo#3](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#3)]
     [!code-csharp[DynamicMethodHowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#3)]
     [!code-vb[DynamicMethodHowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#3)]  
  
3. <xref:System.Reflection.Emit.DynamicMethod>를 만듭니다. 이 예제에서 메서드 이름은 `SquareIt`입니다.  
  
    > [!NOTE]
    > 동적 메서드에는 이름을 지정할 필요가 없으며, 이름으로 호출할 수 없습니다. 여러 동적 메서드가 동일한 이름을 가질 수 있습니다. 그러나 이름은 호출 스택에 표시되며 디버그하는 데 유용할 수 있습니다.  
  
     반환 값의 형식은 `long`으로 지정됩니다. 메서드는 예제 코드가 들어 있는 `Example` 클래스를 포함하는 모듈에 연결되어 있습니다. 로드된 모든 모듈을 지정할 수 있습니다. 동적 메서드는 모듈 수준 `static` 메서드(Visual Basic에서는 `Shared`)처럼 동작합니다.  
  
     [!code-cpp[DynamicMethodHowTo#4](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#4)]
     [!code-csharp[DynamicMethodHowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#4)]
     [!code-vb[DynamicMethodHowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#4)]  
  
4. 메서드 본문을 내보냅니다. 이 예제에서 <xref:System.Reflection.Emit.ILGenerator> 개체는 MSIL(Microsoft Intermediate Language)을 내보내는 데 사용됩니다. 또는 <xref:System.Reflection.Emit.DynamicILInfo> 개체를 비관리 코드 생성기와 함께 사용하여 <xref:System.Reflection.Emit.DynamicMethod>에 대한 메서드 본문을 내보낼 수 있습니다.  
  
     이 예제의 MSIL은 `int`인 인수를 스택에 로드하고, `long`으로 변환한 다음 `long`을 복제하고 두 개의 숫자를 곱합니다. 이렇게 하면 스택의 거듭제곱 결과가 구해지며, 메서드가 반환하기만 하면 됩니다.  
  
     [!code-cpp[DynamicMethodHowTo#5](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#5)]
     [!code-csharp[DynamicMethodHowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#5)]
     [!code-vb[DynamicMethodHowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#5)]  
  
5. <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> 메서드를 호출하여 동적 메서드를 나타내는 대리자 인스턴스(1단계에서 선언됨)를 만듭니다. 대리자를 만들면 메서드가 완성되고, MSIL 추가 등 메서드를 변경하려는 이후의 모든 시도는 무시됩니다. 다음 코드는 대리자를 만들고 제네릭 대리자를 사용하여 호출합니다.  
  
     [!code-cpp[DynamicMethodHowTo#6](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#6)]
     [!code-csharp[DynamicMethodHowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#6)]
     [!code-vb[DynamicMethodHowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#6)]  
  
### <a name="to-define-and-execute-a-dynamic-method-that-is-bound-to-an-object"></a>개체에 바인딩된 동적 메서드를 정의하고 실행하려면  
  
1. 메서드를 실행할 대리자 형식을 선언합니다. 제네릭 대리자를 사용하여 선언해야 하는 대리자 형식 수를 최소화하는 것이 좋습니다. 다음 코드는 매개 변수 하나가 있는 메서드 및 대리자가 개체에 바인딩된 경우 매개 변수 두 개와 반환 값이 있는 메서드를 실행하는 데 사용할 수 있는 제네릭 대리자 형식을 선언합니다.  
  
     [!code-cpp[DynamicMethodHowTo#12](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#12)]
     [!code-csharp[DynamicMethodHowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#12)]
     [!code-vb[DynamicMethodHowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#12)]  
  
2. 동적 메서드에 대한 매개 변수 형식을 지정하는 배열을 만듭니다. 메서드를 나타내는 대리자가 개체에 바인딩된 경우 첫 번째 매개 변수는 대리자가 바인딩된 형식과 일치해야 합니다. 이 예제에는 `Example` 형식과 `int`(Visual Basic에서는 `Integer`) 형식의 두 매개 변수가 있습니다.  
  
     [!code-cpp[DynamicMethodHowTo#13](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#13)]
     [!code-csharp[DynamicMethodHowTo#13](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#13)]
     [!code-vb[DynamicMethodHowTo#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#13)]  
  
3. <xref:System.Reflection.Emit.DynamicMethod>를 만듭니다. 이 예제에서는 메서드에 이름이 없습니다. 반환 값의 형식은 `int`(Visual Basic에서는 `Integer`)로 지정됩니다. 메서드는 `Example` 클래스의 private 및 protected 멤버에 액세스할 수 있습니다.  
  
     [!code-cpp[DynamicMethodHowTo#14](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#14)]
     [!code-csharp[DynamicMethodHowTo#14](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#14)]
     [!code-vb[DynamicMethodHowTo#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#14)]  
  
4. 메서드 본문을 내보냅니다. 이 예제에서 <xref:System.Reflection.Emit.ILGenerator> 개체는 MSIL(Microsoft Intermediate Language)을 내보내는 데 사용됩니다. 또는 <xref:System.Reflection.Emit.DynamicILInfo> 개체를 비관리 코드 생성기와 함께 사용하여 <xref:System.Reflection.Emit.DynamicMethod>에 대한 메서드 본문을 내보낼 수 있습니다.  
  
     이 예제의 MSIL은 `Example` 클래스 인스턴스인 첫 번째 인수를 로드하고 `int` 형식의 private 인스턴스 필드 값을 로드하는 데 사용합니다. 두 번째 인수가 로드되고, 두 개의 숫자를 곱합니다. 결과가 `int`보다 크면 값이 잘리고, 최상위 비트는 무시됩니다. 메서드가 반환하고 반환 값이 스택에 포함됩니다.  
  
     [!code-cpp[DynamicMethodHowTo#15](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#15)]
     [!code-csharp[DynamicMethodHowTo#15](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#15)]
     [!code-vb[DynamicMethodHowTo#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#15)]  
  
5. <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%28System.Type%2CSystem.Object%29> 메서드 오버로드를 호출하여 동적 메서드를 나타내는 대리자 인스턴스(1단계에서 선언됨)를 만듭니다. 대리자를 만들면 메서드가 완성되고, MSIL 추가 등 메서드를 변경하려는 이후의 모든 시도는 무시됩니다.  
  
    > [!NOTE]
    > <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> 메서드를 여러 번 호출하여 대상 형식의 다른 인스턴스에 바인딩된 대리자를 만들 수 있습니다.  
  
     다음 코드는 private 테스트 필드가 42로 설정된 `Example` 클래스의 새 인스턴스에 메서드를 바인딩합니다. 즉, 대리자를 호출할 때마다 `Example` 인스턴스가 메서드의 첫 번째 매개 변수에 전달됩니다.  
  
     메서드의 첫 번째 매개 변수는 항상 `Example` 인스턴스를 받기 때문에 `OneParameter` 대리자가 사용됩니다. 대리자를 호출하는 경우 두 번째 매개 변수만 필요합니다.  
  
     [!code-cpp[DynamicMethodHowTo#16](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#16)]
     [!code-csharp[DynamicMethodHowTo#16](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#16)]
     [!code-vb[DynamicMethodHowTo#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#16)]  
  
## <a name="example"></a>예  
 다음 코드 예제에서는 간단한 동적 메서드 및 클래스 인스턴스에 바인딩된 동적 메서드를 보여 줍니다.  
  
 간단한 동적 메서드는 32비트 정수인 인수 하나를 사용하고 해당 정수의 64비트 거듭제곱을 반환합니다. 제네릭 대리자는 메서드를 호출하는 데 사용됩니다.  
  
 두 번째 동적 메서드에는 `Example` 형식과 `int`(Visual Basic에서는 `Integer`) 형식의 두 매개 변수가 있습니다. 동적 메서드를 만들면 `int` 형식의 인수 하나가 있는 제네릭 대리자를 사용하여 `Example` 인스턴스에 바인딩됩니다. 메서드의 첫 번째 매개 변수는 항상 `Example`의 바인딩된 인스턴스를 받기 때문에 대리자에 `Example` 형식의 인수가 없습니다. 대리자를 호출할 때 `int` 인수만 제공됩니다. 이 동적 메서드는 `Example` 클래스의 private 필드에 액세스하고 private 필드와 `int` 인수의 곱을 반환합니다.  
  
 코드 예제에서는 메서드 실행에 사용할 수 있는 대리자를 정의합니다.  
  
 [!code-cpp[DynamicMethodHowTo#1](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#1)]
 [!code-csharp[DynamicMethodHowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#1)]
 [!code-vb[DynamicMethodHowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.Emit.DynamicMethod>
- [리플렉션 내보내기 사용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y322t50(v=vs.100))
- [리플렉션 내보내기 동적 메서드 시나리오](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sfk2s47t(v=vs.100))
