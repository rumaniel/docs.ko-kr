---
title: 사용자 지정 컨트롤에 대한 애플리케이션 설정
ms.date: 03/30/2017
helpviewer_keywords:
- custom controls [Windows Forms], application settings
- application settings [Windows Forms], custom controls
ms.assetid: f44afb74-76cc-44f2-890a-44b7cdc211a1
ms.openlocfilehash: a4e477ce1c171b514482623595b2c5565564a2cb
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040469"
---
# <a name="application-settings-for-custom-controls"></a>사용자 지정 컨트롤에 대한 애플리케이션 설정
컨트롤이 타사 응용 프로그램에서 호스팅될 때 응용 프로그램 설정을 유지 하는 기능을 사용자 지정 컨트롤에 제공 하려면 특정 작업을 완료 해야 합니다.

 응용 프로그램 설정 기능에 대 한 대부분의 설명서는 독립 실행형 응용 프로그램을 만드는 것으로 가정 하 여 작성 됩니다. 그러나 다른 개발자가 자신의 응용 프로그램에서 호스팅하는 컨트롤을 만드는 경우에는 컨트롤의 설정을 적절히 유지 하기 위해 몇 가지 추가 단계를 수행 해야 합니다.

## <a name="application-settings-and-custom-controls"></a>응용 프로그램 설정 및 사용자 지정 컨트롤
 컨트롤의 설정을 제대로 유지 하려면에서 <xref:System.Configuration.ApplicationSettingsBase>파생 된 고유한 전용 응용 프로그램 설정 래퍼 클래스를 만들어 프로세스를 캡슐화 해야 합니다. 또한 주 컨트롤 클래스는를 <xref:System.Configuration.IPersistComponentSettings>구현 해야 합니다. 인터페이스에는 및 라는 두 가지 메서드를 <xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A> 비롯 한 <xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>여러 속성이 포함 되어 있습니다. Visual Studio에서 **Windows Forms 디자이너** 를 사용 하 여 폼에 컨트롤을 추가 하는 경우 컨트롤을 <xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A> 초기화할 때 Windows Forms가 자동으로 호출 됩니다. 컨트롤 <xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A> 의 `Dispose` 메서드에서 직접 호출 해야 합니다.

 또한 사용자 지정 컨트롤에 대 한 응용 프로그램 설정이 Visual Studio와 같은 디자인 타임 환경에서 제대로 작동 하도록 하려면 다음을 구현 해야 합니다.

1. 을 단일 매개 변수로 사용 <xref:System.ComponentModel.IComponent> 하는 생성자가 포함 된 사용자 지정 응용 프로그램 설정 클래스입니다. 이 클래스를 사용 하 여 모든 응용 프로그램 설정을 저장 하 고 로드 합니다. 이 클래스의 새 인스턴스를 만들 때 생성자를 사용 하 여 사용자 지정 컨트롤을 전달 합니다.

2. 컨트롤이 만들어지고 폼의 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기 등의 폼에 배치 된 후이 사용자 지정 설정 클래스를 만듭니다.

 사용자 지정 설정 클래스를 만드는 방법에 대 한 [자세한 내용은 방법: 응용 프로그램 설정을](how-to-create-application-settings.md)만듭니다.

## <a name="settings-keys-and-shared-settings"></a>설정 키 및 공유 설정
 일부 컨트롤은 같은 폼 내에서 여러 번 사용할 수 있습니다. 대부분의 경우 이러한 컨트롤은 자체의 개별 설정을 유지 하려고 합니다. <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> 의<xref:System.Configuration.IPersistComponentSettings>속성을 사용 하 여 폼에서 여러 버전의 컨트롤을 명확 하 게 구분 하는 고유한 문자열을 제공할 수 있습니다.

 을 구현 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> 하는 가장 간단한 방법은에 대해 <xref:System.Windows.Forms.Control.Name%2A> 컨트롤 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>의 속성을 사용 하는 것입니다. 컨트롤의 설정을 로드 하거나 저장 하는 경우의 값 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> <xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A> 을 <xref:System.Configuration.ApplicationSettingsBase> 클래스의 속성에 전달 합니다. 응용 프로그램 설정은 사용자의 설정을 XML로 유지 하는 경우이 고유 키를 사용 합니다. 다음 코드 예제에서는 섹션에서 `<userSettings>` 해당 `Text` 속성에 대 한 설정을 저장 하는 이라는 `CustomControl1` 사용자 지정 컨트롤의 인스턴스를 찾는 방법을 보여 줍니다.

```xml
<userSettings>
    <CustomControl1>
        <setting name="Text" serializedAs="string">
            <value>Hello, World</value>
        </setting>
    </CustomControl1>
</userSettings>
```

 에 대 한 <xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A> 값을 제공 하지 않는 컨트롤의 모든 인스턴스는 동일한 설정을 공유 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.IPersistComponentSettings>
- [응용 프로그램 설정 아키텍처](application-settings-architecture.md)
