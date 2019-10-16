---
title: 애플리케이션 설정 특성
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], attributes
- attributes [Windows Forms], application settings
- wrapper classes [Windows Forms], application settings
ms.assetid: 53caa66c-a9fb-43a5-953c-ad092590098d
ms.openlocfilehash: b38ed931cab3a333a56dd027d5843b1c8f00dcb9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916675"
---
# <a name="application-settings-attributes"></a>애플리케이션 설정 특성
응용 프로그램 설정 아키텍처는 응용 프로그램 설정 래퍼 클래스 또는 개별 속성에 적용 될 수 있는 여러 특성을 제공 합니다. 이러한 특성은 런타임에 응용 프로그램 설정 인프라 (특히 설정 공급자)에 의해 검사 되 고, 사용자 지정 래퍼의 명시 된 요구에 맞게 조정 됩니다.  
  
 다음 표에서는 응용 프로그램 설정 래퍼 클래스,이 클래스의 개별 속성 또는 둘 다에 적용할 수 있는 특성을 보여 줍니다. 정의에 따라 각 및 모든 설정 속성에 단일 범위 특성 (**system.configuration.userscopedsettingattribute>** 또는 **ApplicationScopedSettingAttribute**)만 적용 해야 합니다.  
  
> [!NOTE]
> <xref:System.Configuration.SettingsProvider> 클래스에서 파생 된 사용자 지정 설정 공급자는 다음 세 가지 특성을 인식 하는 데에만 필요 합니다. **ApplicationScopedSettingAttribute**, **System.configuration.userscopedsettingattribute>** 및 **defaultsettingvalueattribute**입니다.  
  
|특성|대상|설명|  
|---------------|------------|-----------------|  
|<xref:System.Configuration.SettingsProviderAttribute>|Both|지 속성에 사용할 설정 공급자의 짧은 이름을 지정 합니다.<br /><br /> 이 특성을 지정 하지 않으면 기본 공급자 <xref:System.Configuration.LocalFileSettingsProvider>인가 가정 됩니다.|  
|<xref:System.Configuration.UserScopedSettingAttribute>|Both|속성을 사용자 범위 응용 프로그램 설정으로 정의 합니다.|  
|<xref:System.Configuration.ApplicationScopedSettingAttribute>|Both|응용 프로그램 범위 응용 프로그램 설정으로 속성을 정의 합니다.|  
|<xref:System.Configuration.DefaultSettingValueAttribute>|속성|공급자가이 속성에 대 한 하드 코딩 된 기본값으로 deserialize 할 수 있는 문자열을 지정 합니다.<br /><br /> 에 <xref:System.Configuration.LocalFileSettingsProvider> 는이 특성이 필요 하지 않으며, 이미 지속 된 값이 있는 경우이 특성이 제공 하는 모든 값을 재정의 합니다.|  
|<xref:System.Configuration.SettingsDescriptionAttribute>|속성|런타임 및 디자인 타임 도구에서 주로 사용 되는 개별 설정에 대 한 설명이 포함 된 테스트를 제공 합니다.|  
|<xref:System.Configuration.SettingsGroupNameAttribute>|클래스|설정 그룹에 대 한 명시적 이름을 제공 합니다. 이 특성이 없는 <xref:System.Configuration.ApplicationSettingsBase> 경우는 래퍼 클래스 이름을 사용 합니다.|  
|<xref:System.Configuration.SettingsGroupDescriptionAttribute>|클래스|런타임 및 디자인 타임 도구에서 주로 사용 되는 설정 그룹에 대 한 설명이 포함 된 테스트를 제공 합니다.|  
|<xref:System.Configuration.SettingsManageabilityAttribute>|Both|설정 그룹 또는 속성에 제공 해야 하는 관리 서비스를 0 개 이상 지정 합니다. 사용 가능한 서비스는 <xref:System.Configuration.SettingsManageability> 열거형에서 설명 합니다.|  
|<xref:System.Configuration.SpecialSettingAttribute>|속성|설정이 설정 공급자에의 한 특수 처리를 제안 하는 연결 문자열과 같은 미리 정의 된 특수 범주에 속하도록 지정 합니다. 이 특성에 대해 미리 정의 된 범주는 <xref:System.Configuration.SpecialSetting> 열거형에 의해 정의 됩니다.|  
|<xref:System.Configuration.SettingsSerializeAsAttribute>|Both|설정 그룹 또는 속성에 대해 기본 설정 된 serialization 메커니즘을 지정 합니다. 사용 가능한 serialization 메커니즘은 <xref:System.Configuration.SettingsSerializeAs> 열거형에 의해 정의 됩니다.|  
|<xref:System.Configuration.NoSettingsVersionUpgradeAttribute>|속성|설정 공급자가 표시 된 속성에 대 한 모든 응용 프로그램 업그레이드 기능을 사용 하지 않도록 지정 합니다.|  
  
 *클래스* 는 특성이 응용 프로그램 설정 래퍼 클래스에만 적용 될 수 있음을 나타냅니다. *속성* 은 특성을 설정 속성에만 적용할 수 있음을 나타냅니다. *두 수준 모두* 에서 특성을 적용할 수 있음을 나타냅니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.SettingsProvider>
- [응용 프로그램 설정 아키텍처](application-settings-architecture.md)
- [방법: 응용 프로그램 설정 만들기](how-to-create-application-settings.md)
