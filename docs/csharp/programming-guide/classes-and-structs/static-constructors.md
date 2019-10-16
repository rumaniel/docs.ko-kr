---
title: 정적 생성자 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- static constructors [C#]
- constructors [C#], static
ms.assetid: 151ec95e-3c4d-4ed7-885d-95b7a3be2e7d
ms.openlocfilehash: 6d1a39008ebb965649104c2e74241780731911bb
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596028"
---
# <a name="static-constructors-c-programming-guide"></a>정적 생성자(C# 프로그래밍 가이드)
정적 생성자는 [정적](../../language-reference/keywords/static.md) 데이터를 초기화하거나 한 번만 수행해야 하는 특정 작업을 수행하는 데 사용됩니다. 첫 번째 인스턴스가 만들어지거나 정적 멤버가 참조되기 전에 자동으로 호출됩니다.  
  
 [!code-csharp[csProgGuideObjects#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#14)]  
 
## <a name="remarks"></a>설명
정적 생성자에는 다음과 같은 속성이 있습니다.  
  
- 정적 생성자는 액세스 한정자를 사용하거나 매개 변수를 갖지 않습니다.  

- 클래스 또는 구조체에는 한 개의 정적 생성자만 사용할 수 있습니다.

- 정적 생성자는 상속하거나 오버로드할 수 없습니다.

- 정적 생성자는 직접 호출할 수 없으며, CLR(공용 언어 런타임)을 통해서만 호출할 수 있습니다. 자동으로 호출됩니다.

- 사용자는 프로그램에서 정적 생성자가 실행되는 시기를 제어할 수 없습니다.
  
- 정적 생성자는 첫 번째 인스턴스가 만들어지거나 정적 멤버가 참조되기 전에 자동으로 호출되어 [클래스](../../language-reference/keywords/class.md)를 초기화합니다. 정적 생성자는 인스턴스 생성자보다 먼저 실행됩니다. 유형의 정적 생성자는 이벤트 또는 대리자에 할당된 정적 메서드가 호출될 때 호출되며 할당될 때는 호출되지 않는다는 점에 유의합니다. 정적 필드 변수 이니셜라이저가 정적 생성자의 클래스에 있는 경우 정적 생성자가 실행되기 직전에, 클래스 선언에 나타나는 텍스트 순서대로 실행됩니다.

- 정적 필드를 초기화하는 정적 생성자를 제공하지 않으면 모든 정적 필드가 [기본값 표](../../language-reference/keywords/default-values-table.md)에 나열된 기본값으로 초기화됩니다. 
  
- 정적 생성자가 예외를 throw하는 경우 런타임에서 생성자를 다시 호출하지 않으며, 프로그램을 실행 중인 애플리케이션 도메인의 수명 동안 형식이 초기화되지 않은 상태로 유지됩니다. 가장 일반적으로, 정적 생성자가 형식을 인스턴스화할 수 없는 경우 또는 정적 생성자 내에서 발생하는 처리되지 않은 예외에 대해 <xref:System.TypeInitializationException> 예외가 throw됩니다. 소스 코드에서 명시적으로 정의되지 않은 암시적 정적 생성자의 경우 문제 해결을 위해 IL(중간 언어) 코드를 검사해야 할 수 있습니다.

- 정적 생성자가 있으면 <xref:System.Reflection.TypeAttributes.BeforeFieldInit> 형식 특성을 추가할 수 없습니다. 이 때문에 런타임 최적화가 제한됩니다.

- `static readonly`로 선언된 필드는 해당 선언의 일부로 또는 정적 생성자에서만 할당할 수 있습니다. 명시적 정적 생성자가 필요하지 않은 경우, 런타임 최적화 향상을 위해 정적 생성자를 통하지 않고 선언에서 정적 필드를 초기화합니다.

> [!Note]
> 직접 액세스할 수 없더라도, 명시적 정적 생성자가 있을 경우 초기화 예외 문제 해결에 도움이 되도록 문서화해야 합니다.

### <a name="usage"></a>사용

- 정적 생성자는 일반적으로 클래스가 로그 파일을 사용하고, 생성자를 사용하여 이 파일에 항목을 쓰는 경우에 사용됩니다.  
- 정적 생성자는 생성자가 `LoadLibrary` 메서드를 호출할 수 있을 때 비관리 코드에 대한 래퍼 클래스를 만드는 경우에도 유용합니다.  

- 또한 정적 생성자를 사용하면 제약 조건(형식 매개 변수 제약 조건)을 통해 컴파일 시간에 검사할 수 없는 형식 매개 변수에 런타임 검사를 편리하게 적용할 수 있습니다.

## <a name="example"></a>예
 이 예제에서 `Bus` 클래스에는 정적 생성자가 있습니다. `Bus`의 첫 번째 인스턴스를 만들 때(`bus1`) 정적 생성자가 호출되어 클래스를 초기화합니다. 샘플 출력은 `Bus`의 두 인스턴스가 생성된 경우에도 정적 생성자가 한 번만 실행되고, 인스턴스 생성자를 실행하기 전에 실행되는지 확인합니다.  
  
 [!code-csharp[csProgGuideObjects#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#15)]
 
## <a name="c-language-specification"></a>C# 언어 사양
자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [정적 생성자](~/_csharplang/spec/classes.md#static-constructors) 섹션을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [생성자](./constructors.md)
- [정적 클래스 및 정적 클래스 멤버](./static-classes-and-static-class-members.md)
- [종료자](./destructors.md)
- [생성자 디자인 지침](../../../standard/design-guidelines/constructor.md#type-constructor-guidelines)
- [보안 경고 - CA2121: 정적 생성자는 private이어야 합니다.](https://docs.microsoft.com/visualstudio/code-quality/ca2121-static-constructors-should-be-private)
