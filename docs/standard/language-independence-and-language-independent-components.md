---
title: 언어 독립성 및 언어 독립적 구성 요소
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- language interoperability
- Common Language Specification
- cross-language interoperability
- CLS
- runtime, language interoperability
- common language runtime, language interoperability
ms.assetid: 4f0b77d0-4844-464f-af73-6e06bedeafc6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6ecb2c2e6a80f36ea1426b6145fd89b869a77f1b
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663015"
---
# <a name="language-independence-and-language-independent-components"></a>언어 독립성 및 언어 독립적 구성 요소

.NET Framework는 언어에 국한되지 않습니다. 즉, 개발자로서 .NET Framework를 대상으로 하는 많은 언어 중 하나로 개발할 수 있습니다(예: C#, C++/CLI, Eiffel, F#, IronPython, IronRuby, PowerBuilder, Visual Basic, Visual COBOL 및 Windows PowerShell). 원래 작성된 언어를 모르거나 원래의 언어 규칙을 따르지 않고도 .NET Framework를 위해 개발된 클래스 라이브러리의 형식과 멤버에 액세스할 수 있습니다. 사용자가 구성 요소 개발자일 경우 언어와 상관없이 모든 .NET Framework 응용 프로그램에서 구성 요소를 액세스할 수 있습니다.

> [!NOTE]
> 이 문서의 첫 부분에서는 언어 독립 구성 요소를 만드는 방법에 대해 설명합니다. 즉, 이러한 구성 요소는 어떠한 언어로 작성된 앱에서도 사용할 수 있습니다. 여러 언어로 작성된 소스 코드에서 구성 요소나 앱을 하나 만들 수도 있습니다. 이 문서의 두 번째 부분에서 [언어 간 상호 운용성](#CrossLang)을 참조하세요.

어떠한 언어로 작성된 다른 개체와도 완전하게 상호 작용하려면 개체는 모든 언어에 공통적인 기능만 호출자에게 노출해야 합니다. 기능의 공통 집합은 생성된 어셈블리에 적용되는 규칙 집합인 CLS(공용 언어 사양)에서 정의됩니다. 공용 언어 사양은 [ECMA-335 Standard: Common Language Infrastructure](https://www.ecma-international.org/publications/standards/Ecma-335.htm)의 Partition I, Clauses 7~11에 정의되어 있습니다.

구성 요소가 공용 언어 사양을 따르는 경우, 이 구성 요소는 CLS 규격임이 보장되고 CLS를 지원하는 모든 프로그래밍 언어로 작성된 어셈블리 코드에서 액세스할 수 있습니다. <xref:System.CLSCompliantAttribute> 특성을 소스 코드에 적용하여 구성 요소가 컴파일 타임에 공용 언어 사양을 준수하는지 여부를 결정할 수 있습니다. 자세한 내용은 [CLSCompliantAttribute 특성](#CLSAttribute)을 참조하세요.

이 문서의 내용

- [CLS 준수 규칙](#Rules)

  - [형식 및 형식 멤버 시그니처](#Types)

  - [명명 규칙](#naming)

  - [형식 변환](#conversion)

  - [배열](#arrays)

  - [인터페이스](#Interfaces)

  - [열거형](#enums)

  - [형식 멤버 일반 사항](#members)

  - [멤버 접근성](#MemberAccess)

  - [제네릭 형식 및 멤버](#Generics)

  - [생성자](#ctors)

  - [속성](#properties)

  - [이벤트](#events)

  - [오버로드](#overloads)

  - [예외](#exceptions)

  - [특성](#attributes)

- [CLSCompliantAttribute 특성](#CLSAttribute)

- [언어 간 상호 운용성](#CrossLang)

<a name="Rules"></a>

## <a name="cls-compliance-rules"></a>CLS 규격 규칙

이 섹션에서는 CLS 규격 구성 요소를 만드는 규칙을 설명합니다. 규칙의 전체 목록은 [ECMA-335 Standard: Common Language Infrastructure](https://www.ecma-international.org/publications/standards/Ecma-335.htm)의 Partition I, Clauses 11에 정의되어 있습니다.

> [!NOTE]
> 공용 언어 사양에서는 소비자(CLS 규격인 구성 요소를 프로그래밍 방식으로 액세스하는 개발자), 프레임워크(언어 컴파일러를 사용하여 CLS 규격 라이브러리를 만드는 개발자) 및 extender(CLS 규격 구성 요소를 생성하는 언어 컴파일러 또는 코드 파서 등의 도구를 만드는 개발자)에게 적용되는 CLS 규격에 대한 각 규칙을 설명합니다. 이 문서에서는 프레임워크에 적용되는 규칙에 초점을 맞춥니다. 그러나 extender에 적용되는 규칙 중 일부를 Reflection.Emit을 사용하여 만든 어셈블리에도 적용할 수 있습니다.

언어 독립적인 구성 요소를 디자인하려면 CLS 규격의 규칙을 구성 요소의 공용 인터페이스에 적용하기만 하면 됩니다. private 구현은 사양을 준수할 필요가 없습니다.

> [!IMPORTANT]
> CLS 규격의 규칙은 구성 요소의 public 인터페이스에만 적용되고 private 구현에는 적용되지 않습니다.

예를 들어 <xref:System.Byte> 이외의 부호 없는 정수는 CLS 규격이 아닙니다. 다음 예제의 `Person` 클래스는 `Age` 형식의 <xref:System.UInt16> 속성을 노출시키므로 다음 코드는 컴파일러 경고를 표시합니다.

[!code-csharp[Conceptual.CLSCompliant#1](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/public1.cs#1)]
[!code-vb[Conceptual.CLSCompliant#1](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/public1.vb#1)]

`Person` 속성의 형식을 `Age`에서 CLS 규격 16비트 부호 있는 정수인 <xref:System.UInt16>으로 변경하여 <xref:System.Int16> 클래스를 CLS 규격으로 만들 수 있습니다. private `personAge` 필드의 형식을 변경할 필요가 없습니다.

[!code-csharp[Conceptual.CLSCompliant#2](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/public2.cs#2)]
[!code-vb[Conceptual.CLSCompliant#2](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/public2.vb#2)]

라이브러리의 공용 인터페이스는 다음으로 구성됩니다.

- 공용 클래스의 정의

- 공용 클래스의 공용 멤버에 대한 정의 및 파생 클래스에서 액세스할 수 있는 멤버에 대한 정의(즉, protected 멤버)

- 공용 클래스의 공용 메서드에 대한 매개 변수 및 반환 형식, 파생 클래스에서 액세스할 수 있는 메서드에 대한 매개 변수 및 반환 형식

CLS 규격의 규칙은 다음 표에 나와 있습니다. 규칙의 텍스트는 [ECMA-335 Standard: Common Language Infrastructure](https://www.ecma-international.org/publications/standards/Ecma-335.htm)(Copyright 2012 by Ecma International)에서 가져온 약어입니다. 이러한 규칙에 대한 보다 자세한 내용은 다음 섹션에서 찾을 수 있습니다.

|범주|참조|규칙|규칙 번호|
|--------------|---------|----------|-----------------|
|액세스 가능성|[멤버 접근성](#MemberAccess)|`family-or-assembly` 액세스 가능성을 갖는 다른 어셈블리에서 상속된 메서드를 재정의하는 경우를 제외하고는, 상속된 메서드를 재정의할 때 액세스 가능성이 변경되어서는 안 됩니다. 이 경우, 재정의는 `family` 액세스 가능성을 가져야 합니다.|10|
|액세스 가능성|[멤버 접근성](#MemberAccess)|형식과 멤버의 표시 유형 및 접근성은 해당 멤버가 표시되고 액세스 가능한 경우 모든 멤버의 시그니처에 있는 해당 형식이 표시되고 액세스 가능해야 합니다. 예를 들어 어셈블리 외부에 표시되는 공용 메서드는 어셈블리 내부에서만 표시되는 형식의 인수를 가질 수 없습니다. 해당 멤버가 표시되고 액세스 가능한 경우 모든 멤버의 시그니처에 사용된 인스턴스화된 제네릭 형식을 구성하는 형식의 표시 유형과 액세스 가능성은 표시되고 액세스 가능해야 합니다. 예를 들어 어셈블리 외부에 표시되는 멤버의 시그니처에 있는 인스턴스화된 제네릭 형식은 어셈블리 내부에서만 표시되는 형식의 제네릭 인수를 가질 수 없습니다.|12|
|배열|[배열](#arrays)|배열에는 CLS 규격 형식의 요소가 있어야 하며 배열의 모든 차원은 하한이 0이어야 합니다. 항목은 배열이며 이 배열의 요소 형식은 오버로드 간에 구분되어야 합니다. 오버로드가 2개 이상의 배열 형식에 기반하는 경우 요소 형식은 명명된 형식이어야 합니다.|16|
|특성|[특성](#attributes)|특성은 <xref:System.Attribute?displayProperty=nameWithType> 형식 또는 여기에서 상속된 형식이어야 합니다.|41|
|특성|[특성](#attributes)|CLS에서는 사용자 지정 특성 인코딩의 하위 집합만을 허용합니다. 이들 인코딩에 표시될 수 있는 형식은(Partition IV 참조) <xref:System.Type?displayProperty=nameWithType>, <xref:System.String?displayProperty=nameWithType>, <xref:System.Char?displayProperty=nameWithType>, <xref:System.Boolean?displayProperty=nameWithType>, <xref:System.Byte?displayProperty=nameWithType>, <xref:System.Int16?displayProperty=nameWithType>, <xref:System.Int32?displayProperty=nameWithType>, <xref:System.Int64?displayProperty=nameWithType>, <xref:System.Single?displayProperty=nameWithType>, <xref:System.Double?displayProperty=nameWithType> 및 CLS 규격 기본 정수 형식에 기반한 열거형 형식 뿐입니다.|34|
|특성|[특성](#attributes)|CLS에서는 공개적으로 표시되는 필수 한정자(`modreq`)를 허용하지 않지만, CLS에서 인식할 수 없는 선택적 한정자(`modopt`, Partition II 참조)는 허용합니다.|35|
|생성자|[생성자](#ctors)|개체 생성자는 상속된 인스턴스 데이터에 액세스하기 전에 기본 클래스의 일부 인스턴스 생성자를 호출해야 합니다. (생성자가 필요하지 않은 값 형식에는 적용되지 않습니다.)|21|
|생성자|[생성자](#ctors)|개체 생성자는 개체 만들기 작업의 일부로 호출되는 것을 제외하고 호출되어서는 안 되며 개체는 두 번 초기화해서는 안 됩니다.|22|
|열거형|[열거형](#enums)|열거형의 기본 형식은 기본 제공 CLS 정수 형식이고, 필드의 이름은 "value__"이며, 해당 필드는 `RTSpecialName`으로 표시되어야 합니다.|7|
|열거형|[열거형](#enums)|<xref:System.FlagsAttribute?displayProperty=nameWithType>(Partition IV 라이브러리 참조) 사용자 지정 특성의 존재 여부에 따라 표시되는 다음 두 가지 구분되는 열거형이 있습니다. 하나는 명명된 정수 값을 나타내며, 다른 하나는 명명되지 않은 값을 생성하도록 결합될 수 있는 명명된 비트 플래그를 나타냅니다. `enum`의 값은 지정된 값으로 제한되지 않습니다.|8|
|열거형|[열거형](#enums)|열거형의 리터럴 정적 필드는 그 자체가 열거형 형식을 갖습니다.|9|
|이벤트|[이벤트](#events)|이벤트를 구현하는 메서드는 메타데이터에서 `SpecialName`으로 표시됩니다.|29|
|이벤트|[이벤트](#events)|이벤트와 접근자의 액세스 가능성이 동일해야 합니다.|30|
|이벤트|[이벤트](#events)|이벤트에 대한 `add` 및 `remove` 메서드는 모두 있거나 모두 없어야 합니다.|31|
|이벤트|[이벤트](#events)|이벤트에 대한 `add` 및 `remove` 메서드는 이벤트 형식 정의 형식을 갖는 하나의 매개 변수를 각각 사용해야 하며, 해당 형식은 <xref:System.Delegate?displayProperty=nameWithType>에서 파생된 것이어야 합니다.|32|
|이벤트|[이벤트](#events)|이벤트는 특정 이름 지정 패턴을 따라야 합니다. CLS 규칙 29에서 참조되는 `SpecialName` 특성은 적절한 이름 비교에서 무시되고 식별자 규칙을 따릅니다.|33|
|예외|[예외](#exceptions)|throw되는 개체는 <xref:System.Exception?displayProperty=nameWithType> 형식 또는 이 형식에서 상속되는 형식이어야 합니다. 그렇더라도 다른 형식의 예외 전파를 차단하는 데 CLS 규격 메서드는 필요하지 않습니다.|40|
|일반|[CLS 규격: 규칙](#Rules)|CLS 규칙은 정의 어셈블리 외부에서 액세스하거나 볼 수 있는 형식의 해당 부분에만 적용됩니다.|1|
|일반|[CLS 규격: 규칙](#Rules)|CLS 규격 형식이 아닌 멤버를 CLS 규격으로 표시해서는 안 됩니다.|2|
|제네릭|[제네릭 형식 및 멤버](#Generics)|중첩 형식에는 적어도 바깥쪽 형식과 같은 수의 제네릭 매개 변수가 있어야 합니다. 중첩 형식의 제네릭 매개 변수는 바깥쪽 형식의 제네릭 매개 변수와 위치가 같습니다.|42|
|제네릭|[제네릭 형식 및 멤버](#Generics)|제네릭 형식의 이름은 중첩되지 않은 형식이나 중첩된 경우 앞에서 정의된 규칙에 따라 새롭게 도입된 형식으로 선언된 형식 매개 변수의 개수를 인코딩합니다.|43|
|제네릭|[제네릭 형식 및 멤버](#Generics)|제네릭 형식에서는 제네릭 형식 제약 조건이 기본 형식이나 인터페이스에 대한 모든 제약 조건을 만족할 수 있도록 충분한 제약 조건을 다시 선언해야 합니다.|4444|
|제네릭|[제네릭 형식 및 멤버](#Generics)|제네릭 매개 변수에 대한 제약 조건으로 사용되는 형식 자체는 CLS 규격이어야 합니다.|45|
|제네릭|[제네릭 형식 및 멤버](#Generics)|인스턴스화된 제네릭 형식에서 중첩 형식을 포함한 멤버의 표시 여부와 액세스 가능성의 범위는 전체 제네릭 형식이 아닌 특정 인스턴스로 제한됩니다. 이러한 가정 하에 CLS 규칙 12의 표시 유형 및 액세스 가능성 규칙이 계속 적용됩니다.|46|
|제네릭|[제네릭 형식 및 멤버](#Generics)|각 추상 또는 가상 제네릭 메서드마다 구체적인(비추상) 기본 구현이 있습니다.|47|
|인터페이스|[인터페이스](#Interfaces)|CLS 규격 인터페이스는 구현을 위해 CLS 규격이 아닌 메서드의 정의가 필요하지 않습니다.|18|
|인터페이스|[인터페이스](#Interfaces)|CLS 규격 인터페이스에서는 정적 메서드나 필드를 정의할 수 없습니다.|19|
|멤버|[형식 멤버 일반 사항](#members)|전역 정적 필드 및 메서드는 CLS 규격입니다.|36|
|멤버|--|리터럴 정적 값은 필드 초기화 메타데이터를 사용하여 지정됩니다. CLS 규격 리터럴에는 리터럴(또는 해당 리터럴이 `enum`인 경우 기본 형식)과 정확히 같은 형식인 필드 초기화 메타데이터에 지정된 값이 있어야 합니다.|13|
|멤버|[형식 멤버 일반 사항](#members)|vararg 제약 조건은 CLS의 일부가 아니며, CLS에서는 관리되는 표준 호출 규칙만 지원합니다.|15|
|명명 규칙|[명명 규칙](#naming)|어셈블리는 시작하고 식별자에 포함할 수 있는 문자 집합을 규정하는 유니코드 표준 3.0 기술 보고서 15의 부록 7을 준수합니다. <https://www.unicode.org/unicode/reports/tr15/tr15-18.html>에서 온라인으로 확인할 수 있습니다. 식별자는 유니코드 정규화 형식 C에서 정의된 정규 형식입니다. CLS에서 소문자 매핑(유니코드 로캘 비구분으로 지정된, 일 대 일 소문자 매핑)이 같은 두 개의 식별자는 서로 같습니다. 즉, 두 식별자가 CLS에서 서로 다른 것으로 간주되는 경우 단순히 대/소문자 이상의 차이가 있습니다. 그러나 상속된 정의를 재정의하기 위해서는 CLI가 원래 선언에 정확한 인코딩을 사용해야 합니다.|4|
|오버로딩|[명명 규칙](#naming)|CLS 규격 범위에 소개된 모든 이름은 이름이 동일한 경우를 제외하고는 종류가 독립적이고 고유한 이름이어야 하며 오버로드를 통해 확인됩니다. 즉, CTS에서는 메서드 및 필드에 동일한 이름을 사용하는 단일 형식이 허용되지만, CLS에서는 그렇지 않습니다.|5|
|오버로딩|[명명 규칙](#naming)|CTS로 고유 시그니처가 구분될 수 있지만 필드 및 중첩 형식은 식별자 비교만으로 구분됩니다. 식별자를 비교했을 때 CLS 규칙 39에 지정된 경우를 제외하고 동일한 이름을 갖는 메서드, 속성 및 이벤트는 반환 형식 이상의 차이가 있습니다.|6|
|오버로딩|[오버로드](#overloads)|속성 및 메서드만 오버로드될 수 있습니다.|37|
|오버로딩|[오버로드](#overloads)|반환 형식에 따라서도 오버로드될 수 있는 이름이 `op_Implicit` 및 `op_Explicit`인 변환 연산자를 제외하고, 속성 및 메서드는 매개 변수의 형식과 수에 따라서만 오버로드될 수 있습니다.|38|
|오버로딩|--|한 형식에서 선언된 둘 이상의 CLS 규격 메서드의 이름이 같고 형식 인스턴스화의 특정 집합에 대해 매개 변수와 반환 형식이 같다면 이러한 모든 메서드는 해당 형식 인스턴스화에서 의미상 동일합니다.|48|
|유형|[형식 및 형식 멤버 시그니처](#Types)|<xref:System.Object?displayProperty=nameWithType>는 CLS 규격입니다. 다른 CLS 규격 클래스는 모두 CLS 규격 클래스에서 상속해야 합니다.|23|
|속성|[속성](#properties)|속성의 getter 및 setter 메서드를 구현하는 메서드는 메타데이터에서 `SpecialName`으로 표시됩니다.|24|
|속성|[속성](#properties)|속성의 접근자는 모두 static이거나 모두 virtual이거나 또는 모두 instance여야 합니다.|26|
|속성|[속성](#properties)|속성의 형식은 getter의 반환 형식이며 setter의 마지막 인수의 형식이어야 합니다. 속성의 매개 변수 형식은 getter의 매개 변수 형식 및 setter의 마지막 매개 변수 형식을 제외한 모든 형식이어야 합니다. 이들 형식은 모두 CLS 규격이어야 하며 관리되는 포인터일 수 없습니다. 즉, 참조로 전달될 수 없습니다.|27|
|속성|[속성](#properties)|속성은 특정 이름 지정 패턴을 따라야 합니다. CLS 규칙 24에서 참조되는 `SpecialName` 특성은 적절한 이름 비교에서 무시되고 식별자 규칙을 따릅니다. 속성에는 getter 메서드, setter 메서드 또는 둘 모두가 있어야 합니다.|28|
|형식 변환|[형식 변환](#conversion)|`op_Implicit` 또는 `op_Explicit`이 제공될 경우 강제 변환을 제공하는 다른 방법이 제공됩니다.|39|
|유형|[형식 및 형식 멤버 시그니처](#Types)|boxed 값 형식은 CLS 규격이 아닙니다.|3|
|유형|[형식 및 형식 멤버 시그니처](#Types)|시그니처에 나타나는 모든 형식은 CLS 규격이어야 합니다. 인스턴스화된 제네릭 형식을 구성하는 모든 형식은 CLS 규격이어야 합니다.|11|
|유형|[형식 및 형식 멤버 시그니처](#Types)|형식화된 참조는 CLS 규격이 아닙니다.|14|
|유형|[형식 및 형식 멤버 시그니처](#Types)|관리되지 않는 포인터 형식은 CLS 규격이 아닙니다.|17|
|유형|[형식 및 형식 멤버 시그니처](#Types)|CLS 규격 클래스, 값 형식 및 인터페이스에는 CLS 규격이 아닌 멤버 구현이 필요하지 않습니다.|20|

<a name="Types"></a>

### <a name="types-and-type-member-signatures"></a>형식 및 형식 멤버 시그니처

<xref:System.Object?displayProperty=nameWithType> 형식은 CLS 규격이고 .NET Framework 형식 시스템의 모든 개체 형식의 기본 형식입니다. .NET Framework의 상속은 암시적(예: <xref:System.String> 클래스는 <xref:System.Object> 클래스에서 암시적으로 상속됨)이거나 명시적(예: <xref:System.Globalization.CultureNotFoundException> 클래스는 <xref:System.ArgumentException> 클래스에서 명시적으로 상속되고, 이 클래스는 다시 <xref:System.SystemException> 클래스에서 명시적으로 상속되며, 이 클래스는 다시 <xref:System.Exception> 클래스에서 명시적으로 상속됨)입니다. 파생된 형식은 CLS 규격이어야 하며, 그 기본 형식도 CLS 규격이어야 합니다.

다음 예제에서는 기본 형식이 CLS 규격이 아닌 파생 형식을 보여 줍니다. 부호 없는 32비트 정수를 카운터로 사용하는 기본 `Counter` 클래스를 정의합니다. 이 클래스는 부호 없는 정수를 래핑하여 카운터 기능을 제공하므로 CLS 비규격으로 표시됩니다. 따라서 파생된 클래스인 `NonZeroCounter`도 CLS 규격이 아닙니다.

[!code-csharp[Conceptual.CLSCompliant#12](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/type3.cs#12)]
[!code-vb[Conceptual.CLSCompliant#12](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/type3.vb#12)]

메서드의 반환 형식 또는 속성 형식을 포함하여 멤버 시그니처에 나타나는 모든 형식은 CLS 규격이어야 합니다. 또한 제네릭 형식의 경우,

- 인스턴스화된 제네릭 형식을 구성하는 모든 형식은 CLS 규격이어야 합니다.

- 제네릭 매개 변수에 대한 제약 조건으로 사용되는 모든 형식은 CLS 규격이어야 합니다.

.NET Framework [공용 형식 시스템](../../docs/standard/base-types/common-type-system.md)은 공용 언어 런타임에 의해 직접 지원되고 어셈블리의 메타데이터에서 특수 인코딩되는 여러 기본 형식을 포함합니다. 이러한 내장 형식 중에서 다음 표에 나열된 형식은 CLS 규격입니다.

|CLS 규격 형식|설명|
|-------------------------|-----------------|
|<xref:System.Byte>|8비트 부호 없는 정수|
|<xref:System.Int16>|16비트 부호 있는 정수|
|<xref:System.Int32>|32비트 부호 있는 정수|
|<xref:System.Int64>|64비트 부호 있는 정수|
|<xref:System.Single>|단정밀도 부동 소수점 값|
|<xref:System.Double>|배정밀도 부동 소수점 값|
|<xref:System.Boolean>|`true` 또는 `false` 값 형식|
|<xref:System.Char>|UTF-16으로 인코딩된 코드 단위|
|<xref:System.Decimal>|비 부동 소수점 10진수|
|<xref:System.IntPtr>|플랫폼 정의 크기의 포인터 또는 핸들|
|<xref:System.String>|0개, 1개 또는 2개 이상 <xref:System.Char> 개체의 컬렉션|

다음 표에 나열된 내장 형식은 CLS 규격이 아닙니다.

|비규격 형식|설명|CLS 규격 대체 항목|
|-------------------------|-----------------|--------------------------------|
|<xref:System.SByte>|8비트 부호 있는 정수 데이터 형식|<xref:System.Int16>|
|<xref:System.TypedReference>|개체 및 해당 런타임 형식에 대한 포인터|없음|
|<xref:System.UInt16>|16비트 부호 없는 정수|<xref:System.Int32>|
|<xref:System.UInt32>|32비트 부호 없는 정수|<xref:System.Int64>|
|<xref:System.UInt64>|64비트 부호 없는 정수|<xref:System.Int64>(오버플로될 수 있음), <xref:System.Numerics.BigInteger> 또는 <xref:System.Double>|
|<xref:System.UIntPtr>|부호 없는 포인터 또는 핸들|<xref:System.IntPtr>|

.NET Framework 클래스 라이브러리 또는 기타 다른 클래스 라이브러리는 다음 예시와 같은 CLS 규격이 아닌 기타 형식을 포함할 수 있습니다.

- boxed 값 형식. 다음 C# 예제는 이름이 `int*`인 public 속성 `Value` 형식을 가진 클래스를 만듭니다. `int*`는 boxed 값 형식이므로 컴파일러에서 CLS 비규격으로 플래그를 지정합니다.

  [!code-csharp[Conceptual.CLSCompliant#26](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/box2.cs#26)]

- 형식화된 참조란 개체에 대한 참조 및 형식에 대한 참조를 포함하는 특수 생성자로서, 형식화된 참조는 .NET Framework에서 <xref:System.TypedReference> 클래스에 의해 표시됩니다.

형식이 CLS 규격이 아닌 경우 <xref:System.CLSCompliantAttribute>의 `isCompliant` 값으로 `false` 특성을 해당 형식에 적용해야 합니다. 자세한 내용은 [CLSCompliantAttribute 특성](#CLSAttribute) 섹션을 참조하세요.

다음 예제에서는 메서드 시그니처와 제네릭 형식 인스턴스화의 CLS 규격 문제를 보여 줍니다. `InvoiceItem` 클래스를 <xref:System.UInt32> 형식의 속성, `Nullable(Of UInt32)` 형식의 속성, <xref:System.UInt32> 및 `Nullable(Of UInt32)` 형식의 매개 변수를 가진 생성자로 정의합니다. 이 예제를 컴파일하려고 할 때 4개의 컴파일러 경고가 표시됩니다.

[!code-csharp[Conceptual.CLSCompliant#3](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/type1.cs#3)]
[!code-vb[Conceptual.CLSCompliant#3](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/type1.vb#3)]

컴파일러 경고를 없애려면 `InvoiceItem` 공용 인터페이스의 CLS 규격이 아닌 형식을 CLS 규격 형식으로 대체합니다.

[!code-csharp[Conceptual.CLSCompliant#4](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/type2.cs#4)]
[!code-vb[Conceptual.CLSCompliant#4](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/type2.vb#4)]

나열된 특정 형식 외에도 일부 형식 범주가 CLS 규격이 아닙니다. 여기에는 관리되지 않는 포인터 형식 및 함수 포인터 형식이 포함됩니다. 다음 예제에서는 정수에 대한 포인터를 사용하여 정수 배열을 만들기 때문에 컴파일러 경고가 발생합니다.

[!code-csharp[Conceptual.CLSCompliant#5](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/unmanagedptr1.cs#5)]

CLS 규격인 추상 클래스(C#에서 `abstract` 또는 Visual Basic에서 `MustInherit`로 표시되는 클래스)의 경우 이 클래스의 모든 멤버 역시 CLS 규격이어야 합니다.

<a name="naming"></a>

### <a name="naming-conventions"></a>명명 규칙

일부 프로그래밍 언어에서는 대/소문자를 구분하기 때문에 식별자(네임스페이스, 형식 및 멤버 이름 등)는 대/소문자 그 이상의 차이가 있어야 합니다. 소문자 매핑이 같은 두 개의 식별자는 서로 동일한 것으로 간주됩니다. 다음 C# 예제에서는 `Person` 및 `person`이라는 두 가지 공용 클래스를 정의합니다. 이들 클래스는 대/소문자만 다르므로 C# 컴파일러는 CLS 규격이 아니라는 플래그를 지정합니다.

[!code-csharp[Conceptual.CLSCompliant#16](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/naming1.cs#16)]

네임스페이스, 형식 및 멤버의 이름과 같은 언어 식별자 프로그래밍은 [유니코드 표준 3.0, 기술 보고서 15, 부록 7](https://www.unicode.org/reports/tr15/tr15-18.html)을 준수해야 합니다. 이는 다음을 의미합니다.

- 식별자의 첫 문자로는 유니코드 대문자, 소문자, 제목 대/소문자, 한정자 문자, 기타 문자 또는 문자 숫자가 올 수 있습니다. 유니코드 문자 범주에 대한 자세한 내용은 <xref:System.Globalization.UnicodeCategory?displayProperty=nameWithType> 열거형을 참조하세요.

- 연속되는 문자는 첫 번째 문자로서 가능한 모든 범주의 문자가 올 수 있으며 간격 없음 표시, 간격 결합 기호, 10진수, 연결 문장 부호 및 형식 지정 코드를 포함할 수 있습니다.

단일 문자를 다중 UTF-16 인코딩 코드 단위로 표시할 수 있으므로 식별자를 비교하기 전에 형식 지정 코드를 필터링하고 식별자를 유니코드 정규화 형식 C로 변환해야 합니다. 유니코드 정규화 형식 C에서 동일한 코드 단위를 만드는 문자 시퀀스는 CLS 규격이 아닙니다. 다음 예제에서는 ANGSTROM SIGN(U+212B) 문자로 구성된 `Å`이라는 속성과 LATIN CAPITAL LETTER A WITH RING ABOVE(U+00C5) 문자로 구성된 두 번째 `Å`이라는 속성을 정의합니다. C# 및 Visual Basic 컴파일러 모두 소스 코드를 CLS 비규격으로 플래그를 지정합니다.

[!code-csharp[Conceptual.CLSCompliant#17](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/naming1.cs#17)]
[!code-vb[Conceptual.CLSCompliant#17](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/naming1.vb#17)]

오버로드를 통해 확인되는 이름을 제외한 특정 범위 내의 멤버 이름(예: 어셈블리 내 네임스페이스, 네임스페이스 내 형식 또는 형식 내 멤버)은 고유해야 합니다. 이 요구 사항은 한 범위 내의 여러 멤버가 다른 종류의 멤버인 경우(예를 들어 하나는 메서드이고 하나는 필드인 경우) 고유한 이름을 사용할 수 있는 공용 형식 시스템의 요구 사항보다 더 엄격합니다. 특히, 형식 멤버가

- 필드 및 중첩된 형식인 경우 이름으로만 구분됩니다.

- 이름이 같은 메서드, 속성 및 이벤트인 경우 반환 형식 이외의 차이점이 있어야 합니다.

다음 예제에서는 멤버 이름이 해당 범위 내에서 고유해야 한다는 요구 사항을 보여 줍니다. `Converter`이라는 4개 멤버를 포함하는 `Conversion`라는 클래스를 정의합니다. 세 가지는 메서드이고 한 가지는 속성입니다. <xref:System.Int64> 매개 변수가 포함된 메서드의 이름은 고유하지만, <xref:System.Int32> 매개 변수가 포함된 두 메서드의 이름은 반환 값이 멤버 시그니처의 일부로 간주되지 않으므로 고유하지 않습니다. 속성은 오버로드된 메서드와 동일한 이름을 가질 수 없으므로 `Conversion` 속성 또한 이 요구 사항을 위반합니다.

[!code-csharp[Conceptual.CLSCompliant#19](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/naming3.cs#19)]
[!code-vb[Conceptual.CLSCompliant#19](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/naming3.vb#19)]

개별 언어는 고유 키워드를 포함하기 때문에 공용 언어 런타임을 대상으로 하는 언어는 키워드와 일치하는 식별자(예: 형식 이름)를 참조하기 위한 일부 메커니즘도 제공해야 합니다. 예를 들어, `case`는 C# 및 Visual Basic 모두의 키워드입니다. 그러나 다음 Visual Basic 예제에서는 열고 닫는 중괄호를 사용하여 `case` 키워드에서 `case`라는 이름의 클래스를 구분할 수 있습니다. 중괄호가 없다면 이 예제에서는 "키워드를 식별자로 사용할 수 없습니다."와 같은 오류 메시지가 발생하고 컴파일되지 않습니다.

[!code-vb[Conceptual.CLSCompliant#22](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/keyword1.vb#22)]

다음 C# 예제에서는 `case` 기호를 사용하여 언어 키워드에서 식별자를 구분하여 `@` 클래스를 인스턴스화할 수 있습니다. 이 기호가 없으면 C# 컴파일러에서는 "형식이 필요합니다" 및 "식의 'case' 항이 잘못되었습니다"라는 두 개의 오류 메시지가 표시됩니다.

[!code-csharp[Conceptual.CLSCompliant#23](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/keyword2.cs#23)]

<a name="conversion"></a>

### <a name="type-conversion"></a>형식 변환

공용 언어 사양은 다음과 같은 두 변환 연산자를 정의합니다.

- `op_Implicit`는 데이터 또는 정밀도가 손실되지 않는 확대 변환에 사용됩니다. 예를 들어 <xref:System.Decimal> 구조체에 오버로드된 `op_Implicit` 연산자를 포함하여 정수 형식의 값과 <xref:System.Char> 값을 <xref:System.Decimal> 값으로 변환합니다.

- `op_Explicit`는 크기 손실(보다 작은 범위의 값으로 변환) 또는 정밀도 손실이 발생할 수 있는 축소 변환에 사용됩니다. 예를 들어 <xref:System.Decimal> 구조체에 오버로드된 `op_Explicit`연산자를 포함하여 <xref:System.Double> 및 <xref:System.Single> 값을 <xref:System.Decimal> 값으로 변환하고, <xref:System.Decimal> 값을 정수 값, <xref:System.Double>, <xref:System.Single> 및 <xref:System.Char>로 변환합니다.

그러나 모든 언어가 연산자 오버로드 또는 사용자 지정 연산자 정의를 지원하는 것은 아닙니다. 이러한 변환 연산자를 구현하도록 선택한 경우, 변환을 수행하기 위한 다른 방법도 제공해야 합니다. `From`*Xxx* 및 `To`*Xxx* 메서드를 제공하는 것이 좋습니다.

다음 예제에서는 CLS 규격의 암시적 및 명시적 변환을 정의합니다. 부호 있는 배정밀도, 부동 소수점 숫자를 나타내는 `UDouble` 클래스를 만듭니다. `UDouble`에서 <xref:System.Double>로의 암시적 변환 및 `UDouble`에서 <xref:System.Single>로, <xref:System.Double>에서 `UDouble`로, <xref:System.Single>에서 `UDouble`로의 명시적 변환이 제공됩니다. 또한 `ToDouble` 메서드를 암시적 변환 연산자에 대한 대안으로 정의하고 `ToSingle`, `FromDouble` 및 `FromSingle` 메서드를 명시적 변환 연산자에 대한 대안으로 정의합니다.

[!code-csharp[Conceptual.CLSCompliant#15](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/convert1.cs#15)]
[!code-vb[Conceptual.CLSCompliant#15](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/convert1.vb#15)]

<a name="arrays"></a>

### <a name="arrays"></a>배열

CLS 규격 배열은 다음 규칙을 따릅니다.

- 배열의 모든 크기는 하한이 0이어야 합니다. 다음 예제에서는 하한이 1인 CLS 비규격 배열을 만듭니다. <xref:System.CLSCompliantAttribute> 특성이 있음에도 불구하고 `Numbers.GetTenPrimes` 메서드에서 반환된 배열이 CLS 규격이 아님을 컴파일러에서 감지하지 못합니다.

  [!code-csharp[Conceptual.CLSCompliant#8](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/array1.cs#8)]
  [!code-vb[Conceptual.CLSCompliant#8](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/array1.vb#8)]

- 모든 배열 요소는 CLS 규격 형식으로 구성되어야 합니다. 다음 예제에서는 CLS 비규격 배열을 반환하는 두 개의 메서드를 정의합니다. 첫 번째는 <xref:System.UInt32> 값의 배열을 반환합니다. 두 번째는 <xref:System.Object> 및 <xref:System.Int32> 값이 포함된 <xref:System.UInt32> 배열을 반환합니다. 컴파일러는 <xref:System.UInt32> 형식 때문에 첫 번째 배열을 비규격으로 식별하지만 두 번째 배열이 CLS 비규격 요소를 포함하는지 인식하지 못합니다.

  [!code-csharp[Conceptual.CLSCompliant#9](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/array2.cs#9)]
  [!code-vb[Conceptual.CLSCompliant#9](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/array2.vb#9)]

- 배열 매개 변수가 있는 메서드에 대한 오버로드 확인은 이들이 배열인지 여부와 해당 요소 형식을 기반으로 합니다. 따라서 오버로드된 `GetSquares` 메서드의 다음 정의는 CLS 규격입니다.

  [!code-csharp[Conceptual.CLSCompliant#10](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/array3.cs#10)]
  [!code-vb[Conceptual.CLSCompliant#10](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/array3.vb#10)]

<a name="Interfaces"></a>

### <a name="interfaces"></a>인터페이스

CLS 규격 인터페이스는 속성, 이벤트 및 가상 메서드를 정의할 수 있습니다(구현이 없는 메서드). CLS 규격 인터페이스에는 다음이 포함될 수 없습니다.

- 정적 메서드 또는 정적 필드. 인터페이스에 정적 멤버를 정의할 경우 C# 및 Visual Basic 컴파일러 모두에서 컴파일러 오류가 발생합니다.

- 필드. 인터페이스에 필드를 정의할 경우 C# 및 Visual Basic 컴파일러 모두에서 컴파일러 오류가 발생합니다.

- CLS 규격이 아닌 메서드. 예를 들어 다음 인터페이스 정의에는 CLS 비규격으로 표시된 `INumber.GetUnsigned` 메서드가 포함되어 있습니다. 이 예제에서는 컴파일러 경고가 발생합니다.

  [!code-csharp[Conceptual.CLSCompliant#6](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/interface2.cs#6)]
  [!code-vb[Conceptual.CLSCompliant#6](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/interface2.vb#6)]

  이 규칙 때문에 CLS 규격이 아닌 멤버를 구현하는 데에는 CLS 규격 형식이 필요하지 않습니다. CLS 규격 프레임워크에서 CLS 비규격 인터페이스를 구현하는 클래스를 노출하는 경우, 모든 CLS 비규격 멤버의 구체적 구현도 제공해야 합니다.

CLS 규격 언어 컴파일러를 사용하면 클래스는 다중 인터페이스에서 동일한 이름과 시그니처를 가진 멤버를 개별적으로 구현할 수 있습니다.  C# 및 Visual Basic 모두에서 [명시적 인터페이스 구현](../csharp/programming-guide/interfaces/explicit-interface-implementation.md)을 지원하여 동일한 이름의 메서드를 다르게 구현할 수 있습니다. Visual Basic에서는 `Implements` 키워드도 지원하므로 특정 멤버가 구현하는 인터페이스와 멤버를 명시적으로 지정할 수 있습니다. 다음 예제에서는 `Temperature` 및 `ICelsius` 인터페이스를 명시적 인터페이스 구현으로 구현하는 `IFahrenheit` 클래스를 정의하여 이 시나리오를 보여 줍니다.

[!code-csharp[Conceptual.CLSCompliant#24](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/eii1.cs#24)]
[!code-vb[Conceptual.CLSCompliant#24](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/eii1.vb#24)]

<a name="enums"></a>

### <a name="enumerations"></a>열거형

CLS 규격 열거형은 다음 규칙을 따라야 합니다.

- 열거형의 기본 형식은 내장 CLS 규격 정수(<xref:System.Byte>, <xref:System.Int16>, <xref:System.Int32> 또는 <xref:System.Int64>)여야 합니다. 예를 들어 다음 코드에서는 기본 형식이 <xref:System.UInt32>이고 컴파일러 경고를 발생시키는 열거형을 정의하려 합니다.

  [!code-csharp[Conceptual.CLSCompliant#7](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/enum3.cs#7)]
  [!code-vb[Conceptual.CLSCompliant#7](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/enum3.vb#7)]

- 열거형 형식에는 `Value__` 특성으로 표시되는 <xref:System.Reflection.FieldAttributes.RTSpecialName?displayProperty=nameWithType>라는 단일 인스턴스 필드가 있어야 합니다. 이를 통해 필드 값을 암시적으로 참조할 수 있습니다.

- 열거형에는 형식이 해당 열거형의 형식과 일치하는 리터럴 정적 필드가 포함됩니다. 예를 들어 `State` 및 `State.On`의 값으로 `State.Off` 열거형을 정의하는 경우, `State.On` 및 `State.Off`는 모두 `State` 형식 리터럴 정적 필드입니다.

- 열거형에는 다음 두 가지 종류가 있습니다.

  - 상호 배타적인 명명된 정수 값 집합을 나타내는 열거형. 이러한 유형의 열거형은 <xref:System.FlagsAttribute?displayProperty=nameWithType> 사용자 지정 특성이 없는 것으로 표시됩니다.

  - 결합하여 명명되지 않은 값을 생성할 수 있는 비트 플래그 집합을 나타내는 열거형. 이러한 유형의 열거형은 <xref:System.FlagsAttribute?displayProperty=nameWithType> 사용자 지정 특성이 있는 것으로 표시됩니다.

  자세한 내용은 <xref:System.Enum> 구조체에 대한 설명서를 참조하십시오.

- 열거형의 값은 지정된 값의 범위로 제한되지 않습니다. 즉, 열거형의 값 범위는 기본 값의 범위입니다. <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> 메서드를 사용하여 지정된 값이 열거형 멤버인지 여부를 확인할 수 있습니다.

<a name="members"></a>

### <a name="type-members-in-general"></a>형식 멤버 일반 사항

공용 언어 사양에서는 모든 필드와 메서드가 특정 클래스의 멤버로 액세스할 수 있어야 합니다. 따라서 전역 정적 필드와 메서드(즉, 형식과 별도로 정의된 정적 필드 또는 메서드)는 CLS 규격이 아닙니다. 소스 코드에 전역 필드 또는 메서드를 포함하려고 하면 C# 및 Visual Basic 컴파일러 모두에서 컴파일러 오류가 발생합니다.

공용 언어 사양은 관리되는 표준 호출 규칙만 지원합니다. `varargs` 키워드로 표시된 가변 인수 목록을 사용하여 관리되지 않는 호출 규칙 및 메서드를 지원하지 않습니다. 관리되는 표준 호출 규칙과 호환되는 가변 인수 목록을 얻으려면 <xref:System.ParamArrayAttribute> 특성 또는 C#의 `params` 키워드와 Visual Basic의 `ParamArray` 키워드와 같은 개별 언어의 구현을 이용합니다.

<a name="MemberAccess"></a>

### <a name="member-accessibility"></a>멤버 접근성

상속된 멤버를 재정의하면 해당 멤버의 액세스 가능성을 변경할 수 없습니다. 예를 들어 파생된 클래스의 private 메서드가 기본 클래스의 public 메서드를 재정의할 수 없습니다. 한 가지 예외는 다른 어셈블리의 형식으로 재정의된 한 어셈블리에 있는 `protected internal`(C#의 경우) 또는 `Protected Friend`(Visual Basic의 경우) 멤버입니다. 이 경우, 재정의에 대한 액세스 가능성은 `Protected`입니다.

다음 예제에서는 <xref:System.CLSCompliantAttribute> 특성이 `true`로 설정되고 `Human`에서 파생된 `Animal` 클래스가 `Species` 속성의 액세스 가능성을 public에서 private으로 변경하려고 할 때 생성되는 오류를 보여 줍니다. 이 예제는 해당 액세스 가능성이 public으로 변경되는 경우 성공적으로 컴파일됩니다.

[!code-csharp[Conceptual.CLSCompliant#28](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/accessibility1.cs#28)]
[!code-vb[Conceptual.CLSCompliant#28](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/accessibility1.vb#28)]

멤버 시그니처의 형식은 해당 멤버를 액세스할 수 있는 경우 항상 액세스할 수 있어야 합니다. 예를 들어 public 멤버는 형식이 private, protected 또는 internal인 매개 변수를 포함할 수 없습니다. 다음 예제에서는 `StringWrapper` 클래스 생성자가 문자열 값을 래핑하는 방법을 결정하는 internal `StringOperationType` 열거형 값을 노출할 때 결과로 발생하는 컴파일러 오류를 보여 줍니다.

[!code-csharp[Conceptual.CLSCompliant#27](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/accessibility3.cs#27)]
[!code-vb[Conceptual.CLSCompliant#27](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/accessibility3.vb#27)]

<a name="Generics"></a>

### <a name="generic-types-and-members"></a>제네릭 형식 및 멤버

중첩 형식에는 적어도 바깥쪽 형식과 같은 수의 제네릭 매개 변수가 항상 있어야 합니다. 이러한 값은 바깥쪽 형식의 제네릭 매개 변수와 위치가 같습니다. 제네릭 형식은 새 제네릭 매개 변수를 포함할 수도 있습니다.

포함 형식의 제네릭 형식 매개 변수와 중첩 형식 사이의 관계는 개별 언어의 구문에 의해 숨겨질 수 있습니다. 다음 예제에서 제네릭 형식 `Outer<T>`에는 두 개의 중첩된 클래스인 `Inner1A` 및 `Inner1B<U>`가 포함됩니다. `ToString`에서 각 클래스를 상속하는 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드에 대한 호출은 포함하는 해당 클래스의 형식 매개 변수가 각 중첩 클래스에 포함되는 것을 보여 줍니다.

[!code-csharp[Conceptual.CLSCompliant#29](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/nestedgenerics2.cs#29)]
[!code-vb[Conceptual.CLSCompliant#29](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/nestedgenerics2.vb#29)]

제네릭 형식 이름을 *name\`n* 형식으로 인코딩합니다. 여기서 *name*은 형식 이름, \`는 문자 리터럴, *n*은 이 형식에서 선언된 매개 변수의 개수 또는 중첩된 제네릭 형식의 경우 새로 도입된 형식 매개 변수의 개수입니다. 제네릭 형식 이름의 이러한 인코딩은 라이브러리에서 CLS 규격 제네릭 형식에 액세스하기 위해 리플렉션을 사용하는 개발자들에게 주로 유용합니다.

제약 조건이 제네릭 형식에 적용될 경우 제약 조건으로 사용되는 모든 형식도 CLS 규격이어야 합니다. 다음 예제에서는 CLS 규격 및 `BaseClass` 제네릭 클래스가 아닌 이름이 `BaseCollection`인 클래스를 정의합니다. 해당 형식 매개 변수는 `BaseClass`에서 파생되어야 합니다. 하지만 `BaseClass`는 CLS 규격이 아니므로 컴파일러에서 경고를 발생시킵니다.

[!code-csharp[Conceptual.CLSCompliant#34](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics5.cs#34)]
[!code-vb[Conceptual.CLSCompliant#34](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics5.vb#34)]

제네릭 형식이 제네릭 기본 형식에서 파생되는 경우 기본 형식에 대한 제약 조건이 충족됨을 보장할 수 있도록 모든 제약 조건을 다시 선언해야 합니다. 다음 예제에서는 임의의 숫자 형식을 나타낼 수 있는 `Number<T>`를 정의합니다. 또한 부동 소수점 값을 나타내는 `FloatingPoint<T>` 클래스도 정의합니다. 하지만 이 소스 코드는 `Number<T>`(여기서 T는 값 형식이어야 함)에 대한 제약 조건을 `FloatingPoint<T>`에 적용하지 못하므로 컴파일되지 못합니다.

[!code-csharp[Conceptual.CLSCompliant#30](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics2a.cs#30)]
[!code-vb[Conceptual.CLSCompliant#30](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics2a.vb#30)]

이 예제는 제약 조건이 `FloatingPoint<T>` 클래스에 추가되는 경우 성공적으로 컴파일됩니다.

[!code-csharp[Conceptual.CLSCompliant#31](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics2.cs#31)]
[!code-vb[Conceptual.CLSCompliant#31](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics2.vb#31)]

공용 언어 사양에서는 중첩된 형식 및 protected 멤버에 대해 보수적인 인스턴스화별 모델을 적용합니다. 개방형 제네릭 형식은 protected 중첩 제네릭 형식의 특정 인스턴스화를 포함하는 시그니처로 필드 또는 멤버를 노출할 수 없습니다. 제네릭 기본 클래스나 인터페이스의 특정 인스턴스화를 확장하는 제네릭이 아닌 형식은 protected 중첩 제네릭 형식의 다른 인스턴스화를 포함하는 서명이 있는 필드나 멤버를 노출할 수 없습니다.

다음 예제에서는 제네릭 형식 `C1<T>`(Visual Basic의 경우 `C1(Of T)`)와 protected 클래스 `C1<T>.N`(Visual Basic의 경우 `C1(Of T).N`)을 정의합니다. `C1<T>`에는 `M1` 및 `M2`의 두 메서드가 있습니다. 하지만 `M1`은 C1\<T>(또는 `C1(Of T)`)에서 `C1<int>.N`(또는 `C1(Of Integer).N`) 개체를 반환하려 하므로 CLS 규격이 아닙니다. 두 번째 클래스인 `C2`는 `C1<long>`(또는 `C1(Of Long)`)에서 파생됩니다. 여기에는 `M3` 및 `M4`의 두 메서드가 있습니다. `M3`는 `C1<int>.N`의 하위 클래스에서 `C1(Of Integer).N`(또는 `C1<long>`) 개체를 반환하려 하므로 CLS 규격이 아닙니다. 언어 컴파일러는 훨씬 더 제한적일 수 있습니다. 이 예제에서는 Visual Basic에서 `M4`를 컴파일하려고 하면 오류를 표시합니다.

[!code-csharp[Conceptual.CLSCompliant#32](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics4.cs#32)]
[!code-vb[Conceptual.CLSCompliant#32](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics4.vb#32)]

<a name="ctors"></a>

### <a name="constructors"></a>생성자

CLS 규격 클래스의 생성자와 구조체는 다음 규칙을 따라야 합니다.

- 파생된 클래스의 생성자는 상속된 인스턴스 데이터에 액세스하기 전에 기본 클래스의 인스턴스 생성자를 호출해야 합니다. 이 요구 사항은 파생된 클래스에서 기본 클래스 생성자가 상속되지 않기 때문입니다. 이 규칙은 직접 상속을 지원하지 않는 구조체에는 적용되지 않습니다.

  일반적으로 컴파일러는 다음 예제에서처럼 CLS 규격 여부와는 독립적으로 이 규칙을 적용합니다. 이 예제에서는 `Doctor` 클래스에서 파생되는 `Person` 클래스를 만들지만 `Doctor` 클래스는 `Person` 클래스 생성자를 호출하여 상속된 인스턴스 필드를 초기화하는 데 실패합니다.

  [!code-csharp[Conceptual.CLSCompliant#11](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/ctor1.cs#11)]
  [!code-vb[Conceptual.CLSCompliant#11](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/ctor1.vb#11)]

- 개체 생성자는 개체를 만드는 경우를 제외하고는 호출할 수 없습니다. 또한 개체는 두 번 초기화할 수 없습니다. 예를 들어 <xref:System.Object.MemberwiseClone%2A?displayProperty=nameWithType> 및 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> 와 같은 deserialization 메서드는 생성자를 호출해서는 안 됩니다.

<a name="properties"></a>

### <a name="properties"></a>속성

CLS 규격 형식의 속성은 다음 규칙을 따라야 합니다.

- 속성에는 setter, getter 또는 둘 모두가 있어야 합니다. 어셈블리에서 이러한 메서드는 특수한 메서드로 구현됩니다. 즉, 어셈블리의 메타데이터에 `SpecialName`으로 표시되는 별도 메서드(이름이 getter는 `get_`*propertyname*, setter는 `set_`*propertyname*임)로 나타납니다. C# 및 Visual Basic 컴파일러에서는 <xref:System.CLSCompliantAttribute> 특성을 적용할 필요 없이 자동으로 이 규칙이 적용됩니다.

- 속성의 형식은 속성 getter의 반환 형식이며 setter의 마지막 인수입니다. 이러한 형식은 CLS 규격이어야 하며 인수는 참조로 속성에 할당할 수 없습니다. 즉, 관리되는 포인터일 수 없습니다.

- 속성에 getter와 setter가 모두 있는 경우, 둘 다 virtual이거나 static이거나 instance여야 합니다. C# 및 Visual Basic 컴파일러에서는 속성 정의 구문을 통해 이 규칙을 자동으로 적용합니다.

<a name="events"></a>

### <a name="events"></a>이벤트

이벤트는 이름 및 해당 형식으로 정의됩니다. 이벤트 유형은 이벤트를 나타내는 데 사용되는 대리자입니다. 예를 들어 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트는 <xref:System.ResolveEventHandler> 형식입니다. 해당 이벤트에 추가로 이 이벤트 이름을 기반으로 한 이름의 다음 세 가지 메서드가 이벤트를 구현하고 어셈블리의 메타데이터에 `SpecialName`으로 표시됩니다.

- 이벤트 처리기를 추가하는 `add_`*EventName* 메서드. 예를 들어 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트의 이벤트 구독 메서드 이름은 `add_AssemblyResolve`입니다.

- 이벤트 처리기를 제거하는 `remove_`*EventName* 메서드. 예를 들어 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트의 제거 메서드 이름은 `remove_AssemblyResolve`입니다.

- 이벤트가 발생했음을 나타내는 `raise_`*EventName* 메서드

> [!NOTE]
> 이벤트에 관련된 대부분의 공용 언어 사양 규칙은 언어 컴파일러에서 구현되며 구성 요소 개발자에게 투명하게 공개됩니다.

이벤트를 추가, 제거 또는 발생시키는 메서드의 액세스 가능성은 모두 동일해야 합니다. 또한 모두 동일하게 static, instance 또는 virtual이어야 합니다. 이벤트를 추가하고 제거하는 메서드에는 이벤트 대리자 형식의 매개 변수가 하나 있습니다. 추가 메서드와 제거 메서드는 모두 있거나 모두 없어야 합니다.

다음 예제에서는 두 계측값 사이의 온도 변화가 임계값과 같거나 이를 넘어설 때 `Temperature` 이벤트를 발생시키는 CLS 규격 클래스 `TemperatureChanged`를 정의합니다. `Temperature` 클래스는 이벤트 처리기를 선택적으로 실행할 수 있도록 `raise_TemperatureChanged` 메서드를 명시적으로 정의합니다.

[!code-csharp[Conceptual.CLSCompliant#20](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/event1.cs#20)]
[!code-vb[Conceptual.CLSCompliant#20](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/event1.vb#20)]

<a name="overloads"></a>

### <a name="overloads"></a>Overloads

공용 언어 사양에서는 오버로드된 멤버에 대해 다음과 같은 요구 사항을 적용합니다.

- 매개 변수 개수와 매개 변수 형식에 따라 멤버를 오버로드할 수 있습니다. 호출 규칙, 반환 형식, 사용자 지정 한정자는 메서드 또는 해당 매개 변수에 적용되며, 오버로드 간에 구별하는 경우 매개 변수가 값으로 전달되는지 또는 참조로 전달되는지 여부는 고려되지 않습니다. 예를 들어 이름이 [명명 규칙](#naming) 섹션의 적용 범위 내에서 고유해야 한다는 요구 사항에 대한 코드를 참조하세요.

- 속성 및 메서드만 오버로드될 수 있습니다. 필드 및 이벤트는 오버로드할 수 없습니다.

- 제네릭 메서드는 제네릭 매개 변수의 개수에 따라 오버로드될 수 있습니다.

> [!NOTE]
> `op_Explicit` 연산자와 `op_Implicit` 연산자는 반환 값은 오버로드 확인을 위한 메서드 시그니처의 일부로 고려되지 않는다는 규칙의 예외입니다. 이러한 두 연산자는 매개 변수 및 해당 반환 값에 따라 오버로드될 수 있습니다.

<a name="exceptions"></a>

### <a name="exceptions"></a>예외

예외 개체는 <xref:System.Exception?displayProperty=nameWithType>에서 파생되거나 <xref:System.Exception?displayProperty=nameWithType>에서 파생된 또 다른 형식에서 파생되어야 합니다. 다음 예제에서는 사용자 지정 클래스 `ErrorClass`가 예외 처리에 사용될 때 결과로 발생하는 컴파일러 오류를 보여 줍니다.

[!code-csharp[Conceptual.CLSCompliant#13](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/exceptions1.cs#13)]
[!code-vb[Conceptual.CLSCompliant#13](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/exceptions1.vb#13)]

이 오류를 수정하려면 `ErrorClass` 클래스는 <xref:System.Exception?displayProperty=nameWithType>에서 상속해야 합니다. 또한 `Message` 속성을 재정의해야 합니다. 다음 예제에서는 이러한 오류를 해결하여 CLS 규격 `ErrorClass` 클래스를 정의합니다.

[!code-csharp[Conceptual.CLSCompliant#14](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/exceptions2.cs#14)]
[!code-vb[Conceptual.CLSCompliant#14](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/exceptions2.vb#14)]

<a name="attributes"></a>

### <a name="attributes"></a>특성

.NET Framework 어셈블리에서 사용자 지정 특성은 확장 가능한 메커니즘을 제공하여 사용자 지정 특성을 저장하고 어셈블리, 형식, 멤버, 메서드 매개 변수 등의 개체 프로그래밍에 대한 메타데이터를 검색할 수 있도록 합니다. 사용자 지정 특성은 <xref:System.Attribute?displayProperty=nameWithType>에서 파생되거나 <xref:System.Attribute?displayProperty=nameWithType>에서 파생된 형식에서 파생되어야 합니다.

다음은 이 규칙을 위반하는 예제입니다. 이 예제에서는 `NumericAttribute`에서 파생되지 않은 <xref:System.Attribute?displayProperty=nameWithType> 클래스를 정의합니다. 컴파일러 오류는 클래스를 정의하지 않은 경우가 아닌 CLS 규격이 아닌 특성이 적용되는 경우에만 발생합니다.

[!code-csharp[Conceptual.CLSCompliant#18](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/attribute1.cs#18)]
[!code-vb[Conceptual.CLSCompliant#18](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/attribute1.vb#18)]

CLS 규격 특성의 속성 또는 생성자는 다음과 같은 형식만 노출할 수 있습니다.

- <xref:System.Boolean>

- <xref:System.Byte>

- <xref:System.Char>

- <xref:System.Double>

- <xref:System.Int16>

- <xref:System.Int32>

- <xref:System.Int64>

- <xref:System.Single>

- <xref:System.String>

- <xref:System.Type>

- 기본 형식이 <xref:System.Byte>, <xref:System.Int16>, <xref:System.Int32> 또는 <xref:System.Int64>인 열거형 형식입니다.

다음 예제에서는 `DescriptionAttribute`에서 파생되는 <xref:System.Attribute> 클래스를 정의합니다. 클래스 생성자에 `Descriptor` 형식의 매개 변수가 있으므로 이 클래스는 CLS 규격이 아닙니다. Visual Basic 컴파일러에서 경고나 오류를 발생시키지 않는 데 반면 C# 컴파일러에서는 경고를 표시하긴 하지만 성공적으로 컴파일됩니다.

[!code-csharp[Conceptual.CLSCompliant#33](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/attribute2.cs#33)]
[!code-vb[Conceptual.CLSCompliant#33](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/attribute2.vb#33)]

<a name="CLSAttribute"></a>

## <a name="the-clscompliantattribute-attribute"></a>CLSCompliantAttribute 특성

<xref:System.CLSCompliantAttribute> 특성은 프로그램 요소가 공용 언어 사양을 준수하는지 여부를 나타내는 데 사용됩니다. <xref:System.CLSCompliantAttribute.%23ctor%28System.Boolean%29?displayProperty=nameWithType> 생성자에는 프로그램 요소가 CLS 규격인지 여부를 나타내는 단일 필수 매개 변수 `isCompliant`가 포함되어 있습니다.

컴파일 타임에 컴파일러는 CLS 규격으로 우선 간주되었던 비규격 요소를 검색하고 경고를 발생시킵니다. 컴파일러는 비규격으로 명시적 선언된 형식 또는 멤버에 대해서는 경고를 발생시키지 않습니다.

구성 요소 개발자는 다음 두 가지 방식으로 <xref:System.CLSCompliantAttribute> 특성을 사용할 수 있습니다.

- CLS 규격인 구성 요소에서 노출된 공용 인터페이스 부분과 CLS 규격이 아닌 부분을 정의합니다. 특정 프로그램 요소를 CLS 규격으로 표시하도록 특성을 사용하면, 해당 요소는 .NET Framework를 대상으로 하는 모든 언어 및 도구에서 액세스 가능성이 보장됩니다.

- 구성 요소 라이브러리의 공용 인터페이스에서 CLS 규격인 프로그램 요소만을 노출시키도록 합니다. 요소가 CLS 규격이 아닌 경우, 일반적으로 컴파일러에서 경고가 발생합니다.

> [!WARNING]
> 경우에 따라 언어 컴파일러는 <xref:System.CLSCompliantAttribute> 특성 사용 여부에 관계없이 CLS 규격 규칙을 적용합니다. 예를 들어, 인터페이스에서 정적 멤버를 정의하면 CLS 규칙에 위반됩니다. 이와 관련하여 인터페이스의 `static`(C#) 또는 `Shared`(Visual Basic) 멤버를 정의하는 경우, C# 및 Visual Basic 컴파일러 모두에서 오류 메시지가 표시되고 앱이 컴파일되지 않습니다.

<xref:System.CLSCompliantAttribute> 특성은 <xref:System.AttributeUsageAttribute>의 값을 갖는 <xref:System.AttributeTargets.All?displayProperty=nameWithType> 특성으로 표시됩니다. 이 값을 사용하면 <xref:System.CLSCompliantAttribute> 특성을 어셈블리, 모듈, 형식(클래스, 구조체, 열거형, 인터페이스 및 대리자), 형식 멤버(생성자, 메서드, 속성, 필드 및 이벤트), 매개 변수, 제네릭 매개 변수 및 반환 값 등 어떤 프로그램 요소에도 적용할 수 있습니다. 그러나 실제로는 어셈블리, 형식 및 형식 멤버에만 이 특성을 적용해야 합니다. 그러지 않으면 컴파일러는 특성을 무시하고 라이브러리의 공용 인터페이스에서 비규격 매개 변수, 제네릭 매개 변수 또는 반환 값이 발생할 때마다 컴파일러 경고를 계속해서 생성합니다.

<xref:System.CLSCompliantAttribute> 특성의 값은 포함된 프로그램 요소에 의해 상속됩니다. 예를 들어, 어셈블리가 CLS 규격으로 표시되어 있으면 해당 형식도 CLS 규격입니다. 또한 형식이 CLS 규격으로 표시되어 있으면 해당 중첩 형식 및 멤버도 CLS 규격입니다.

포함된 프로그램 요소에 <xref:System.CLSCompliantAttribute> 특성을 적용하여 상속된 규격을 명시적으로 재정의할 수 있습니다. 예를 들어 <xref:System.CLSCompliantAttribute>의 `isCompliant` 값으로 `false` 특성을 사용하면 규격 어셈블리에서 비규격 형식을 정의할 수 있고, `isCompliant`의 `true` 값으로 해당 특성을 사용하면 비규격 어셈블리에서 규격 형식을 정의할 수 있습니다. 또한 규격 형식으로 비규격 멤버를 정의할 수도 있습니다. 하지만 비규격 형식은 규격 멤버를 가질 수 없기 때문에 비규격 형식의 상속을 재정의하기 위해서 `isCompliant`의 `true` 값으로 이 특성을 사용할 수는 없습니다.

구성 요소를 개발하는 경우 어셈블리 및 해당 형식과 멤버가 CLS 규격인지 여부를 나타내는 <xref:System.CLSCompliantAttribute> 특성을 반드시 사용해야 합니다.

CLS 규격 구성 요소를 만들려면

1. <xref:System.CLSCompliantAttribute>를 사용하여 어셈블리를 CLS 규격으로 표시합니다.

2. CLS 규격이 아닌 어셈블리의 공개적으로 노출되는 모든 형식을 비규격으로 표시합니다.

3. CLS 규격 형식의 공개적으로 노출되는 모든 멤버를 비규격으로 표시합니다.

4. CLS 규격이 아닌 멤버에 대해 CLS 규격 대체 멤버를 제공합니다.

모든 비규격 형식 및 멤버를 성공적으로 표시한 경우 컴파일러에서 미준수 경고가 발생하지 않아야 합니다. 그러나 제품 설명서에 CLS 규격이 아닌 멤버를 표시하고 이들의 CLS 규격 대체 멤버를 명시해야 합니다.

다음 예제에서는 <xref:System.CLSCompliantAttribute> 특성을 사용하여 CLS 규격 어셈블리와 CLS 규격이 아닌 멤버 두 개가 포함된 `CharacterUtilities` 형식을 정의합니다. 두 멤버 모두 `CLSCompliant(false)` 특성으로 태그가 지정되어 있으므로 컴파일러에서 경고를 생성하지 않습니다. 또한 이 클래스는 두 메서드 모두에 대해 CLS 규격 대체 메서드를 제공합니다. 일반적으로 두 오버로드를 `ToUTF16` 메서드에 추가하여 CLS 규격 대체 메서드를 제공할 수 있습니다. 하지만 메서드는 반환 값을 기반으로 오버로드될 수 없기 때문에, CLS 규격 메서드의 이름은 비규격 메서드의 이름과는 다릅니다.

[!code-csharp[Conceptual.CLSCompliant#35](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/indicator3.cs#35)]
[!code-vb[Conceptual.CLSCompliant#35](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/indicator3.vb#35)]

라이브러리가 아닌 응용 프로그램을 개발하는 경우(다른 응용 프로그램 개발자가 사용할 수 있는 형식 또는 멤버를 노출하지 않으려는 경우) 응용 프로그램이 사용하는 프로그램 요소의 CLS 규격은 해당 언어가 지원하지 않는 경우에만 관련됩니다. 이 경우에 CLS 규격이 아닌 요소를 사용하려고 하면 언어 컴파일러에서 오류가 발생합니다.

<a name="CrossLang"></a>

## <a name="cross-language-interoperability"></a>언어 간 상호 운용성

언어 독립성은 여러 가지 의미를 가질 수 있습니다. [언어 독립성 및 언어 독립 구성 요소](../../docs/standard/language-independence-and-language-independent-components.md) 문서에 설명된 한 가지 의미는 한 언어로 작성된 형식을 다른 언어로 작성된 앱에서 원활하게 사용하는 것입니다. 이 문서의 핵심이기도 한 두 번째 의미는 여러 언어로 작성된 코드를 단일 .NET Framework 어셈블리로 결합하는 것입니다.

다음 예제에서는 두 클래스 `NumericLib` 및 `StringLib`를 포함하는 Utilities.dll이라는 클래스 라이브러리를 만들어 언어 간 상호 운용성을 보여 줍니다. `NumericLib` 클래스는 C#으로 작성되었고 `StringLib` 클래스는 Visual Basic으로 작성되었습니다. 다음은 단일 멤버 `ToTitleCase`를 해당 `StringLib` 클래스에 포함하는 StringUtil.vb용 소스 코드입니다.

[!code-vb[Conceptual.CrossLanguage#1](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.crosslanguage/vb/stringutil.vb#1)]

다음은 `NumericLib` 및 `IsEven`라는 두 가지 멤버를 가진 `NearZero` 클래스를 정의하는 NumberUtil.cs용 소스 코드입니다.

[!code-csharp[Conceptual.CrossLanguage#2](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.crosslanguage/cs/numberutil.cs#2)]

두 클래스를 단일 어셈블리로 패키징하려면 모듈로 컴파일해야 합니다. Visual Basic 소스 코드 파일을 모듈로 컴파일하려면 다음 명령을 사용합니다.

```console
vbc /t:module StringUtil.vb
```

Visual Basic 컴파일러의 명령줄 구문에 대한 자세한 내용은 [명령줄에서 빌드](../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)를 참조하세요.

C# 소스 코드 파일을 모듈로 컴파일하려면 다음 명령을 사용합니다.

```console
csc /t:module NumberUtil.cs
```

C# 컴파일러의 명령줄 구문에 대한 자세한 내용은 [csc.exe를 사용한 명령줄 빌드](../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)를 참조하세요.

그런 다음, [링커 옵션](/cpp/build/reference/linker-options)을 사용하여 두 모듈을 하나의 어셈블리로 컴파일합니다.

```console
link numberutil.netmodule stringutil.netmodule /out:UtilityLib.dll /dll
```

다음 예제에서는 `NumericLib.NearZero` 및 `StringLib.ToTitleCase` 메서드를 호출합니다. Visual Basic 코드와 C# 코드 둘 다 두 클래스의 메서드에 액세스할 수 있습니다.

[!code-csharp[Conceptual.CrossLanguage#3](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.crosslanguage/cs/useutilities1.cs#3)]
[!code-vb[Conceptual.CrossLanguage#3](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.crosslanguage/vb/useutilities1.vb#3)]

Visual Basic 코드를 컴파일하려면 다음 명령을 사용합니다.

```console
vbc example.vb /r:UtilityLib.dll
```

C#으로 컴파일하려면 **vbc**에서 **csc**로 컴파일러의 이름을 변경하고 .vb에서 .cs로 파일 확장명을 변경합니다.

```console
csc example.cs /r:UtilityLib.dll
```

## <a name="see-also"></a>참고 항목

- <xref:System.CLSCompliantAttribute>
