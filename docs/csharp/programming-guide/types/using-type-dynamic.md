---
title: dynamic 형식 사용 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- dynamic [C#], about dynamic type
- dynamic type [C#]
ms.assetid: 3828989d-c967-4a51-b948-857ebc8fdf26
ms.openlocfilehash: 4141c64ff6dbbec60b53a41862a4273df6ef51ab
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588353"
---
# <a name="using-type-dynamic-c-programming-guide"></a>dynamic 형식 사용(C# 프로그래밍 가이드)

C# 4에서는 새로운 `dynamic` 형식이 도입되었습니다. 이 형식은 정적 형식이지만 `dynamic` 형식의 개체가 정적 형식 검사를 건너뜁니다. 대부분의 경우 이 형식은 `object` 형식을 가지고 있는 것처럼 작동합니다. 컴파일 시간에 `dynamic` 형식의 요소는 모든 연산을 지원하는 것으로 간주됩니다. 따라서 개체가 값을 COM API, IronPython 같은 동적 언어, HTML DOM(문서 개체 모델), 리플렉션 또는 프로그램의 다른 곳 등 어디서 가져오든 신경을 쓸 필요가 없습니다. 그러나 코드가 유효하지 않으면 런타임 시 오류가 catch됩니다.

예를 들어 다음 코드의 인스턴스 메서드 `exampleMethod1`에 매개 변수가 하나뿐인 경우, 컴파일러는 메서드 `ec.exampleMethod1(10, 4)`에 대한 첫 번째 호출이 유효하지 않음을 인식합니다. 여기에 인수가 두 개 포함되었기 때문입니다. 호출 시 컴파일러 오류가 발생합니다. 컴파일러는 메서드 `dynamic_ec.exampleMethod1(10, 4)`에 대한 두 번째 호출을 확인하지 않습니다. `dynamic_ec`의 형식이 `dynamic`이기 때문입니다. 따라서 컴파일러 오류가 보고되지 않습니다. 그러나 이 오류는 알림을 무기한 이스케이프하지 않고, 런타임에 catch되며 런타임 예외를 일으킵니다.

[!code-csharp[CsProgGuideTypes#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#50)]

[!code-csharp[CsProgGuideTypes#56](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#56)]

이 예제에서 컴파일러의 역할은 `dynamic`으로 형식이 지정된 개체 또는 식에 대해 각 문이 해야 할 일에 대한 정보를 패키지하는 것입니다. 런타임에는 저장된 정보의 검사가 수행되며, 유효하지 않은 문에서 런타임 예외가 발생합니다.

대부분의 동적 작업은 결과 그 자체가 `dynamic`입니다. 다음 예제에서 `testSum`이 사용된 곳에 마우스 포인터를 올려두면 IntelliSense에서 **(지역 변수) dynamic testSum** 형식을 표시합니다.

[!code-csharp[CsProgGuideTypes#51](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#51)]

결과가 `dynamic`이 아닌 작업은 다음을 포함합니다.

* `dynamic`에서 다른 형식으로의 전환.
* `dynamic` 형식의 인수를 포함하는 생성자 호출.

예를 들어 다음 선언에서 `testInstance`의 형식은 `dynamic`이 아니라 `ExampleClass`입니다.

[!code-csharp[CsProgGuideTypes#52](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#52)]

변환 예제는 다음 섹션인 "변환"에 나와 있습니다.

## <a name="conversions"></a>변환

동적 개체와 다른 형식 간에 손쉽게 변환할 수 있습니다. 따라서 개발자는 동적 동작과 비동적 동작 간에 전환할 수 있습니다.

다음 예제와 같이 개체를 동적 형식으로 암시적으로 변환할 수 있습니다.

[!code-csharp[CsProgGuideTypes#53](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#53)]

반대로, 암시적 변환을 `dynamic` 형식의 식에 동적으로 적용할 수 있습니다.

[!code-csharp[CsProgGuideTypes#54](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#54)]

## <a name="overload-resolution-with-arguments-of-type-dynamic"></a>동적 형식의 인수로 오버로드 확인

메서드 호출 내 하나 이상의 인수에 `dynamic` 형식이 있거나 메서드 호출의 수신자가 `dynamic` 형식인 경우 오버로드 확인은 컴파일 시간이 아니라 런타임에 발생합니다. 다음 예제에서 액세스 가능한 유일한 `exampleMethod2` 메서드가 문자열 인수를 사용하도록 정의되는 경우, `d1`을 인수로서 전송하면 컴파일러 오류는 발생하지 않지만 런타임 예외가 발생합니다. `d1`의 런타임 형식은 `int`인데 `exampleMethod2`에는 문자열이 필요하므로 오버로드 확인이 런타임에 실패합니다.

[!code-csharp[CsProgGuideTypes#55](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#55)]

## <a name="dynamic-language-runtime"></a>동적 언어 런타임

DLR(동적 언어 런타임)은 .NET Framework 4의 새로운 API입니다. DLR은 C#에서 `dynamic` 형식을 지원하는 인프라를 제공하며, IronPython 및 IronRuby와 같은 동적 프로그래밍 언어를 구현합니다. DLR에 대한 자세한 내용은 [동적 언어 런타임 개요](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)를 참조하세요.

## <a name="com-interop"></a>COM interop

C# 4에는 Office Automation API 등의 COM API와 상호 운용 환경을 개선하는 몇 가지 기능이 포함되어 있습니다. 개선 사항 중에는 `dynamic` 형식의 사용 및 [명명된 인수 및 선택적 인수](../classes-and-structs/named-and-optional-arguments.md)의 사용이 포함됩니다.

많은 COM 메서드는 형식을 `object`로 지정하여 인수 형식 및 반환 형식의 변환을 허용합니다. C#에서는 강력한 형식의 변수로 조정하기 위해 값을 명시적으로 캐스팅해야 했습니다. [/link(C# 컴파일러 옵션)](../../language-reference/compiler-options/link-compiler-option.md) 옵션을 사용하여 컴파일하는 경우 `dynamic` 형식을 사용하면 COM 서명에서 `object`의 발생을 마치 `dynamic` 형식인 것처럼 취급하여 캐스팅을 상당 부분 피할 수 있습니다. 예를 들어 다음 문은 `dynamic` 형식은 있고 `dynamic` 형식은 없는 Microsoft Office Excel 스프레드시트의 셀에 액세스하는 방법과 대조됩니다.

[!code-csharp[csOfficeWalkthrough#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csofficewalkthrough/cs/thisaddin.cs#12)]

[!code-csharp[csOfficeWalkthrough#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csofficewalkthrough/cs/thisaddin.cs#13)]

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[dynamic](../../language-reference/keywords/dynamic.md)|`dynamic` 키워드의 사용법을 설명합니다.|
|[동적 언어 런타임 개요](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)|동적 언어에 대한 서비스 집합을 CLR(공용 언어 런타임)에 추가하는 런타임 환경인 DLR 개요를 제공합니다.|
|[연습: 동적 개체 만들기 및 사용](walkthrough-creating-and-using-dynamic-objects.md)|사용자 지정 동적 개체를 만들고 `IronPython` 라이브러리에 액세스하는 프로젝트를 만드는 데 필요한 단계별 지침을 제공합니다.|
|[방법: Visual C# 기능을 사용하여 Office Interop 개체에 액세스](../interop/how-to-access-office-onterop-objects.md)|명명된 인수와 선택적 인수, `dynamic` 형식, Office API 개체에 대한 액세스를 간소화하는 기타 향상된 기능을 사용하는 프로젝트를 만드는 방법을 보여 줍니다.|
