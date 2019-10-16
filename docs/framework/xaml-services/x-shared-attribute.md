---
title: x:Shared 특성
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], x:Shared attribute
- x:Shared attribute [XAML Services]
- Shared attribute in XAML [XAML Services]
ms.assetid: c8cff434-2785-405f-9f95-16deb34c9e64
ms.openlocfilehash: 0e9003f22c488ec35f7cc9c7be7f72c7fb8241df
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622777"
---
# <a name="xshared-attribute"></a>x:Shared 특성
로 설정 하면 `false`, 요청 특성 사용된 하는 리소스에 대 한 모든 요청에 대해 동일한 인스턴스를 공유 하는 대신 각 요청에 대 한 새 인스턴스를 만들 수 있도록 WPF 리소스 검색 동작을 수정 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<ResourceDictionary>  
  <object x:Shared="false".../>  
</ResourceDictionary>  
```  
  
## <a name="remarks"></a>설명  
 `x:Shared` XAML 언어 XAML 네임 스페이스에 매핑되고.NET Framework XAML 서비스 및 해당 XAML 판독기에서 유효한 XAML 언어 요소로 인식 됩니다. 그러나 명시 된 기능의 `x:Shared` 만 WPF XAML 파서 및 WPF 응용 프로그램에 적용 됩니다. Wpf에서는 `x:Shared` 유용만 특성으로 WPF 내에 존재 하는 개체에 적용 되는 경우 <xref:System.Windows.ResourceDictionary>합니다. 다른 용도의 구문 분석 예외 또는 기타 오류를 throw 하지 않습니다 하지만 영향을 주지 않습니다.  
  
 의미를 `x:Shared` XAML 언어 사양에 지정 되지 않은 합니다. .NET Framework XAML 서비스를 빌드하는 것과 같은 다른 XAML 구현 지원 리소스 공유를 반드시 제공 하지 않습니다. 이러한 XAML 구현 에서도 지 원하는 프레임 워크에서 유사한 동작을 제공할 수 있습니다 `x:Shared` 값입니다.  
  
 Wpf에서 기본값 `x:Shared` 리소스에 대 한 조건은 `true`합니다. 이 조건이 의미 하는 모든 리소스 요청이 항상 동일한 인스턴스를 반환 합니다.  
  
 와 같은 리소스 API 통해 반환 되는 개체를 수정 <xref:System.Windows.FrameworkElement.FindResource%2A>, 내에서 직접 개체를 수정 하거나는 <xref:System.Windows.ResourceDictionary>을 원래 리소스를 변경 합니다. 해당 리소스에 대 한 참조의 동적 리소스 참조 인 경우 해당 리소스의 소비자가 변경 된 리소스를 가져옵니다.  
  
 리소스에 대 한 참조는 정적 리소스 참조 인 경우 변경 후 리소스 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 처리 시간 관련이 없습니다. 정적 및 동적 리소스 참조에 대 한 자세한 내용은 참조 하세요. [XAML 리소스](../wpf/advanced/xaml-resources.md)합니다.  
  
 명시적으로 지정 `x:Shared="true"` 작업이 거의 완료 기본 이미 이므로 합니다. 에 대 한 해당 직접 코드가 없는 `x:Shared` WPF에서 개체 모델; XAML 사용량에서만 지정할 수 있습니다 하 고 처리 해야 기본 WPF 동작에 의해 또는 로드 경로에서 중간 XAML 노드 스트림에서.NET Framework XAML Se를 사용 하 여 처리 하는 경우 서비스 및 해당 XAML 판독기입니다.  
  
 에 대 한 시나리오 `x:Shared="false"` 정의 하는 경우는 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement> 리소스로 클래스를 파생 하 고 다음 콘텐츠 모델에 요소 리소스를 도입 하 합니다. `x:Shared="false"` 동일한 컬렉션에 여러 번 시켜야 요소 리소스를 사용 하도록 설정 (예를 <xref:System.Windows.Controls.UIElementCollection>). 없이 `x:Shared="false"` 이 없기 때문에 컬렉션은 해당 내용의 고유성을 적용 합니다. 그러나는 `x:Shared="false"` 동작은 동일한 인스턴스를 반환 하는 대신 리소스의 다른 동일한 인스턴스를 만듭니다.  
  
 다른 시나리오에 대 한 `x:Shared="false"` 사용 하는 경우는 <xref:System.Windows.Freezable> 애니메이션 값 이지만 애니메이션 별로에서 리소스를 수정 하려면에 대 한 리소스입니다.  
  
 문자열 처리 `false` 대/소문자 구분 아닙니다.  
  
 Wpf에서 `x:Shared` 다음 조건 에서만 유효 합니다.  
  
- 합니다 <xref:System.Windows.ResourceDictionary> 인 항목을 포함 하는 `x:Shared` 컴파일해야 합니다. <xref:System.Windows.ResourceDictionary> 테마에 대 한 하거나 느슨한 XAML 내에서 사용할 수 없습니다.  
  
- <xref:System.Windows.ResourceDictionary> 항목이 포함 된 다른 내에 중첩 되어야 하지 <xref:System.Windows.ResourceDictionary>합니다. 예를 들어 사용할 수 없습니다 `x:Shared` 항목에 대 한는 <xref:System.Windows.ResourceDictionary> 내는 <xref:System.Windows.Style> 는 이미는 <xref:System.Windows.ResourceDictionary> 항목입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.ResourceDictionary>
- [XAML 리소스](../wpf/advanced/xaml-resources.md)
- [기본 요소](../wpf/advanced/base-elements.md)
