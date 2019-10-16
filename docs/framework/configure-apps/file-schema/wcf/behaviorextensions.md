---
title: <behaviorExtensions>
ms.date: 03/30/2017
ms.assetid: 59f2791a-c78f-40d7-aa80-0d9cd10135d9
ms.openlocfilehash: bcf1f1dcdba50c3e7fba8eb170132d0cf47c4271
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919810"
---
# <a name="behaviorextensions"></a>\<behaviorExtensions>
동작 확장을 사용하면 사용자 정의 동작 요소를 만들 수 있습니다. 이러한 요소는 표준 WCF(Windows Communication Foundation) 동작 요소 구성과 함께 사용할 수 있습니다. `behaviorExtensions` 섹션은 구성에 사용할 수 있도록 요소를 정의합니다. 다음은 일반적인 동작 확장 예제입니다.  
  
```xml  
<system.serviceModel>
  <extensions>
    <behaviorExtensions>
      <add name="myBehavior"
           type="Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </behaviorExtensions>
  </extensions>
</system.serviceModel>
```  
  
 요소에 구성 기능을 추가하려면 구성 요소를 작성하고 등록해야 합니다. 이에 대한 자세한 내용은 <xref:System.Configuration> 설명서를 참조하세요.  
  
 요소 및 해당 구성 형식이 정의되면 다음 예제와 같이 확장을 사용할 수 있습니다.  
  
```xml  
<behaviors>
  <behavior configurationName="testChannelBehavior">
    <myBehavior />
    <channelSecurity cacheCookies="false"
                     detectReplays="false"
                     maxCachedNonces="9"
                     maxClockSkew="00:00:03"
                     maxCookieCachingTime="00:07:24"
                     replayWindow="00:07:22.2190000" />
  </behavior>
</behaviors>
```  
  
## <a name="security"></a>보안  
 `machine.config` 및 `app.config` 파일에 형식을 등록할 때는 정규화된 어셈블리 이름을 사용할 것을 강력히 권장합니다. 형식이 고유하게 정의되지 않으면 CLR 형식 로더는 다음 위치에서 지정한 순서로 형식을 검색합니다.  
  
 형식의 어셈블리를 알 수 있으면 로더는 구성 파일의 리디렉션 위치, GAC, 현재 어셈블리(구성 정보 사용) 및 애플리케이션 기본 디렉터리를 검색합니다. 어셈블리를 알 수 없으면 로더는 현재 어셈블리, mscorlib 및 `TypeResolve` 이벤트 처리기가 반환한 위치를 검색합니다. CLR 검색 순서는 형식 전달 메커니즘 및 AppDomain.TypeResolve 이벤트와 같은 후크로 수정할 수 있습니다.  
  
 공격자는 CLR 검색 순서를 탐색하고 허가되지 않은 코드를 실행할 수 있습니다. 정규화된(강력한) 이름을 사용하면 형식이 고유하게 식별되며 시스템 보안이 강화됩니다.  
  
 자세한 내용은 [런타임에서 어셈블리를 찾는 방법](https://go.microsoft.com/fwlink/?LinkId=95336) 및 <xref:System.AppDomain.TypeResolve>을 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>
- [동작을 사용하여 런타임 구성 및 확장](../../../wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)
