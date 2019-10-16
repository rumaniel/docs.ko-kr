---
title: XamlWriter.Save의 serialization 제한
ms.date: 03/30/2017
helpviewer_keywords:
- XamlWriter.Save [WPF], serialization limitations of
- limitations of XamlWriter.Save
- serialization limitations of XamlWriter.Save
ms.assetid: f86acc91-2b67-4039-8555-505734491d36
ms.openlocfilehash: f743f3de505904854be8aab59e9d3ad14ee64581
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68238615"
---
# <a name="serialization-limitations-of-xamlwritersave"></a>XamlWriter.Save의 serialization 제한
API <xref:System.Windows.Markup.XamlWriter.Save%2A> 의 콘텐츠를 serialize 할 수는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램을 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 파일입니다. 하지만 정확히 serialize되는 항목에 대한 눈에 띄는 몇 가지 제한 사항이 있습니다. 이러한 제한 사항과 몇몇 일반적인 고려 사항은 이 항목에서 설명합니다.  

<a name="Run_Time__Not_Design_Time_Representation"></a>   
## <a name="run-time-not-design-time-representation"></a>런타임으로, 디자인 타임 표현이 아님  
 호출 하 여 serialize 되는 항목의 기본 원리 <xref:System.Windows.Markup.XamlWriter.Save%2A> 된다는 결과 런타임에 serialize 되는 개체의 표현입니다. 많은 디자인 타임 속성을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일 최적화 되거나 손실 될 수 있습니다 이미는 합니다 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 메모리 내 개체로 로드 되 고 호출 하는 경우에 유지 되지 않습니다 <xref:System.Windows.Markup.XamlWriter.Save%2A> serialize 하 합니다. serialize된 결과는 생성된 애플리케이션 논리 트리의 효과적인 표현이지만 논리 트리를 생성한 원래 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에는 효과적인 표현이 아닐 수 있습니다. 이러한 문제를 확인 사용 하기가 매우 어렵습니다 합니다 <xref:System.Windows.Markup.XamlWriter.Save%2A> 는 광범위 한의 일부로 serialization [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 디자인 화면입니다.  
  
<a name="Serialization_is_Self_Contained"></a>   
## <a name="serialization-is-self-contained"></a>Serialization은 자체 포함됨  
 serialize 된 출력 <xref:System.Windows.Markup.XamlWriter.Save%2A> 독립적 이기 때문에; 내에 포함 되어 serialize 되는 모든 항목을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 이외의 외부 참조가 없는 및 단일 루트 요소를 사용 하 여 단일 페이지 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]합니다. 예를 들어 페이지에서 애플리케이션 리소스의 리소스를 참조한 경우 리소스는 serialize되는 페이지의 구성 요소인 것처럼 표시됩니다.  
  
<a name="Extension_References_are_Dereferenced"></a>   
## <a name="extension-references-are-dereferenced"></a>확장 참조가 역참조됨  
 `StaticResource` 또는 `Binding`과 같은 다양한 태그 확장 서식으로 만들어진 개체에 대한 일반 참조는 serialization 프로세스에서 역참조됩니다. 메모리 내 개체에는 응용 프로그램 런타임에 의해 생성 된 시점에 이미 역참조 된 이러한 및 <xref:System.Windows.Markup.XamlWriter.Save%2A> 논리 원래 다시 방문 하지 않습니다 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] serialize 된 출력에 대 한 이러한 참조를 복원 합니다. 이로 인해 데이터 바인딩된 값이나 리소스에서 얻은 값은 해당 값을 로컬에서 설정된 다른 값과 구분하는 제한되거나 간접적인 기능만으로 런타임 표현에서 마지막으로 사용된 값으로 고정될 수 있습니다. 이미지는 프로젝트에 있을 경우 원래 소스 참조가 아닌 이미지에 대한 개체 참조로 serialize되므로 원래 참조된 파일 이름 또는 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]가 모두 손실됩니다. 같은 페이지에서 선언된 리소스도 리소스 컬렉션의 키로 유지되지 않고 참조된 지점으로 serialize된 것으로 보입니다.  
  
<a name="Event_Handling_is_Not_Preserved"></a>   
## <a name="event-handling-is-not-preserved"></a>이벤트 처리가 유지되지 않음  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 통해 이벤트 처리기가 serialize될 경우 이벤트 처리기는 유지되지 않습니다. 코드 숨김이 없고 관련 x:Code 메커니즘이 없는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]은 런타임 절차 논리를 serialize할 수 없습니다. serialization은 자체 포함되고 논리 트리로 제한되므로 이벤트 처리기를 저장하는 기능이 없습니다. 따라서 이벤트 처리기 특성(특성 자체 및 처리기를 명명하는 문자열 값)이 출력 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 제거됩니다.  
  
<a name="Realistic_Scenarios_for_Use_of_XAMLWriter_Save"></a>   
## <a name="realistic-scenarios-for-use-of-xamlwritersave"></a>XAMLWriter.Save 사용에 대한 실제 시나리오  
 같습니다 꽤, 여전히 몇 가지 적절 한 시나리오를 사용 하 여에 대 한 제한 사항을 나열 하는 동안 <xref:System.Windows.Markup.XamlWriter.Save%2A> serialization에 대 한 합니다.  
  
- 벡터 또는 그래픽 출력: 렌더링 된 영역의 출력 재현 같은 벡터 나 그래픽을 다시 로드할 때 사용할 수 있습니다.  
  
- 서식 있는 텍스트 및 유동 문서: 텍스트 및 그 모든 요소 서식 및 요소 포함은 출력에 유지 됩니다. 이는 클립보드 기능과 비슷한 메커니즘에 유용할 수 있습니다.  
  
- 비즈니스 개체 데이터를 보존 합니다. 저장 한 경우 데이터를 사용자 지정 요소와 같은 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터를 비즈니스 개체에 따라 기본 서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 같은 사용자 지정 생성자 및 참조로 속성 값에 대 한 변환 규칙, 이러한 비즈니스 개체 수 serialization을 통해 지속 됩니다.
