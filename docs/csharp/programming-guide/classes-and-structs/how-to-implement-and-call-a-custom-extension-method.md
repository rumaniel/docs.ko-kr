---
title: '방법: 사용자 지정 확장 메서드 구현 및 호출 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- extension methods [C#], implementing and calling
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
ms.openlocfilehash: 26ad1d2251388237e186d1ba0e885fd7def66467
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596872"
---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a>방법: 사용자 지정 확장 메서드 구현 및 호출(C# 프로그래밍 가이드)
이 항목에서는 모든 .NET 형식에 대한 사용자 고유의 확장 메서드를 구현하는 방법을 보여 줍니다. 클라이언트 코드는 확장 메서드를 포함하는 DLL에 대한 참조를 추가하고 확장 메서드가 정의된 네임스페이스를 지정하는 [using](../../language-reference/keywords/using-directive.md) 지시문을 추가하여 확장 메서드를 사용할 수 있습니다.  
  
## <a name="to-define-and-call-the-extension-method"></a>확장 메서드를 정의하고 호출하려면  
  
1. 확장 메서드가 포함될 정적 [클래스](./static-classes-and-static-class-members.md)를 정의합니다.  
  
     클래스가 클라이언트 코드에 표시되어야 합니다. 액세스 가능성 규칙에 대한 자세한 내용은 [액세스 한정자](./access-modifiers.md)를 참조하세요.  
  
2. 최소한 포함하는 클래스와 동일한 표시 유형으로 확장 메서드를 정적 메서드로 구현합니다.  
  
3. 메서드의 첫 번째 매개 변수는 메서드가 작동하는 형식을 지정합니다. [this](../../language-reference/keywords/this.md) 한정자가 앞에 와야 합니다.  
  
4. 호출 코드에 `using` 지시문을 추가하여 확장 메서드 클래스를 포함하는 [네임스페이스](../../language-reference/keywords/namespace.md)를 지정합니다.  
  
5. 형식의 인스턴스 메서드인 것처럼 메서드를 호출합니다.  
  
     연산자가 적용되는 형식을 나타내기 때문에 첫 번째 매개 변수는 호출 코드에서 지정되지 않고 컴파일러가 개체 형식을 이미 알고 있습니다. 매개 변수 2 ~ `n`에 대한 인수만 제공하면 됩니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 `CustomExtensions.StringExtension` 클래스에 `WordCount`라는 확장 메서드를 구현합니다. 이 메서드는 첫 번째 메서드 매개 변수로 지정된 <xref:System.String> 클래스에 대해 작동합니다. `CustomExtensions` 네임스페이스를 애플리케이션 네임스페이스로 가져오고, `Main` 메서드 내부에서 메서드가 호출됩니다.  
  
 [!code-csharp[csProgGuideExtensionMethods#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#1)]  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 확장 메서드는 특정 보안 취약성은 없습니다. 형식 자체에서 정의된 인스턴스 또는 정적 메서드를 기준으로 모든 이름 충돌이 해결되기 때문에 확장 메서드를 사용하여 형식의 기존 메서드를 가장할 수는 없습니다. 확장 메서드는 확장된 클래스의 개인 데이터에 액세스할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [확장명 메서드](./extension-methods.md)
- [LINQ(Language-Integrated Query)](../../linq/linq-in-csharp.md)
- [정적 클래스 및 정적 클래스 멤버](./static-classes-and-static-class-members.md)
- [protected](../../language-reference/keywords/protected.md)
- [internal](../../language-reference/keywords/internal.md)
- [public](../../language-reference/keywords/public.md)
- [this](../../language-reference/keywords/this.md)
- [namespace](../../language-reference/keywords/namespace.md)
