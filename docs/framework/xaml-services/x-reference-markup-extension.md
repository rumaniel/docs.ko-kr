---
title: x:Reference 태그 확장
ms.date: 03/30/2017
helpviewer_keywords:
- x:Reference markup extension [XAML Services]
- XAML [XAML Services], x:Reference Markup Extension
- Reference markup extension [XAML Services]
ms.assetid: 2982e68b-d26b-4aa3-826a-34c57a9c5199
ms.openlocfilehash: 960f5c0e4192df72090c1a571dfc2fc5e3fd8ba3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938881"
---
# <a name="xreference-markup-extension"></a>x:Reference 태그 확장
XAML 태그에 선언 된 인스턴스를 참조 합니다. 참조가 요소의 `x:Name`합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object property="{x:Reference instancexName}" .../>  
```  
  
## <a name="xaml-object-element-usage"></a>XAML 개체 요소 사용  
  
```xaml  
<object>  
  <object.property>  
    <x:Reference Name="instancexName"/>  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`instancexName`|`x:Name` 값 (또는 값을 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>-식별 된 속성) 참조 된 인스턴스.|  
  
## <a name="remarks"></a>설명  
 `x:Reference` WPF와 같은 특정 프레임 워크에서 구현 된 요소 참조 개념에 대 한 XAML 언어 수준 지원을 제공 합니다.  
  
## <a name="xreference-and-wpf"></a>X:reference 및 WPF  
 WPF 및 XAML 2006에서는 요소 참조의 프레임 워크 수준 기능을 통해 사항은 <xref:System.Windows.Data.Binding.ElementName%2A> 바인딩. 대부분의 WPF 응용 프로그램 및 시나리오에 대 한 <xref:System.Windows.Data.Binding.ElementName%2A> 바인딩을 사용 해야 합니다. 데이터 컨텍스트 또는 데이터 바인딩이 불가능 하는 다른 범위 지정 고려 하 고 태그 컴파일에 포함 되지 않습니다.이 일반 지침에 대 한 예외 사례를 포함할 수 있습니다.  
  
 `x:Reference` XAML 2009 년에 정의 된 구문입니다. WPF에서 XAML 2009 기능을 사용할 수 있지만 WPF 태그 컴파일된 XAML에만 사용할 수 있습니다. 태그 컴파일된 XAML 및 BAML 형식의 XAML은 현재 XAML 2009 언어 키워드 및 기능을 지원하지 않습니다.
