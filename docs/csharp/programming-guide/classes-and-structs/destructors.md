---
title: 종료자 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 10/08/2018
helpviewer_keywords:
- ~ [C#], in finalizers
- C# language, finalizers
- finalizers [C#]
ms.assetid: 1ae6e46d-a4b1-4a49-abe5-b97f53d9e049
ms.openlocfilehash: 9936d56582afd160bf3464d18efd3acf47c7af60
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924490"
---
# <a name="finalizers-c-programming-guide"></a>종료자(C# 프로그래밍 가이드)
종료자(**소멸자**라고도 함)는 가비지 수집기에서 클래스 인스턴스를 수집할 때 필요한 최종 정리를 수행하는 데 사용됩니다.  
  
## <a name="remarks"></a>설명  
  
- 종료자는 구조체에서 정의할 수 없으며, 클래스에서만 사용됩니다.  
  
- 클래스에는 종료자가 하나만 있을 수 있습니다.  
  
- 종료자는 상속하거나 오버로드할 수 없습니다.  
  
- 종료자를 호출할 수 없습니다. 자동으로 호출됩니다.  
  
- 종료자는 한정자를 사용하거나 매개 변수를 갖지 않습니다.  
  
 예를 들어 다음은 `Car` 클래스에 대한 종료자의 선언입니다.
  
 [!code-csharp[csProgGuideObjects#86](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#86)]  

다음 예제와 같이 종료자를 식 본문 정의로 구현할 수도 있습니다.

[!code-csharp[expression-bodied-finalizer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-destructor.cs#1)]  
  
 종료자는 개체의 기본 클래스에서 <xref:System.Object.Finalize%2A>를 암시적으로 호출합니다. 따라서 종료자 호출은 다음 코드로 암시적으로 변환됩니다.  
  
```csharp  
protected override void Finalize()  
{  
    try  
    {  
        // Cleanup statements...  
    }  
    finally  
    {  
        base.Finalize();  
    }  
}  
```  
  
 즉, `Finalize` 메서드가 상속 체인의 모든 인스턴스에 대해 최다 파생에서 최소 파생까지 재귀적으로 호출됩니다.  
  
> [!NOTE]
> 빈 종료자는 사용할 수 없습니다. 클래스에 종료자가 포함되어 있으면 `Finalize` 큐에서 항목이 생성됩니다. 종료자를 호출하면 가비지 수집기가 호출되어 큐를 처리합니다. 종료자가 비어 있으면 성능이 불필요하게 저하됩니다.  
  
 종료자가 호출되는 시기는 가비지 수집기에 의해 결정되기 때문에 프로그래머가 제어할 수 없습니다. 가비지 수집기는 애플리케이션에서 더 이상 사용되지 않는 개체를 확인합니다. 개체를 종료할 수 있는 것으로 판단되면 종료자(있는 경우)를 호출하고 개체를 저장하는 데 사용된 메모리를 회수합니다. 
 
 .NET Framework 애플리케이션에서(.NET Core 애플리케이션에서가 아닌) 프로그램이 종료될 때 종료자도 호출됩니다. 
  
 <xref:System.GC.Collect%2A>를 호출하여 강제로 가비지 수집할 수 있지만 대부분의 경우 성능 문제가 발생할 수 있으므로 방지해야 합니다.  
  
## <a name="using-finalizers-to-release-resources"></a>종료자를 사용하여 리소스 해제  
 일반적으로 C#에서는 가비지 수집을 사용하는 런타임을 대상으로 하지 않는 언어로 개발할 때 필요한 만큼 많은 메모리 관리가 필요하지 않습니다. 이는 .NET Framework 가비지 수집기에서 개체에 대한 메모리 할당 및 해제를 암시적으로 관리하기 때문입니다. 그러나 애플리케이션에서 창, 파일 및 네트워크 연결 등의 관리되지 않는 리소스를 캡슐화하는 경우 종료자를 사용하여 해당 리소스를 해제해야 합니다. 개체를 종료할 수 있으면 가비지 수집기에서 개체의 `Finalize` 메서드를 실행합니다.  
  
## <a name="explicit-release-of-resources"></a>리소스의 명시적 해제  
 애플리케이션에서 비용이 많이 드는 외부 리소스를 사용하는 경우 가비지 수집기에서 개체를 해제하기 전에 리소스를 명시적으로 해제하는 방법을 제공하는 것이 좋습니다. 이렇게 하려면 <xref:System.IDisposable> 인터페이스에서 개체에 필요한 정리를 수행하는 `Dispose` 메서드를 구현합니다. 이렇게 하면 애플리케이션의 성능을 상당히 향상시킬 수 있습니다. 이렇게 리소스를 명시적으로 제어하는 경우에도 종료자는 `Dispose` 메서드 호출에 실패할 경우 리소스를 정리하는 안전한 방법이 됩니다.  
  
 리소스 정리에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
- [관리되지 않는 리소스 정리](../../../standard/garbage-collection/unmanaged.md)  
  
- [Dispose 메서드 구현](../../../standard/garbage-collection/implementing-dispose.md)  
  
- [using 문](../../language-reference/keywords/using-statement.md)  
  
## <a name="example"></a>예  
 다음 예제에서는 상속 체인을 구성하는 세 가지 클래스를 만듭니다. `First` 클래스는 기본 클래스이고, `Second`는 `First`에서 파생되며, `Third`는 `Second`에서 파생됩니다. 세 클래스 모두 종료자가 있습니다. `Main`에서 최다 파생 클래스의 인스턴스가 만들어집니다. 프로그램이 실행되면 세 클래스에 대한 종료자가 최다 파생부터 최소 파생까지 순서대로 자동으로 호출됩니다.  
  
 [!code-csharp[csProgGuideObjects#85](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#85)]  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [소멸자](~/_csharplang/spec/classes.md#destructors) 섹션을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- <xref:System.IDisposable>
- [C# 프로그래밍 가이드](../index.md)
- [생성자](./constructors.md)
- [가비지 수집](../../../standard/garbage-collection/index.md)
