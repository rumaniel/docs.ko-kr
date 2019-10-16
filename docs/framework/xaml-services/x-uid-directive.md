---
title: x:Uid 지시문
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], localizable content attribute
- XAML [XAML Services], x:Uid attribute
- x:Uid attribute [XAML Services]
- Uid attribute [XAML Services]
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
ms.openlocfilehash: c8f0580c987b87193b5b6a38559043e50fc7cb89
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938842"
---
# <a name="xuid-directive"></a>x:Uid 지시문
태그 요소에 대 한 고유 식별자를 제공합니다. 대부분의 시나리오에서이 고유 식별자는 XAML 지역화 프로세스와 도구에서 사용 됩니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object x:Uid="identifier"... />  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`identifier`|수동으로 만든 또는으로 해석 될 때 파일에서 고유 해야 하는 자동으로 생성 된 문자열을 `x:Uid` 소비자입니다.|  
  
## <a name="remarks"></a>설명  
 [MS-XAML]에서 `x:Uid` 지시문으로 정의 됩니다. 자세한 내용은 [ \[MS XAML\] 5.3.6 섹션](https://go.microsoft.com/fwlink/?LinkId=114525)합니다.  
  
 `x:Uid` 불연속 `x:Name` 명시 된 XAML 지역화 시나리오를 때문에 모두 지역화에 사용 되는 식별자의 프로그래밍 모델 의미에 대 한 종속성이 없는 되도록 `x:Name`합니다. 그러나 또한 `x:Name` XAML 이름 범위;에 의해 관리 됩니다 `x:Uid` 고유성이 적용의 모든 XAML 정의 된 언어 개념의 적용을 받지 않는 합니다. (지역화 프로세스의 일부분이 아닌 프로세서)는 넓은 의미에서 XAML 프로세서의 고유성을 강제 적용 되지 않는 `x:Uid` 값입니다. 해당 책임 값의 출처 개념적으로 켜져 있습니다. 고유성을 기대 `x:Uid` 전용된 세계화 프로세스나 도구와 같은 값의 소비자에 대 한 적절 한 값은 단일 XAML 소스 내 값입니다. 일반적인 고유성 모델 `x:Uid` 값은 XAML을 나타내는 XML로 인코딩된 파일 내에서 고유 합니다.  
  
 도구에 게 중요 한 지식이 특정 XAML 스키마를 적용 하도록 선택할 수 `x:Uid` 에 대해서만 지역화 가능한 문자열 대신 텍스트 문자열 값을 태그에서 발생 하는 모든 경우에 대해 true를 반환 합니다.  
  
 프레임 워크에 대 한 별칭이 되도록 해당 개체 모델에서 특정 속성을 지정할 수 있습니다 `x:Uid` 특성을 적용 하 여 <xref:System.Windows.Markup.UidPropertyAttribute> 정의 형식입니다. 프레임 워크는 특정 속성을 지정 하는 경우 유효 하지 않은 두 가지 다 지정할 `x:Uid` 와 같은 개체에 별칭이 지정 된 멤버입니다. 둘 다 `x:Uid` 별칭이 지정 된 멤버는 지정 된,.NET Framework XAML 서비스 API는 일반적으로 throw <xref:System.Xaml.XamlDuplicateMemberException> 이 사례에 대 한 합니다.  
  
## <a name="wpf-usage-notes"></a>WPF 사용 정보  
 역할에 대 한 자세한 내용은 `x:Uid` WPF 지역화 프로세스와 XAML의 BAML 양식에서 참조 [WPF의 전역화](../wpf/advanced/globalization-for-wpf.md) 또는 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>
- <xref:Microsoft.Build.Tasks.Windows.UidManager>
- [WPF의 전역화](../wpf/advanced/globalization-for-wpf.md)
