---
title: 인터페이스 속성 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], on interfaces
- interfaces [C#], properties
ms.assetid: 6503e9ed-33d7-44ec-b4c1-cc16c084b795
ms.openlocfilehash: cdd425970442e284d6fd6488bbb13394c12e939a
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596446"
---
# <a name="interface-properties-c-programming-guide"></a>인터페이스 속성(C# 프로그래밍 가이드)
[interface](../../language-reference/keywords/interface.md)에 속성을 선언할 수 있습니다. 다음은 인터페이스 속성 접근자의 예입니다.  
  
 [!code-csharp[csProgGuideProperties#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#14)]  
  
 인터페이스 속성의 접근자에는 본문이 없습니다. 따라서 접근자의 목적은 속성이 읽기/쓰기인지, 읽기 전용인지, 쓰기 전용인지를 지정하는 것입니다.  
  
## <a name="example"></a>예  
 이 예제에서 `IEmployee` 인터페이스에는 읽기/쓰기 속성 `Name`과 읽기 전용 속성 `Counter`가 있습니다. `Employee` 클래스는 `IEmployee` 인터페이스를 구현하고 이러한 두 속성을 사용합니다. 프로그램은 새 직원의 이름과 현재 직원 수를 읽고 직원 이름과 계산된 직원 수를 표시합니다.  
  
 멤버가 선언된 인터페이스를 참조하는 속성의 정규화된 이름을 사용할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideProperties#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#16)]  
  
 이를 [명시적 인터페이스 구현](../interfaces/explicit-interface-implementation.md)이라고 합니다. 예를 들어 `Employee` 클래스가 두 인터페이스 `ICitizen` 및 `IEmployee`를 구현하고 두 인터페이스에 모두 `Name` 속성이 있으면 명시적 인터페이스 멤버 구현이 필요합니다. 즉, 다음과 같은 속성 선언이 있다고 가정합니다.  
  
 [!code-csharp[csProgGuideProperties#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#16)]  
  
 이 선언은 `IEmployee` 인터페이스의 `Name` 속성을 구현합니다. 또한 다음과 같은 선언이 있다고 가정합니다.  
  
 [!code-csharp[csProgGuideProperties#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#17)]  
  
 이 선언은 `ICitizen` 인터페이스의 `Name` 속성을 구현합니다.  
  
 [!code-csharp[csProgGuideProperties#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideProperties/CS/Properties.cs#15)]  
  
  **`210 Hazem Abolrous`**    
## <a name="sample-output"></a>샘플 출력  
 `Enter number of employees: 210`  
  
 `Enter the name of the new employee: Hazem Abolrous`  
  
 `The employee information:`  
  
 `Employee number: 211`  
  
 `Employee name: Hazem Abolrous`  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [속성](./properties.md)
- [속성 사용](./using-properties.md)
- [속성 및 인덱서 비교](../indexers/comparison-between-properties-and-indexers.md)
- [인덱서](../indexers/index.md)
- [인터페이스](../interfaces/index.md)
