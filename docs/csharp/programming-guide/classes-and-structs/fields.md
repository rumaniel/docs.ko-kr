---
title: 필드 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- fields [C#]
ms.assetid: 3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7
ms.openlocfilehash: c07f058eb081fa1c9e0a3756959570d1ba9e47f6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924526"
---
# <a name="fields-c-programming-guide"></a>필드(C# 프로그래밍 가이드)
*필드*는 [클래스](../../language-reference/keywords/class.md) 또는 [구조체](../../language-reference/keywords/struct.md)에서 직접 선언되는 모든 형식의 변수입니다. 필드는 포함하는 형식의 *멤버*입니다.  
  
 클래스 또는 구조체에는 인스턴스 필드, 정적 필드 또는 둘 다 있을 수 있습니다. 인스턴스 필드는 형식의 인스턴스와 관련이 있습니다. 인스턴스 필드가 F인 T 클래스가 있는 경우 형식이 T인 개체 두 개를 만들고 각 개체에서 다른 개체의 값에 영향을 주지 않고 F 값을 수정할 수 있습니다. 반면 정적 필드는 클래스 자체에 속하며 해당 클래스의 모든 인스턴스에서 공유됩니다. 인스턴스 A에서 변경한 내용은 인스턴스 B와 C가 필드에 액세스하는 경우 바로 인스턴스 B와 C에 표시됩니다.  
  
 일반적으로 필드는 액세스 가능성이 private 또는 protected인 변수에만 사용해야 합니다. 클래스에서 클라이언트 코드에 노출하는 데이터는 [메서드](./methods.md), [속성](./properties.md) 및 [인덱서](../indexers/index.md)를 통해 제공해야 합니다. 내부 필드에 직접 액세스하는 데 이러한 구문을 사용하면 잘못된 입력 값으로부터 보호할 수 있습니다. 공용 속성에 의해 노출된 데이터를 저장하는 private 필드는 *백업 저장소* 또는 *지원 필드*라고 합니다.  
  
 필드는 일반적으로 둘 이상의 클래스 메서드에서 액세스할 수 있고 단일 메서드의 수명보다 오랫동안 저장되어야 하는 데이터를 저장합니다. 예를 들어 달력 날짜를 나타내는 클래스에는 각각 월, 일 및 연도에 대한 세 개의 정수 필드가 있을 수 있습니다. 단일 메서드 범위 내에서만 사용되는 변수는 메서드 본문 자체 내에 *지역 변수*로 선언해야 합니다.  
  
 필드는 필드의 액세스 수준을 지정한 다음 필드의 형식, 필드의 이름순으로 지정하여 클래스 블록에서 선언됩니다. 예:  
  
 [!code-csharp[csProgGuideObjects#61](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#61)]  
  
 개체의 필드에 액세스하려면 `objectname.fieldname`와 같이 개체 이름과 필드 이름 뒤에 마침표를 추가합니다. 예:  
  
 [!code-csharp[csProgGuideObjects#62](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#62)]  
  
 필드를 선언할 때 대입 연산자를 사용하여 필드에 초기 값을 지정할 수 있습니다. 예를 들어 `day` 필드를 `"Monday"`에 자동으로 할당하려면 다음 예제와 같이 `day`를 선언합니다.  
  
 [!code-csharp[csProgGuideObjects#63](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#63)]  
  
 필드는 개체 인스턴스에 대한 생성자를 호출 하기 직전에 초기화됩니다. 생성자가 필드의 값을 할당하면 필드 선언 중에 지정된 모든 값을 덮어씁니다. 자세한 내용은 [생성자 사용](./using-constructors.md)을 참조하세요.  
  
> [!NOTE]
> 필드 이니셜라이저는 다른 인스턴스 필드를 참조할 수 없습니다.  
  
 필드는 [public](../../language-reference/keywords/public.md), [private](../../language-reference/keywords/private.md), [protected](../../language-reference/keywords/protected.md), [internal](../../language-reference/keywords/internal.md), [protected internal](../../language-reference/keywords/protected-internal.md) 또는 [private protected](../../language-reference/keywords/private-protected.md)로 표시될 수 있습니다. 이러한 액세스 한정자는 클래스 사용자가 필드에 액세스 하는 방법을 정의합니다. 자세한 내용은 [액세스 한정자](./access-modifiers.md)를 참조하세요.  
  
 필요에 따라 필드를 [static](../../language-reference/keywords/static.md)으로 선언할 수 있습니다. 그러면 클래스의 인스턴스가 없는 경우에도 언제든지 호출자가 필드를 사용할 수 있습니다. 자세한 내용은 [static 클래스 및 static 클래스 멤버](./static-classes-and-static-class-members.md)를 참조하세요.  
  
 필드를 [readonly](../../language-reference/keywords/readonly.md)로 선언할 수 있습니다. 읽기 전용 필드는 초기화 중이나 생성자에서만 값을 할당할 수 있습니다. C# 컴파일러가 컴파일 시간에는 정적 읽기 전용 필드의 값에 액세스할 수 없고 런타임 시에만 액세스할 수 있다는 점을 제외하면`static readonly` 필드는 상수와 매우 유사합니다. 자세한 내용은 [상수](./constants.md)를 참조하세요.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [생성자 사용](./using-constructors.md)
- [상속](./inheritance.md)
- [액세스 한정자](./access-modifiers.md)
- [추상/봉인된 클래스 및 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)
