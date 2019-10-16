---
title: x:Members 지시문
ms.date: 03/30/2017
ms.assetid: 155b393d-3b49-4c5a-8c9e-b3d9893af4e4
ms.openlocfilehash: ca42079c1c40a8fb3b1ddfc8f4a6f742768fa9e1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053763"
---
# <a name="xmembers-directive"></a>x:Members 지시문
부모 요소의 x:Class에 적용 되는 태그에 정의 된 멤버 집합을 보유 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object x:Class="className">  
  <x:Members>  
    oneOrMoreMembers  
  </x:Members  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`className`|XAML 프로덕션에 대한 지원 클래스 또는 partial 클래스의 이름입니다. 설명 부분을 참조하세요.|  
|`oneOrMoreMembers`|멤버 정의를 나타내는 하나 이상의 개체 요소입니다. 일반적으로 이러한 요소 `x:Property` 는 개체 요소입니다. 설명 부분을 참조하세요.|  
  
## <a name="remarks"></a>설명  
 .NET Framework XAML 서비스 구현에는에 대 한 `x:Members`지원 클래스 또는 기본 멤버 구현이 없습니다. `x:Members`는 모든 형식의 멤버로 존재할 수 있는 특수 한 XAML 멤버입니다. Xaml 노드 스트림에서 `x:Members` 는 xaml 언어 xaml 네임 스페이스에서 라는 `Members`멤버로 표현 됩니다. 멤버 `Members` 는 개체의 `Member` 읽기 전용 제네릭 목록을 포함 합니다. 일반적인 태그에서 개별 멤버는 `x:Property` 속성 요소로 지정 됩니다. `x:Property`는 형식의 속성에 대 한 보다 정확한 형식이 며에 `x:Member`할당할 수 있습니다. 자세한 내용은 [X:property 지시문](x-property-directive.md)을 참조 하세요.  
  
 태그로 멤버 정의를 지정하기 위한 수단으로서 `x:Members`의 실제 사용을 지원하려면 멤버가 수정할 수 있는 클래스와 연결되어야 합니다. 의도한 모델은 `x:Members`가 `x:Class`를 지정하는 형식의 멤버로 존재하는 것입니다. 그러나 형식 및 멤버를 연결하거나 동적 멤버 정의를 생성하기 위한 메커니즘은 .NET Framework XAML 서비스 수준에서 지원되지 않습니다. 이 작업은 XAML의 멤버 정의를 지원하는 애플리케이션 모델이 있는 개별 프레임워크에서 수행해야 합니다. 일반적으로 해당 기능을 지원하려면 XAML을 태그로 컴파일하고 코드 숨김과 통합하거나 XAML 어셈블리에서만 생성하는 MSBUILD 빌드 작업이 필요합니다.  
  
## <a name="xmembers-for-windows-workflow-foundation"></a>Windows Workflow Foundation에 대 한 x:Members  
 Windows Workflow Foundation의 경우 `x:Members` xaml로 완전히 구성 된 사용자 지정 활동의 멤버 또는 코드 숨김으로 활동 디자이너에 대해 xaml로 정의 된 동적 멤버를 포함 합니다. 또한 XAML 프로덕션의 루트 요소에 `x:Class`를 지정해야 합니다. 이는 .NET Framework XAML 서비스 수준에서의 요구 사항은 아니지만 사용자 지정 활동과 Windows Workflow Foundation XAML을 일반적으로 지원하는 MSBUILD 빌드 작업에 의해 XAML 프로덕션이 로드될 때 요구 사항이 됩니다. `x:Members`는를 `x:Class`선언 하는 개체 요소의 태그에서 첫 번째 자식 요소 여야 합니다.
