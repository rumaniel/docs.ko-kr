---
title: <disableFusionUpdatesFromADManager> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- disableFusionUpdatesFromADManager element
- <disableFusionUpdatesFromADManager> element
ms.assetid: 58d2866c-37bd-4ffa-abaf-ff35926a2939
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b65711ad8c404d1c4f54a6197faf598e2215226f
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252659"
---
# <a name="disablefusionupdatesfromadmanager-element"></a>\<disableFusionUpdatesFromADManager > 요소
런타임 호스트가 애플리케이션 도메인에 대한 구성 설정을 재정의할 수 있도록 허용하는 기본 동작을 사용하지 않도록 설정할지를 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<disableFusionUpdatesFromADManager>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<disableFusionUpdatesFromADManager enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|사용|필수 특성입니다.<br /><br /> Fusion 설정을 재정의 하는 기본 기능을 사용할 수 없는지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|0|Fusion 설정을 재정의 하는 기능을 사용 하지 않도록 설정 하지 마십시오. 이는 .NET Framework 4부터 시작 하는 기본 동작입니다.|  
|1|Fusion 설정을 재정의 하는 기능을 사용 하지 않도록 설정 합니다. 이는 이전 버전의 .NET Framework 동작으로 되돌아갑니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 4부터 기본 동작은 구현에 전달 <xref:System.AppDomainManager> 되는 <xref:System.AppDomainSetup> 개체의 <xref:System.AppDomainSetup.ConfigurationFile%2A> 속성 또는 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 메서드를 사용 하 여 개체가 구성 설정을 재정의할 수 있도록 하는 것입니다. 메서드의는의 <xref:System.AppDomainManager>서브 클래스에 있습니다. <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=nameWithType> 기본 응용 프로그램 도메인의 경우 변경 하는 설정이 응용 프로그램 구성 파일에 지정 된 설정을 재정의 합니다. 다른 응용 프로그램 도메인의 경우 <xref:System.AppDomainManager.CreateDomain%2A?displayProperty=nameWithType> 또는 <xref:System.AppDomain.CreateDomain%2A?displayProperty=nameWithType> 메서드에 전달 된 구성 설정을 재정의 합니다.  
  
 새 구성 정보를 전달 하거나 null (`Nothing` Visual Basic)을 전달 하 여 전달 된 구성 정보를 제거할 수 있습니다.  
  
 구성 정보 <xref:System.AppDomainSetup.ConfigurationFile%2A> 를 속성과 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 메서드에 전달 하지 마십시오. 구성 정보를 둘 다에 전달 하는 경우 <xref:System.AppDomainSetup.ConfigurationFile%2A> <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 메서드가 응용 프로그램 구성 파일에서 구성 정보를 재정의 하기 때문에 속성에 전달 하는 정보는 무시 됩니다. 속성을 사용 하 <xref:System.AppDomainSetup.ConfigurationFile%2A> 는 경우 <xref:System.AppDomainSetup.SetConfigurationBytes%2A> 메서드에 null (`Nothing` Visual Basic)을 전달 하 여 <xref:System.AppDomainManager.CreateDomain%2A?displayProperty=nameWithType> 또는 <xref:System.AppDomain.CreateDomain%2A?displayProperty=nameWithType> 메서드에 대 한 호출에 지정 된 모든 구성 바이트를 제거할 수 있습니다.  
  
 구성 정보 <xref:System.AppDomainSetup> 외에도, <xref:System.AppDomainSetup.ApplicationBase%2A> <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=nameWithType> <xref:System.AppDomainSetup.ApplicationName%2A>, ,<xref:System.AppDomainSetup.DisallowApplicationBaseProbing%2A>, 메서드의구현에전달되는개체에서다음설정을변경할수있습니다.<xref:System.AppDomainSetup.DisallowBindingRedirects%2A> <xref:System.AppDomainSetup.CachePath%2A> <xref:System.AppDomainSetup.DisallowCodeDownload%2A> <xref:System.AppDomainSetup.DisallowPublisherPolicy%2A> ,,<xref:System.AppDomainSetup.ShadowCopyFiles%2A>,,,,, 및가 있습니다. <xref:System.AppDomainSetup.DynamicBase%2A> <xref:System.AppDomainSetup.LoaderOptimization%2A> <xref:System.AppDomainSetup.PrivateBinPath%2A> <xref:System.AppDomainSetup.PrivateBinPathProbe%2A> <xref:System.AppDomainSetup.ShadowCopyDirectories%2A>  
  
 `<disableFusionUpdatesFromADManager>` 요소를 사용 하는 대신 레지스트리 설정을 만들거나 환경 변수를 설정 하 여 기본 동작을 사용 하지 않도록 설정할 수 있습니다. 레지스트리에서 또는 `COMPLUS_disableFusionUpdatesFromADManager` 아래`HKLM\Software\Microsoft\.NETFramework`에 라는 DWORD 값을 만들고 값을 1로 설정 합니다. `HKCU\Software\Microsoft\.NETFramework` 명령줄에서 환경 변수 `COMPLUS_disableFusionUpdatesFromADManager` 를 1로 설정 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 요소를 `<disableFusionUpdatesFromADManager>` 사용 하 여 Fusion 설정을 재정의 하는 기능을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <disableFusionUpdatesFromADManager enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [런타임에서 어셈블리를 찾는 방법](../../../deployment/how-the-runtime-locates-assemblies.md)
