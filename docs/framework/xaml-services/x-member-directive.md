---
title: x:Member 지시문
ms.date: 03/30/2017
ms.assetid: 4d8394ef-644c-4331-b6c5-be855d392980
ms.openlocfilehash: d3d023873aab2039913a78108440a2e2d4ea77fb
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053737"
---
# <a name="xmember-directive"></a>x:Member 지시문
태그로 XAML 멤버를 선언합니다.  
  
## <a name="xaml-object-element-usage"></a>XAML 개체 요소 사용  
  
```xaml  
<object x:Class="className">  
  <x:Members>  
    <x:Member Name="propertyName"/>  
    additionalMembers  
  </x:Members>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`className`|XAML 프로덕션에 대한 지원 클래스 또는 partial 클래스의 이름입니다.|  
|`memberName`|정의되는 속성의 멤버 이름입니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework XAML 서비스 구현에서 `x:Member`는 직접적인 형식 지원이 없지만 <xref:System.Windows.Markup.MemberDefinition> 클래스에 의해 지원됩니다. XAML 노드 스트림에서 `x:Member` 요소는 XAML 언어 XAML 네임스페이스의 `Member`라는 멤버로 표시됩니다. `Member` 멤버는 태그로 선언된 특성을 보유합니다.  
  
 `Name` 및 `Type`의 의미는 .NET Framework XAML 서비스 수준에서 할당되지 않습니다. 나중에 특정 프레임워크에서 적용할 수 있는 규칙으로 해석되기 위해 초기 XAML 노드 스트림에 문자열 값으로 저장됩니다. 의미는 XAML 이름 및 XAML 형식 의미와 일치되거나, 구현에 따라 지원 형식 시스템에서만 유효할 수도 있습니다.  
  
 태그로 멤버 정의를 지정하기 위한 수단으로서 `x:Members`의 실제 사용을 지원하려면 멤버가 수정할 수 있는 클래스와 연결되어야 합니다. 의도한 모델은 `x:Members`가 `x:Class`를 지정하는 형식의 멤버로 존재하는 것입니다. 그러나 형식 및 멤버를 연결하거나 동적 멤버 정의를 생성하기 위한 메커니즘은 .NET Framework XAML 서비스 수준에서 지원되지 않습니다. 이 작업은 XAML의 멤버 정의를 지원하는 애플리케이션 모델이 있는 개별 프레임워크에서 수행해야 합니다. 일반적으로 해당 기능을 지원하려면 XAML을 태그로 컴파일하고 코드 숨김과 통합하거나 XAML 어셈블리에서만 생성하는 MSBUILD 빌드 작업이 필요합니다.  
  
## <a name="xproperty-for-windows-workflow-foundation"></a>Windows Workflow Foundation에 대한 x:Property  
 Windows Workflow Foundation에서 `x:Property`는 XAML로만 작성된 사용자 지정 활동의 멤버 또는 코드 숨김을 사용하여 활동 디자이너에 대해 XAML로 정의된 동적 멤버를 정의합니다. 또한 XAML 프로덕션의 루트 요소에 `x:Class`를 지정해야 합니다. 이는 .NET Framework XAML 서비스 수준에서의 요구 사항은 아니지만 사용자 지정 활동과 Windows Workflow Foundation XAML을 일반적으로 지원하는 MSBUILD 빌드 작업에 의해 XAML 프로덕션이 로드될 때 요구 사항이 됩니다. Windows Workflow Foundation는 순수 XAML 형식 이름을 `x:Property` `Type` 특성에 대 한 의도 된 값으로 사용 하지 않으며, 대신 여기에 설명 되지 않은 규칙을 사용 합니다. 자세한 내용은 [DynamicActivity 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd807392(v=vs.100))를 참조 하세요.
