---
title: mc:ProcessContent 특성
ms.date: 03/30/2017
helpviewer_keywords:
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: 2689b2c8-b4dc-4b71-b9bd-f95e619122d7
ms.openlocfilehash: e625d99cdb30368a798b4829d103f8f26b2c9274
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991862"
---
# <a name="mcprocesscontent-attribute"></a>mc:ProcessContent 특성
[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [Mc: Ignorable 특성](mc-ignorable-attribute.md)을 지정 하 여 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서에서 직계 부모 요소를 무시할 수 있는 경우에도 관련 부모 요소에 의해 처리 되는 콘텐츠를 계속 포함 해야 하는 요소를 지정 합니다. 특성 `mc:ProcessContent` 은 사용자 지정 네임 스페이스 매핑과 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 버전 관리에 대 한 태그 호환성을 모두 지원 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...  
  mc:ProcessContent="ignorablePrefix:ThisElementCanBeIgnored"  
>  
    <ignorablePrefix:ThisElementCanBeIgnored>  
        [content]  
    </ignorablePrefix:ThisElementCanBeIgnored>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|*ignorablePrefix*|XML 1.0 사양에 따라 유효한 접두사 문자열입니다.|  
|*ignorableUri*|XML 1.0 사양에 따라 네임 스페이스를 지정 하는 데 사용할 수 있는 모든 유효한 URI입니다.|  
|*ThisElementCanBeIgnored*|내부 형식을 확인할 수 없는 경우 프로세서 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 구현에서 무시할 수 있는 요소입니다.|  
|*[content]*|*ThisElementCanBeIgnored* 은 무시할 수 있는 것으로 표시 됩니다. 프로세서에서 해당 요소를 무시 하면 *[content]* 는 *개체*에 의해 처리 됩니다.|  
  
## <a name="remarks"></a>설명  
 기본적으로 프로세서는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 무시 된 요소 내의 콘텐츠를 무시 합니다. 를 기준 `mc:ProcessContent`으로 특정 요소를 지정할 수 있으며, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서는 무시 된 요소 내에서 콘텐츠를 계속 처리 합니다. 이는 일반적으로 콘텐츠가 여러 태그 내에 중첩 되어 있고, 하나 이상의 태그를 무시할 수 있으며,이 중 하나 이상이 무시할 수 없는 경우에 사용 됩니다.  
  
 공백 구분 기호를 사용 하 여 특성에 여러 접두사를 지정할 수 있습니다 (예 `mc:ProcessContent="ignore:Element1 ignore:Element2"`:).  
  
 네임 `http://schemas.openxmlformats.org/markup-compatibility/2006` 스페이스는 SDK의이 영역에 문서화 되지 않은 다른 요소 및 특성을 정의 합니다. 자세한 내용은 [XML 태그 호환성 사양](https://go.microsoft.com/fwlink/?LinkId=73824)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [mc:Ignorable 특성](mc-ignorable-attribute.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
