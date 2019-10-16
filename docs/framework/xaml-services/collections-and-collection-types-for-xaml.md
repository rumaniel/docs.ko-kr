---
title: XAML을 위한 컬렉션 및 컬렉션 형식
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 63f6346837f77dbdbdcb4a90ec5af725be69ee02
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68364330"
---
# <a name="collections-and-collection-types-for-xaml"></a>XAML을 위한 컬렉션 및 컬렉션 형식

이 항목에서는 컬렉션을 지원 하기 위해 사용 되는 형식의 속성을 정의 하 고 부모 개체 요소나 속성 요소의 요소 자식으로 컬렉션 항목을 인스턴스화하는 XAML 구문을 지 원하는 방법에 대해 설명 합니다.

## <a name="xaml-collection-concepts"></a>XAML 컬렉션 개념

Xaml 개체 요소 또는 XAML 속성 요소의 범위 내에 자식 항목이 여러 개 있는 XAML의 모든 관계는 개념적으로 구현 해야 합니다. 해당 컬렉션은 해당 관계의 부모인 XAML 형식의 특정 XAML 속성과 연결 되어야 합니다. XAML 프로세서가 태그의 각 항목을 지원 컬렉션 속성의 새로 추가 된 항목으로 할당 해야 하므로이 속성은 컬렉션 이어야 합니다.

XAML 언어 수준에서 컬렉션 지원의 정확한 요구 사항은 완전히 정의 되지 않았습니다. 컬렉션은 목록 또는 사전 (둘 다는 아님)이 XAML 언어 수준에서 정의 될 수 있지만, 목록 또는 사전을 나타내는 백업 형식은 XAML 언어로 정의 되지 않습니다.

.NET Framework XAML 서비스에서 XAML 컬렉션 지원의 개념은 .NET Framework 지원 형식 측면에서 보다 명확 하 게 정의 됩니다. 특히 컬렉션에 대 한 XAML 지원은 일반적인 .NET Framework 프로그래밍에서 목록과 사전에 사용 되는 여러 .NET Framework 개념과 Api를 기반으로 합니다.

1. 인터페이스 <xref:System.Collections.IList> 는 목록 컬렉션을 나타냅니다.

2. 인터페이스 <xref:System.Collections.IDictionary> 는 사전 컬렉션을 나타냅니다.

3. <xref:System.Array>는 배열을 나타내며 배열은 메서드를 지원 <xref:System.Collections.IList> 합니다.

이러한 각 컬렉션 개념에서 .NET Framework xaml 서비스 xaml 프로세서는 컬렉션 속성 형식의 특정 인스턴스에 대해 `Add` 메서드를 호출 해야 합니다. 또는 serialization 시나리오에서 XAML 프로세서는 "Items"의 각 컬렉션의 특정 개념을 기준으로 목록, 사전 또는 배열에 있는 각 항목에 대해 불연속 XAML 형식 인스턴스를 생성 합니다. 는 다음과 같습니다 <xref:System.Collections.IList.Item%2A>. <xref:System.Collections.IDictionary.Item%2A>, <xref:System.Array.System%23Collections%23IList%23Item%2A> 의 경우<xref:System.Array>explicit입니다.

## <a name="generic-collections"></a>제네릭 컬렉션

제네릭 컬렉션은 일반적인 .NET Framework 프로그래밍에 유용할 수 있으며 XAML 컬렉션 속성에도 사용할 수 있습니다. 그러나 제네릭 인터페이스 <xref:System.Collections.Generic.IList%601> 및 <xref:System.Collections.Generic.IDictionary%602> 는 .NET Framework xaml 서비스 xaml 프로세서에서 제네릭이 <xref:System.Collections.IList> 아닌 또는 <xref:System.Collections.IDictionary>와 동등한 것으로 식별 되지 않습니다. 인터페이스를 구현 하는 대신 제네릭 컬렉션 속성 형식에 권장 되는 방법은 클래스 <xref:System.Collections.Generic.List%601> 또는 <xref:System.Collections.Generic.Dictionary%602>에서 파생 하는 것입니다. 이러한 클래스는 제네릭이 아닌 인터페이스를 구현 하므로 기본 구현에서 XAML 컬렉션에 대해 예상 되는 지원이 포함 됩니다.

## <a name="read-only-collections-and-initialization-logic"></a>읽기 전용 컬렉션 및 초기화 논리

.NET Framework 프로그래밍에서 컬렉션의 값을 포함 하는 모든 속성을 읽기 전용 컬렉션으로 설정 하는 것은 일반적인 디자인 패턴입니다. 이 패턴은 컬렉션 속성을 소유 하는 인스턴스가 컬렉션의 결과를 더 잘 제어할 수 있도록 합니다. 특히이 패턴은 속성을 설정 하 여 기존 컬렉션 전체를 실수로 대체 하지 못하도록 합니다. 이 패턴에서 호출자가 컬렉션에 액세스 하는 것은 대신 컬렉션 형식 및/또는 관련 컬렉션 인터페이스 (예: <xref:System.Collections.IList>)에서 지 원하는 메서드나 속성을 호출 하 여 수행 해야 합니다.

이 패턴을 사용 하는 경우 읽기 전용 컬렉션 속성을 노출 하는 모든 클래스는 먼저 빈 컬렉션을 포함 하도록 해당 속성을 초기화 해야 합니다. 일반적으로 초기화는 클래스에 대 한 생성 동작의 일부로 수행 됩니다. Xaml에 유용 하 게 사용할 수 있습니다. XAML은 일반적으로 속성 (컬렉션 속성 또는 기타)을 처리 하기 전에 매개 변수가 없는 생성자를 호출 하기 때문에 매개 변수가 없는 생성자가 항상 이러한 논리를 참조 하는 것이 중요 합니다.

## <a name="xaml-type-system-support-and-collections"></a>XAML 형식 시스템 지원 및 컬렉션

Xaml을 구문 분석 하 고 컬렉션 속성을 채우거 나 직렬화 하는 기본 메커니즘 외에도 .NET Framework XAML 서비스에 구현 된 XAML 형식 시스템에는 XAML의 컬렉션과 관련 된 몇 가지 디자인 기능이 포함 되어 있습니다.

1. <xref:System.Xaml.XamlType.IsCollection%2A>xaml 형식이 XAML 컬렉션 지원을 제공 하는 형식으로 지원 되는 경우 true를 반환 합니다.

2. <xref:System.Xaml.XamlType.IsDictionary%2A>및 <xref:System.Xaml.XamlType.IsArray%2A> 는 XAML 형식이 지 원하는 컬렉션 모드를 추가로 식별할 수 있습니다. .NET Framework xaml 서비스 및 xaml 형식 시스템을 기반으로 하지만 기존 <xref:System.Xaml.XamlWriter> 구현을 기반으로 하지 않는 사용자 지정 xaml 프로세서의 경우 호출할 메서드를 파악 하기 위해 사용 되는 컬렉션 모드가 무엇 인지 파악 해야 할 수 있습니다. 컬렉션 처리

3. 위의 각 속성 값은 XAML 형식에 대 한의 <xref:System.Xaml.XamlType.LookupCollectionKind%2A> 재정의에 의해 영향을 받을 수 있습니다.
