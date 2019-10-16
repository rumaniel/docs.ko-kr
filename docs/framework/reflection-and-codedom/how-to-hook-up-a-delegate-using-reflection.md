---
title: '방법: 리플렉션을 사용하여 대리자 후크'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- events [.NET Framework], adding event handlers with reflection
- reflection, adding event-handler delegates
- delegates [.NET Framework], adding event handlers with reflection
ms.assetid: 076ee62d-a964-449e-a447-c31b33518b81
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 937dca59be8b83526ebf6cd4c369532b1a8b9afe
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045976"
---
# <a name="how-to-hook-up-a-delegate-using-reflection"></a>방법: 리플렉션을 사용하여 대리자 후크
리플렉션을 사용하여 어셈블리를 로드하고 실행하는 경우 C# `+=` 연산자 또는 Visual Basic [AddHandler 문](../../visual-basic/language-reference/statements/addhandler-statement.md)과 같은 언어 기능을 사용하여 이벤트를 연결할 수 없습니다. 다음 절차에서는 리플렉션을 통해 필요한 모든 형식을 가져와 기존 메서드를 이벤트에 연결하는 방법 및 리플렉션 내보내기를 사용하여 동적 메서드를 만들고 이벤트에 연결하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이벤트 처리 대리자를 연결하는 다른 방법은 <xref:System.Reflection.EventInfo> 클래스의 <xref:System.Reflection.EventInfo.AddEventHandler%2A> 메서드에 대한 코드 예제를 참조하세요.  
  
### <a name="to-hook-up-a-delegate-using-reflection"></a>리플렉션을 사용하여 대리자를 연결하려면  
  
1. 이벤트를 발생시키는 형식을 포함하는 어셈블리를 로드합니다. 어셈블리는 일반적으로 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 사용하여 로드됩니다. 이 예제를 단순하게 유지하기 위해 현재 어셈블리의 파생 양식이 사용되므로 <xref:System.Reflection.Assembly.GetExecutingAssembly%2A> 메서드가 현재 어셈블리를 로드하는 데 사용됩니다.  
  
     [!code-cpp[HookUpDelegate#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#3)]
     [!code-csharp[HookUpDelegate#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#3)]
     [!code-vb[HookUpDelegate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#3)]  
  
2. 형식을 나타내는 <xref:System.Type> 개체를 가져오고 형식 인스턴스를 만듭니다. 양식에 매개 변수가 없는 생성자가 있기 때문에 다음 코드에서는 <xref:System.Activator.CreateInstance%28System.Type%29> 메서드가 사용됩니다. 만들려는 형식에 매개 변수가 없는 생성자가 없는 경우 사용할 수 있는 <xref:System.Activator.CreateInstance%2A> 메서드의 여러 다른 오버로드가 있습니다. 새 인스턴스는 어셈블리에 대해 알려진 것이 없다는 가정을 유지하기 위해 <xref:System.Object> 형식으로 저장됩니다. 이름을 미리 알지 못해도 리플렉션을 통해 어셈블리의 형식을 가져올 수 있습니다.  
  
     [!code-cpp[HookUpDelegate#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#4)]
     [!code-csharp[HookUpDelegate#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#4)]
     [!code-vb[HookUpDelegate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#4)]  
  
3. 이벤트를 나타내는 <xref:System.Reflection.EventInfo> 개체를 가져오고, <xref:System.Reflection.EventInfo.EventHandlerType%2A> 속성을 사용하여 이벤트를 처리하는 데 사용되는 대리자 형식을 가져옵니다. 다음 코드에서는 <xref:System.Windows.Forms.Control.Click> 이벤트에 대한 <xref:System.Reflection.EventInfo>를 가져옵니다.  
  
     [!code-cpp[HookUpDelegate#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#5)]
     [!code-csharp[HookUpDelegate#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#5)]
     [!code-vb[HookUpDelegate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#5)]  
  
4. 이벤트를 처리하는 메서드를 나타내는 <xref:System.Reflection.MethodInfo> 개체를 가져옵니다. 이 항목의 뒷부분에 나오는 예제 섹션의 완성된 프로그램 코드에 <xref:System.EventHandler> 이벤트를 처리하는 <xref:System.Windows.Forms.Control.Click> 대리자의 시그니처와 일치하는 메서드가 포함되어 있지만, 런타임에 동적 메서드를 생성할 수도 있습니다. 동적 메서드를 사용하여 런타임에 이벤트 처리기를 생성하는 것에 대한 자세한 내용은 다음에 나오는 절차를 참조하십시오.  
  
     [!code-cpp[HookUpDelegate#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#6)]
     [!code-csharp[HookUpDelegate#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#6)]
     [!code-vb[HookUpDelegate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#6)]  
  
5. <xref:System.Delegate.CreateDelegate%2A> 메서드를 사용하여 대리자 인스턴스를 만듭니다. 이 메서드는 static(Visual Basic에서는 `Shared`)이므로 대리자 형식을 지정해야 합니다. <xref:System.Reflection.MethodInfo>를 사용하는 <xref:System.Delegate.CreateDelegate%2A>의 오버로드를 사용하는 것이 좋습니다.  
  
     [!code-cpp[HookUpDelegate#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#7)]
     [!code-csharp[HookUpDelegate#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#7)]
     [!code-vb[HookUpDelegate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#7)]  
  
6. `add` 접근자 메서드를 가져온 다음 호출하여 이벤트를 연결합니다. 모든 이벤트에는 상위 수준 언어 구문에서 숨겨지는 `add` 접근자 및 `remove` 접근자가 있습니다. 예를 들어 C#에서는 `+=` 연산자를 사용하여 이벤트를 연결하고, Visual Basic에서는 [AddHandler 문](../../visual-basic/language-reference/statements/addhandler-statement.md)을 사용합니다. 다음 코드는 <xref:System.Windows.Forms.Control.Click> 이벤트의 `add` 접근자를 가져온 다음 대리자 인스턴스를 전달하여 런타임에 바인딩해서 호출합니다. 인수를 배열로 전달해야 합니다.  
  
     [!code-cpp[HookUpDelegate#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#8)]
     [!code-csharp[HookUpDelegate#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#8)]
     [!code-vb[HookUpDelegate#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#8)]  
  
7. 이벤트를 테스트합니다. 다음 코드는 코드 예제에서 정의된 양식을 보여 줍니다. 양식을 클릭하면 이벤트 처리기가 호출됩니다.  
  
     [!code-cpp[HookUpDelegate#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#12)]
     [!code-csharp[HookUpDelegate#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#12)]
     [!code-vb[HookUpDelegate#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#12)]  
  
<a name="procedureSection1"></a>   
### <a name="to-generate-an-event-handler-at-run-time-by-using-a-dynamic-method"></a>동적 메서드를 사용하여 런타임에 이벤트 처리기를 생성하려면  
  
1. 경량 동적 메서드 및 리플렉션 내보내기를 사용하여 런타임에 이벤트 처리기 메서드를 생성할 수 있습니다. 이벤트 처리기를 생성하려면 대리자의 매개 변수 형식과 반환 형식이 필요합니다. 대리자의 `Invoke` 메서드를 검사하여 가져올 수 있습니다. 다음 코드는 `GetDelegateReturnType` 및 `GetDelegateParameterTypes` 메서드를 사용하여 이 정보를 가져옵니다. 이러한 메서드에 대한 코드는 이 항목의 뒷부분에 나오는 예제 섹션에서 확인할 수 있습니다.  
  
     <xref:System.Reflection.Emit.DynamicMethod>에 이름을 지정할 필요는 없으므로 빈 문자열을 사용할 수 있습니다. 다음 코드에서 마지막 인수는 동적 메서드를 현재 형식과 연결하여 대리자가 `Example` 클래스의 모든 public 및 private 멤버에 액세스할 수 있도록 합니다.  
  
     [!code-cpp[HookUpDelegate#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#9)]
     [!code-csharp[HookUpDelegate#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#9)]
     [!code-vb[HookUpDelegate#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#9)]  
  
2. 메서드 본문을 생성합니다. 이 메서드는 문자열을 로드하고, 문자열을 사용하는 <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=nameWithType> 메서드의 오버로드를 호출한 다음 스택에서 반환 값을 팝하고(처리기에 반환 형식이 없으므로) 반환됩니다. 동적 메서드를 내보내는 방법에 대한 자세한 내용은 [방법: 동적 메서드 정의 및 실행](how-to-define-and-execute-dynamic-methods.md)을 참조하세요.  
  
     [!code-cpp[HookUpDelegate#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#10)]
     [!code-csharp[HookUpDelegate#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#10)]
     [!code-vb[HookUpDelegate#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#10)]  
  
3. 해당 <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> 메서드를 호출하여 동적 메서드를 완료합니다. `add` 접근자를 사용하여 이벤트에 대한 호출 목록에 대리자를 추가합니다.  
  
     [!code-cpp[HookUpDelegate#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#11)]
     [!code-csharp[HookUpDelegate#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#11)]
     [!code-vb[HookUpDelegate#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#11)]  
  
4. 이벤트를 테스트합니다. 다음 코드는 코드 예제에서 정의된 양식을 로드합니다. 양식을 클릭하면 미리 정의된 이벤트 처리기와 내보낸 이벤트 처리기가 둘 다 호출됩니다.  
  
     [!code-cpp[HookUpDelegate#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#12)]
     [!code-csharp[HookUpDelegate#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#12)]
     [!code-vb[HookUpDelegate#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#12)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 리플렉션을 사용하여 기존 메서드를 이벤트에 연결하는 방법 및 <xref:System.Reflection.Emit.DynamicMethod> 클래스를 사용하여 런타임에 메서드를 내보내고 이벤트에 연결하는 방법을 보여 줍니다.  
  
 [!code-cpp[HookUpDelegate#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#1)]
 [!code-csharp[HookUpDelegate#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#1)]
 [!code-vb[HookUpDelegate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Emit.DynamicMethod>
- <xref:System.Activator.CreateInstance%2A>
- <xref:System.Delegate.CreateDelegate%2A>
- [방법: 동적 메서드 정의 및 실행](how-to-define-and-execute-dynamic-methods.md)
- [리플렉션](reflection.md)
