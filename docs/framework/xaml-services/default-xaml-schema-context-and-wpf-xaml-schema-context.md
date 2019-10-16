---
title: 기본 XAML 스키마 컨텍스트 및 WPF XAML 스키마 컨텍스트
ms.date: 03/30/2017
ms.assetid: 04e06a15-09b3-4210-9bdf-9a64c2eccb83
ms.openlocfilehash: f29d9eb481903b06ee1f35424baeb055a396b7c1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64663264"
---
# <a name="default-xaml-schema-context-and-wpf-xaml-schema-context"></a>기본 XAML 스키마 컨텍스트 및 WPF XAML 스키마 컨텍스트
XAML 스키마 컨텍스트는 특정 XAML 어휘를 사용 하는 XAML 프로덕션 간의 형식 매핑을 확인 하는 방법, 어셈블리를 로드 하는 방법, 어떻게 특정 판독기 및 기록기를 포함 하 여 동작을 작성 하는 개체 상호 작용 하는 방식을 정규화 하는 개념적 엔터티 설정은 해석 됩니다. 이 항목에서는.NET Framework XAML 서비스 및 CLR 형식 시스템을 기반으로 하는 연결 된 기본 XAML 스키마 컨텍스트의 기능을 설명 합니다. 이 항목에는 WPF에 사용 되는 XAML 스키마 컨텍스트를 설명 합니다.  
  
## <a name="default-xaml-schema-context"></a>기본 XAML 스키마 컨텍스트  
 .NET framework XAML 서비스 구현 및 기본 XAML 스키마 컨텍스트를 사용 합니다. 기본 XAML 스키마 컨텍스트 동작이 항상 완전히 보이지 않으면 api에 <xref:System.Xaml.XamlSchemaContext> 클래스입니다. 그러나 대부분의 경우에서 기본 XAML 스키마 컨텍스트에 영향을 주는 동작은 관찰 가능 개체의 멤버와 같이 XAML 형식 시스템의 공용 API 통해 <xref:System.Xaml.XamlMember> 또는 <xref:System.Xaml.XamlType>, 또는 XAML 판독기 및 XAML 작성기를 사용 하는에 노출 된 Api를 통해 기본 XAML 스키마 컨텍스트입니다.  
  
 만들 수 있습니다는 <xref:System.Xaml.XamlSchemaContext> 를 호출 하 여 기본 동작을 캡슐화 하는 <xref:System.Xaml.XamlSchemaContext> 생성자입니다. 이 기본 XAML 스키마 컨텍스트를 명시적으로 만듭니다. XAML 판독기 또는 명시적으로 사용 하지 않는 Api를 사용 하 여 XAML 작성기를 초기화 하는 경우 동일한 기본 XAML 스키마 컨텍스트를 암시적으로 만들어지고는 <xref:System.Xaml.XamlSchemaContext> 입력된 매개 변수입니다.  
  
 기본 XAML 스키마 컨텍스트 CLR 리플렉션 형식 매핑 동작에 의존합니다. 여기에 검사를 정의 하는 CLR <xref:System.Type>, 및 관련 <xref:System.Reflection.PropertyInfo> 또는 <xref:System.Reflection.MethodInfo>합니다. 또한 형식 또는 멤버의 CLR 특성이 XAML 형식 또는 CLR 지원 형식을 사용 하는 XAML 멤버 정보에 대 한 세부 사항을 채우기 위해 사용 됩니다. 기본 XAML 스키마 컨텍스트 형식 같은 시스템 확장 기술이 필요 하지 않습니다는 `Invoker` 패턴에 필요한 정보를 CLR 형식 시스템에서 사용할 수 있습니다.  
  
 논리를 로드 하는 어셈블리에 대 한 기본 XAML 스키마 컨텍스트는 XAML 네임 스페이스 매핑을 제공 하는 어셈블리 값에 주로 사용 합니다. 또한 <xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A> 어셈블리 내부 형식을 로드 하는 등의 시나리오에 대 한 로드 힌트 수 있습니다.  
  
## <a name="wpf-xaml-schema-context"></a>WPF XAML 스키마 컨텍스트  
 WPF XAML 스키마 컨텍스트는 WPF 구현은 기본이 아닌 XAML 스키마 컨텍스트를 구현 하 여 발생할 수 있는 기능 유형의 흥미로운 예시를 제공 하기 때문에이 항목에서 설명 되어 있습니다. 또한 XAML 스키마 컨텍스트 개념에서에서 다루지 않습니다 거의 WPF XAML; 주소는 WPF 설명서 XAML 스키마 컨텍스트를 사용 하면 동작을 함께 기본 XAML 스키마 컨텍스트 작동 방식을 설명 하는 경우에 완벽 하 게 이해할 수만 있습니다. 다음 동작을 구현 하는 WPF XAML 스키마 컨텍스트입니다.  
  
 **조회를 재정의 합니다.** WPF XAML에 대 한 몇 가지 정적 콘텐츠 모델이 있는 되지 않아도 작동 하는 XAML 콘텐츠 속성 <xref:System.Windows.Markup.ContentPropertyAttribute> 특성을 사용 합니다. <xref:System.Xaml.XamlType.LookupContentProperty%2A> WPF에 대 한 재정의이 동작을 구현합니다.  
  
 **WPF 식에 대 한 지연 합니다.** WPF는 런타임 컨텍스트를 사용할 때까지 값을 지연 시키는 여러 식 클래스를 제공 합니다. 또한 템플릿 확장은 지연 기술을 사용 하는 런타임 동작입니다.  
  
 **시스템 조회 최적화를 입력 합니다.** WPF는 광범위 한 XAML 어휘 및 개체 모델을 수백 개의 WPF에 정의 된 클래스를 상속 하는 기본 클래스 멤버 정의 포함 합니다. 또한 자체 WPF는 여러 어셈블리에서 분산 됩니다. WPF 조회 테이블 및 기타 기술을 사용 하 여 형식 조회를 최적화 합니다. 이 기본 XAML 스키마 컨텍스트 및 해당 CLR 기반 형식 조회를 통해 성능 향상을 제공합니다. 형식 조회 테이블에 존재 하지 않는 경우 동작에는 XAML 스키마 컨텍스트과 비슷한 기법 기본 XAML 스키마 컨텍스트를 사용 합니다.  
  
 **XamlType 및 XamlMember 확장:** WPF는 종속성 속성을 사용 하 여 속성 개념 및 라우트된 이벤트를 사용 하 여 이벤트 개념을 확장 합니다. WPF는 XAML 처리 작업에 대 한 이러한 개념 가시성을 제공, 다음을 확장 합니다. <xref:System.Xaml.XamlType> 고 <xref:System.Xaml.XamlMember>, 라우트된 이벤트 특징 및 종속성 속성을 보고 하는 내부 속성을 추가 합니다.  
  
### <a name="accessing-the-wpf-xaml-schema-context"></a>WPF XAML 스키마 컨텍스트 액세스  
 WPF를 기반으로 하는 XAML 기술을 사용 하는 경우 <xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType> 또는 <xref:System.Windows.Markup.XamlWriter?displayProperty=nameWithType>, WPF XAML 스키마 컨텍스트를 사용 하 여 해당 XAML 판독기 및 XAML 작성기 구현에 이미 있습니다.  
  
 를 사용 중인 다른 XAML 판독기 또는 XAML 작성기 구현을 초기화 하지 않는 WPF XAML 스키마 컨텍스트를 사용 하는 경우에 작동 하는 WPF XAML 스키마 컨텍스트를 가져올 수 있습니다 <xref:System.Windows.Markup.XamlReader.GetWpfSchemaContext%2A?displayProperty=nameWithType>합니다. 이 값을 사용 하는 다른 API에 대 한 초기화로 사용할 수 있습니다는 <xref:System.Xaml.XamlSchemaContext>합니다. 예를 들어, 호출할 수 있습니다 <xref:System.Xaml.XamlXmlReader.%23ctor%2A> 초기화 및 WPF XAML 스키마 컨텍스트를 전달 합니다. 또는 XAML 형식 시스템 작업에 대 한 WPF XAML 스키마 컨텍스트를 사용할 수 있습니다. 초기화 생성이 포함 된 <xref:System.Xaml.XamlType> 또는 <xref:System.Xaml.XamlMember>, 호출 또는 <xref:System.Xaml.XamlSchemaContext.GetXamlType%2A?displayProperty=nameWithType>합니다.  
  
 WPF XAML의 특정 측면에는 순수 XAML 노드 스트림의 관점에서 액세스 하는 경우 WPF 프레임 워크 기능 중 일부를 수 있습니다 아직 작동 하지 note 합니다. 예를 들어, 컨트롤에 대 한 WPF 템플릿은 아직 적용 되지 않습니다. 따라서 런타임 시 전체 시각적 트리를 사용 하 여 채울 수 있는 속성에 액세스 하는 경우 서식 파일을 참조 하는 속성 값만 표시 될 수 있습니다. WPF 태그 확장에 대 한 제공 하는 서비스 컨텍스트에 정확 하지 않을 런타임 이외의 경우에서 제공 하는 경우 및 개체 그래프를 작성 하려고 시도할 때 예외가 발생할 수 있습니다.  
  
## <a name="xaml-and-assembly-loading"></a>XAML 및 어셈블리 로딩  
 XAML 및.NET Framework XAML 서비스에 대 한 로드 하는 어셈블리의 CLR 정의 개념 통합 <xref:System.AppDomain>합니다. 어셈블리를 로드 또는 사용에 따라 런타임 또는 디자인 타임에 형식을 찾을 방법을 해석 하는 XAML 스키마 컨텍스트를 <xref:System.AppDomain> 및 기타 요인입니다. 논리는 XAML을 XAML 판독기에 대 한 느슨한 XAML 인지에 따라 약간 다릅니다는 XAML에서 DLL로 컴파일됩니다 `XamlBuildTask`에 WPF의에서 생성 된 BAML `PresentationBuildTask`합니다.  
  
 WPF의 XAML 스키마 컨텍스트를 사용 하 여 WPF 응용 프로그램 모델은 통합 <xref:System.AppDomain> WPF 구현 세부 정보가 있는 다른 요소 뿐만 아니라 합니다.  
  
#### <a name="xaml-reader-input-loose-xaml"></a>XAML 판독기 입력 (느슨한 XAML)  
  
1. XAML 스키마 컨텍스트를 반복 합니다 <xref:System.AppDomain> 이름의 모든 요소와 일치 하는 이미 로드 된 어셈블리를 찾고, 응용 프로그램의 가장 최근에 로드 에서부터 어셈블리입니다. 일치 하는 항목이 있으면 해당 어셈블리 확인에 사용 됩니다.  
  
2. CLR에 따라 다음 방법 중 하나이 고, 그렇지 <xref:System.Reflection.Assembly> API는 어셈블리를 로드 하는 데 사용 됩니다.  
  
    - 매핑의 이름을 qualified 인 경우 호출 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 정규화 된 이름에 있습니다.  
  
    - 이전 단계가 실패 하면 짧은 이름 (및 공개 키 토큰이 있는 경우)를 사용 하려면 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>합니다.  
  
    - 이름 매개 변수 매핑에서 정규화 되지 않은, 경우 호출 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>합니다.  
  
#### <a name="xamlbuildtask"></a>XamlBuildTask  
 `XamlBuildTask` Windows Communication Foundation (WCF) 및 Windows Workflow Foundation에 사용 됩니다.  
  
 어셈블리 참조를 통해 `XamlBuildTask` 는 항상 정규화 합니다.  
  
1. 호출 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 정규화 된 이름에 있습니다.  
  
2. 이전 단계가 실패 하면 짧은 이름 (및 공개 키 토큰이 있는 경우)를 사용 하려면 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>합니다.  
  
#### <a name="baml-presentationbuildtask"></a>BAML (PresentationBuildTask)  
 BAML에 대 한 어셈블리 로드를 두 가지 측면이 있습니다: 초기 구성 요소로 BAML이 들어 있는 어셈블리를 로드 하 고 BAML 프로덕션에서 참조 하는 모든 형식에 대 한 형식 지원 어셈블리를 로드 합니다.  
  
##### <a name="assembly-load-for-initial-markup"></a>초기 태그에 대 한 어셈블리를 로드 합니다.  
 태그를 로드할 어셈블리에 대 한 참조 항상 정규화 된 것은 아닙니다.  
  
1. WPF XAML 스키마 컨텍스트를 반복 합니다 <xref:System.AppDomain> 이름의 모든 요소와 일치 하는 이미 로드 된 어셈블리를 찾습니다는 WPF 응용 프로그램을 가장 최근에 로드 에서부터 어셈블리입니다. 일치 하는 항목이 있으면 해당 어셈블리 확인에 사용 됩니다.  
  
2. 이전 단계가 실패 하면 짧은 이름 (및 공개 키 토큰이 있는 경우)를 사용 하려면 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>합니다.  
  
##### <a name="assembly-references-by-baml-types"></a>BAML 형식에서 어셈블리 참조:  
 BAML 프로덕션 환경에서 사용 되는 형식에 대 한 어셈블리 참조는 항상 빌드 작업의 출력으로 정규화 합니다.  
  
1. WPF XAML 스키마 컨텍스트를 반복 합니다 <xref:System.AppDomain> 이름의 모든 요소와 일치 하는 이미 로드 된 어셈블리를 찾습니다는 WPF 응용 프로그램을 가장 최근에 로드 에서부터 어셈블리입니다. 일치 하는 항목이 있으면 해당 어셈블리 확인에 사용 됩니다.  
  
2. 이 고, 그렇지 어셈블리를 로드 하는 다음 방법 중 하나:  
  
    - 호출 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 정규화 된 이름에 있습니다.  
  
    - 약식 이름 + 공개 키 토큰 조합이 BAML에서 로드 된 어셈블리와 일치 하는 경우 해당 어셈블리를 사용 합니다.  
  
    - 약식 이름 + 공개 키 토큰을 사용 하 여 호출 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>합니다.  
  
## <a name="see-also"></a>참고자료

- [XAML 노드 스트림 구조 및 개념 이해](understanding-xaml-node-stream-structures-and-concepts.md)
