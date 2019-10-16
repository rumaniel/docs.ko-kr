---
title: 매개 변수 디자인
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines [.NET Framework], parameters
- members [.NET Framework], parameters
- names [.NET Framework], parameters
- parameters, design guidelines
- reserved parameters
ms.assetid: 3f33bf46-4a7b-43b3-bb78-1ffebe0dcfa6
author: KrzysztofCwalina
ms.openlocfilehash: 28b00f5911bb47536ec44b96f284e47b6c671149
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353734"
---
# <a name="parameter-design"></a>매개 변수 디자인
이 섹션에서는 인수 확인에 대 한 지침을 포함 하 여 매개 변수 디자인에 대 한 광범위 한 지침을 제공 합니다. 또한 [명명 매개 변수](../../../docs/standard/design-guidelines/naming-parameters.md)에 설명 된 지침을 참조 해야 합니다.  
  
 **✓ DO** 멤버에 필요한 기능을 제공 하는 최소 파생 된 매개 변수 형식을 사용 합니다.  
  
 예를 들어 컬렉션을 열거 하 고 각 항목을 콘솔에 출력 하는 메서드를 디자인 하려는 경우를 가정해 보겠습니다. 이러한 메서드는 <xref:System.Collections.ArrayList> 또는 <xref:System.Collections.IList>가 아닌 <xref:System.Collections.IEnumerable>을 매개 변수로 사용 해야 합니다.  
  
 **X DO NOT** 예약 된 매개 변수를 사용 합니다.  
  
 이후 버전에서 멤버에 대 한 추가 입력이 필요한 경우에는 새 오버 로드를 추가할 수 있습니다.  
  
 **X DO NOT** 가 공개적으로 포인터, 포인터, 배열 또는 다차원 배열을 매개 변수로 사용 하는 메서드를 노출 합니다.  
  
 포인터와 다차원 배열을 제대로 사용 하기가 비교적 어렵습니다. 거의 모든 경우에 Api는 이러한 형식을 매개 변수로 사용 하지 않도록 다시 디자인 될 수 있습니다.  
  
 **✓ DO** 모든 배치 `out` 다음 값으로의 모든 매개 변수 및 `ref` 매개 변수 (매개 변수 배열 제외) 매개 변수 오버 로드 간의 순서 지정에 불일치가 발생 하는 경우에 (참조 [멤버 오버 로드](../../../docs/standard/design-guidelines/member-overloading.md)).  
  
 @No__t-0 매개 변수는 추가 반환 값으로 표시 될 수 있으며,이를 함께 그룹화 하면 메서드 서명을 보다 쉽게 이해할 수 있습니다.  
  
 **✓ DO** 멤버를 재정의 하는 경우 매개 변수를 명명 또는 인터페이스 멤버 구현 일관 되 게 합니다.  
  
 이는 메서드 간의 관계를 더 잘 전달 합니다.  
  
### <a name="choosing-between-enum-and-boolean-parameters"></a>열거 및 부울 매개 변수 중에서 선택  
 **✓ DO** 구성원 부울 매개 변수 두 개 이상의 미칠 경우 열거형을 사용 합니다.  
  
 **X DO NOT** 확실히 될 수 없으므로 두 개 이상의 값에 대 한 필요 하지 않는 한 부울을 사용 합니다.  
  
 열거형은 나중에 값을 추가할 수 있는 공간을 제공 하지만 열거형 [디자인](../../../docs/standard/design-guidelines/enum.md)에 설명 된 열거형에 값을 추가할 경우의 모든 의미를 알고 있어야 합니다.  
  
 **✓ CONSIDER** 부울 값이 실제로 두 가지 상태는 부울 속성을 초기화 하는 생성자 매개 변수를 사용 하 여 합니다.  
  
### <a name="validating-arguments"></a>인수 유효성 검사  
 **✓ DO** public, protected 또는 명시적으로 구현 된 멤버에 전달 되는 인수의 유효성을 검사 합니다. 유효성 검사가 실패 하는 경우 <xref:System.ArgumentException?displayProperty=nameWithType> 또는 해당 하위 클래스 중 하나를 Throw 합니다.  
  
 실제 유효성 검사가 public 또는 protected 멤버 자체에서 발생할 필요는 없습니다. 일부 전용 또는 내부 루틴에서 하위 수준으로 발생할 수 있습니다. 주된 점은 최종 사용자에 게 노출 되는 전체 노출 영역에서 인수를 확인 하는 것입니다.  
  
 **✓ DO** throw <xref:System.ArgumentNullException> 에 null 인수가 전달 되 고 멤버가 null 인수를 지원 하지 않는 경우.  
  
 **✓ DO** enum 매개 변수 유효성 검사 합니다.  
  
 Enum 인수가 열거형으로 정의 된 범위에 있을 것으로 가정 하지 마십시오. CLR에서는 열거형에 값이 정의 되지 않은 경우에도 정수 값을 열거형 값으로 캐스팅할 수 있습니다.  
  
 **X DO NOT** 사용 <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> 열거형 범위 검사 합니다.  
  
 **✓ DO** 유효성을 검사 한 후 인수가 변경할 수 있는 변경 수에 유의 합니다.  
  
 멤버가 보안에 중요 한 경우에는 복사본을 만든 다음 인수의 유효성을 검사 하 고 처리 하는 것이 좋습니다.  
  
### <a name="parameter-passing"></a>매개 변수 전달  
 프레임 워크 디자이너의 관점에서 매개 변수의 기본 그룹에는 값으로 매개 변수, `ref` 매개 변수 및 `out` 매개 변수가 있습니다.  
  
 인수가 값으로 매개 변수를 통해 전달 되 면 멤버는 전달 된 실제 인수의 복사본을 받습니다. 인수가 값 형식인 경우에는 인수의 복사본이 스택에 배치 됩니다. 인수가 참조 형식이 면 참조의 복사본이 스택에 배치 됩니다. VB.NET 및 C# C++와 같은 가장 인기 있는 CLR 언어는 기본적으로 매개 변수를 값으로 전달 합니다.  
  
 인수가 `ref` 매개 변수를 통해 전달 되 면 멤버는 전달 된 실제 인수에 대 한 참조를 받습니다. 인수가 값 형식인 경우 인수에 대 한 참조가 스택에 배치 됩니다. 인수가 참조 형식이 면 참조에 대 한 참조가 스택에 배치 됩니다. `Ref` 매개 변수를 사용 하 여 멤버가 호출자가 전달한 인수를 수정할 수 있습니다.  
  
 `Out` 매개 변수는 `ref` 매개 변수와 비슷하며 약간의 차이가 있습니다. 매개 변수는 처음에 할당 되지 않은 것으로 간주 되며, 일부 값이 할당 되기 전에 멤버 본문에서 읽을 수 없습니다. 또한 멤버에서 반환 하기 전에 매개 변수에 값을 할당 해야 합니다.  
  
 **X AVOID** 를 사용 하 여 `out` 또는 `ref` 매개 변수입니다.  
  
 @No__t-0 또는 `ref` 매개 변수를 사용 하려면 포인터를 사용 하 고, 값 형식과 참조 형식이 어떻게 다른 지 이해 하 고, 여러 개의 반환 값이 있는 메서드를 처리 해야 합니다. 또한 `out` 와`ref` 매개 변수의 차이는 널리 이해 되지 않습니다. 일반 사용자를 위해 설계 된 프레임 워크 설계자는 `out` 또는 `ref` 매개 변수를 사용 하 여 작업할 수 없습니다.  
  
 **X DO NOT** 참조 형식을 참조로 전달 합니다.  
  
 참조를 교환 하는 데 사용할 수 있는 메서드와 같이 규칙에 몇 가지 제한 된 예외가 있습니다.  
  
### <a name="members-with-variable-number-of-parameters"></a>매개 변수 개수가 가변적인 멤버  
 가변 개수의 인수를 사용할 수 있는 멤버는 배열 매개 변수를 제공 하 여 표현 됩니다. 예를 들어 <xref:System.String>은 다음 메서드를 제공 합니다.  
  
```csharp  
public class String {  
    public static string Format(string format, object[] parameters);  
}  
```  
  
 사용자는 다음과 같이 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드를 호출할 수 있습니다.  
  
 `String.Format("File {0} not found in {1}",new object[]{filename,directory});`  
  
 C# Params 키워드를 배열 매개 변수에 추가 하면 매개 변수를 매개 변수를 호출한 params 배열 매개 변수로 변경 하 고 임시 배열을 만드는 바로 가기를 제공 합니다.  
  
```csharp  
public class String {  
    public static string Format(string format, params object[] parameters);  
}  
```  
  
 이렇게 하면 사용자가 인수 목록에서 직접 배열 요소를 전달 하 여 메서드를 호출할 수 있습니다.  
  
 `String.Format("File {0} not found in {1}",filename,directory);`  
  
 Params 키워드는 매개 변수 목록의 마지막 매개 변수에만 추가할 수 있습니다.  
  
 **✓ CONSIDER** 는 적은 수의 요소 배열을 전달 하는 최종 사용자가 예상 되는 경우에 params 키워드 배열 매개 변수를 추가 합니다. 일반적인 시나리오에서 많은 요소가 전달 될 것으로 예상 되는 경우 사용자는 이러한 요소를 인라인으로 전달 하지 않을 수 있으므로 params 키워드가 필요 하지 않습니다.  
  
 **X AVOID** 호출자에 게는 거의 항상 이미 입력 배열의 경우 매개 변수 배열을 사용 하 여 합니다.  
  
 예를 들어 바이트 배열 매개 변수가 있는 멤버는 개별 바이트를 전달 하 여 거의 호출 되지 않습니다. 따라서 .NET Framework의 바이트 배열 매개 변수는 params 키워드를 사용 하지 않습니다.  
  
 **X DO NOT** 배열 멤버 params 배열 매개 변수를 사용 하 여 수정 된 경우 매개 변수 배열을 사용 합니다.  
  
 대부분의 컴파일러는 멤버에 대 한 인수를 호출 사이트의 임시 배열로 변환 하기 때문에 배열이 임시 개체 일 수 있으므로 배열에 대 한 모든 수정 내용이 손실 됩니다.  
  
 **✓ CONSIDER** 단순 오버 로드에서에 params 키워드를 사용 하 여 경우에 더 복잡 한 오버 로드를 사용 하지 못했습니다.  
  
 사용자가 모든 오버 로드에 포함 되지 않은 경우에도 하나의 오버 로드에서 params 배열을 포함 하 고 있는지 확인 합니다.  
  
 **✓ DO** params 키워드를 사용할 수 있도록 적절 한 매개 변수를 하려고 합니다.  
  
 **✓ CONSIDER** 적은 수의 성능에 민감한 매우 Api에는 인수를 사용 하 여 호출에 대 한 특별 한 오버 로드와 코드 경로 제공 합니다.  
  
 이를 통해 적은 수의 인수를 사용 하 여 API를 호출 하는 경우 배열 개체를 만들지 않도록 할 수 있습니다. 단일 형식의 배열 매개 변수를 가져와 숫자 접미사를 추가 하 여 매개 변수의 이름을 구성 합니다.  
  
 배열을 만들고 보다 일반적인 메서드를 호출 하는 것이 아니라 전체 코드 경로를 특별 한 경우에만이 작업을 수행 해야 합니다.  
  
 **✓ DO** 유의 매개 변수 배열 인수는 null을 전달할 수 있습니다.  
  
 처리 하기 전에 배열이 null이 아닌 지 유효성을 검사 해야 합니다.  
  
 **X DO NOT** 사용는 `varargs` 메서드, 줄임표 라고도 합니다.  
  
 과 C++같은 일부 CLR 언어는 `varargs` 메서드 라는 변수 매개 변수 목록을 전달 하는 대체 규칙을 지원 합니다. 규칙은 CLS 규격이 아니므로 프레임 워크에서 사용 하면 안 됩니다.  
  
### <a name="pointer-parameters"></a>포인터 매개 변수  
 일반적으로 잘 디자인 된 관리 코드 프레임 워크의 공개 노출 영역에는 포인터가 표시 되지 않아야 합니다. 대부분의 경우 포인터는 캡슐화 되어야 합니다. 그러나 일부 경우에는 상호 운용성을 위해 포인터가 필요 하며, 이러한 경우에는 포인터를 사용 하는 것이 적절 합니다.  
  
 **✓ DO** 포인터 CLS 규격이 아닙니다. 때문에 포인터 인수를 사용 하는 멤버에 대 한 대체 방법을 제공 합니다.  
  
 **X AVOID** 과도 한 인수 포인터 인수의 검사를 수행 합니다.  
  
 **✓ DO** 포인터로 멤버를 디자인 하는 경우 일반 포인터와 관련 된 규칙을 따릅니다.  
  
 예를 들어 단순한 포인터 산술 연산을 사용 하 여 동일한 결과를 얻을 수 있으므로 시작 인덱스를 전달할 필요가 없습니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 @no__t-[Framework 디자인 지침에서 피어슨 교육부, Inc.의 권한으로 0Reprinted. 다시 사용할 수 있는 .NET 라이브러리에 대 한 규칙, 관용구 및 패턴, Microsoft Windows 개발 @no__t 시리즈의 일부로 Addison-Wesley Professional에서 2008 no__t, Krzysztof Cwalina 및 Brad Abrams 성  
  
## <a name="see-also"></a>참조

- [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
