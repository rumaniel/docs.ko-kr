---
title: 컬렉션 형식 종속성 속성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties [WPF], dependency
- properties [WPF], collection-type
- dependency properties [WPF]
- collection-type properties [WPF]
ms.assetid: 99f96a42-3ab7-4f64-a16b-2e10d654e97c
ms.openlocfilehash: dd268c0c132f4ecefe7b2336432442d9569ca38f
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401564"
---
# <a name="collection-type-dependency-properties"></a>컬렉션 형식 종속성 속성
이 항목에서는 속성 형식이 컬렉션 형식인 종속성 속성을 구현하는 방법에 대한 지침과 제안된 패턴을 제공합니다.  

<a name="implementing"></a>   
## <a name="implementing-a-collection-type-dependency-property"></a>컬렉션 형식 종속성 속성 구현  
 일반적으로 종속성 속성의 경우, 수행 하는 구현 패턴은 CLR 속성 래퍼를 정의 하는 것입니다. 여기서 해당 속성은 필드 또는 <xref:System.Windows.DependencyProperty> 다른 구문이 아닌 식별자에 의해 지원 됩니다. 콜렉션 형식 속성을 구현할 때도 이와 동일한 패턴을 따릅니다. 그러나 컬렉션 형식 속성은 컬렉션 <xref:System.Windows.DependencyObject> 에 포함 된 형식이 또는 <xref:System.Windows.Freezable> 파생 클래스인 경우 항상 패턴의 복잡성을 제공 합니다.  
  
<a name="initializing"></a>   
## <a name="initializing-the-collection-beyond-the-default-value"></a>기본값 이외의 컬렉션 초기화  
 종속성 속성을 만들 때는 속성 기본값을 초기 필드 값으로 지정하지 않습니다. 대신 종속성 속성 메타데이터를 통해 기본값을 지정합니다. 속성이 참조 형식인 경우 종속성 속성 메타데이터에 지정된 기본값은 인스턴스별 기본값이 아니라 해당 형식의 모든 인스턴스에 적용되는 기본값입니다. 따라서 컬렉션 속성 메타데이터로 정의된 단일 정적 컬렉션을 형식에 대해 새로 만든 인스턴스의 작업 기본값으로 사용하지 않도록 주의해야 합니다. 대신 클래스 생성자 논리의 일부로서 의도적으로 컬렉션 값을 고유한(인스턴스) 컬렉션으로 설정해야 합니다. 그렇지 않으면 의도하지 않은 Singleton 클래스가 만들어집니다.  
  
 다음 예제를 살펴보십시오. 예제의 다음 섹션에서는 `Aquarium` 클래스에 대한 정의를 보여 줍니다. 클래스는 <xref:System.Windows.FrameworkElement> 형식 제약 조건과 함께 제네릭 <xref:System.Collections.Generic.List%601> 형식을 `AquariumObjects`사용 하는 컬렉션 형식 종속성 속성을 정의 합니다. 종속성 속성에 대 한 <xref:System.Collections.Generic.List%601> 호출에서메타데이터는기본값을새제네릭로설정합니다.<xref:System.Windows.DependencyProperty.Register%28System.String%2CSystem.Type%2CSystem.Type%2CSystem.Windows.PropertyMetadata%29>  
  
 [!code-csharp[PropertiesOvwSupport2#CollectionProblemDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport2/CSharp/page.xaml.cs#collectionproblemdefinition)]
 [!code-vb[PropertiesOvwSupport2#CollectionProblemDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport2/visualbasic/page.xaml.vb#collectionproblemdefinition)]  
  
 그러나 설명한 대로 코드를 방금 벗어나면 모든 `Aquarium` 인스턴스에서 단일 목록 기본값을 공유합니다. 두 개의 개별 `Aquarium` 인스턴스를 인스턴스화하고 각 인스턴스에 서로 다른 단일 `Fish`를 추가하는 방법을 보여 주는 다음 테스트 코드를 실행하면 놀라운 결과를 볼 수 있습니다.  
  
 [!code-csharp[PropertiesOvwSupport#CollectionProblemTestCode](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemtestcode)]
 [!code-vb[PropertiesOvwSupport#CollectionProblemTestCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemtestcode)]  
  
 각 콜렉션의 개수는 1이 아니라 2입니다! 이는 메타데이터의 단일 생성자 호출로 인해 각 `Aquarium`에서 해당 `Fish`를 기본값 컬렉션에 추가했기 때문이며, 이에 따라 모든 인스턴스 간에 공유됩니다. 이 상황은 결코 바람직한 작업이 아닙니다.  
  
 이 문제를 해결하려면 클래스 생성자 호출의 일부로 컬렉션 종속성 속성 값을 고유한 인스턴스로 다시 설정해야 합니다. 속성은 읽기 전용 종속성 속성 <xref:System.Windows.DependencyObject.SetValue%28System.Windows.DependencyPropertyKey%2CSystem.Object%29> 이므로 클래스 내 에서만 액세스할 수 <xref:System.Windows.DependencyPropertyKey> 있는를 사용 하 여 메서드를 설정 합니다.  
  
 [!code-csharp[PropertiesOvwSupport#CollectionProblemCtor](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemctor)]
 [!code-vb[PropertiesOvwSupport#CollectionProblemCtor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemctor)]  
  
 이제 동일한 테스트 코드를 다시 실행하면 각 `Aquarium`에서 자체의 고유한 컬렉션을 지원하는 예상 결과를 더 많이 볼 수 있습니다.  
  
 읽기/쓰기 컬렉션 속성이 되도록 선택한 경우 이 패턴에 약간의 변형이 있습니다. 이 경우 생성자에서 public set 접근자를 호출 하 여 초기화를 수행할 수 있으며,이는 공용 <xref:System.Windows.DependencyObject.SetValue%28System.Windows.DependencyProperty%2CSystem.Object%29> <xref:System.Windows.DependencyProperty> 식별자를 사용 하 여 집합 래퍼 내에서 키가 아닌 시그니처를 호출 합니다.  
  
## <a name="reporting-binding-value-changes-from-collection-properties"></a>컬렉션 속성에서 바인딩 값 변경 보고  
 자체적으로 종속성 속성인 콜렉션 속성은 변경 내용을 하위 속성에 자동으로 보고하지 않습니다. 컬렉션에 바인딩을 만들면 바인딩에서 변경 내용을 보고하지 못하도록 하여 일부 데이터 바인딩 시나리오가 무효화될 수 있습니다. 그러나 컬렉션 형식을 컬렉션 형식 <xref:System.Windows.FreezableCollection%601> 으로 사용 하는 경우 컬렉션의 포함 된 요소에 대 한 하위 속성 변경 내용이 제대로 보고 되 고 바인딩이 예상 대로 작동 합니다.  
  
 종속성 개체 컬렉션에서 하위 속성 바인딩을 사용 하려면 <xref:System.Windows.FreezableCollection%601> <xref:System.Windows.DependencyObject> 파생 클래스에 대 한 컬렉션 속성을 형식 제약 조건으로 만듭니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FreezableCollection%601>
- [WPF에 대한 XAML 및 사용자 지정 클래스](xaml-and-custom-classes-for-wpf.md)
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [종속성 속성 개요](dependency-properties-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
- [종속성 속성 메타데이터](dependency-property-metadata.md)
