---
title: 인터페이스 디자인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- interfaces [.NET Framework], design guidelines
- type design guidelines, interfaces
- class library design guidelines [.NET Framework], interfaces
ms.assetid: a016bd18-6710-4358-9438-9f190a295392
author: KrzysztofCwalina
ms.openlocfilehash: 1f982aa37f92b7270725574d949989ca120297d5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026369"
---
# <a name="interface-design"></a>인터페이스 디자인
대부분의 Api는 클래스 및 구조체를 사용 하 여 모델링 가장 하지만 인터페이스 더 적합 하거나 옵션만 경우가 있습니다.  
  
 CLR 다중 상속을 지원 하지 않습니다 (즉, CLR 클래스 수 없습니다. 둘 이상의 기본 클래스에서 상속), 않지만 형식을 기본 클래스에서 상속 하는 것 외에도 하나 이상의 인터페이스를 구현할 수 있습니다. 따라서 인터페이스 다중 상속의 효과 달성 하기 위해 자주 사용 됩니다. 예를 들어 <xref:System.IDisposable> disposability 참여 하고자 하는 다른 상속 계층 구조 관계 없이 지원 하기 위한 형식을 허용 하는 인터페이스입니다.  
  
 인터페이스는 적절 한 정의 다른 상황에서 일부 값 형식을 비롯 한 여러 형식을 지원할 수 있는 공통 인터페이스를 만드는 경우 값 형식 이외의 형식에서 상속할 수 없습니다 <xref:System.ValueType>, 공통 기본 형식을 제공 하기 위해 유일한 옵션은 인터페이스를 사용 하 여 하지만 인터페이스를 구현할 수 있습니다.  
  
 **✓ DO** 값 형식을 포함 하는 형식의 집합 지원을 받기 위해 일부 공통 API 해야 하는 경우 인터페이스를 정의 합니다.  
  
 **✓ CONSIDER** 이미 다른 형식에서 상속 되는 형식에서 해당 기능을 지 원하는 데 필요한 경우 인터페이스를 정의 합니다.  
  
 **X AVOID** 표식 인터페이스 (멤버 없이 인터페이스)를 사용 합니다.  
  
 클래스 (표식) 특정 특성을 가진 것으로 표시 하는 경우 일반적으로 사용 하 여 인터페이스 보다는 사용자 지정 특성을 합니다.  
  
 **✓ DO** 인터페이스의 구현 하는 하나 이상의 형식을 제공 합니다.  
  
 이 사용이 하면 인터페이스의 디자인 유효성 검사를 수행 합니다. 예를 들어 <xref:System.Collections.Generic.List%601> 구현인는 <xref:System.Collections.Generic.IList%601> 인터페이스입니다.  
  
 **✓ DO** 정의 하는 각 인터페이스를 사용 하는 하나 이상의 API를 제공 (매개 변수 또는 속성으로 인터페이스 하는 메서드는 인터페이스와 입력).  
  
 이 사용이 하면 인터페이스 디자인 유효성 검사를 수행 합니다. 예를 들어 <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> 소비는 <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> 인터페이스입니다.  
  
 **X DO NOT** 이전에 제공한 하는 인터페이스에 멤버를 추가 합니다.  
  
 이렇게 하면 인터페이스의 구현 작동 하지 않으므로 합니다. 버전 관리 문제를 방지 하기 위해 새 인터페이스를 만들어야 합니다.  
  
 이러한 지침에 설명 된 경우를 제외 하 고, 일반적으로 선택 해야 인터페이스 대신 클래스 재사용 가능한 라이브러리를 관리 되는 코드를 디자인 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [형식 디자인 지침](../../../docs/standard/design-guidelines/type.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
