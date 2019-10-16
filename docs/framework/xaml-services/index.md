---
title: XAML 서비스
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], System.Xaml concepts
- XAML Services in WPF [XAML Services]
- System.Xaml [XAML Services], conceptual documentation
ms.assetid: 0e11f386-808c-4eae-9ba6-029ad7ba2211
ms.openlocfilehash: 61b141642fa3745c3abcf8d0234f70373fa5485e
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66491112"
---
# <a name="xaml-services"></a>XAML 서비스
이 항목에서는.NET Framework XAML 서비스 라고 하는 기술 집합의 기능을 설명 합니다. 대부분의 서비스와 설명 되는 Api는.NET core 어셈블리 집합은.NET Framework 4를 사용 하 여 도입 된 어셈블리인 System.Xaml 어셈블리에 있습니다. 판독기 및 작성기, 스키마 클래스 및 스키마 지원이 팩터리를 포함 하는 서비스 클래스, XAML 언어 내장 함수 지원을 및 다른 XAML 언어 기능 특성을 지정 합니다.  
  
## <a name="about-this-documentation"></a>이 설명서에 대 한  
 .NET Framework XAML 서비스에 대 한 개념 설명서는 XAML 언어 및 어떻게이 적용 될 수 있습니다 특정 프레임 워크, 예를 들어 사용 경험이 있다고 가정 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] Windows Workflow Foundation 또는 특정 기술 기능 영역, 예를 들어 빌드 사용자 지정 기능 <xref:Microsoft.Build.Framework.XamlTypes>합니다. 이 설명서 태그 언어, XAML 구문 용어 또는 기타 입문 자료로 XAML의 기본 사항을 설명 하지 않습니다. 대신,이 설명서에 특별히 사용할 수 있는.NET Framework XAML 서비스를 사용 하 여 System.Xaml 어셈블리 라이브러리의 중점을 둡니다. 대부분의 이러한 Api는 XAML 언어 통합 및 확장성에 대 한 시나리오에 대 한 합니다. 다음 중 하나를이 포함 될 수 있습니다.  
  
- 기본 XAML 판독기 또는 XAML 작성기 (직접 XAML 노드 스트림을 처리, 사용자 고유의 XAML 판독기 또는 XAML 작성기를 파생)의 기능을 확장 합니다.  
  
- 특정 프레임 워크 종속성이 없는 XAML에서 사용 가능한 사용자 지정 형식 정의 및 해당 XAML을 전달 하기 위해 형식 특성 설정.NET Framework XAML 서비스에 시스템 특성을 입력 합니다.  
  
- XAML 판독기 또는 XAML 작성기 비주얼 디자이너 또는 XAML 태그 원본에 대 한 대화식 편집기 등의 응용 프로그램의 구성 요소로 호스트 합니다.  
  
- XAML 값 변환기 (태그 확장, 사용자 지정 형식에 대 한 형식 변환기)을 작성합니다.  
  
- 사용자 지정 XAML 스키마 컨텍스트 정의 (백업 형식 원본에 대 한 어셈블리 로드 기술을 대체를 사용 하 여; 어셈블리를 반영; CLR을 사용 하지 않는 어셈블리를 로드 개념을 사용 하 여 알려진 형식 조회 기법을 사용 하 여 항상 대신 `AppDomain` 및 연결 된 보안 모델)입니다.  
  
- 기본 XAML 형식 시스템을 확장 합니다.  
  
- 사용 하는 `Lookup` 또는 `Invoker` 시스템 및 형식 지원의 평가 하는 방법에 XAML을 영향을 주는 기술 입력 합니다.  
  
 소개 자료 언어로 XAML에서 찾으려는 경우 시도해 보십시오 [XAML 개요 (WPF)](../wpf/advanced/xaml-overview-wpf.md)합니다. 해당 항목에 설명 XAML 새로 추가 된 대상에 대 한 두 가지를 모두 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 및 XAML 태그와 XAML 언어 기능을 사용 하도 합니다. 다른 유용한 문서가 소개 자료는 [XAML 언어 사양](https://go.microsoft.com/fwlink/?LinkId=114525)합니다.  
  
## <a name="net-framework-xaml-services-and-systemxaml-in-the-net-architecture"></a>.NET framework XAML 서비스 및 System.Xaml에.NET 아키텍처  
 이전 버전의 Microsoft.NET Framework, Microsoft.NET Framework에서 구축 하는 프레임 워크에서 구현 되었습니다 XAML 언어 기능에 대 한 지원이 ([!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], Windows Workflow Foundation 및 Windows Communication Foundation (WCF)), 즉 동작 및 사용 되는 API를 사용 하는 특정 프레임 워크에 따라 달라 집니다. 이 포함 된 XAML 파서 및 해당 개체 그래프 생성 메커니즘, XAML 언어 내장, serialization 지원 및 등입니다.  
  
 .NET Framework 4,.NET Framework XAML 서비스 및 System.Xaml 어셈블리에는 XAML 언어 기능을 지원 하기 위해 필요한 많은 정의 합니다. XAML 판독기 및 XAML 작성기에 대 한 기본 클래스가 포함 됩니다. 프레임 워크별 XAML 구현 중 하나에 존재 하지 않는.NET Framework XAML 서비스에 추가 하는 가장 중요 한 기능에는 XAML에 대 한 형식 시스템 표현입니다. 형식 시스템 표현을 XAML 프레임 워크의 특정 기능에 의존 하지 않고 XAML 기능에 집중 하는 개체 지향 방식으로 제공 합니다.  
  
 XAML 형식 시스템의 XAML 원본; 런타임 세부 정보 또는 태그 형식으로 제한 되지 않습니다. 또는 모든 특정 지원 형식 시스템에 의해 제한 됩니다. XAML 형식 시스템 형식, 멤버, XAML 스키마 컨텍스트, XML 수준 개념 및 다른 XAML 언어 개념 또는 XAML 내장 함수에 대 한 개체 표현을 포함합니다. 사용 하거나 XAML 형식 시스템을 확장 가능 하도록 XAML 판독기 및 XAML 작성기와 같은 클래스에서 파생 하 고 프레임 워크, 기술 또는 사용 하는 응용 프로그램으로 사용 하도록 설정 하는 특정 기능에 대 한 XAML 표현의 기능 확장 또는 XAML을 내보냅니다. XAML 스키마 컨텍스트를 개념이 XAML 개체 작성기 구현, 어셈블리는 컨텍스트 및 XAML 노드 정보를 통해 전달 되는 기술 지원 형식 시스템의 조합을 통해 실제 개체 그래프 쓰기 작업을 실행할 수 소스입니다. XAML 스키마 개념에 대 한 자세한 내용은 합니다. 참조 [기본 XAML 스키마 컨텍스트 및 WPF XAML 스키마 컨텍스트](default-xaml-schema-context-and-wpf-xaml-schema-context.md)합니다.  
  
## <a name="xaml-node-streams-xaml-readers-and-xaml-writers"></a>XAML 노드 스트림, XAML 판독기 및 XAML 작성기  
 .NET Framework XAML 서비스 XAML 언어 및 XAML을 언어로 사용 하는 특정 기술 간의 관계에서 수행 하는 역할을 이해 하려면 XAML 노드 스트림 및 해당 개념 API 셰이프 하는 방법의 개념을 이해 하는 데 도움이 되 고 용어입니다. XAML 노드 스트림이 XAML 언어 표시는 XAML을 나타내거나 정의 하는 개체 그래프 사이의 개념적 중간입니다.  
  
- XAML 판독기는 어떤 형태로 XAML을 처리 하 고 XAML 노드 스트림을 생성 하는 엔터티입니다. Api에서 XAML 판독기가 기본 클래스에 의해 표시 됩니다 <xref:System.Xaml.XamlReader>합니다.  
  
- XAML 작성기는 XAML 노드 스트림을 처리 하 고 다른 항목을 생성 하는 엔터티입니다. Api에서 XAML 작성기 기본 클래스에 의해 표시 됩니다 <xref:System.Xaml.XamlWriter>합니다.  
  
 XAML 관련 된 두 가지 가장 일반적인 시나리오 개체 그래프를 인스턴스화하는 XAML 로드 응용 프로그램이 나 도구에서 개체 그래프를 저장 하 고 (일반적으로 텍스트 파일로 저장 된 태그 형식)에 XAML 표현을 생성 합니다. XAML을 로드 하 고 개체 그래프를 만든 라고 로드 경로 사용 하 여이 설명서에 있습니다. 저장 하거나 기존 개체 그래프를 XAML 직렬화 라고 저장이이 설명서에서는 경로입니다.  
  
 가장 일반적인 유형의 로드 경로 다음과 같이 설명할 수 있습니다.  
  
- U t F-인코딩된 XML 형식으로 XAML 표현을 시작 하 고 텍스트 파일로 저장 합니다.  
  
- 에 XAML 로드 <xref:System.Xaml.XamlXmlReader>합니다. <xref:System.Xaml.XamlXmlReader> 가 <xref:System.Xaml.XamlReader> 하위 클래스입니다.  
  
- 결과 XAML 노드 스트림입니다. 사용 하 여 XAML 노드 스트림에 개별 노드에 액세스할 수 있습니다 <xref:System.Xaml.XamlXmlReader>  /  <xref:System.Xaml.XamlReader> API. 여기서는 가장 일반적인 작업은 XAML 노드 스트림, "현재 레코드"를 사용 하 여 각 노드 처리를 진행 하려면 메타포입니다.  
  
- XAML 노드 스트림의 결과 노드를 통과 한 <xref:System.Xaml.XamlObjectWriter> API. <xref:System.Xaml.XamlObjectWriter> 가 <xref:System.Xaml.XamlWriter> 하위 클래스입니다.  
  
- <xref:System.Xaml.XamlObjectWriter> 소스 XAML 노드 스트림에서 진행에 따라에서 개체 그래프를 한 번에 하나의 개체를 씁니다. XAML 스키마 컨텍스트 및 구현을 지원 형식 시스템 및 프레임 워크의 형식과 어셈블리에 액세스할 수 있는 지원을 사용 하 여 수행 됩니다.  
  
- 호출 <xref:System.Xaml.XamlObjectWriter.Result%2A> 개체 그래프의 루트 개체를 가져올 XAML 노드 스트림의 끝입니다.  
  
 가장 일반적인 유형의 저장 경로 다음과 같이 설명할 수 있습니다.  
  
- 실행 하는 전체 응용 프로그램 시간, UI 콘텐츠 및 실행 시간, 상태 또는 전체 응용 프로그램의 개체 표현 런타임 시 작은 세그먼트의 개체 그래프를 사용 하 여 시작 합니다.  
  
- 응용 프로그램 루트 또는 문서 루트와 같은 논리적 시작 개체에 개체를 로드할 <xref:System.Xaml.XamlObjectReader>합니다. <xref:System.Xaml.XamlObjectReader> 가 <xref:System.Xaml.XamlReader> 하위 클래스입니다.  
  
- 결과 XAML 노드 스트림입니다. 사용 하 여 XAML 노드 스트림에 개별 노드에 액세스할 수 있습니다 <xref:System.Xaml.XamlObjectReader> 고 <xref:System.Xaml.XamlReader> API. 여기서는 가장 일반적인 작업은 XAML 노드 스트림, "현재 레코드"를 사용 하 여 각 노드 처리를 진행 하려면 메타포입니다.  
  
- XAML 노드 스트림의 결과 노드를 통과 한 <xref:System.Xaml.XamlXmlWriter> API. <xref:System.Xaml.XamlXmlWriter> 가 <xref:System.Xaml.XamlWriter> 하위 클래스입니다.  
  
- <xref:System.Xaml.XamlXmlWriter> 인코딩 XML utf는 XAML을 씁니다. 이 텍스트 파일을 스트림으로 또는 다른 형식으로 저장할 수 있습니다.  
  
- 호출 <xref:System.Xaml.XamlXmlWriter.Flush%2A> 최종 출력을 가져오려고 합니다.  
  
 XAML 노드 스트림 개념에 대 한 자세한 내용은 참조 하십시오 [Understanding XAML 노드 Stream 구조 및 개념](understanding-xaml-node-stream-structures-and-concepts.md)합니다.  
  
### <a name="the-xamlservices-class"></a>XamlServices 클래스  
 항상 필요 없는 XAML 노드 스트림을 사용 하 여 처리 합니다. 기본 로드 경로 또는 경로 저장 기본을 하려는 경우에 Api를 사용할 수 있습니다는 <xref:System.Xaml.XamlServices> 클래스입니다.  
  
- 여러 시그니처가 <xref:System.Xaml.XamlServices.Load%2A> 로드 경로 구현 합니다. 파일 또는 스트림을 로드 하거나 또는 로드할 수는 <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> 또는 <xref:System.Xaml.XamlReader> 는 판독기의 Api를 사용 하 여 로드 하 여 XAML 입력을 래핑하는 합니다.  
  
- 여러 시그니처가 <xref:System.Xaml.XamlServices.Save%2A> 개체 그래프를 저장 하 고 출력을 스트림, 파일 또는 <xref:System.Xml.XmlWriter> / <xref:System.IO.TextWriter> 인스턴스.  
  
- <xref:System.Xaml.XamlServices.Transform%2A> XAML 로드 경로 및 저장을 연결 하 여 변환 경로 단일 작업으로 합니다. 다른 스키마 컨텍스트 또는 다른 지원 형식 시스템에 사용할 수 없습니다 <xref:System.Xaml.XamlReader> 및 <xref:System.Xaml.XamlWriter>, 결과 XAML이 변환 되는 방식을 영향을 줄입니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 <xref:System.Xaml.XamlServices>를 참조 하세요 [XAMLServices 클래스 및 기본 XAML 읽기 또는 쓰기](xamlservices-class-and-basic-xaml-reading-or-writing.md)합니다.  
  
## <a name="xaml-type-system"></a>XAML 형식 시스템  
 XAML 형식 시스템을 XAML 노드 스트림의 특정된 개별 노드를 사용 하는 데 필요한 Api를 제공 합니다.  
  
 <xref:System.Xaml.XamlType> 개체 노드 시작 및 끝 개체 노드 간에 처리 중인 개체에 대 한 표현이입니다.  
  
 <xref:System.Xaml.XamlMember> 멤버 노드 시작 및 끝 멤버 노드 간에 처리 중인 개체의 멤버에 대 한 표현이입니다.  
  
 등의 Api <xref:System.Xaml.XamlType.GetAllMembers%2A> 하 고 <xref:System.Xaml.XamlType.GetMember%2A> 하 고 <xref:System.Xaml.XamlMember.DeclaringType%2A> 간의 관계를 보고를 <xref:System.Xaml.XamlType> 및 <xref:System.Xaml.XamlMember>합니다.  
  
 .NET Framework XAML 서비스에 의해 구현 된 XAML 형식 시스템의 기본 동작은 리플렉션을 사용 하 여 CLR (공용 언어 런타임), 및 어셈블리의 CLR 형식의 정적 분석에 기반 합니다. 따라서 특정 CLR 형식의 경우 XAML 형식 시스템의 기본 구현을 해당 형식 및 해당 멤버의 XAML 스키마를 노출할 수 있습니다 및 XAML 형식 시스템 측면에서 보고 합니다. 기본 XAML 형식 시스템의 가능성 형식의 개념이 CLR 상속에 매핑되고 인스턴스, 값 형식 및 등의 개념 지원 동작 및 CLR의 기능에 매핑됩니다.  
  
## <a name="reference-for-xaml-language-features"></a>XAML 언어 기능에 대 한 참조  
 XAML을 지원 하려면.NET Framework XAML 서비스 XAML 언어 XAML 네임 스페이스에 정의 된 대로 XAML 언어 개념의 특정 구현을 제공 합니다. 이러한 특정 참조 페이지로 나와 있습니다. 언어 기능 언어 기능이 XAML 판독기 또는.NET Framework XAML 서비스에 정의 되어 있는 XAML 작성기에 의해 처리 될 때 동작 하는 방법의 관점에서 나와 있습니다. 자세한 내용은 참조 하세요. [XAML Namespace (x:) 언어 기능](xaml-namespace-x-language-features.md)합니다.
