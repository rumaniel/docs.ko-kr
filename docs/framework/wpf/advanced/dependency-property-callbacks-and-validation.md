---
title: 종속성 속성 콜백 및 유효성 검사
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dependency properties [WPF], validation
- coerce value callbacks [WPF]
- callbacks [WPF], validation
- dependency properties [WPF], callbacks
- validation of dependency properties [WPF]
ms.assetid: 48db5fb2-da7f-49a6-8e81-3540e7b25825
ms.openlocfilehash: 7f00961ba100700c68936cc33facfdc758c77d3f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940820"
---
# <a name="dependency-property-callbacks-and-validation"></a>종속성 속성 콜백 및 유효성 검사
이 항목에서는 유효성 검사 확인, 속성의 유효 값이 변경될 때마다 호출되는 콜백, 값 결정에 대한 가능한 외부 영향 재정의 등 속성 관련 기능에 대체 사용자 지정 구현을 사용하여 종속성 속성을 만드는 방법에 대해 설명합니다. 또한 이 항목에서는 이러한 기술을 사용한 기본 속성 시스템 동작 확장이 적절한 시나리오에 대해서도 설명합니다.  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목에서는 종속성 속성을 구현하는 기본 시나리오와 메타데이터가 사용자 지정 종속성 속성에 적용되는 방법을 이해하고 있다고 가정합니다. 컨텍스트는 [사용자 지정 종속성 속성](custom-dependency-properties.md) 및 [종속성 속성 메타데이터](dependency-property-metadata.md)를 참조하세요.  
  
<a name="Validation_Callbacks"></a>   
## <a name="validation-callbacks"></a>유효성 검사 콜백  
 유효성 검사 콜백은 종속성 속성을 처음 등록할 때 이 속성에 할당할 수 있습니다. 유효성 검사 콜백은 속성 메타 데이터의 일부가 아닙니다. <xref:System.Windows.DependencyProperty.Register%2A> 메서드를 직접 입력 하는 것입니다. 따라서 종속성 속성에 대해 유효성 검사 콜백을 만든 다음에는 새 구현으로 재정의할 수 없습니다.  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 콜백은 개체 값이 제공되도록 구현됩니다. 제공된 값이 속성에 유효하면 `true`를 반환하고, 그러지 않으면 `false`를 반환합니다. 속성은 속성 시스템에 등록된 형식에 따라 올바른 형식이 되므로 콜백 내에서 형식 검사가 일반적으로 수행되지 않는다고 간주합니다. 콜백은 다양한 작업에서 속성 시스템에 의해 사용됩니다. 여기에는 기본적으로 초기 형식 초기화,를 호출 <xref:System.Windows.DependencyObject.SetValue%2A>하 여 프로그래밍 방식으로 변경 또는 제공 된 새 기본값을 사용 하 여 메타 데이터 재정의를 시도 하는 작업이 포함 됩니다. 유효성 검사 콜백이 이러한 작업에 의해 호출되고 `false`를 반환하면 예외가 발생합니다. 애플리케이션 작성자는 이러한 예외를 처리할 수 있도록 준비해야 합니다. 유효성 검사 콜백의 일반적인 용도는 열거형 값의 유효성을 검사하거나 속성이 0 이상이어야 하는 측정값을 설정할 때 정수 또는 double 값을 제약하는 것입니다.  
  
 유효성 검사 콜백은 특별히 인스턴스 유효성 검사기가 아닌 클래스 유효성 검사기입니다. 콜백의 매개 변수는 유효성을 검사할 속성이 설정 된 <xref:System.Windows.DependencyObject> 특정를 전달 하지 않습니다. 따라서 유효성 검사 콜백은 속성 값에 영향을 줄 수 있는 가능한 "종속성"을 적용하는 데 유용하지 않으며, 속성의 인스턴스 관련 값은 다른 속성의 인스턴스 관련 값이나 런타임 상태와 같은 요소에 따라 달라집니다.  
  
 다음은 매우 간단한 유효성 검사 콜백 시나리오에 대 한 예제 코드입니다. <xref:System.Double> 기본 형식으로 입력 된 속성이 또는 <xref:System.Double.NegativeInfinity>이 아닌 <xref:System.Double.PositiveInfinity> 경우의 유효성 검사입니다.  
  
 [!code-csharp[DPCallbackOverride#ValidateValueCallback](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#validatevaluecallback)]
 [!code-vb[DPCallbackOverride#ValidateValueCallback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#validatevaluecallback)]  
  
<a name="Coerce_Value_Callbacks_and_Property_Changed_Events"></a>   
## <a name="coerce-value-callbacks-and-property-changed-events"></a>강제 값 콜백 및 속성 변경 이벤트  
 강제 값 콜백은 종속성 속성 값이 <xref:System.Windows.DependencyObject> 변경 될 때마다 속성 시스템에서 <xref:System.Windows.PropertyChangedCallback> 호출 하는 구현과 같이 속성에 대해 특정 인스턴스를 전달 합니다. 이 두 콜백을 함께 사용하여 한 속성이 변경되면 다른 속성의 강제 변환이나 재계산이 강제로 적용될 요소에 일련의 속성을 만들 수 있습니다.  
  
 종속성 속성의 연결을 사용하는 일반적인 시나리오는 요소가 최소값 및 최대값에 대해 각각 하나씩 속성을 보유하고 실제 또는 현재 값에 대해 세 번째 속성을 보유하는 사용자 인터페이스 기반 속성이 있는 경우입니다. 여기에서 현재 값이 새 최대값을 초과하는 방식으로 최대값을 조정한 경우 새 최대값보다 크지 않도록 현재 값을 강제 변환하고 최소값에 대한 유사한 관계를 현재값으로 강제 변환하려고 합니다.  
  
 다음은 이 관계를 보여 주는 세 가지 종속성 속성 중 하나에 대한 매우 간단한 예제 코드입니다. 이 예제에서는 관련 *Reading 속성의 Min/Max/Current 집합 중 `CurrentReading` 속성이 등록되는 방법을 보여 주며, 이전 섹션에 표시된 유효성 검사를 사용합니다.  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 Current에 대한 속성 변경 콜백은 다른 속성에 대해 등록된 강제 값 콜백을 명시적으로 호출하여 다른 종속 속성에 변경 내용을 전달하는 데 사용됩니다.  
  
 [!code-csharp[DPCallbackOverride#OnPCCurrent](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#onpccurrent)]
 [!code-vb[DPCallbackOverride#OnPCCurrent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#onpccurrent)]  
  
 강제 값 콜백은 현재 속성이 잠재적으로 종속되어 있는 속성의 값을 확인하고 필요한 경우 현재 값을 강제 변환합니다.  
  
 [!code-csharp[DPCallbackOverride#CoerceCurrent](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#coercecurrent)]
 [!code-vb[DPCallbackOverride#CoerceCurrent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#coercecurrent)]  
  
> [!NOTE]
> 속성의 기본값은 강제 변환되지 않습니다. 속성 값에 초기 기본값이 있는 경우 또는에서 <xref:System.Windows.DependencyObject.ClearValue%2A>다른 값의 선택을 취소 하는 경우 기본값 값과 같은 속성 값이 발생할 수 있습니다.  
  
 강제 값 및 속성 변경 콜백은 속성 메타데이터의 일부입니다. 따라서 특정 형식의 속성에 대한 메타데이터를 재정의하여 종속성 속성을 소유하는 형식에서 파생된 형식에 있는 특정 종속성 속성에 대한 콜백을 변경할 수 있습니다.  
  
<a name="Advanced"></a>   
## <a name="advanced-coercion-and-callback-scenarios"></a>고급 강제 변환 및 콜백 시나리오  
  
### <a name="constraints-and-desired-values"></a>제약 조건 및 원하는 값  
 이 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 콜백은 속성 시스템에서 선언 하는 논리에 따라 값을 강제 변환 하는 데 사용 되지만 로컬로 설정 된 속성의 강제 변환 된 값은 "desired value"를 내부적으로 유지 합니다. 제약 조건이 애플리케이션 수명 동안 동적으로 변경될 수 있는 다른 속성 값을 기반으로 하는 경우 강제 변환 제약 조건도 동적으로 변경되며 제한된 속성은 원하는 값에 최대한 가깝게 값을 변경하여 새 제약 조건을 제공할 수 있습니다. 모든 제약 조건이 적용되면 해당 값은 원하는 값이 됩니다. 여러 속성이 순환 방식으로 서로 종속되어 있는 경우 다소 복잡한 종속성 시나리오를 도입할 수 있습니다. 예를 들어 Min/Max/Current 시나리오에서 최소값과 최대값을 사용자가 설정할 수 있도록 선택할 수 있습니다. 그렇다면 최대값이 항상 최소값보다 크거나 그 반대가 되도록 강제 변환해야 할 수 있습니다. 그러나 해당 강제 변환이 활성화되고 최대값이 최소값으로 강제 변환되면 현재 값은 두 값에 종속되어 있고 두 값 사이의 범위(0)로 제한되기 때문에 설정할 수 없는 상태로 유지됩니다. 그런 다음 최대값이나 최소값을 조정하면 현재 값의 원하는 값이 계속 저장되고 제약 조건이 완화되면 원하는 값에 도달하려고 시도하기 때문에 현재 값은 두 값 중 하나를 "따르는" 것처럼 보입니다.  
  
 복잡한 종속성에서 기술적으로 잘못된 것은 없지만 많은 재계산이 필요한 경우 성능이 약간 저하될 수 있으며 UI에 직접 영향을 주는 경우 사용자에게 혼동을 줄 수도 있습니다. 속성 변경 및 강제 값 콜백을 사용할 때는 주의해야 하며 시도하려는 강제 변환이 최대한 명확하게 처리되고 "지나치게 제약"하지 않도록 해야 합니다.  
  
### <a name="using-coercevalue-to-cancel-value-changes"></a>CoerceValue를 사용하여 값 변경 내용 취소  
 속성 시스템은 특수 한 경우 <xref:System.Windows.CoerceValueCallback> 에 값 <xref:System.Windows.DependencyProperty.UnsetValue> 을 반환 하는 모든를 처리 합니다. 이 특수 한 경우는를 <xref:System.Windows.CoerceValueCallback> 호출 하는 속성 변경이 속성 시스템에서 거부 되어야 하 고 속성 시스템은 속성에서 이전의 모든 값을 보고 해야 함을 의미 합니다. 이 메커니즘은 비동기적으로 시작된 속성의 변경 내용이 현재 개체 상태에 여전히 유효한지 확인하고 유효하지 않을 경우 변경 내용을 무시하는 데 유용할 수 있습니다. 다른 가능한 시나리오에서는 보고할 값을 담당하는 속성 값 결정의 구성 요소에 따라 선택적으로 값을 무시할 수 있습니다. 이렇게 하려면 콜백에 <xref:System.Windows.DependencyProperty> 전달 된와 속성 식별자를에 대 한 <xref:System.Windows.DependencyPropertyHelper.GetValueSource%2A>입력으로 사용한 다음를 <xref:System.Windows.ValueSource>처리할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [종속성 속성 개요](dependency-properties-overview.md)
- [종속성 속성 메타데이터](dependency-property-metadata.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
