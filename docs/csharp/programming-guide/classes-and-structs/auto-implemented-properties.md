---
title: 자동으로 구현된 속성 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- auto-implemented properties [C#]
- properties [C#], auto-implemented
ms.assetid: aa55fa97-ccec-431f-b5e9-5ac789fd32b7
ms.openlocfilehash: 44f3beb9de8c9d339c42db26bb9c510998abc7d7
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597140"
---
# <a name="auto-implemented-properties-c-programming-guide"></a>자동으로 구현된 속성(C# 프로그래밍 가이드)
C# 3.0 이상에서는 속성 접근자에 추가적인 논리가 필요하지 않을 경우 자동 구현 속성을 통해 속성 선언이 더 간결해집니다. 이를 통해 클라이언트 코드에서 개체를 만들 수도 있습니다. 다음 예제와 같이 속성을 선언할 때 컴파일러는 속성의 `get` 및 `set` 접근자를 통해서만 액세스할 수 있는 전용 익명 지원 필드를 만듭니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 일부 자동 구현 속성이 있는 간단한 클래스를 보여 줍니다.  
  
 [!code-csharp[csProgGuideLINQ#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#28)]  
  
 C# 6 이상 버전에서는 필드와 유사하게 자동 구현 속성을 초기화할 수 있습니다.  
  
```csharp  
public string FirstName { get; set; } = "Jane";  
```  
  
 앞의 예제에 표시된 클래스는 변경할 수 있습니다. 클라이언트 코드에서는 개체가 만들어진 후 개체의 값을 변경할 수 있습니다. 데이터 및 중요 동작(메서드)을 포함하는 복잡한 클래스에는 공용 속성을 포함해야 할 수 있습니다. 그러나 값 집합(데이터)만 캡슐화하고 동작이 적거나 없는 작은 클래스나 구조체의 경우 set 접근자를 [private](../../language-reference/keywords/private.md)로 선언하거나(소비자에 대한 변경 불가능) get 접근자만 선언하여(생성자를 제외한 모든 위치에서 변경 불가능) 개체를 변경 불가능으로 설정해야 합니다.  자세한 내용은 [방법: 자동으로 구현된 속성을 사용하여 간단한 클래스 구현](./how-to-implement-a-lightweight-class-with-auto-implemented-properties.md)  
  
## <a name="see-also"></a>참고 항목

- [속성](./properties.md)
- [한정자](../../language-reference/keywords/modifiers.md)
