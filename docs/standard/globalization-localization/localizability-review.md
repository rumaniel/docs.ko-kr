---
title: 지역화 가능성 검토
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- world-ready applications, localizability
- application development [.NET Framework], localization
- localizability [.NET Framework]
- international applications [.NET Framework], localizability
- globalization [.NET Framework], localizability
- culture, localizability
- localization [.NET Framework], localizability
- global applications, localizability
- localizing resources
ms.assetid: 3aee2fbb-de47-4e37-8fe4-ddebb9719247
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b19bc78f44781923df6873ccc9720f4605731976
ms.sourcegitcommit: 2eb5ca4956231c1a0efd34b6a9cab6153a5438af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49086507"
---
# <a name="localizability-review"></a>지역화 가능성 검토
지역화 가능성 검토는 지역화 대비 응용 프로그램 개발의 중간 단계로, 전역화된 응용 프로그램이 지역화될 준비가 되어 있는지 점검하고 특별한 처리가 필요한 사용자 인터페이스의 모든 코드 또는 측면을 확인합니다. 또한 이 단계를 통해 지역화 과정 후에도 응용 프로그램에 기능적 결함이 발생되지 않도록 합니다. 지역화 가능성 검토에서 제기된 모든 문제가 해결되면 응용 프로그램은 지역화될 준비가 됩니다. 지역화 가능성 검토가 철저할 경우 지역화 과정 중에 소스 코드를 수정할 필요가 없습니다.  
  
 지역화 가능성 검토는 다음 세 가지 검사로 이루어져 있습니다.  
  
-   [전역화 권장 사항이 구현되었습니까?](#global)  
  
-   [문화권 구분 기능이 올바르게 처리되었습니까?](#culture)  
  
-   [국가별 데이터를 사용하여 응용 프로그램을 테스트했습니까?](#test)  
  
<a name="global"></a>   
## <a name="implementing-globalization-recommendations"></a>전역화 권장 사항 구현  
 지역화를 염두에 두고 응용 프로그램을 설계 및 개발했고 [세계화](../../../docs/standard/globalization-localization/globalization.md) 문서에 설명된 권장 사항을 따른 경우 지역화 가능성 검토는 대개 품질 보증 단계에서 통과하게 됩니다. 그러지 않은 경우 이 단계 중에 [세계화](../../../docs/standard/globalization-localization/globalization.md)를 위한 권장 사항을 검토 및 구현하고 지역화를 방해하는 소스 코드의 오류를 수정해야 합니다.  
  
<a name="culture"></a>   
## <a name="handling-culture-sensitive-features"></a>문화권 구분 기능 처리  
 .NET Framework는 문화권마다 크게 다른 다양한 영역에서 프로그래밍 방식 지원을 제공하지 않습니다. 대부분의 경우 사용자 지정 코드를 작성하여 다음과 같은 기능 영역을 처리해야 합니다.  
  
-   주소.  
  
-   전화 번호.  
  
-   용지 크기.  
  
-   길이, 무게, 영역, 볼륨 및 온도에 사용되는 측정 단위. .NET Framework에서 측정 단위 간의 변환에 대한 기본 지원을 제공하지 않지만, 다음 예제와 같이 <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=nameWithType> 속성을 사용하여 특정 국가 또는 지역이 미터법을 사용하는지 여부를 확인할 수 있습니다.  
  
     [!code-csharp[Conceptual.Localizability#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.localizability/cs/ismetric1.cs#1)]
     [!code-vb[Conceptual.Localizability#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.localizability/vb/ismetric1.vb#1)]  
  
<a name="test"></a>   
## <a name="testing-your-application"></a>응용 프로그램 테스트  
 응용 프로그램을 지역화하기 전에 운영 체제의 국가별 버전에서 국가별 데이터를 사용하여 테스트해야 합니다. 대부분의 사용자 인터페이스는 이 시점에서 지역화되지 않지만, 다음과 같은 문제를 발견할 수 있습니다.  
  
-   운영 체제 버전마다 제대로 deserialize하지 않는 serialize된 데이터.  
  
-   현재 문화권의 규칙을 반영하지 않는 숫자 데이터. 예를 들어, 숫자가 정확하지 않은 그룹 구분 기호, 소수 구분 기호 또는 통화 기호를 사용하여 표시될 수 있습니다.  
  
-   현재 문화권의 규칙을 반영하지 않는 날짜 및 시간 데이터. 예를 들어, 월 및 일을 나타내는 숫자가 잘못된 순서로 나타나고, 날짜 구분 기호가 올바르지 않거나 표준 시간대 정보가 잘못될 수 있습니다.  
  
-   응용 프로그램에 대한 기본 문화권을 확인하지 않았으므로 찾을 수 없는 리소스.  
  
-   특정 문화권에 대해 비정상적인 순서로 표시되는 문자열.  
  
-   예기치 않은 결과를 반환하는 같음 비교 또는 문자열 비교.  
  
 응용 프로그램을 개발할 때 세계화 권장 사항을 따르고 문화권 구분 기능을 올바르게 처리하고 테스트 중 발생한 지역화 문제를 해결했다면 다음 단계인 [지역화](../../../docs/standard/globalization-localization/localization.md)로 진행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [전역화 및 지역화](../../../docs/standard/globalization-localization/index.md)  
- [지역화](../../../docs/standard/globalization-localization/localization.md)  
- [전역화](../../../docs/standard/globalization-localization/globalization.md)  
- [데스크톱 앱의 리소스](../../../docs/framework/resources/index.md)
