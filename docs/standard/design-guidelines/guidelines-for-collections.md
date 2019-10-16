---
title: 컬렉션에 대한 지침
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 297b8f1d-b11f-4dc6-960a-8e990817304e
author: KrzysztofCwalina
ms.openlocfilehash: a8e8672d71500478dbbe28512e413e8ada501f45
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61669051"
---
# <a name="guidelines-for-collections"></a>컬렉션에 대한 지침
몇 가지 일반적인 특징이 포함 된 개체의 그룹을 조작 하도록 특별히 설계 된 모든 형식에 컬렉션을 간주할 수 있습니다. 이러한 형식 구현에 대 한 적절 한 것은 항상 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.Generic.IEnumerable%601>이므로이 섹션에서는 고려 컬렉션 되도록 해당 인터페이스 중 하나 또는 모두를 구현 하는 형식입니다.  
  
 **X DO NOT** 공용 Api에서 약한 형식의 컬렉션을 사용 합니다.  
  
 모든 반환 값 및 컬렉션 항목을 나타내는 매개 변수 형식 (컬렉션의 public 멤버에만 적용) 해당 기본 형식의 하지 정확한 항목 형식에 있어야 합니다.  
  
 **X DO NOT** 사용 <xref:System.Collections.ArrayList> 또는 <xref:System.Collections.Generic.List%601> 공용 Api에서 합니다.  
  
 이러한 유형은 공용 Api에 없는 내부 구현에 사용 하기 위한 데이터 구조입니다. `List<T>` Api 및 유연성 cleanness 하더라도 기능과 성능을 위해 최적화 됩니다. 예를 들어, 반환 하는 경우 `List<T>`, 어느 됩니다 클라이언트 코드에서 컬렉션을 수정할 때 알림을 받을 수 있게 합니다. 또한 `List<T>` 와 같은 많은 멤버를 노출 <xref:System.Collections.Generic.List%601.BinarySearch%2A>를 유용 하거나 다양 한 시나리오에 적용 됩니다. 다음 두 섹션에서는 형식 (추상화) 공용 Api에서 사용 하기 위해 특별히 설계를 설명 합니다.  
  
 **X DO NOT** 사용 `Hashtable` 또는 `Dictionary<TKey,TValue>` 공용 Api에서 합니다.  
  
 이러한 유형은 내부 구현에 사용 하기 위한 데이터 구조입니다. 공용 Api를 사용할지 <xref:System.Collections.IDictionary>, `IDictionary <TKey, TValue>`, 또는 인터페이스 중 하나 또는 모두를 구현 하는 사용자 지정 형식입니다.  
  
 **X DO NOT** 사용 <xref:System.Collections.Generic.IEnumerator%601>, <xref:System.Collections.IEnumerator>, 또는 다른 종류의 반환 형식으로 제외 하 고 이러한 인터페이스를 구현 하는 `GetEnumerator` 메서드.  
  
 이외의 다른 메서드에서 열거자를 반환 하는 형식 `GetEnumerator` 와 함께 사용할 수는 `foreach` 문입니다.  
  
 **X DO NOT** 둘 다 구현 `IEnumerator<T>` 및 `IEnumerable<T>` 을 같은 형식의 합니다. 제네릭이 아닌 인터페이스에도 마찬가지 `IEnumerator` 고 `IEnumerable`입니다.  
  
## <a name="collection-parameters"></a>컬렉션 매개 변수  
 **✓ DO** 는 최소 특수 형식 가능한 매개 변수 형식으로 사용 합니다. 사용 하는 매개 변수 컬렉션을 수행 하는 대부분의 멤버는 `IEnumerable<T>` 인터페이스입니다.  
  
 **X AVOID** 를 사용 하 여 <xref:System.Collections.Generic.ICollection%601> 또는 <xref:System.Collections.ICollection> 액세스를 매개 변수로 `Count` 속성입니다.  
  
 대신 사용 하는 것이 좋습니다 `IEnumerable<T>` 나 `IEnumerable` 동적으로 개체를 구현 하는지 여부를 확인 하 고 `ICollection<T>` 또는 `ICollection`합니다.  
  
## <a name="collection-properties-and-return-values"></a>컬렉션의 속성 및 반환 값  
 **X DO NOT** 설정 가능한 컬렉션 속성을 제공 합니다.  
  
 컬렉션을 먼저 선택 취소 한 다음 새 콘텐츠를 추가 하 여 컬렉션의 콘텐츠를 바꿀 수 있습니다. 일반적인 시나리오를 전체 컬렉션을 대체 하는 경우 사용 하십시오는 `AddRange` 메서드 컬렉션입니다.  
  
 **✓ DO** 사용 `Collection<T>` 또는 하위 클래스 `Collection<T>` 속성 또는 반환 값 나타내는 읽기/쓰기 컬렉션입니다.  
  
 하는 경우 `Collection<T>` 몇 가지 요구 사항을 충족 하지 않습니다 (예를 들어, 컬렉션 구현 하지 해야 합니다 <xref:System.Collections.IList>)를 구현 하 여 사용자 지정 컬렉션을 사용 하 여 `IEnumerable<T>`, `ICollection<T>`, 또는 <xref:System.Collections.Generic.IList%601>합니다.  
  
 **✓ DO** 사용 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>의 서브 클래스 `ReadOnlyCollection<T>`, 또는 드물지만에서 `IEnumerable<T>` 속성 또는 반환 값을 나타내는 읽기 전용 컬렉션에 대 한 합니다.  
  
 일반적으로 선호 `ReadOnlyCollection<T>`합니다. 일부 요구 사항에 맞지 않는 경우 (예를 들어, 컬렉션 구현 하지 해야 `IList`)를 구현 하 여 사용자 지정 컬렉션을 사용 하 여 `IEnumerable<T>`, `ICollection<T>`, 또는 `IList<T>`합니다. 사용자 지정 읽기 전용 컬렉션을 구현 하는 경우 구현 `ICollection<T>.IsReadOnly` 반환할 `true`합니다.  
  
 지원 하려는 유일한 시나리오는 앞 으로만 이동 가능한 반복 인지는 경우에 사용할 수 있습니다 단순히 `IEnumerable<T>`합니다.  
  
 **✓ CONSIDER** 제네릭 기본 컬렉션의 하위 클래스를 사용 하 여 컬렉션을 직접 사용 하는 대신 합니다.  
  
 이렇게 하면 기본 컬렉션 형식에 존재 하지 않는 도우미 멤버를 추가 하는 더 나은 이름에 대 한 합니다. 특히 한 상위 수준 Api에 적용 됩니다.  
  
 **✓ CONSIDER** 의 서브 클래스를 반환 `Collection<T>` 또는 `ReadOnlyCollection<T>` 에서 매우 흔히 사용 되는 메서드 및 속성입니다.  
  
 이렇게 하면 해당 도우미 메서드를 추가 하거나 컬렉션 구현을 나중에 변경할 수 있습니다.  
  
 **✓ CONSIDER** 컬렉션에 저장 된 항목에는 고유 키가 있는 경우 키 컬렉션을 사용 하 여 (이름, Id 등.). 키가 지정 된 컬렉션은 정수 키와 키 모두에 인덱싱될 수 및에서 상속 하 여 일반적으로 구현 되는 컬렉션 `KeyedCollection<TKey,TItem>`합니다.  
  
 키 컬렉션 일반적으로 더 큰 메모리 용량 있고 메모리 오버 헤드는 키를 갖는 것의 이점을 능가 하는 경우 사용할 수 해야 합니다.  
  
 **X DO NOT** 컬렉션 속성에서 또는 컬렉션을 반환 하는 방법 중에서 null 값을 반환 합니다. 빈 컬렉션 또는 빈 배열을 대신 반환 합니다.  
  
 Null 및 빈 (항목 0) 컬렉션 또는 배열 이어야 합니다는 일반적인 규칙은 동일 하 게 처리 합니다.  
  
### <a name="snapshots-versus-live-collections"></a>라이브 컬렉션 및 스냅숏  
 컬렉션의에서 일부 지점에서 상태를 나타내는 스냅숏 컬렉션 이라고 합니다. 예를 들어 데이터베이스 쿼리에서 반환 되는 행을 포함 하는 컬렉션 스냅숏을 것입니다. 항상 현재 상태를 나타내는 컬렉션 라이브 컬렉션 이라고 합니다. 예를 들어 컬렉션인 `ComboBox` 항목은 라이브 컬렉션입니다.  
  
 **X DO NOT** 속성에서 스냅숏 컬렉션을 반환 합니다. 속성은 라이브 컬렉션을 반환 합니다.  
  
 속성 getter를 매우 간단한 작업 해야 합니다. O (n) 작업에서 내부 컬렉션의 복사본을 만들어야 스냅숏을 반환 합니다.  
  
 **✓ DO** 스냅숏 컬렉션 또는 라이브를 사용 하 여 `IEnumerable<T>` (또는 해당 하위 유형)을 휘발성 하는 컬렉션을 나타내는 (즉, 하는 변경할 수 명시적으로 컬렉션을 수정 하지 않고).  
  
 일반적으로 공유 리소스 (예: 디렉터리의 파일)을 나타내는 하는 모든 컬렉션은 일시적입니다. 이러한 컬렉션은 단순히 정방향 전용 열거자를 구현 하지 않는 한 라이브 컬렉션으로 구현 하기가 매우 어렵거나은입니다.  
  
## <a name="choosing-between-arrays-and-collections"></a>배열 및 컬렉션 중에서 선택  
 **✓ DO** 배열을 통해 컬렉션을 선호 합니다.  
  
 컬렉션은 내용 보다 잘 제어할 시간이 지나면서 수 및 더 사용할 수 있습니다. 또한 읽기 전용 시나리오에 대 한 배열 사용은 권장 되지 않습니다 배열 복제의 비용 중 감당 하기 어려운 이므로 합니다. 일부 개발자는 컬렉션 기반 Api를 사용 하 여 불편 함을 느끼지 유용성 연구 표시 합니다.  
  
 그러나 하위 수준 Api를 개발 하는 경우 읽기 / 쓰기 시나리오에 대 한 배열을 사용 하 여 수 있습니다. 배열 작업 집합을 줄일 수 있습니다, 작은 메모리 공간을 있고 런타임에서 최적화 되기 때문에 배열의 요소에 대 한 액세스 빠릅니다.  
  
 **✓ CONSIDER** 메모리 소비를 최소화 하 고 성능을 최대화 하려면 배열 낮은 수준의 Api에서 사용 합니다.  
  
 **✓ DO** 바이트 배열 바이트의 컬렉션 대신 사용 합니다.  
  
 **X DO NOT** 속성 getter 속성을 호출할 때마다 새 배열 (예: 내부 배열 복사본)을 반환 해야 하는 경우 속성에 대 한 배열을 사용 합니다.  
  
## <a name="implementing-custom-collections"></a>사용자 지정 컬렉션 구현  
 **✓ CONSIDER** 에서 상속 `Collection<T>`, `ReadOnlyCollection<T>`, 또는 `KeyedCollection<TKey,TItem>` 새 컬렉션을 디자인 하는 경우.  
  
 **✓ DO** 구현 `IEnumerable<T>` 새 컬렉션을 디자인 하는 경우. 구현 하는 것이 좋습니다 `ICollection<T>` 심지어 `IList<T>` 것이 적합 합니다.  
  
 이러한 사용자 지정 컬렉션을 구현할 때 설정한 API 패턴을 따릅니다 `Collection<T>` 고 `ReadOnlyCollection<T>` 최대한 근접 하 게 합니다. 즉, 동일한 멤버를 명시적으로 구현, 및 등이 두 컬렉션 이름 같은 매개 변수 이름을 지정 합니다.  
  
 **✓ CONSIDER** 제네릭이 아닌 컬렉션 인터페이스를 구현 (`IList` 및 `ICollection`) 컬렉션 입력으로 이러한 인터페이스를 라인 Api에 전달 경우가 많습니다.  
  
 **X AVOID** 관련 되지 않은 컬렉션의 개념을 복잡 한 Api와 형식에 컬렉션 인터페이스를 구현 합니다.  
  
 **X DO NOT** 와 같은 제네릭이 아닌 기본 컬렉션에서 상속할 `CollectionBase`합니다. 사용 하 여 `Collection<T>`하십시오 `ReadOnlyCollection<T>`, 및 `KeyedCollection<TKey,TItem>` 대신 합니다.  
  
### <a name="naming-custom-collections"></a>사용자 지정 컬렉션 이름 지정  
 컬렉션 (구현 하는 형식을 `IEnumerable`) 주로 두 가지 이유로 생성 됩니다. (1) 구조를 만들려면 새 데이터에 자주 구조 별 작업을 사용 하 여 기존 데이터 구조 보다 다양 한 성능 특성 (예를 들어 <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.LinkedList%601>, <xref:System.Collections.Generic.Stack%601>), 및 (2)에 대 한 특수 한 컬렉션 만들기 항목의 특정 집합을 보유 합니다. (예를 들어 <xref:System.Collections.Specialized.StringCollection>). 데이터 구조는 응용 프로그램 및 라이브러리의 내부 구현에서 가장 자주 사용 됩니다. 특수 컬렉션 Api에서 (속성 및 매개 변수 형식)으로 표시 되기 위해 주로 됩니다.  
  
 **✓ DO** 의 추상화를 구현 하는 이름에 "사전" 접미사를 사용 하 여 `IDictionary` 또는 `IDictionary<TKey,TValue>`합니다.  
  
 **✓ DO** 구현 하는 형식 이름에 "Collection" 접미사 사용 `IEnumerable` (또는 해당 하위 항목의) 및 항목 목록을 표시 합니다.  
  
 **✓ DO** 사용자 지정 데이터 구조에 대 한 적절 한 데이터 구조 이름을 사용 합니다.  
  
 **X AVOID** 컬렉션 추상화의 이름에 "LinkedList" 또는 "Hashtable" 등의 특정 구현 암시 모든 접미사를 사용 합니다.  
  
 **✓ CONSIDER** 항목 형식의 이름이 포함 된 컬렉션 이름을 접두사로 사용 합니다. 예를 들어, 형식 항목을 저장 하면 컬렉션인 `Address` (구현 `IEnumerable<Address>`) 이름을 지정 해야 `AddressCollection`합니다. 접두사 "I" 항목 형식이 인터페이스 이면 항목의 종류를 생략할 수 있습니다. 따라서 컬렉션인 <xref:System.IDisposable> 항목을 호출할 수 있습니다 `DisposableCollection`합니다.  
  
 **✓ CONSIDER** 해당 쓰기 가능한 컬렉션 추가 될 수 있는 프레임 워크에 이미 있는 경우 읽기 전용 컬렉션의 이름에 "ReadOnly" 접두사를 사용 합니다.  
  
 문자열의 읽기 전용 컬렉션을 호출 해야 하는 예를 들어 `ReadOnlyStringCollection`합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [사용 지침](../../../docs/standard/design-guidelines/usage-guidelines.md)
