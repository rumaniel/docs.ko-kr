---
title: 애플리케이션 설정 개요
ms.date: 03/30/2017
f1_keywords:
- ApplicationsSettingsOverview
helpviewer_keywords:
- application settings [Windows Forms], about application settings
- dynamic properties
- user preferences [Windows Forms], tracking
ms.assetid: 0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc
ms.openlocfilehash: ec73fb61f0a4b43e47936c864e73355ee777aeb7
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040419"
---
# <a name="application-settings-overview"></a>애플리케이션 설정 개요
이 항목은 애플리케이션 및 사용자를 대신하여 설정 데이터를 만들고 저장하는 방법을 설명합니다.

 Windows Forms의 애플리케이션 설정 기능을 사용하면 클라이언트 컴퓨터에서 사용자 지정 애플리케이션과 사용자 기본 설정을 쉽게 만들고 저장 및 유지 관리할 수 있습니다. Windows Forms 애플리케이션 설정을 통해 데이터베이스 연결 문자열과 같은 애플리케이션 데이터뿐 아니라 사용자 애플리케이션 기본 설정과 같은 사용자별 데이터도 저장할 수 있습니다. Visual Studio 또는 사용자 지정 관리 코드를 사용하여 새 설정을 만들고, 디스크에서 읽거나 쓰고, 폼의 속성에 바인딩하고, 설정 데이터를 로드 및 저장하기 전에 유효성을 검사할 수 있습니다.

 개발자는 응용 프로그램 설정을 사용 하 여 사용자 지정 코드를 거의 사용 하지 않는 응용 프로그램의 상태를 저장할 수 있으며 이전 버전의 .NET Framework에서 동적 속성을 대체 합니다. 애플리케이션 설정은 읽기 전용이고 런타임에 바인딩되며 더 많은 사용자 지정 프로그래밍을 요구하는 동적 속성보다 많은 향상된 기능을 포함합니다. 동적 속성 클래스는 .NET Framework 2.0에 유지 되었지만 응용 프로그램 설정 클래스를 씬 래핑하는 셸 클래스일 뿐입니다.

## <a name="what-are-application-settings"></a>애플리케이션 설정이란?
 Windows Forms 애플리케이션은 애플리케이션 실행에 중요하지만 애플리케이션 코드에 직접 포함되지 않는 데이터를 요구하는 경우가 많습니다. 애플리케이션이 웹 서비스나 데이터베이스 서버를 사용하는 경우 나중에 다시 컴파일하지 않고 변경할 수 있도록 이 정보를 별도 파일에 저장할 수 있습니다. 마찬가지로, 애플리케이션에서 현재 사용자와 관련된 데이터를 저장해야 할 수도 있습니다. 예를 들어 대부분의 애플리케이션에는 애플리케이션의 모양과 동작을 사용자 지정하는 사용자 기본 설정이 있습니다.

 애플리케이션 설정은 클라이언트 컴퓨터에 애플리케이션 범위 설정과 사용자 범위 설정 둘 다를 쉽게 저장할 수 있는 방법을 제공하여 두 가지 요구를 모두 충족합니다. Visual Studio 또는 코드 편집기에서 속성 이름, 데이터 형식 및 범위(애플리케이션 또는 사용자)를 지정하여 지정된 속성에 대한 설정을 정의합니다. 사용하기 편하고 읽기 쉽도록 관련 설정을 명명된 그룹에 배치할 수도 있습니다. 정의된 설정은 유지되며 런타임에 자동으로 메모리에 읽어옵니다. 플러그형 아키텍처에서는 지속성 메커니즘을 변경할 수 있지만 기본적으로 로컬 파일 시스템이 사용됩니다.

 애플리케이션 설정은 설정이 애플리케이션 범위인지 또는 사용자 범위인지에 따라 데이터를 다른 구성(.config) 파일에 XML로 유지하여 작동합니다. 대부분의 경우 애플리케이션 범위 설정은 읽기 전용입니다. 프로그램 정보이기 때문에 일반적으로 덮어쓸 필요가 없습니다. 반면, 사용자 범위 설정은 애플리케이션이 부분 신뢰로 실행되는 경우에도 런타임에 안전하게 읽고 쓸 수 있습니다. 부분 신뢰에 대한 자세한 내용은 [Windows Forms의 보안 개요](../security-in-windows-forms-overview.md)를 참조하세요.

 설정은 구성 파일에 XML 조각으로 저장됩니다. 애플리케이션 범위 설정은 `<application.Settings>` 요소로 표시되며 일반적으로 *app*.exe.config에 배치됩니다. 여기서 *app* 은 주 실행 파일의 이름입니다. 사용자 범위 설정은 `<userSettings>` 요소로 표시되며 *user*.config에 배치됩니다. 여기서 *user* 는 현재 애플리케이션을 실행 중인 사람의 사용자 이름입니다. *app*.exe.config 파일은 응용 프로그램과 함께 배포해야 합니다. *user*.config 파일은 응용 프로그램이 해당 사용자에 대한 설정을 처음 저장할 때 요청 시 설정 아키텍처에서 만듭니다. `<userSettings>` app *.exe.config 내에*블록을 정의하여 사용자 범위 설정의 기본값을 제공할 수도 있습니다.

 사용자 지정 컨트롤은 <xref:System.Configuration.IPersistComponentSettings> 메서드를 노출하는 <xref:System.Configuration.IPersistComponentSettings.SaveSettings%2A> 인터페이스를 구현하여 고유한 설정을 저장할 수도 있습니다. Windows Forms <xref:System.Windows.Forms.ToolStrip> 컨트롤은 이 인터페이스를 구현하여 애플리케이션 세션 간에 도구 모음 위치와 도구 모음 항목을 저장합니다. 사용자 지정 컨트롤과 애플리케이션 설정에 대한 자세한 내용은 [Application Settings for Custom Controls](application-settings-for-custom-controls.md)을 참조하세요.

## <a name="limitations-of-application-settings"></a>애플리케이션 설정의 제한 사항
 .NET Framework를 호스트 하는 관리 되지 않는 응용 프로그램에서는 응용 프로그램 설정을 사용할 수 없습니다. Visual Studio 추가 기능, Microsoft Office용 C++, Internet Explorer에 호스트되는 컨트롤 또는 Microsoft Outlook 추가 기능 및 프로젝트와 같은 환경에서는 설정이 작동하지 않습니다.

 현재 Windows Forms의 일부 속성에는 바인딩할 수 없습니다. 가장 두드러진 예로 <xref:System.Windows.Forms.Form.ClientSize%2A> 속성이 있습니다. 이 속성에 바인딩하면 런타임에 예측할 수 없는 동작이 발생합니다. 일반적으로 이러한 설정을 프로그래밍 방식으로 저장하고 로드하면 문제를 해결할 수 있습니다.

 애플리케이션 설정에는 자동으로 정보를 암호화하는 기본 제공 기능이 없습니다. 데이터베이스 암호와 같은 보안 관련 정보는 일반 텍스트로 저장하면 안 됩니다. 이러한 중요 정보를 저장하려면 애플리케이션 개발자가 보안을 책임져야 합니다. 연결 문자열을 저장하려면 URL에 암호를 하드 코딩하는 대신 Windows 통합 보안을 사용하는 것이 좋습니다. 자세한 내용은 [코드 액세스 보안 및 ADO.NET](../../data/adonet/code-access-security.md)을 참조하세요.

## <a name="getting-started-with-application-settings"></a>애플리케이션 설정 시작
 Visual Studio를 사용하는 경우 Windows Forms 디자이너 내에서 **속성** 창의 **(ApplicationSettings)** 속성을 통해 설정을 정의할 수 있습니다. 이런 방식으로 설정을 정의하면 Visual Studio에서 각 설정을 클래스 속성에 연결하는 사용자 지정 관리되는 래퍼 클래스를 자동으로 만듭니다. 또한 Visual Studio는 폼을 표시할 때 컨트롤 설정이 자동으로 복원되고 폼을 닫을 때 자동으로 저장되도록 폼이나 컨트롤의 속성에 설정을 바인딩합니다.

 설정을 더 세부적으로 제어하려는 경우 고유한 사용자 지정 애플리케이션 설정 래퍼 클래스를 정의할 수 있습니다. 이렇게 하려면 <xref:System.Configuration.ApplicationSettingsBase>에서 클래스를 파생시키고 각 설정에 해당하는 속성을 추가한 다음 이러한 속성에 특수 특성을 적용합니다. 래퍼 클래스 만들기에 대한 자세한 내용은 [Application Settings Architecture](application-settings-architecture.md)를 참조하세요.

 <xref:System.Windows.Forms.Binding> 클래스를 사용하여 프로그래밍 방식으로 폼과 컨트롤의 속성에 설정을 바인딩할 수도 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.SettingsProvider>
- <xref:System.Configuration.LocalFileSettingsProvider>
- <xref:System.Configuration.IPersistComponentSettings>
- [방법: 응용 프로그램 설정 유효성 검사](how-to-validate-application-settings.md)
- [응용 프로그램 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)
- [방법: 런타임에 설정 읽기C#](how-to-read-settings-at-run-time-with-csharp.md)
- [응용 프로그램 설정 및 사용자 설정 사용](using-application-settings-and-user-settings.md)
- [응용 프로그램 설정 아키텍처](application-settings-architecture.md)
- [사용자 지정 컨트롤에 대한 응용 프로그램 설정](application-settings-for-custom-controls.md)
