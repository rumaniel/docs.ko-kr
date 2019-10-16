---
title: 생성자 디자인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines, constructors
- constructors, design guidelines
- instance constructors
- type constructors
- virtual members
- constructors, types
- parameterless constructors
- static constructors
ms.assetid: b4496afe-5fa7-4bb0-85ca-70b0ef21e6fc
author: KrzysztofCwalina
ms.openlocfilehash: a43ec815275e58f4bc6462fb4f5cb4733267de31
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68972110"
---
# <a name="constructor-design"></a>생성자 디자인

생성자에는 형식 생성자와 인스턴스 생성자의 두 종류가 있습니다.

형식 생성자는 정적 이며 형식을 사용 하기 전에 CLR에서 실행 됩니다. 인스턴스 생성자는 형식의 인스턴스를 만들 때 실행 됩니다.

형식 생성자는 매개 변수를 사용할 수 없습니다. 인스턴스 생성자는 가능 합니다. 매개 변수를 사용 하지 않는 인스턴스 생성자를 종종 매개 변수가 없는 생성자 라고 합니다.

생성자는 형식의 인스턴스를 만드는 가장 일반적인 방법입니다. 대부분의 개발자는 인스턴스를 만드는 다른 방법 (예: 팩터리 메서드)을 고려 하기 전에 생성자를 검색 하 고 사용 하려고 합니다.

**✓ CONSIDER** 단순, 이상적으로 기본적으로 생성자를 제공 합니다.

간단한 생성자에는 매우 적은 수의 매개 변수가 있고 모든 매개 변수는 기본 형식 또는 열거형입니다. 이러한 간단한 생성자는 프레임 워크의 유용성을 향상 시킵니다.

**✓ CONSIDER** 원하는 작업의 의미 체계의 새 인스턴스를 생성에 직접 매핑되지 않는 경우 또는 비 자연 느낌 생성자 설계 지침을 따르는 경우 생성자를 대신 정적 팩터리 메서드를 사용 합니다.

**✓ DO** 가기로 생성자 매개 변수를 사용 하 여 기본 속성을 설정 합니다.

빈 생성자와 몇 가지 속성 집합을 사용 하 고 여러 인수를 사용 하는 생성자를 사용 하는 경우에는 의미 체계가 차이가 없어야 합니다.

**✓ DO** 생성자 매개 변수는 단순히 속성을 설정 하는 데 사용 되는 경우 생성자 매개 변수 및 속성에 대 한 동일한 이름을 사용 합니다.

이러한 매개 변수와 속성의 유일한 차이점은 대/소문자를 구분 해야 합니다.

**✓ DO** 생성자에서 최소한의 작업만 있습니다.

생성자는 생성자 매개 변수를 캡처하는 것 보다 많은 작업을 수행 하면 안 됩니다. 다른 처리 비용은 필요할 때까지 지연 되어야 합니다.

**✓ DO** 해당 되는 경우에 인스턴스 생성자에서 예외를 throw 합니다.

이러한 생성자가 필요한 경우 **✓** 은 클래스에서 매개 변수가 없는 public 생성자를 명시적으로 선언 합니다.

형식에 대 한 생성자를 명시적으로 선언 하지 않으면와 C#같은 많은 언어에서 매개 변수가 없는 public 생성자가 자동으로 추가 됩니다. 추상 클래스는 보호 된 생성자를 가져옵니다.

매개 변수가 있는 생성자를 클래스에 추가 하면 컴파일러가 매개 변수가 없는 생성자를 추가 하지 않습니다. 이로 인해 실수로 인 한 변경 사항이 발생할 수도 있습니다.

X 구조체에서 매개 변수가 없는 생성자를 명시적으로 정의 **하지 않습니다** .

이렇게 하면 매개 변수가 없는 생성자가 정의 되지 않은 경우 배열의 모든 슬롯에서 실행할 필요가 없기 때문에 배열을 더 빠르게 만들 수 있습니다. 를 비롯 C#한 대부분의 컴파일러에서는 이러한 이유로 구조체에 매개 변수가 없는 생성자를 포함할 수 없습니다.

**X AVOID** 개체의 생성자 내에서 가상 멤버를 호출 합니다.

가장 많이 파생 된 형식의 생성자가 아직 완전히 실행 되지 않은 경우에도 가상 멤버를 호출 하면 가장 많이 파생 된 재정의가 호출 됩니다.

## <a name="type-constructor-guidelines"></a>형식 생성자 지침

**✓ DO** 정적 생성자를 private입니다.

클래스 생성자 라고도 하는 정적 생성자는 형식을 초기화 하는 데 사용 됩니다. CLR에서는 형식의 첫 번째 인스턴스가 만들어지거나 해당 형식의 정적 멤버가 호출 되기 전에 정적 생성자를 호출 합니다. 사용자는 정적 생성자가 호출 되는 시기를 제어할 수 없습니다. Static 생성자가 private이 아니면 CLR 이외의 코드에서 호출 될 수 있습니다. 생성자에서 수행 되는 작업에 따라 예기치 않은 동작이 발생할 수 있습니다. 컴파일러 C# 는 정적 생성자를 private로 강제로 적용 합니다.

**X DO NOT** 정적 생성자에서 예외를 throw 합니다.

형식 생성자에서 예외가 throw 되는 경우 현재 응용 프로그램 도메인에서 형식을 사용할 수 없습니다.

**✓ CONSIDER** 런타임 형식에서 명시적으로 정의 된 정적 생성자를 갖지 않는의 성능을 최적화할 수 있기 때문에 정적 생성자를 사용 하 여 명시적으로 보다는 정적 필드 인라인을 초기화 합니다.

*Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*

*받고 재인쇄 되었습니다는 피어슨 교육, inc. 프레임 워크 디자인 지침 [에서 사용 권한입니다. 다시 사용할 수 있는 .net 라이브러리에 대 한 규칙, 관용구 및](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 패턴, Microsoft Windows 개발 시리즈의 일부로 addison-Wesley Professional에서 2008 년 10 월 22 일에 게시 된 Krzysztof Cwalina 및 Brad abrams 성*

## <a name="see-also"></a>참고자료

- [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
