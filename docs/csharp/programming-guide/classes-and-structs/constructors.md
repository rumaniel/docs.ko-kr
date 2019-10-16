---
title: 생성자 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 05/05/2017
helpviewer_keywords:
- constructors [C#]
- classes [C#], constructors
- C# language, constructors
ms.assetid: df2e2e9d-7998-418b-8e7d-890c17ff6c95
ms.openlocfilehash: ea780fc983ed46c8a5ccb54ab618d1a0a2a928d1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597095"
---
# <a name="constructors-c-programming-guide"></a>생성자(C# 프로그래밍 가이드)

[class](../../language-reference/keywords/class.md) 또는 [struct](../../language-reference/keywords/struct.md)를 만들 때마다 해당 생성자가 호출됩니다. 클래스 또는 구조체에는 서로 다른 인수를 사용하는 여러 생성자가 있을 수 있습니다. 프로그래머는 생성자를 통해 기본값을 설정하고, 인스턴스화를 제한하며, 유연하고 읽기 쉬운 코드를 작성할 수 있습니다. 자세한 내용 및 예제는 [생성자 사용](./using-constructors.md) 및 [인스턴스 생성자](./instance-constructors.md)를 참조하세요.  

## <a name="parameterless-constructors"></a>매개 변수 없는 생성자
  
클래스에 대한 생성자를 제공하지 않으면 C#이 기본적으로 개체를 인스턴스화하고 멤버 변수를 [기본값 표](../../language-reference/keywords/default-values-table.md)에 나열된 기본값으로 설정하는 생성자를 새로 만듭니다. 구조체에 대한 생성자를 제공하지 않으면 C#이 *암시적 매개 변수 없는 생성자*에서 응답하여 값 형식의 각 필드를 [기본값 표](../../language-reference/keywords/default-values-table.md)에 나열된 기본값으로 자동으로 초기화합니다. 자세한 내용 및 예제는 [인스턴스 생성자](./instance-constructors.md)를 참조하세요.  

## <a name="constructor-syntax"></a>생성자 구문

생성자는 이름이 해당 형식의 이름과 동일한 메서드입니다. 해당 메서드 시그니처에는 메서드 이름과 매개 변수 목록만 포함되고 반환 형식은 포함되지 않습니다. 다음 예제에서는 `Person`이라는 클래스에 대한 생성자를 보여 줍니다.

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#1)]  

생성자를 단일 문으로 구현할 수 있는 경우 [식 본문 정의](../statements-expressions-operators/expression-bodied-members.md)를 사용할 수 있습니다. 다음 예제에서는 생성자에 *name*이라는 단일 문자열 매개 변수가 있는 `Location` 클래스를 정의합니다. 식 본문 정의에서 `locationName` 필드에 인수를 할당합니다.

[!code-csharp[expression-bodied-constructor](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-ctor.cs#1)]  

## <a name="static-constructors"></a>정적 생성자

앞의 예제에서는 새 개체를 만드는 인스턴스 생성자를 모두 보여 주었습니다. 클래스 또는 구조체에 형식의 정적 멤버를 초기화하는 정적 생성자도 있을 수 있습니다.  정적 생성자에는 매개 변수가 없습니다. 정적 필드를 초기화하는 정적 생성자를 제공하지 않으면 C# 컴파일러는 정적 필드를 [기본값 표](../../language-reference/keywords/default-values-table.md)에 나열된 기본값으로 초기화합니다.

다음 예제에서는 정적 생성자를 사용하여 정적 필드를 초기화합니다.

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#2)]  

다음 예제와 같이 식 본문 정의를 사용하여 정적 생성자를 정의할 수도 있습니다. 

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#3)]  

자세한 내용 및 예제는 [정적 생성자](./static-constructors.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [생성자 사용](./using-constructors.md)  
  
 [인스턴스 생성자](./instance-constructors.md)  
  
 [전용 생성자](./private-constructors.md)  
  
 [정적 생성자](./static-constructors.md)  
  
 [방법: 복사 생성자 작성](./how-to-write-a-copy-constructor.md)  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [종료자](./destructors.md)
- [static](../../language-reference/keywords/static.md)
- [이니셜라이저가 생성자와 반대 순서로 실행되는 이유는 무엇인가요? 1부](https://blogs.msdn.microsoft.com/ericlippert/2008/02/15/why-do-initializers-run-in-the-opposite-order-as-constructors-part-one)
