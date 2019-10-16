---
title: 형식 디자인 지침
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines
- type design guidelines, about type design guidelines
- class library design guidelines [.NET Framework], type design guidelines
- types [.NET Framework], design guidelines
ms.assetid: 6b49314e-8bba-43ea-97ca-4e0255812f95
author: KrzysztofCwalina
ms.openlocfilehash: 16f2a095f461a406eedbd2b34b0c91d3ac43bbe5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61650104"
---
# <a name="type-design-guidelines"></a>형식 디자인 지침
CLR 관점에서 보면는 두 가지 범주의 형식-참조 형식과 값 형식-있지만 프레임 워크 디자인에 대 한 토론을 하기 위해 고유한 특정 디자인 규칙을 사용 하 여 각 논리적인 그룹으로 형식 나눕니다.  
  
 클래스는 참조 형식의 일반적인 경우입니다. 이러한 대부분의 프레임 워크에서 형식의 대량 구성 합니다. 클래스 일반 적용 가능성을 다양 한 지 원하는 개체 지향 기능 집합을 해당 인기도 미납 합니다. 기본 클래스가 추상 클래스와 확장성 관련 된 특별 한 논리 그룹입니다.  
  
 인터페이스는 형식을 구현할 수 있는 참조 형식과 값 형식입니다. 따라서 참조 형식과 값 형식의 다형 계층의 루트로 사용 수 있습니다. 또한 기본적으로 CLR에서 지원 되지 않는 여러 상속을 시뮬레이트하려 인터페이스를 사용할 수 있습니다.  
  
 구조체 값 형식의 일반적인 경우는 및 언어 기본 형식에 유사한 간단한 형식에 대 한 예약 해야 합니다.  
  
 열거형은 특수 한 일의 주, 콘솔 색 등과 같은 값의 간단한 집합을 정의 하는 데 사용 되는 값 형식입니다.  
  
 정적 클래스는 정적 멤버에 대 한 컨테이너를 사용 하는 형식입니다. 일반적으로 다른 작업에 대 한 바로 가기를 제공에 사용 됩니다.  
  
 대리자, 예외, 특성, 배열 및 컬렉션은 특정 용도 위한 참조 형식의 모든 특별 한 경우 및 해당 디자인 및 사용에 대 한 지침은이 가이드의 다른 곳에서 설명 합니다.  
  
 **✓ DO** 각 형식이 관련 되지 않은 기능의 임의 컬렉션 뿐 아니라 관련된 멤버의 잘 정의 된 집합 지 확인 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [클래스와 구조체 간의 선택](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)  
 [추상 클래스 디자인](../../../docs/standard/design-guidelines/abstract-class.md)  
 [정적 클래스 디자인](../../../docs/standard/design-guidelines/static-class.md)  
 [인터페이스 디자인](../../../docs/standard/design-guidelines/interface.md)  
 [구조체 디자인](../../../docs/standard/design-guidelines/struct.md)  
 [열거형 디자인](../../../docs/standard/design-guidelines/enum.md)  
 [중첩 형식](../../../docs/standard/design-guidelines/nested-types.md)  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
