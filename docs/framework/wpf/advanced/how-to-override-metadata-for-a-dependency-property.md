---
title: '방법: 종속성 속성에 대한 메타데이터 재정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- metadata [WPF], overriding for dependency properties
- dependency properties [WPF], overriding metadata for
- overriding metadata for dependency properties [WPF]
ms.assetid: f90f026e-60d8-428a-933d-edf0dba4441f
ms.openlocfilehash: ef0309ae0d03c8278134012e645960996c6f93c4
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67610503"
---
# <a name="how-to-override-metadata-for-a-dependency-property"></a>방법: 종속성 속성에 대한 메타데이터 재정의
호출 하 여 상속된 된 클래스에서 제공 되는 기본 종속성 속성 메타 데이터를 재정의 하는 방법을 보여 주는이 예제는 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 메서드와 형식별 메타 데이터를 제공 합니다.  
  
## <a name="example"></a>예제  
 정의 하 여 해당 <xref:System.Windows.PropertyMetadata>, 클래스의 기본 값 및 속성 시스템 콜백과 같은 종속성 속성의 동작을 정의할 수 있습니다. 여러 종속성 속성 클래스에는 이미 등록 프로세스의 일부로 설정된 기본 메타데이터가 있습니다. 여기에 포함 된 종속성 속성은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API. 해당 클래스 상속을 통해 종속성 속성을 상속받는 클래스에서는 원래 메타데이터를 재정의할 수 있으므로 메타데이터를 통해 변경할 수 있는 속성의 특성이 모든 서브클래스별 요구 사항과 일치합니다.  
  
 종속성 속성에 대한 메타데이터의 재정의는 속성 시스템이 해당 속성을 사용하기 전에 수행되어야 합니다(속성을 등록하는 개체의 특정 인스턴스가 인스턴스화되는 시간과 같은 것으로 간주). 에 대 한 호출 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 서 자신을 제공 하는 형식의 정적 생성자 내에서 수행 해야 합니다 `forType` 의 매개 변수 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>. 소유자 형식의 인스턴스가 존재하는 메타데이터를 변경하려고 하면 예외가 발생하지는 않지만 속성 시스템에서 일관성 없는 동작이 발생합니다. 또한 메타데이터 형식별로 한 번만 재정의할 수 있습니다. 동일한 형식의 메타데이터를 이어서 재정의하려고 하면 예외가 발생합니다.  
  
 다음 예제에서는 사용자 정의 클래스 `MyAdvancedStateControl`은 `MyAdvancedStateControl`에 의해 `StateProperty`에 제공된 메타데이터를 새 속성 메타데이터로 재정의합니다. 예를 들어 새로 생성된 `MyAdvancedStateControl` 인스턴스에서 속성을 쿼리하면 `StateProperty`의 기본값이 `true`가 됩니다.  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#MyAdvancedStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#myadvancedstatecontrol)]
[!code-vb[PropertySystemEsoterics#MyAdvancedStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#myadvancedstatecontrol)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.DependencyProperty>
- [종속성 속성 개요](dependency-properties-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
- [방법 항목](properties-how-to-topics.md)
