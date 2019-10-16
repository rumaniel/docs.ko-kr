---
title: 열거형 디자인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, enumerations
- simple enumerations
- enumerations [.NET Framework], design guidelines
- class library design guidelines [.NET Framework], enumerations
- flags enumerations
ms.assetid: dd53c952-9d9a-4736-86ff-9540e815d545
author: KrzysztofCwalina
ms.openlocfilehash: e890ebbbeb04ca424b84c11791e5ce7fa55db72e
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663473"
---
# <a name="enum-design"></a>열거형 디자인

열거형은 값 형식의 특수 한 종류입니다. 두 가지 종류의 열거형: 단순 열거형 및 플래그 열거형입니다.

단순 열거형 선택 닫힌된 작은 집합을 나타냅니다. 단순 열거형의 일반적인 예로 색 집합입니다.

플래그 열거형은 열거형 값에 비트 작업을 지원 하도록 설계 되었습니다. 플래그 열거형의 일반적인 예로 옵션 목록입니다.

**✓ DO** 열거형을 사용 하 여 강력한 형식의 매개 변수, 속성 및 값 집합을 나타내는 값을 반환 합니다.

**✓ DO** 정적 상수 대신 열거형을 사용 합니다.

**X DO NOT** 집합 (예: 운영 체제 버전, 친구, 등의 이름입니다.)에 대 한 열거형을 사용 합니다.

**X DO NOT** 나중에 사용할 수는 예약 된 열거형 값을 제공 합니다.

이후 단계에서 기존 열거형에 값을 항상 간단히 추가할 수 있습니다. 참조 [열거형에 값 추가](#add_value) 열거형에 값을 추가 하는 대 한 자세한 내용은 합니다. 예약 된 값만 실제 값 집합을 손상 시 키 지 하 고 사용자 오류가 발생 하는 경향이 있습니다.

**X AVOID** 열거형 값을 하나만로 공개적으로 노출 합니다.

C Api의 향후 확장성을 보장 하기 위한 일반적인 방법은 예약 된 매개 변수 메서드 시그니처를 추가 합니다. 이러한 예약 된 매개 변수는 단일 기본 값을 사용 하 여 열거형으로 표현할 수 있습니다. 관리 되는 Api에서 수행 되어야이 합니다. 메서드 오버 로드 매개 변수는 이후 릴리스에서 추가할 수 있습니다.

**X DO NOT** 열거형에 센티널 값을 포함 합니다.

Framework 개발자에 게 도움이 되기도 하지만 sentinel 값은 프레임 워크의 사용자에 게 혼동 합니다. 열거형을 나타내는 집합에서 값 중 하나가 되 고 아니라 열거형의 상태를 추적에 사용 됩니다.

**✓ DO** 단순 열거형에는 0 값을 제공 합니다.

"None"입니다. 같은 값을 호출 하는 것이 좋습니다. 이러한 값이 특정 열거형에 대 한 적합 하지 않은 경우 0의 내부 값을 열거형에 대 한 가장 일반적인 기본 값을 할당 되어야 합니다.

**✓ CONSIDER** 를 사용 하 여 <xref:System.Int32> (대부분의 프로그래밍 언어의 기본값) 열거형의 내부 형식으로 다음 중 하나에 해당 하지 않는 한 합니다.

- 열거형 플래그 열거형 이며 32 개 플래그 했거나 나중에 더 하기를 원합니다.

- 기본 형식이 다를 수 해야 <xref:System.Int32> 다른 크기로 열거형을 예상 하는 관리 되지 않는 코드를 사용 하 여 원활한 상호 운용성에 대 한 합니다.

- 작은 기본 형식 결과로 공간이 크게 절약 됩니다. 제어 흐름에 대 한 인수로 서 주로 사용할 열거형을 예상 하는 경우 크기가 거의 차이가 있습니다. 한 크기 절감 효과가 매우 길어질 수 있습니다 하는 경우:

  - 예상한 매우 자주 인스턴스화된 구조체 또는 클래스의 필드로 사용할 열거형입니다.

  - 예상한 큰 배열 또는 열거형 인스턴스의 컬렉션을 만들 수 있습니다.

  - Serialize 할 열거형의 인스턴스 수가 많은 예상 합니다.

메모리 사용량에 대 한 관리 되는 개체는 수 항상 `DWORD`-정렬 되므로 효과적으로 여러 열거형 또는 총 인스턴스 크기는 항상 때문에 차이 확인 하기 위해 사용 하 여 더 작은 열거형을 압축 인스턴스에 다른 작은 구조 로 반올림 됨 것인지는 `DWORD`합니다.

**✓ DO** 단 수 명사 또는 명사구 단순 열거형 및 플래그 열거형 복수 명사 또는 명사구로 이름을 지정 합니다.

**X DO NOT** 확장 <xref:System.Enum?displayProperty=nameWithType> 직접 합니다.

<xref:System.Enum?displayProperty=nameWithType> 특별 한 형식에서 데 CLR 사용자 정의 열거형을 만듭니다. 대부분의 프로그래밍 언어에는이 기능에 액세스할 수 있는 프로그래밍 요소를 제공 합니다. 예를 들어 C#에서 `enum` 키워드 열거형을 정의 하는 데 사용 됩니다.

<a name="design"></a>

### <a name="designing-flag-enums"></a>디자인 플래그 열거형

**✓ DO** 적용 된 <xref:System.FlagsAttribute?displayProperty=nameWithType> 플래그 열거형에 있습니다. 단순 열거형에는이 특성을 적용 되지 않습니다.

**✓ DO** 수 자유롭게 결합 비트 OR 연산을 사용 하 여 플래그 열거형 값에 2의 제곱을 사용 합니다.

**✓ CONSIDER** 플래그의 조합을 사용 되는 일반적으로 특수 한 열거 값을 제공 합니다.

비트 연산은 고급 개념 및 간단한 작업에 대 한 요구 하지 않아야 합니다. <xref:System.IO.FileAccess.ReadWrite> 이러한 특수 값의 예시입니다.

**X AVOID** 만들기 플래그 열거형 값의 조합이 올바르지 않습니다.

**X AVOID** 값 "플래그를 모두 선택 취소"를 나타내는 적절 하 게 다음 지침에서 설명 했 듯이 라는 하지 않는 한 enum 값이 0 인 플래그를 사용 하 여 합니다.

**✓ DO** 0 플래그 열거형의 값 이름을 `None`합니다. 플래그 열거형에 대 한 값을 항상 수도 "플래그를 모두 취소 됩니다."

<a name="add_value"></a>

### <a name="adding-value-to-enums"></a>열거형에 값 추가

것은 매우 일반적 검색 후 이미 운송 열거형에 값을 추가 해야 합니다. 잠재적인 응용 프로그램 호환성 문제가 있습니다 새로 추가 된 값이 기존 API에서 반환 되 면 잘못 작성 된 응용 프로그램 새 값을 올바르게 처리 하지 않을 수 있습니다.

**✓ CONSIDER** 작은 호환성 위험 불구 하 고 열거형에 값을 추가 합니다.

열거형에 대 한 추가 하 여 발생 하는 응용 프로그램 호환성 문제에 대 한 실제 데이터를 사용 하는 경우 새 일정과 이전 값을 반환 하는 새 API를 추가 하는 것이 좋습니다. 및 이전 값만 반환을 계속 해야 하는 이전 API의 사용을 중단 합니다. 이렇게 하면 기존 응용 프로그램 호환성을 유지 하 합니다.

*Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*

*사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*

## <a name="see-also"></a>참고자료

- [형식 디자인 지침](../../../docs/standard/design-guidelines/type.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
