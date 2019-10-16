---
title: 속성 및 인덱서 비교 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], vs. indexers
- indexers [C#], vs. properties
ms.assetid: 3358a89f-44a0-4a4d-bf8c-07237a90af39
ms.openlocfilehash: 4a14c2bf80ff203c5db7fc7663afeb816dc4a2c0
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589474"
---
# <a name="comparison-between-properties-and-indexers-c-programming-guide"></a>속성 및 인덱서 비교(C# 프로그래밍 가이드)
인덱서는 속성과 비슷합니다. 다음 표에 나와 있는 차이점을 제외하면 속성 접근자에 대해 정의된 모든 규칙이 인덱서 접근자에도 적용됩니다.  
  
|속성|인덱서|  
|--------------|-------------|  
|공용 데이터 멤버인 것처럼 메서드를 호출할 수 있게 합니다.|개체 자체에 배열 표기법을 사용하여 개체의 내부 컬렉션 요소에 액세스할 수 있게 합니다.|  
|단순한 이름을 통해 액세스합니다.|인덱스를 통해 액세스합니다.|  
|정적 또는 인스턴스 멤버일 수 있습니다.|인스턴스 멤버여야 합니다.|  
|속성의 [get](../../language-reference/keywords/get.md) 접근자에는 매개 변수가 없습니다.|인덱서의 `get` 접근자에는 인덱서와 동일한 형식 매개 변수 목록이 있습니다.|  
|속성의 [set](../../language-reference/keywords/set.md) 접근자에는 암시적 `value` 매개 변수가 포함되어 있습니다.|인덱서의 `set` 접근자에는 인덱서와 동일한 형식 매개 변수 목록이 있으며 [value](../../language-reference/keywords/value.md) 매개 변수도 있습니다.|  
|[자동으로 구현된 속성](../classes-and-structs/auto-implemented-properties.md)을 사용하여 약식 구문을 지원합니다.|가져오기만 수행(Get only) 인덱서를 위한 식 본문 멤버를 지원합니다.|  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [인덱서](./index.md)
- [속성](../classes-and-structs/properties.md)
