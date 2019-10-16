---
title: 대리자 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
ms.openlocfilehash: 80878ec1a592a368db246fc294ebc42556874832
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921935"
---
# <a name="delegates-c-programming-guide"></a>대리자(C# 프로그래밍 가이드)
[대리자](../../language-reference/keywords/delegate.md)는 특정 매개 변수 목록 및 반환 형식이 있는 메서드에 대한 참조를 나타내는 형식입니다. 대리자를 인스턴스화하면 모든 메서드가 있는 인스턴스를 호환되는 시그니처 및 반환 형식에 연결할 수 있습니다. 대리자 인스턴스를 통해 메서드를 호출할 수 있습니다.  
  
 대리자는 메서드를 다른 메서드에 인수로 전달하는 데 사용됩니다. 이벤트 처리기는 대리자를 통해 호출되는 메서드라고 할 수 있습니다. 사용자 지정 메서드를 만들면 Windows 컨트롤 같은 클래스가 특정 이벤트가 발생했을 때 해당 메서드를 호출할 수 있습니다. 다음 예제에서는 대리자 선언을 보여 줍니다.  
  
 [!code-csharp[csProgGuideDelegates#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#20)]  
  
 액세스 가능한 클래스 또는 대리자 형식과 일치하는 구조의 모든 메서드는 대리자에 할당할 수 있습니다. 메서드는 정적 메서드이거나 인스턴스 메서드일 수 있습니다. 메서드를 대리자에 할당하면 프로그래밍 방식으로 메서드 호출을 변경하고 기존 클래스에 새 코드를 삽입할 수 있습니다.  
  
> [!NOTE]
> 메서드 오버로드의 컨텍스트에서는 메서드 시그니처에 반환 값이 포함되지 않지만 대리자 컨텍스트에서는 시그니처에 반환 값이 포함됩니다. 즉 메서드의 반환 형식이 대리자의 반환 형식과 같아야 합니다.  
  
 대리자에서는 이와 같이 메서드를 매개 변수로 취급할 수 있으므로 대리자는 콜백 메서드 정의에 이상적입니다. 예를 들어, 두 개체를 비교하는 메서드에 대한 참조를 정렬 알고리즘에 인수로 전달할 수 있습니다. 비교 코드는 별도의 절차이기 때문에 정렬 알고리즘을 보다 일반적인 방식으로 작성할 수 있습니다.  
  
## <a name="delegates-overview"></a>대리자 개요  
 대리자에는 다음과 같은 속성이 있습니다.  
  
- 대리자는 C++ 함수 포인터와 유사하지만 C++ 함수 포인터와 달리 멤버 함수에 대해 완전히 개체 지향입니다. 대리자는 개체 인스턴스 및 메서드를 모두 캡슐화합니다.
  
- 대리자를 통해 메서드를 매개 변수로 전달할 수 있습니다.  
  
- 대리자를 사용하여 콜백 메서드를 정의할 수 있습니다.  
  
- 여러 대리자를 연결할 수 있습니다. 예를 들어 단일 이벤트에 대해 여러 메서드를 호출할 수 있습니다.  
  
- 메서드와 대리자 형식이 정확히 일치할 필요는 없습니다. 자세한 내용은 [대리자의 가변성 사용](../concepts/covariance-contravariance/using-variance-in-delegates.md)을 참조하세요.  
  
- C# 버전 2.0에는 별도로 정의된 메서드 대신 코드 블록을 매개 변수로 전달할 수 있도록 하는 [무명 메서드](../../language-reference/operators/delegate-operator.md)라는 개념이 도입되었습니다. C# 3.0에는 인라인 코드 블록을 더 간단하게 작성할 수 있는 람다 식이 도입되었습니다. 특정 컨텍스트에서는 무명 메서드와 람다 식 모두 대리자 형식으로 컴파일됩니다. 이 두 기능을 익명 함수라고 합니다. 람다 식에 대한 자세한 내용은 [람다 식](../statements-expressions-operators/lambda-expressions.md)을 참조하세요.
  
## <a name="in-this-section"></a>섹션 내용  
  
- [대리자 사용](./using-delegates.md)  
  
- [인터페이스(C# 프로그래밍 가이드) 대신 대리자를 사용하는 경우](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms173173(v=vs.100))  
  
- [명명된 메서드 및 무명 메서드가 있는 대리자](./delegates-with-named-vs-anonymous-methods.md)  
  
- [대리자의 가변성 사용](../concepts/covariance-contravariance/using-variance-in-delegates.md)  
  
- [방법: 대리자 조합(멀티캐스트 대리자)](./how-to-combine-delegates-multicast-delegates.md)  
  
- [방법: 대리자 선언, 인스턴스화 및 사용](./how-to-declare-instantiate-and-use-a-delegate.md)  

## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [대리자](~/_csharplang/spec/delegates.md) 에 [ C# 언어 사양](../../language-reference/language-specification/index.md)합니다. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.
  
## <a name="featured-book-chapters"></a>중요 설명서 장  
 [대리자, Events, and Lambda Expressions](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518994%28v=orm.10%29) 에 [ C# 3.0 Cookbook, Third Edition: 250 개 이상의 솔루션에 대 한 C# 3.0 프로그래머](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518995%28v=orm.10%29)  
  
 [대리자 및 이벤트](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652490%28v=orm.10%29) 에 [학습 C# 3.0. 기본 사항 마스터 C# 3.0](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652493%28v=orm.10%29)  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Delegate>
- [C# 프로그래밍 가이드](../index.md)
- [이벤트](../events/index.md)
