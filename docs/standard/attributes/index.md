---
title: 특성을 사용하여 메타데이터 확장
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- metadata, extending
- attributes [.NET Framework], metadata
- elements [.NET Framework], attributes
- common language runtime, attributes
- annotating programming elements
- keyword-like descriptive declarations
- runtime, attributes
- extending metadata
ms.assetid: 30386922-1e00-4602-9ebf-526b271a8b87
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2a31082604048e71ebc7581b36857a8bfbd333c2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61969795"
---
# <a name="extending-metadata-using-attributes"></a>특성을 사용하여 메타데이터 확장
공용 언어 런타임에서는 형식, 필드, 메서드 및 속성과 같은 프로그래밍 요소에 주석을 달기 위해 특성이라는 키워드 방식의 설명적 선언을 추가할 수 있습니다. 런타임용으로 코드를 컴파일하는 경우 MSIL(Microsoft Intermediate Language)로 변환되고 컴파일러에서 생성된 메타데이터와 함께 PE(이식 가능한 실행) 파일 내에 배치됩니다. 특성을 사용하여 런타임 리플렉션 서비스를 통해 추출할 수 있는 메타데이터에 추가 설명 정보를 배치할 수 있습니다. <xref:System.Attribute?displayProperty=nameWithType>에서 파생되는 특수 클래스 인스턴스를 선언하면 컴파일러에서 특성을 만듭니다.  
  
 .NET Framework는 다양한 이유와 많은 문제를 해결하기 위해 특성을 사용합니다. 특성은 데이터를 직렬화하고, 보안을 적용하는 데 사용되는 특징을 지정하고, 코드를 쉽게 디버그할 수 있도록 JIT(Just-In-Time) 컴파일러에 의한 최적화를 제한하는 방법을 설명합니다. 또한 특성은 폼을 개발하는 동안 파일 이름 또는 코드 작성자를 기록하거나 컨트롤과 멤버의 표시 유형을 제어할 수 있습니다.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[특성 적용](../../../docs/standard/attributes/applying-attributes.md)|코드의 요소에 특성을 적용하는 방법을 설명합니다.|  
|[사용자 지정 특성 작성](../../../docs/standard/attributes/writing-custom-attributes.md)|사용자 지정 특성 클래스를 디자인하는 방법을 설명합니다.|  
|[특성에 저장된 정보 검색](../../../docs/standard/attributes/retrieving-information-stored-in-attributes.md)|실행 컨텍스트에 로드된 코드에 대한 사용자 지정 특성을 검색하는 방법을 설명합니다.|  
|[메타데이터 및 자동 기술 구성 요소](../../../docs/standard/metadata-and-self-describing-components.md)|메타데이터를 개괄적으로 설명하고 .NET Framework PE(이식 가능한 실행) 파일에서 구현하는 방법을 설명합니다.|  
|[방법: 리플렉션 전용 컨텍스트에 어셈블리 로드](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|리플렉션 전용 컨텍스트에서 사용자 지정 특성 정보를 검색하는 방법을 설명합니다.|  
  
## <a name="reference"></a>참조  
 <xref:System.Attribute?displayProperty=nameWithType>
