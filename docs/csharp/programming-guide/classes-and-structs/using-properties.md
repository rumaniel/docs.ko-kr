---
title: 속성 사용 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- set accessor [C#]
- get accessor [C#]
- properties [C#], about properties
ms.assetid: f7f67b05-0983-4cdb-96af-1855d24c967c
ms.openlocfilehash: fdaa4b511b18495d2a35f72ee017a01aab0b4ee8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922052"
---
# <a name="using-properties-c-programming-guide"></a>속성 사용(C# 프로그래밍 가이드)
속성은 필드 및 메서드 모두의 측면을 결합합니다. 개체의 사용자에게 속성은 필드로 표시되며, 속성에 액세스하려면 동일한 구문이 필요합니다. 클래스의 구현자에게 속성은 [get](../../language-reference/keywords/get.md) 접근자 및/또는 [set](../../language-reference/keywords/set.md) 접근자를 나타내는 하나 또는 두 개의 코드 블록입니다. `get` 접근자에 대한 코드 블록은 속성을 읽을 때 실행되고, `set` 접근자에 대한 코드 블록은 속성에 새 값을 할당할 때 실행됩니다. `set` 접근자가 없는 속성은 읽기 전용으로 간주됩니다. `get` 접근자가 없는 속성은 쓰기 전용으로 간주됩니다. 두 접근자가 모두 있는 속성은 읽기/쓰기입니다.  
  
 필드와 달리 속성은 변수로 분류되지 않습니다. 따라서 [ref](../../language-reference/keywords/ref.md) 또는 [out](../../language-reference/keywords/out-parameter-modifier.md) 매개 변수로 속성을 전달할 수 없습니다.  
  
 속성은 여러 가지 용도로 사용됩니다. 변경을 허용하기 전에 데이터의 유효성을 검사하고, 데이터가 실제로 데이터베이스 등의 다른 소스에서 검색되는 클래스에 데이터를 투명하게 공개하고, 데이터 변경 시 이벤트 발생, 다른 필드의 값 변경 등의 작업을 수행할 수 있습니다.  
  
 속성은 필드의 액세스 수준, 속성 형식, 속성 이름, `get` 접근자 및/또는 `set` 접근자를 선언하는 코드 블록을 차례로 지정하여 클래스 블록에서 선언됩니다. 예:  
  
 [!code-csharp[csProgGuideProperties#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#7)]  
  
 이 예제에서 `Month`는 속성으로 선언되었으므로, `set` 접근자를 통해 `Month` 값이 1에서 12 사이로 설정되도록 할 수 있습니다. `Month` 속성은 전용 필드를 사용하여 실제 값을 추적합니다. 속성 데이터의 실제 위치를 속성의 “백업 저장소”라고도 합니다. 일반적으로 속성은 전용 필드를 백업 저장소로 사용합니다. 속성 호출을 통해서만 필드를 변경할 수 있도록 하기 위해 필드는 private로 표시되었습니다. 공용 및 개인 액세스 제한에 대한 자세한 내용은 [액세스 한정자](./access-modifiers.md)를 참조하세요.  
  
 자동 구현 속성은 간단한 속성 선언을 위해 간소화된 구문을 제공합니다. 자세한 내용은 [자동으로 구현된 속성](./auto-implemented-properties.md)을 참조하세요.  
  
## <a name="the-get-accessor"></a>get 접근자  
 `get` 접근자 본문은 메서드 본문과 유사합니다. 속성 형식의 값을 반환해야 합니다. `get` 접근자의 실행은 필드 값을 읽는 것과 같습니다. 예를 들어 `get` 접근자에서 private 변수를 반환하고 최적화가 사용되는 경우 `get` 접근자 메서드 호출이 컴파일러에서 인라인되므로 메서드 호출 오버헤드가 없습니다. 그러나 가상 `get` 접근자 메서드는 컴파일러에서 런타임 시 실제로 호출될 수 있는 메서드를 컴파일 시간에 알 수 없기 때문에 인라인할 수 없습니다. 다음은 전용 필드 `name`의 값을 반환하는 `get` 접근자입니다.  
  
 [!code-csharp[csProgGuideProperties#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#8)]  
  
 할당 대상을 제외하고 속성을 참조하는 경우 속성 값을 읽기 위해 `get` 접근자가 호출됩니다. 예:  
  
 [!code-csharp[csProgGuideProperties#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#9)]  
  
 `get` 접근자는 [return](../../language-reference/keywords/return.md) 또는 [throw](../../language-reference/keywords/throw.md) 문으로 끝나야 하며, 제어가 접근자 본문을 벗어날 수 없습니다.  
  
 `get` 접근자를 사용하여 개체의 상태를 변경하는 것은 잘못된 프로그래밍 스타일입니다. 예를 들어 다음 접근자는 `number` 필드에 액세스할 때마다 개체의 상태가 변경되는 부작용을 생성합니다.  
  
 [!code-csharp[csProgGuideProperties#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#10)]  
  
 `get` 접근자를 사용하여 필드 값을 반환하거나 계산한 후 반환할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideProperties#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#11)]  
  
 앞의 코드 세그먼트에서 `Name` 속성에 값을 할당하지 않으면 NA 값이 반환됩니다.  
  
## <a name="the-set-accessor"></a>set 접근자  
 `set` 접근자는 반환 형식이 [void](../../language-reference/keywords/void.md)인 메서드와 비슷합니다. 형식이 속성의 형식인 `value`라는 암시적 매개 변수를 사용합니다. 다음 예제에서는 `set` 접근자가 `Name` 속성에 추가됩니다.  
  
 [!code-csharp[csProgGuideProperties#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#12)]  
  
 속성에 값을 할당하는 경우 새 값을 제공하는 인수를 사용하여 `set` 접근자가 호출됩니다. 예:  
  
 [!code-csharp[csProgGuideProperties#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#13)]  
  
 `set` 접근자의 지역 변수 선언에 대해 암시적 매개 변수 이름 `value`를 사용하면 오류가 발생합니다.  
  
## <a name="remarks"></a>설명  
 속성은 `public`, `private`, `protected`, `internal`, `protected internal` 또는 `private protected`로 표시될 수 있습니다. 이러한 액세스 한정자는 클래스 사용자가 속성에 액세스하는 방법을 정의합니다. 동일한 속성에 대한 `get` 및 `set` 접근자가 서로 다른 액세스 한정자를 가질 수 있습니다. 예를 들어 `get`은 형식 외부에서 읽기 전용 액세스를 허용하도록 `public`이 되고, `set`은 `private` 또는 `protected`가 될 수 있습니다. 자세한 내용은 [액세스 한정자](./access-modifiers.md)를 참조하세요.  
  
 `static` 키워드를 사용하여 속성을 정적 속성으로 선언할 수 있습니다. 그러면 클래스의 인스턴스가 없는 경우에도 언제든지 호출자가 속성을 사용할 수 있습니다. 자세한 내용은 [static 클래스 및 static 클래스 멤버](./static-classes-and-static-class-members.md)를 참조하세요.  
  
 [virtual](../../language-reference/keywords/virtual.md) 키워드를 사용하여 속성을 가상 속성으로 표시할 수 있습니다. 그러면 파생 클래스에서 [override](../../language-reference/keywords/override.md) 키워드를 사용하여 속성 동작을 재정의할 수 있습니다. 이러한 옵션에 대한 자세한 내용은 [상속](./inheritance.md)을 참조하세요.  
  
 가상 속성을 재정의하는 속성이 [sealed](../../language-reference/keywords/sealed.md)일 수도 있으며, 파생 클래스에 대해 더 이상 가상이 아니도록 지정합니다. 마지막으로, 속성을 [abstract](../../language-reference/keywords/abstract.md)로 선언할 수 있습니다. 즉, 클래스에 구현이 없으며 파생 클래스가 자체 구현을 작성해야 합니다. 이러한 옵션에 대한 자세한 내용은 [추상 및 봉인 클래스와 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)를 참조하세요.  
  
> [!NOTE]
> [static](../../language-reference/keywords/static.md) 속성의 접근자에 [virtual](../../language-reference/keywords/virtual.md), [abstract](../../language-reference/keywords/abstract.md) 또는 [override](../../language-reference/keywords/override.md) 한정자를 사용하면 오류가 발생합니다.  
  
## <a name="example"></a>예  
 이 예제에서는 인스턴스, 정적 및 읽기 전용 속성을 보여 줍니다. 키보드에서 직원 이름을 받고 `NumberOfEmployees`를 1만큼 증가한 다음 직원 이름과 번호를 표시합니다.  
  
 [!code-csharp[csProgGuideProperties#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#2)]  
  
## <a name="example"></a>예  
 이 예제에서는 파생 클래스에서 이름이 같은 다른 속성에 의해 숨겨진 기본 클래스의 속성에 액세스하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideProperties#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#3)]  
  
 다음은 앞의 예제에서 중요한 사항입니다.  
  
- 파생 클래스의 `Name` 속성은 기본 클래스의 `Name` 속성을 숨깁니다. 이러한 경우 `new` 한정자는 파생 클래스의 속성 선언에 사용됩니다.  
  
     [!code-csharp[csProgGuideProperties#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#4)]  
  
- `(Employee)` 캐스트는 기본 클래스의 숨겨진 속성에 액세스하는 데 사용됩니다.  
  
     [!code-csharp[csProgGuideProperties#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#5)]  
  
     멤버를 숨기는 방법에 대한 자세한 내용은 [new 한정자](../../language-reference/keywords/new-modifier.md)를 참조하세요.  
  
## <a name="example"></a>예  
 이 예제에서 두 클래스 `Cube` 및 `Square`는 추상 클래스 `Shape`를 구현하고 해당 abstract `Area` 속성을 재정의합니다. 속성의 [override](../../language-reference/keywords/override.md) 한정자를 사용합니다. 프로그램은 변을 입력으로 사용하고 사각형과 정육면체의 면적을 계산합니다. 또한 면적을 입력으로 사용하고 사각형 및 정육면체의 해당 변을 계산합니다.  
  
 [!code-csharp[csProgGuideProperties#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#6)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [속성](./properties.md)
- [인터페이스 속성](./interface-properties.md)
- [자동으로 구현된 속성](./auto-implemented-properties.md)
