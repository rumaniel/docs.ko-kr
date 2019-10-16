---
title: '방법: 참조 같음(ID) 테스트 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- object identity [C#]
- reference equality [C#]
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
ms.openlocfilehash: 2b4b7b7bdd03077a78aa2a6375764fa86a885ef5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588636"
---
# <a name="how-to-test-for-reference-equality-identity-c-programming-guide"></a>방법: 참조 같음(ID) 테스트(C# 프로그래밍 가이드)
형식에서 참조 같음 비교를 지원하기 위해 사용자 지정 논리를 구현할 필요는 없습니다. 이 기능은 정적 <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> 메서드가 모든 형식에 대해 제공합니다.  
  
 다음 예제에서는 두 변수에 *참조 같음*이 있는지 여부, 즉 메모리의 동일한 개체를 참조하는지 여부를 확인하는 방법을 보여 줍니다.  
  
 또한 이 예제에서는 <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>가 값 형식에 대해 항상 `false`를 반환하는 이유 및 문자열 일치를 확인하는 데 <xref:System.Object.ReferenceEquals%2A>를 사용하면 안 되는 이유를 보여 줍니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[csProgGuideObjects#90](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#90)]  
  
 <xref:System.Object?displayProperty=nameWithType> 유니버설 기본 클래스의 `Equals` 구현에서도 참조 같음 검사를 수행하지만 클래스가 메서드를 재정의할 경우 결과가 예상과 다를 수 있기 때문에 이 기능은 사용하지 않는 것이 좋습니다. `==` 및 `!=` 연산자의 경우도 마찬가지입니다. 참조 형식에서 작동하는 경우 `==` 및 `!=`의 기본 동작은 참조 같음 검사를 수행하는 것입니다. 그러나 파생 클래스에서 연산자를 오버로드하여 값 같음 검사를 수행할 수 있습니다. 잠재적인 오류를 최소화하려면 두 개체에 참조 같음이 있는지 여부를 확인해야 할 때 항상 <xref:System.Object.ReferenceEquals%2A>를 사용하는 것이 좋습니다.  
  
 동일한 어셈블리 내의 상수 문자열은 항상 런타임에서 인턴 지정됩니다. 즉, 고유한 각 리터럴 문자열의 인스턴스 하나만 유지됩니다. 그러나 런타임은 런타임에 생성된 문자열이 인턴 지정되도록 보장하지 않으며, 서로 다른 어셈블리에 있는 동일한 두 상수 문자열이 인턴 지정되도록 보장하지도 않습니다.  
  
## <a name="see-also"></a>참고 항목

- [같음 비교](./equality-comparisons.md)
