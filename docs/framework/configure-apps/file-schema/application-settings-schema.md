---
title: 응용 프로그램 설정 스키마
ms.date: 03/30/2017
helpviewer_keywords:
- schema application settings
- application settings, schema [Windows Forms]
- Windows Forms, application settings schema
- configuration schema [.NET Framework], application settings
ms.assetid: 5797fcff-6081-4e8c-bebf-63d9c70cf14b
ms.openlocfilehash: 89a08434332b0242fe57e9dcaa3b3ebcc5692d06
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927756"
---
# <a name="application-settings-schema"></a>응용 프로그램 설정 스키마

응용 프로그램 설정을 통해 Windows Forms 또는 ASP.NET 응용 프로그램에서 응용 프로그램 범위 및 사용자 범위 설정을 저장 하 고 검색할 수 있습니다. 이 컨텍스트에서 *설정은* 응용 프로그램 또는 현재 사용자와 관련 된 정보 이며, 데이터베이스 연결 문자열에서 사용자의 기본 설정 기본 창 크기에 이르기까지 모든 정보를 지정 합니다.

기본적으로 Windows Forms 응용 프로그램의 응용 프로그램 설정은 <xref:System.Configuration.LocalFileSettingsProvider> 클래스를 사용 합니다 .이 클래스는 .net 구성 시스템을 사용 하 여 설정을 XML 구성 파일에 저장 합니다. 응용 프로그램 설정에 사용 되는 파일에 대 한 자세한 내용은 [응용 프로그램 설정 아키텍처](../../winforms/advanced/application-settings-architecture.md)를 참조 하세요.

응용 프로그램 설정은 사용 하는 구성 파일의 일부로 다음 요소를 정의 합니다.

| 요소                    | Description                                                                           |
| -------------------------- | ------------------------------------------------------------------------------------- |
| **\<applicationSettings>** | 응용 프로그램에 특정 한 모든  **\<설정 >** 태그를 포함 합니다.                         |
| **\<userSettings>**        | 현재 사용자와 관련 된 모든  **\<설정 >** 태그를 포함 합니다.                        |
| **\<setting>**             | 설정을 정의합니다. Applicationsettings > 또는  **\<userSettings >** 의  **\<** 자식입니다. |
| **\<value>**               | 설정 값을 정의 합니다. **\<설정 >** 의 자식입니다.                                   |

## <a name="applicationsettings-element"></a>\<applicationSettings > 요소

이 요소는 클라이언트 컴퓨터의 응용 프로그램 인스턴스와 관련 된 모든  **\<설정 >** 태그를 포함 합니다. 특성 없음을 정의합니다.

## <a name="usersettings-element"></a>\<userSettings > 요소

이 요소는 현재 응용 프로그램을 사용 하 고 있는 사용자에 해당 하는 모든  **\<설정 >** 태그를 포함 합니다. 특성 없음을 정의합니다.

## <a name="setting-element"></a>\<> 요소 설정

이 요소는 설정을 정의 합니다. 여기에는 다음과 같은 특성이 있습니다.

| 특성        | 설명 |
| ---------------- | ----------- |
| **name**         | 필수 요소. 설정의 고유 ID입니다. Visual Studio를 통해 만든 설정은 이름 `ProjectName.Properties.Settings`으로 저장 됩니다. |
| **serializedAs** | 필수 요소. 값을 텍스트로 직렬화 하는 데 사용할 형식입니다. 유효한 값은<br><br>- `string`. 값은을 <xref:System.ComponentModel.TypeConverter>사용 하 여 문자열로 serialize 됩니다.<br>- `xml`. 값은 XML 직렬화를 사용 하 여 serialize 됩니다.<br>- `binary`. 이 값은 이진 serialization을 사용 하 여 텍스트 인코딩 이진으로 serialize 됩니다.<br />- `custom`. 설정 공급자는이 설정에 대 한 기본적인 지식을 갖고 있으며 직렬화 및 역직렬화 합니다. |

## <a name="value-element"></a>\<value > 요소

이 요소는 설정 값을 포함 합니다.

## <a name="example"></a>예제

다음 예제에서는 두 개의 응용 프로그램 범위 설정 및 두 개의 사용자 범위 설정을 정의 하는 응용 프로그램 설정 파일을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
    </sectionGroup>
    <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />
    </sectionGroup>
  </configSections>
  <applicationSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="Cursor" serializeAs="String">
        <value>Default</value>
      </setting>
      <setting name="DoubleBuffering" serializeAs="String">
        <value>False</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </applicationSettings>
  <userSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="FormTitle" serializeAs="String">
        <value>Form1</value>
      </setting>
      <setting name="FormSize" serializeAs="String">
        <value>595, 536</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </userSettings>
</configuration>
```

## <a name="see-also"></a>참고자료

- [응용 프로그램 설정 개요](../../winforms/advanced/application-settings-overview.md)
- [응용 프로그램 설정 아키텍처](../../winforms/advanced/application-settings-architecture.md)
