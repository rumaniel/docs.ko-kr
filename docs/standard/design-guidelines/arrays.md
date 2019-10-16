---
title: 배열
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], arrays
- arrays [.NET Framework], usage guidelines
- empty arrays
ms.assetid: 66a1b3d8-6f3f-4715-b235-e1ff95e32d8e
author: KrzysztofCwalina
ms.openlocfilehash: dd30cdee0440553a9f955f0b3f4ee420e938b9ea
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864119"
---
# <a name="arrays"></a>배열
**✓ DO** 공용 Api에서 배열을 통해 컬렉션을 사용 하는 것을 선호 합니다. 합니다 [컬렉션](../../../docs/standard/design-guidelines/guidelines-for-collections.md) 섹션에서는 컬렉션 및 배열 중에서 선택 하는 방법에 대 한 세부 정보를 제공 합니다.  
  
 **X DO NOT** 읽기 전용 배열 필드를 사용 합니다. 필드 자체 읽기 전용 이며 변경할 수 없습니다. 하지만 배열의 요소를 변경할 수 있습니다.  
  
 **✓ CONSIDER** 다차원 배열 대신 가변된 배열을 사용 합니다.  
  
 가변된 배열에 있는 배열 요소를 사용 하 여 배열이입니다. 요소를 구성 하는 배열의 앞에 공간을 절약할 일부 (예: 스파스 행렬) 데이터 집합에 대 한 다차원 배열에 비해 다양 한 일 수 있습니다. 또한 CLR 하므로 일부 시나리오에서는 런타임 성능이 향상을 나타낼 수 있습니다 이러한 가변된 배열에서 인덱스 작업을 최적화 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- <xref:System.Array>
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [사용 지침](../../../docs/standard/design-guidelines/usage-guidelines.md)
