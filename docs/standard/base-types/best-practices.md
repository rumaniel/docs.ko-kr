---
title: .NET의 정규식에 대한 모범 사례
description: .NET에서 효율적이고 효과적인 정규식을 만드는 방법을 알아봅니다.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework regular expressions, best practices
- regular expressions, best practices
ms.assetid: 618e5afb-3a97-440d-831a-70e4c526a51c
author: rpetrusha
ms.author: ronpet
ms.custom: serodec18
ms.openlocfilehash: a945c53f3206f29cf2b07fea86ba3e8e3af11645
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254219"
---
# <a name="best-practices-for-regular-expressions-in-net"></a>.NET의 정규식에 대한 모범 사례
<a name="top"></a>.NET의 정규식 엔진은 리터럴 텍스트에 대한 비교 및 검색 대신 패턴 일치를 기반으로 텍스트를 처리하는 완벽한 기능을 갖춘 강력한 도구입니다. 대부분의 경우 신속하고 효율적인 방식으로 패턴 일치가 수행됩니다. 하지만 일부 경우에는 정규식 엔진의 실행 속도가 매우 느리게 보일 수 있습니다. 심한 경우에는 입력 크기가 비교적 적은데도 처리하는 데 시간이 몇 시간 또는 며칠씩 걸려서 응답이 멎은 것처럼 보일 수도 있습니다.  
  
 이 항목에서는 개발자가 자신의 정규식 성능을 최적화하기 위해 채택할 수 있는 몇 가지 모범 사례에 대해 설명합니다. 여기에는 다음 단원이 포함되어 있습니다.  
  
- [입력 소스에 대한 고려](#InputSource)  
  
- [적절한 개체 인스턴스화 처리](#ObjectInstantiation)  
  
- [역추적 수행](#Backtracking)  
  
- [시간 제한 값 사용](#Timeouts)  
  
- [캡처는 필요한 경우에만](#Capture)  
  
- [관련 항목](#RelatedTopics)  
  
<a name="InputSource"></a>   
## <a name="consider-the-input-source"></a>입력 소스에 대한 고려  
 일반적으로 정규식은 제한되었거나 제한되지 않은 두 가지 유형의 입력을 받아들일 수 있습니다. 제한된 입력은 알려졌거나 신뢰할 수 있는 소스에서 만들어진 텍스트이며 미리 정의된 서식을 따릅니다. 제한되지 않은 입력은 웹 사용자와 같은 신뢰할 수 없는 소스에서 만들어진 텍스트이며 미리 정의되었거나 예상되는 서식을 따르지 않습니다.  
  
 일반적으로 정규식 패턴은 유효한 입력과 일치하도록 작성됩니다. 즉, 개발자는 일치시키려는 텍스트를 검사하고 이와 일치하는 정규식 패턴을 작성합니다. 그런 다음 개발자는 이 패턴을 여러 가지 유효한 입력 항목으로 테스트하여 패턴 수정이나 추가 작업이 필요한지 여부를 결정합니다. 패턴이 가정된 모든 유효한 입력과 일치하면 패턴을 프로덕션에 사용 가능한 것으로 선언하고 출시 애플리케이션에 포함할 수 있습니다. 이렇게 하면 제한된 입력과 일치하는지 검색하기 위해 사용하는 데 적합한 정규식 패턴을 만들 수 있습니다. 하지만 이러한 패턴은 제한되지 않은 입력과 일치하는지 검색하는 데에는 적합하지 않습니다.  
  
 제한되지 않은 입력과 일치하는지 확인하려면 정규식이 다음과 같은 세 가지 종류의 텍스트를 효율적으로 처리할 수 있어야 합니다.  
  
- 정규식 패턴과 일치하는 텍스트  
  
- 정규식 패턴과 일치하지 않는 텍스트  
  
- 정규식 패턴과 거의 일치하는 텍스트  
  
 마지막 텍스트 형식은 특히 제한된 입력을 처리하도록 작성된 정규식에서 문제가 될 수 있습니다. 또한 이러한 정규식에 [역추적](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)이 광범위하게 사용되는 경우에는 정규식 엔진이 겉보기에는 문제가 없는 텍스트를 처리하느라 비정상적으로 많은 시간(몇 시간 또는 며칠이 걸리는 경우도 있음)을 소비할 수 있습니다.  
  
> [!WARNING]
> 다음 예제에서는 과도한 역추적을 발생시키고 유효한 전자 메일 주소를 거부할 가능성이 있는 정규식을 사용합니다. 전자 메일 유효성 검사 루틴에서 해당 정규식을 사용해서는 안 됩니다. 이메일 주소의 유효성을 검사하는 정규식은 [방법: 문자열이 올바른 이메일 형식인지 확인](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md)을 참조하세요.  
  
 예를 들어 전자 메일 주소 별칭의 유효성을 검증하기 위해 매우 자주 사용되지만 심각한 문제를 일으킬 수 있는 정규식을 하나 보여드리겠습니다. 정규식 `^[0-9A-Z]([-.\w]*[0-9A-Z])*$`는 한 개의 영숫자로 시작하고 이어지는 영숫자, 마침표 또는 하이픈이 0개 이상으로 구성된 텍스트를 유효한 메일 주소로 처리하도록 작성되었습니다. 정규식은 영숫자로 끝나야 합니다. 하지만 다음 예제에서와 같이 이 정규식은 유효한 입력을 쉽게 처리할 수 있지만 거의 유효한 입력을 처리할 때는 성능이 매우 비효율적입니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/design2.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/design2.vb#1)]  
  
 이 예제의 결과에서와 같이 정규식 엔진은 유효한 전자 메일 별칭의 경우 길이에 관계없이 거의 동일한 기간에 처리를 수행합니다. 반면에 문자 수가 5개 더 많은 거의 유효한 전자 메일 주소의 경우 문자열에 포함된 각 추가 문자마다 처리 시간이 약 두 배로 늘어납니다. 즉, 25개 문자로 구성된 거의 유효한 문자열을 처리하려면 한 시간 이상이 소요되고 거의 유효한 문자열의 문자 수가 33자인 경우 처리하는 데 거의 하루가 걸립니다.  
  
 이 정규식은 패턴과 일치하는 입력의 형식만 고려하여 개발되었기 때문에 패턴과 일치하지 않는 입력은 고려하지 못합니다. 따라서 정규식 패턴과 거의 일치하는 제한되지 않은 입력의 경우 성능이 크게 저하될 수 있습니다.  
  
 이 문제를 해결하기 위해서는 다음과 같이 할 수 있습니다.  
  
- 패턴을 개발할 때, 특히 정규식이 제한되지 않은 입력을 처리하도록 디자인된 경우 역추적이 정규식 엔진의 성능에 어떤 영향을 줄 수 있는지 확인해야 합니다. 자세한 내용은 [효율적인 역추적 사용](#Backtracking) 섹션을 참조하세요.  
  
- 유효한 입력뿐만 아니라 유효하지 않은 입력과 거의 유효한 입력을 사용하여 정규식을 철저히 테스트해야 합니다. 특정 정규식에 대한 입력을 무작위로 생성하려면 Microsoft Research에서 제공되는 정규식 탐색 도구인 [Rex](https://www.microsoft.com/en-us/research/project/rex-regular-expression-exploration/)를 사용할 수 있습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="ObjectInstantiation"></a>   
## <a name="handle-object-instantiation-appropriately"></a>적절한 개체 인스턴스화 처리  
 .NET의 정규식 개체 모델의 핵심은 정규식 엔진을 나타내는 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 클래스입니다. 정규식 성능에 영향을 주는 가장 중요한 단일 요소는 종종 <xref:System.Text.RegularExpressions.Regex> 엔진의 사용 방식입니다. 정규식을 정의할 때는 정규식 엔진과 정규식 패턴을 긴밀히 연결하는 작업이 포함됩니다. 해당 생성자에 정규식 패턴을 전달하여 <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화하거나 분석할 문자열과 함께 정규식 패턴을 전달하여 정적 메서드를 호출하든 간에 이러한 연결 프로세스는 필수적으로 비용이 클 수 밖에 없습니다.  
  
> [!NOTE]
> 해석된 정규식과 컴파일된 정규식을 사용할 때 성능에 미치는 영향을 자세히 알아보려면 BCL 팀 블로그의 [Optimizing Regular Expression Performance, Part II: Taking Charge of Backtracking(정규식 성능 최적화, II부:  효율적인 역추적 사용](https://blogs.msdn.microsoft.com/bclteam/2010/08/03/optimizing-regular-expression-performance-part-ii-taking-charge-of-backtracking-ron-petrusha/)을 참조하세요.  
  
 정규식 엔진을 특정 정규식 패턴과 연결하고 엔진을 사용하여 여러 가지 방법으로 일치하는 텍스트를 검색할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType>와 같은 정적 패턴 일치 메서드를 호출할 수 있습니다. 이 방법에서는 정규식 개체를 인스턴스화할 필요가 없습니다.  
  
- <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화하고 해석된 정규식의 인스턴스 패턴 일치 메서드를 호출할 수 있습니다. 이 메서드는 정규식 엔진을 정규식 패턴에 바인딩하는 기본 메서드입니다. 이 메서드는 <xref:System.Text.RegularExpressions.Regex> 플래그를 포함하는 `options` 인수 없이 <xref:System.Text.RegularExpressions.RegexOptions.Compiled> 개체가 인스턴스화될 때 발생합니다.  
  
- <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화하고 컴파일된 정규식의 인스턴스 패턴 일치 메서드를 호출할 수 있습니다. 정규식 개체는 <xref:System.Text.RegularExpressions.Regex> 플래그를 포함하는 `options` 인수를 사용하여 <xref:System.Text.RegularExpressions.RegexOptions.Compiled> 개체가 인스턴스화될 때 컴파일된 패턴을 제공합니다.  
  
- 특정 정규식과 밀접하게 연결된 특수 용도의 <xref:System.Text.RegularExpressions.Regex> 개체를 만들고, 컴파일하고, 독립 실행형 어셈블리에 저장할 수 있습니다. 이 작업은 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> 메서드를 호출하여 수행합니다.  
  
 정규식 일치 메서드를 호출하는 특정 방법마다 애플리케이션에 중대한 영향을 줄 수 있습니다. 다음 단원에서는 애플리케이션의 성능 향상을 위해 정적 메서드 호출, 해석된 정규식 및 컴파일된 정규식을 사용해야 하는 경우에 대해 설명합니다.  
  
> [!IMPORTANT]
> 동일한 정규식을 메서드 호출에 반복해서 사용하거나 애플리케이션에 정규식 개체가 광범위하게 사용될 경우 메서드 호출의 형태(정적, 해석, 컴파일)는 성능에 영향을 줍니다.  
  
### <a name="static-regular-expressions"></a>정적 정규식  
 정적 정규식 메서드는 동일한 정규식으로 정규식 개체를 반복해서 인스턴스화하기 위한 대안으로 권장됩니다. 정규식 개체에 사용되는 정규식 패턴과 달리 정적 메서드 호출에 사용된 패턴으로부터 컴파일된 MSIL(Microsoft Intermediate Language)이나 작업 코드는 정규식 엔진에서 내부적으로 캐시됩니다.  
  
 예를 들어 사용자 입력의 유효성을 검사하기 위해 다른 메서드를 자주 호출하는 이벤트 처리기가 있을 수 있습니다. 다음 코드에서 사용자가 적어도 한 자릿수의 숫자와 함께 통화 기호를 입력했는지 확인하는 <xref:System.Windows.Forms.Button>라는 이름의 메서드를 호출하기 위해 사용되는 <xref:System.Windows.Forms.Control.Click> 컨트롤의 `IsValidCurrency` 이벤트는 이러한 경우를 보여 줍니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/static1.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/static1.vb#2)]  
  
 다음 예제에서는 `IsValidCurrency` 메서드를 구현할 때 매우 비효율적인 형태를 보여 줍니다. 여기에서는 메서드를 호출할 때마다 <xref:System.Text.RegularExpressions.Regex> 개체를 동일한 패턴으로 다시 인스턴스화합니다. 결국 메서드를 호출할 때마다 정규식 패턴을 다시 컴파일해야 합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/static1.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/static1.vb#3)]  
  
 이러한 비효율적인 코드는 정적 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=nameWithType> 메서드에 대한 호출로 바꿔야 합니다. 그러면 패턴 일치 메서드를 호출해야 할 때마다 <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화할 필요가 없고, 정규식 엔진이 캐시에서 컴파일된 정규식을 가져와서 사용할 수 있습니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/static2.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/static2.vb#4)]  
  
 기본적으로 가장 최근에 사용된 15개의 정적 정규식 패턴이 캐시됩니다. 캐시된 정적 정규식이 대량으로 필요한 애플리케이션의 경우 <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=nameWithType> 속성을 설정하여 캐시 크기를 조정할 수 있습니다.  
  
 이 예제에서 사용된 정규식 `\p{Sc}+\s*\d+`는 입력 문자열에 통화 기호와 한 자릿수 이상의 숫자가 포함되었는지를 확인합니다. 패턴은 다음 표와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\p{Sc}+`|유니코드 기호와 통화 범주에 속하는 하나 이상의 문자가 일치하는지 확인합니다.|  
|`\s*`|0개 이상의 공백 문자가 일치하는지 확인합니다.|  
|`\d+`|하나 이상의 10진수 숫자가 일치하는지 확인합니다.|  
  
<a name="Interpreted"></a>   
### <a name="interpreted-vs-compiled-regular-expressions"></a>해석된 정규식 및 컴파일된 정규식  
 <xref:System.Text.RegularExpressions.RegexOptions.Compiled> 옵션의 사양을 통해 정규식 엔진에 바인딩되지 않은 정규식 패턴은 해석된 정규식입니다. 정규식 개체가 인스턴스화되면 정규식 엔진이 정규식을 작업 코드 집합으로 변환합니다. 인스턴스 메서드가 호출되면 이 작업 코드가 MSIL로 변환되고 JIT 컴파일러에서 실행됩니다. 마찬가지로 정적 정규식 메서드를 호출할 때 정규식을 캐시에서 찾을 수 없으면 정규식 엔진이 정규식을 작업 코드 집합으로 변환하고 이를 캐시에 저장합니다. 그런 다음 이러한 작업 코드를 JIT 컴파일러가 실행할 수 있도록 MSIL로 변환합니다. 해석된 정규식은 실행 시간을 늘리는 대신 시작 시간을 줄여 줍니다. 따라서 해석된 정규식은 소규모 메서드 호출에서 정규식을 사용하거나 정규식 메서드에 대한 정확한 호출 수를 알 수 없지만 그래도 그 수가 적을 것으로 예상되는 경우에 사용하는 것이 가장 좋습니다. 메서드 호출 수가 늘어나면 느려진 실행 속도로 인해 줄어든 시작 시간의 성능 이점이 감소합니다.  
  
 <xref:System.Text.RegularExpressions.RegexOptions.Compiled> 옵션의 사양을 통해 정규식 엔진에 바인딩된 정규식 패턴은 컴파일된 정규식입니다. 즉, 정규식 개체가 인스턴스화되거나 정적 정규식 메서드가 호출될 때 캐시에서 정규식을 찾을 수 없으면 정규식 엔진이 정규식을 중간 상태의 작업 코드 집합으로 변환하고 그런 다음 MSIL로 변환합니다. 메서드를 호출하면 JIT가 이 MSIL을 실행합니다. 해석된 정규식과는 달리 컴파일된 정규식은 시작 시간이 늘어나지만 개별 패턴 일치 메서드의 실행 속도가 빨라집니다. 따라서 정규식을 컴파일하여 얻을 수 있는 성능 이점은 정규식 메서드가 호출되는 횟수에 비례하여 증가합니다.  
  
 요약하면, 특정 정규식에 대한 정규식 메서드 호출이 비교적 적게 수행될 경우 해석된 정규식을 사용하는 것이 좋으며, 특정 정규식에 대한 정규식 메서드 호출이 비교적 자주 수행될 경우 컴파일된 정규식을 사용해야 합니다. 해석된 정규식의 실행 속도 감소가 줄어든 시작 시간으로 인해 얻게 된 이점보다 더 커지거나, 컴파일된 정규식의 느려진 시작 시간이 빨라진 실행 속도의 이점보다 더 커지게 되는 정확한 임계점은 쉽게 결정할 수 없는 사항입니다. 이러한 임계점은 정규식의 복잡성과 정규식으로 처리되는 특정 데이터를 비롯한 다양한 요소들에 따라 달라집니다. 특정 애플리케이션 시나리오에서 해석된 정규식과 컴파일된 정규식 중 어느 쪽의 성능이 더 좋은지 확인하기 위해 <xref:System.Diagnostics.Stopwatch> 클래스를 사용하여 각각의 실행 시간을 비교해 볼 수 있습니다.  
  
 다음 예제에서는 Theodore Dreiser가 저술한 *The Financier* 책에서 처음 10개의 문장을 읽을 때와 모든 문장을 읽을 때 컴파일된 정규식과 해석된 정규식의 성능 차이를 비교해서 보여줍니다. 아래 예제의 결과에서와 같이 정규식 일치 메서드를 10번만 호출할 경우에는 해석된 정규식이 컴파일된 정규식보다 나은 성능을 제공합니다. 하지만 호출 횟수가 많은 경우에는(아래 예에서는 13,000번 이상) 컴파일된 정규식이 더 나은 성능을 제공합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/compare1.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/compare1.vb#5)]  
  
 이 예제에 사용된 정규식 패턴 `\b(\w+((\r?\n)|,?\s))*\w+[.?:;!]`는 다음 표와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`\w+`|하나 이상의 단어 문자를 찾습니다.|  
|<code>(\r?\n)&#124;,?\s)</code>|0개 이상의 캐리지 리턴과 이어지는 줄 바꿈 문자 또는 0개 이상의 쉼표와 이어지는 공백 문자가 일치하는지 확인합니다.|  
|<code>(\w+((\r?\n)&#124;,?\s))*</code>|0개 이상의 캐리지 리턴과 줄 바꿈 문자 또는 0개 이상의 쉼표와 공백 문자로 이어지는 한 글자 이상의 단어가 적어도 한 번 이상 일치하는지 확인합니다.|  
|`\w+`|하나 이상의 단어 문자를 찾습니다.|  
|`[.?:;!]`|마침표, 물음표, 콜론, 세미콜론 또는 느낌표가 일치하는지 확인합니다.|  
  
### <a name="regular-expressions-compiled-to-an-assembly"></a>정규식: 어셈블리로 컴파일  
 .NET에서는 또한 컴파일된 정규식이 포함된 어셈블리를 만들 수 있습니다. 따라서 정규식 컴파일로 인한 성능 문제를 런타임에서 디자인 타임으로 이동할 수 있습니다. 그러나 몇 가지 추가적인 작업도 있습니다. 정규식을 미리 정의하고 이를 어셈블리로 컴파일해야 합니다. 그런 다음 컴파일러는 어셈블리의 정규식을 사용하는 소스 코드를 컴파일할 때 이 어셈블리를 참조할 수 있습니다. 어셈블리로 컴파일되는 각 정규식은 <xref:System.Text.RegularExpressions.Regex>에서 파생되는 클래스로 표현됩니다.  
  
 정규식을 어셈블리로 컴파일하려면 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%28System.Text.RegularExpressions.RegexCompilationInfo%5B%5D%2CSystem.Reflection.AssemblyName%29?displayProperty=nameWithType> 메서드를 호출하고 컴파일할 정규식을 나타내는 <xref:System.Text.RegularExpressions.RegexCompilationInfo> 개체 배열과 만들려는 어셈블리에 대한 정보가 포함된 <xref:System.Reflection.AssemblyName> 개체에 메서드 호출을 전달합니다.  
  
 다음과 같은 경우에는 정규식을 어셈블리로 컴파일하는 것이 좋습니다.  
  
- 재사용 가능한 정규식 라이브러리를 만들려는 구성 요소 개발자인 경우  
  
- 정규식의 패턴 일치 메서드가 호출되는 횟수가 한 두 번인지 아니면 수천 또는 수만 번인지 알 수 없는 경우. 컴파일된 정규식이나 해석된 정규식과 달리 개별 어셈블리로 컴파일된 정규식은 메서드 호출 수에 관계없이 일관적인 성능을 제공합니다.  
  
 성능 최적화를 위해 컴파일된 정규식을 사용할 경우에는 어셈블리를 만들고, 정규식 엔진을 로드하고, 패턴 일치 메서드를 실행하기 위해 리플렉션을 사용해서는 안됩니다. 이를 위해서는 정규식 패턴을 동적으로 작성하지 않아야 하며, 어셈블리를 나들 때 모든 패턴 일치 옵션(예: 대/소문자를 구분하지 않는 패턴 일치)을 지정해야 합니다. 또한 정규식을 사용하는 코드와 어셈블리를 만드는 코드를 구분해야 합니다.  
  
 다음 예제에서는 컴파일된 정규식이 포함된 어셈블리를 만드는 방법을 보여 줍니다. 이 예제에서는 [해석된 정규식과 컴파일된 정규식 비교`RegexLib.dll` 섹션에 사용된 문장 일치 정규식 패턴을 포함하는 `SentencePattern`이라는 단일 정규식 클래스가 포함된 ](#Interpreted)이라는 어셈블리를 만듭니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/compile1.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/compile1.vb#6)]  
  
 이 예제를 실행 파일로 컴파일하고 실행하면 `RegexLib.dll`이라는 어셈블리가 만들어집니다. 정규식은 `Utilities.RegularExpressions.SentencePattern`로부터 파생되는 <xref:System.Text.RegularExpressions.Regex>이라는 클래스로 제공됩니다. 그런 후 다음 예제에서는 컴파일된 정규식을 사용하여 시어도어 드라이저(Theodore Dreiser)의 *The Financier* 본문에서 문장을 추출합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/compile2.cs#7)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/compile2.vb#7)]  
  
 [맨 위로 이동](#top)  
  
<a name="Backtracking"></a>   
## <a name="take-charge-of-backtracking"></a>효율적인 역추적 사용  
 일반적으로 정규식 엔진은 선형 진행을 통해 입력 문자열 내를 이동하면서 입력 문자열을 정규식 패턴과 비교합니다. 하지만 정규식 패턴에 `*`, `+` 및 `?`와 같은 정해지지 않은 수량자가 사용될 경우 정규식 엔진은 일부 성공한 부분 일치를 포기하고 이전에 저장된 상태로 돌아와서 전체 패턴에 대해 일치하는 항목을 찾을 수 있습니다. 이 프로세스를 역추적이라고 합니다.  
  
> [!NOTE]
> 역추적에 대한 자세한 내용은 [정규식 동작 정보](../../../docs/standard/base-types/details-of-regular-expression-behavior.md) 및 [역추적](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)을 참조하세요. 역추적에 대해 자세히 알아보려면 BCL 팀 블로그의 [Optimizing Regular Expression Performance, Part II: Taking Charge of Backtracking(정규식 성능 최적화, II부: 효율적인 역추적 사용](https://blogs.msdn.microsoft.com/bclteam/2010/08/03/optimizing-regular-expression-performance-part-ii-taking-charge-of-backtracking-ron-petrusha/)을 참조하세요.  
  
 역추적을 지원할 경우 정규식에 성능과 유연성이 제공됩니다. 또한 정규식 개발자에게 정규식 엔진의 작동에 대한 제어 책임을 맡길 수 있습니다. 개발자가 이러한 책임을 인식하지 못하는 경우가 많기 때문에 역추적을 오용하거나 과도하게 사용하여 정규식 성능이 저하되는 경우가 자주 발생합니다. 최악의 시나리오에서는 실행 시간이 입력 문자열에 있는 추가 문자마다 두 배씩 늘어날 수 있습니다. 실제로 역추적을 과도하게 사용할 경우에는 입력이 정규식 패턴과 거의 일치할 경우 프로그래밍 면에서 무한 루프를 만드는 것과 동일한 결과를 가져올 수 있으며 정규식 엔진이 비교적 간단한 입력 문자열이라도 처리하는 데 몇 시간 또는 심지어 며칠이 걸릴 수도 있습니다.  
  
 역추적이 일치하는 문자열 검색에 반드시 필요하지 않더라도 애플리케이션에서 역추적을 사용하기 위해 성능상의 이점을 포기하는 경우가 많습니다. 예를 들어 `\b\p{Lu}\w*\b`는 다음 표와 같이 대문자로 시작하는 모든 단어를 찾습니다.  
  
|무늬|설명|  
|-|-|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`\p{Lu}`|대문자를 찾습니다.|  
|`\w*`|0개 이상의 단어 문자를 찾습니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 단어 경계는 단어 문자 또는 단어 문자의 일부와 동일하지 않으므로 정규식 엔진이 단어 문자를 찾을 때 단어 경계를 벗어날 가능성은 없습니다. 즉, 이 정규식의 경우 역추적은 전반적인 문자열 검색 성능에 전혀 기여할 수 없으며, 정규식 엔진이 각각의 단어 문자에 대해 성공한 예비 검색에 대한 상태를 강제로 저장해야 하기 때문에 성능 저하만 유발할 수 있습니다.  
  
 역추적이 필요하지 않다고 판단될 경우에는 `(?>subexpression)` 언어 요소를 사용하여 역추적을 비활성화할 수 있습니다. 다음 예제에서는 두 개의 정규식을 사용하여 입력 문자열의 구문을 분석합니다. 첫 번째 정규식인 `\b\p{Lu}\w*\b`에는 역추적이 사용되고, 두 번째 정규식인 `\b\p{Lu}(?>\w*)\b`에는 역추적이 사용되지 않습니다. 아래 예제의 결과에서와 같이 두 정규식 모두 동일한 결과를 가져옵니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/backtrack2.cs#10)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/backtrack2.vb#10)]  
  
 많은 경우에 정규식 패턴을 입력 텍스트에 일치시키기 위해서는 역추적이 필요합니다. 그러나 과도한 역추적은 심각한 성능 저하를 가져오고 애플리케이션이 응답을 멈춘 것과 같은 인상을 줄 수 있습니다. 특히 수량자가 중첩되어 있고 외부 하위 식과 일치하는 텍스트가 내부 하위 식과 일치하는 텍스트의 하위 집합인 경우 문제가 더 심각해질 수 있습니다.  
  
> [!WARNING]
> 과도한 역추적을 방지하는 것 외에도 과도한 역추적이 정규식 성능을 심각하게 저하시키지 않도록 시간 제한 기능을 사용해야 합니다. 자세한 내용은 [시간 제한 값 사용](#Timeouts) 섹션을 참조하세요.  
  
 예를 들어 정규식 패턴 `^[0-9A-Z]([-.\w]*[0-9A-Z])*\$$`는 영숫자 문자가 한 개 이상 포함된 부품 번호를 확인하기 위한 패턴입니다. 마지막 문자는 영숫자여야 하지만 영숫자 문자, 하이픈, 밑줄 또는 마침표가 추가될 수 있습니다. 달러 기호는 부품 번호의 종료 문자입니다. 수량자가 중첩되어 있고 하위 식 `[0-9A-Z]`가 하위 식 `[-.\w]*`의 하위 집합이기 때문에 일부 경우에는 이 정규식 패턴으로 인해 성능이 극히 저하될 수 있습니다.  
  
 이러한 경우 중첩된 수량자를 제거하고 외부 하위 식을 길이가 0인 lookahead 또는 lookbehind 어설션으로 바꿔서 정규식 성능을 최적화할 수 있습니다. Lookahead 및 lookbehind 어설션은 앵커이므로 입력 문자열에서 포인터를 이동하지는 않지만 대신 이전 또는 이후 부분을 조회하여 지정된 조건이 충족되는지 확인합니다. 예를 들어 부품 번호 정규식은 `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])\$$`로 다시 작성할 수 있습니다. 이 정규식 패턴은 다음 표에서와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|입력 문자열의 시작 부분에서 일치 항목 찾기를 시작합니다.|  
|`[0-9A-Z]`|일치하는 영숫자 문자를 찾습니다. 부품 번호는 적어도 이 문자 이상으로 구성되어야 합니다.|  
|`[-.\w]*`|단어 문자, 하이픈 또는 마침표로 구성된 0개 이상의 일치 항목을 찾습니다.|  
|`\$`|달러 기호를 찾습니다.|  
|`(?<=[0-9A-Z])`|종료 문자인 달러 기호의 앞 부분을 조회하여 이전 문자가 영숫자인지 확인합니다.|  
|`$`|입력 문자열의 끝 부분에서 검색을 종료합니다.|  
  
 다음 예제에서는 이 정규식을 사용하여 부품 번호가 포함될 수 있는 배열을 찾는 방법을 보여 줍니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/backtrack4.cs#11)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/backtrack4.vb#11)]  
  
 .NET의 정규식 언어에는 중첩된 수량자를 제거하는 데 사용할 수 있는 다음과 같은 언어 요소가 포함되어 있습니다. 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
|언어 요소|설명|  
|----------------------|-----------------|  
|`(?=` `subexpression` `)`|너비가 0인 긍정 lookahead입니다. `subexpression`이 입력 문자열과 일치하는지 확인하기 위해 현재 위치의 앞부분을 확인합니다.|  
|`(?!` `subexpression` `)`|너비가 0인 부정 lookahead입니다. `subexpression`이 입력 문자열과 일치하지 않는지 확인하기 위해 현재 위치의 앞부분을 확인합니다.|  
|`(?<=` `subexpression` `)`|너비가 0인 긍정 lookbehind입니다. `subexpression`이 입력 문자열과 일치하는지 확인하기 위해 현재 위치의 뒷부분을 확인합니다.|  
|`(?<!` `subexpression` `)`|너비가 0인 부정 lookbehind입니다. `subexpression`이 입력 문자열과 일치하지 않는지 확인하기 위해 현재 위치의 뒷부분을 확인합니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="Timeouts"></a>   
## <a name="use-time-out-values"></a>시간 제한 값 사용  
 정규식이 정규식 패턴과 거의 일치하는 입력을 처리할 경우 정규식 성능에 크게 영향을 주는 과도한 역추적이 사용되는 경우로 볼 수 있습니다. 거의 일치하는 입력에 대해 정규식 역추적 및 테스트 사용을 신중하게 고려하는 것은 물론 과도한 역추적으로 발생할 영향을 최소화하려면 항상 시간 제한 값을 설정해야 합니다.  
  
 정규식 시간 제한 간격은 정규식 엔진이 시간 초과되기 전에 하나의 일치 항목을 찾는 기간을 정의합니다. 기본 시간 제한 간격은 정규식이 시간 초과되지 않아야 하는 <xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout?displayProperty=nameWithType>입니다. 다음과 같이 이 값을 재정의하고 시간 제한 간격을 정의할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.Regex> 생성자를 호출하여 <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=nameWithType> 개체를 인스턴스화할 때 시간 제한 값을 제공합니다.  
  
- <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=nameWithType> 또는 <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=nameWithType>와 같은 정적 패턴 일치 메서드를 호출하여 `matchTimeout` 매개 변수를 포함할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> 메서드를 호출하여 만들어진 컴파일된 정규식에 대해 <xref:System.TimeSpan> 형식의 매개 변수가 있는 생성자를 호출합니다.  
  
 시간 제한 간격을 정의하고 그 간격의 끝에서 일치 항목을 찾을 수 없는 경우 정규식 메서드에서 <xref:System.Text.RegularExpressions.RegexMatchTimeoutException> 예외를 throw합니다. 예외 처리기에서 더 긴 시간 제한 간격으로 일치를 다시 시도하거나, 일치 시도를 중단하고 일치 항목이 없다고 가정하거나, 일치 시도를 중단하고 나중에 분석하기 위해 예외 정보를 로그에 기록할지를 선택할 수 있습니다.  
  
 다음 예제에서는 텍스트 문서의 단어 수 및 단어의 문자 평균 수를 계산하기 위해 350밀리초의 시간 제한 간격으로 정규식을 인스턴스화하는 `GetWordData` 메서드를 정의합니다. 작업 시간 제한이 일치할 경우 시간 제한 간격은 350밀리초로 증가되며 <xref:System.Text.RegularExpressions.Regex> 개체를 다시 인스턴스화합니다. 새 시간 제한 간격이 1초 초과할 경우 메서드는 호출자에게 예외를 다시 throw합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/timeout1.cs#12)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/timeout1.vb#12)]  
  
 [맨 위로 이동](#top)  
  
<a name="Capture"></a>   
## <a name="capture-only-when-necessary"></a>캡처는 필요한 경우에만  
 .NET의 정규식은 정규식 패턴을 하나 이상의 하위 식으로 그룹화할 수 있게 해주는 다양한 그룹화 구문을 지원합니다. .NET 정규식 언어에서 가장 일반적으로 사용되는 그룹화 구문은 번호가 매겨진 캡처 그룹을 정의하는 `(`*subexpression*`)`과 명명된 캡처 그룹을 정의하는 `(?<`*name*`>`*subexpression*`)`입니다. 그룹화 구문은 역참조를 만들고 수량자가 적용되는 하위 식을 정의하는 데 필요합니다.  
  
 하지만 이러한 언어 요소를 사용하려면 비용이 듭니다. 이 언어 요소를 사용할 경우 <xref:System.Text.RegularExpressions.GroupCollection> 속성으로 반환된 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 개체에 최근의 명명되지 않은 캡처 또는 명명된 캡처가 채워집니다. 또는 단일 그룹화 구문으로 입력 문자열에서 여러 부분 문자열이 캡처된 경우 특정 캡처링 그룹의 <xref:System.Text.RegularExpressions.CaptureCollection> 속성으로 반환된 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 개체에 여러 <xref:System.Text.RegularExpressions.Capture> 개체가 채워집니다.  
  
 그룹화 구문은 종종 수량자를 정규식에 적용할 수 있도록 정규식에서만 사용되며, 이러한 하위 식으로 캡처된 그룹은 이후에 사용되지 않습니다. 예를 들어 정규식 `\b(\w+[;,]?\s?)+[.?!]`는 전체 문장을 캡처하도록 디자인되었습니다. 다음 표에서는 이 정규식에 포함된 언어 요소와 <xref:System.Text.RegularExpressions.Match> 개체의 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 및 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 컬렉션에 미치는 영향에 대해 설명합니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`\w+`|하나 이상의 단어 문자를 찾습니다.|  
|`[;,]?`|0개 또는 한 개의 쉼표 또는 세미콜론을 찾습니다.|  
|`\s?`|0번 이상 나오는 공백 문자를 찾습니다.|  
|`(\w+[;,]?\s?)+`|쉼표 또는 세미콜론과 공백 문자가 이어질 수 있는 하나 이상의 단어 문자와 한 번 이상 일치하는 문자를 찾습니다. 이 언어 요소는 정규식 엔진이 문장의 끝에 도달할 때까지 선택적인 구두점 기호로 이어지는 여러 단어 문자의 조합(즉, 단어)이 반복될 수 있도록 하는 데 필수적인 첫 번째 캡처링 그룹을 정의합니다.|  
|`[.?!]`|마침표, 물음표 또는 느낌표를 찾습니다.|  
  
 다음 예제에서와 같이 일치 항목을 찾으면 <xref:System.Text.RegularExpressions.GroupCollection> 및 <xref:System.Text.RegularExpressions.CaptureCollection> 개체에 일치 항목으로부터 캡처한 항목이 채워집니다. 이 경우 캡처 그룹 `(\w+[;,]?\s?)`가 있으므로 `+` 수량자를 적용하여 정규식 패턴이 문장의 각 단어와 일치하도록 할 수 있습니다. 그렇지 않으면 문장에서 일치하는 마지막 단어를 찾습니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/group1.cs#8)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/group1.vb#8)]  
  
 수량자를 언어 요소에 적용하기 위해서만 하위 식을 사용하고 캡처한 텍스트에는 관심이 없을 경우 그룹 캡처를 비활성화해야 합니다. 예를 들어 `(?:subexpression)` 언어 요소는 적용할 대상 그룹이 일치하는 부분 문자열을 캡처하지 못하도록 방지합니다. 다음 예제에서 이전 예의 정규식 패턴은 `\b(?:\w+[;,]?\s?)+[.?!]`로 변경되었습니다. 결과에서와 같이 정규식 엔진이 <xref:System.Text.RegularExpressions.GroupCollection> 및 <xref:System.Text.RegularExpressions.CaptureCollection> 컬렉션을 채우지 못하도록 방지합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/group2.cs#9)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/group2.vb#9)]  
  
 다음 방법 중 하나로 캡처를 비활성화할 수 있습니다.  
  
- `(?:subexpression)` 언어 요소를 사용합니다. 이 요소는 적용된 그룹에서 일치하는 부분 문자열을 캡처하지 않도록 방지합니다. 중첩된 그룹에서 부분 문자열의 캡처는 비활성화하지 않습니다.  
  
- <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture> 옵션을 사용합니다. 이 옵션은 정규식 패턴에서 모든 명명되지 않은 캡처 또는 암시적인 캡처를 비활성화합니다. 이 옵션을 사용하면 `(?<name>subexpression)` 언어 요소로 정의된 명명된 그룹과 일치하는 부분 문자열만 캡처할 수 있습니다. <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture> 플래그는 `options` 클래스 생성자의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 전달하거나 `options` 정적 일치 메서드의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 전달할 수 있습니다.  
  
- `n` 언어 요소에서 `(?imnsx)` 옵션을 사용합니다. 이 옵션은 정규식 패턴에서 요소가 나타나는 지점으로부터 모든 명명되지 않은 캡처 또는 암시적인 캡처를 비활성화합니다. 캡처는 패턴의 끝에 도달하거나 `(-n)` 옵션으로 명명되지 않은 캡처 또는 암시적인 캡처가 활성화될 때가지 비활성화됩니다. 자세한 내용은 [기타 구문](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md)을 참조하세요.  
  
- `n` 언어 요소에서 `(?imnsx:subexpression)` 옵션을 사용합니다. 이 옵션은 `subexpression`에서 모든 명명되지 않은 캡처 또는 암시적인 캡처를 비활성화합니다. 명명되지 않은 또는 암시적인 중첩된 캡처링 그룹에 의한 캡처도 함께 비활성화됩니다.  
  
 [맨 위로 이동](#top)  
  
<a name="RelatedTopics"></a>   
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[정규식 동작 정보](../../../docs/standard/base-types/details-of-regular-expression-behavior.md)|.NET의 정규식 엔진 구현에 대해 자세히 다룹니다. 이 항목에서는 정규식의 유연성에 중점을 두고 정규식 엔진의 효율성과 성능에 대한 개발자의 책임에 대해 설명합니다.|  
|[역추적](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)|역추적의 정의 및 역추적이 정규식 성능에 미치는 영향에 대해 설명하고 역추적 대신 사용할 수 있는 언어 요소에 대해 설명합니다.|  
|[정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)|.NET의 정규식 언어 요소에 대해 설명하고 각 언어 요소에 대한 자세한 설명서 링크를 제공합니다.|
