---
title: 격리된 스토리지
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- data storage using isolated storage
- stores
- storing data using isolated storage
- isolated storage
- location of isolated storage in file system
- standardizing storage systems
- storing data using isolated storage, when not to use
- code, isolated storage
- isolated storage, options
- data storage using isolated storage, when not to use
- storing data using isolated storage, options
- isolated storage, when not to use
- data storage using isolated storage, options
- isolation
ms.assetid: aff939d7-9e49-46f2-a8cd-938d3020e94e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: df5601fb0dbf088bd28da91f7279a330f2bb3494
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170694"
---
# <a name="isolated-storage"></a>격리된 스토리지
<a name="top"></a> 데스크톱 앱에서 격리된 스토리지는 코드와 저장된 데이터를 연결하는 표준화된 방법을 정의하여 격리와 안전을 제공하는 데이터 스토리지 메커니즘입니다. 표준화를 통해 다음과 같은 여러 가지 이점도 활용할 수 있습니다. 관리자는 파일 스토리지 구성, 보안 정책 설정, 사용하지 않은 데이터 삭제를 위해 격리된 스토리지를 조작하는 도구를 사용할 수 있습니다. 격리된 스토리지를 사용하면 더 이상 파일 시스템에서 안전한 위치를 지정하기 위해 코드에 고유 경로를 포함할 필요가 없으며 격리된 스토리지에만 액세스할 수 있는 다른 애플리케이션으로부터 데이터가 보호됩니다. 애플리케이션의 스토리지 영역 위치를 나타내는 하드 코드된 정보는 필요하지 않습니다.

> [!IMPORTANT]
> [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에는 격리된 스토리지를 사용할 수 없습니다. 대신에 Windows Runtime API에 포함된 `Windows.Storage` 네임스페이스의 애플리케이션 데이터 클래스를 사용하여 로컬 데이터 및 파일을 저장합니다. 자세한 내용은 Windows 개발자 센터에서 [애플리케이션 데이터](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10)) 를 참조하세요.

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [데이터 구획 및 저장소](#data_compartments_and_stores)

- [격리된 스토리지의 할당량](#quotas)

- [액세스 보안](#secure_access)

- [허용 수준과 보안 위험](#allowed_usage)

- [격리된 스토리지 위치](#isolated_storage_locations)

- [격리된 스토리지 만들기, 열거 및 삭제](#isolated_storage_tasks)

- [격리된 스토리지 시나리오](#scenarios_for_isolated_storage)

- [관련 항목](#related_topics)

- [참조](#reference)

<a name="data_compartments_and_stores"></a>

## <a name="data-compartments-and-stores"></a>데이터 구획 및 저장소

애플리케이션에서 파일에 데이터를 저장하는 경우, 스토리지 위치가 다른 애플리케이션에 알려져 손상될 가능성을 최소화할 수 있도록 파일 이름과 스토리지 위치는 신중하게 선택되어야 합니다. 이러한 문제를 관리하기 위해 적절한 표준 시스템이 없는 경우 스토리지 충돌을 최소화하는 ad hoc 기법을 개발하는 것은 복잡하고 결과를 신뢰할 수도 없습니다.

격리된 스토리지를 사용하면 데이터는 항상 사용자와 어셈블리별로 격리됩니다. 어셈블리의 원본 또는 강력한 이름과 같은 자격 증명은 어셈블리 ID를 결정합니다. 또한 유사한 자격 증명을 사용하여 데이터가 애플리케이션 도메인별로 격리될 수도 있습니다.

격리된 스토리지를 사용하는 경우, 애플리케이션은 게시자 또는 서명 등과 같은 코드 ID의 몇 가지 측면과 관련된 고유 데이터 구획에 데이터를 저장합니다. 데이터 컴파트먼트는 특정 스토리지 위치가 아니라 추상적인 개념이며 스토리지라고 하는 하나 이상의 격리된 스토리지 파일로 구성됩니다. 이 스토리지는 데이터가 저장되는 실제 디렉터리 위치를 포함합니다. 예를 들어, 애플리케이션은 관련된 데이터 구획을 가질 수 있고 파일 시스템의 디렉터리는 이 애플리케이션의 데이터를 실제로 유지하는 저장소를 구현할 수 있습니다. 저장소에 저장된 데이터는 사용자 기본 설정 정보에서 애플리케이션 상태에 이르기까지 모든 종류의 데이터가 될 수 있습니다. 개발자의 경우, 데이터 구획의 위치는 투명합니다. 저장소는 보통 클라이언트에 있지만, 서버 애플리케이션은 사용자를 대신하여 관련 기능을 수행하면서 그 사용자를 가장하여 정보를 저장하는 격리된 저장소를 사용할 수 있습니다. 또한 격리된 스토리지는 로밍 사용자와 함께 정보가 이동되도록 사용자의 로밍 프로필과 함께 서버의 정보를 저장할 수 있습니다.

<a name="quotas"></a>

## <a name="quotas-for-isolated-storage"></a>격리된 스토리지의 할당량

할당 한도는 사용 가능한 격리된 스토리지 크기의 제한 값입니다. 디렉터리 및 저장소의 다른 정보와 관련된 오버헤드는 물론 파일 공간(바이트)을 포함합니다. 격리된 스토리지는 <xref:System.Security.Permissions.IsolatedStoragePermission> 개체를 사용하여 설정된 스토리지의 제한에 해당하는 사용 권한 할당을 사용합니다. 할당량을 초과하는 데이터를 쓰려고 하면 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 예외가 throw됩니다.  .NET Framework 구성 도구(Mscorcfg.msc)를 사용하여 수정할 수 있는 보안 정책에 따라 코드에 부여될 권한이 결정됩니다. <xref:System.Security.Permissions.IsolatedStoragePermission> 권한이 부여된 코드는 <xref:System.Security.Permissions.IsolatedStoragePermission.UserQuota%2A> 속성이 허용하는 수준의 스토리지만 사용하도록 제한됩니다. 그러나 코드에서 다른 사용자 ID를 제공하여 사용 권한 할당 한도를 무시할 수 있으므로 사용 권한 할당 한도는 코드 동작에 대해 고정된 제한이 아니라 코드 동작 방식에 대한 지침으로 사용됩니다.

로밍 저장소에는 할당 한도가 적용되지 않기 때문에 코드에 약간 높은 수준의 사용 권한이 있어야 이를 사용할 수 있습니다. 열거형 값 <xref:System.Security.Permissions.IsolatedStorageContainment.AssemblyIsolationByRoamingUser> 및 <xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByRoamingUser>는 로밍 사용자를 위한 격리된 스토리지를 사용하여 권한을 지정합니다.

<a name="secure_access"></a>

## <a name="secure-access"></a>액세스 보안

격리된 스토리지를 사용하면 부분적으로 신뢰할 수 있는 애플리케이션은 컴퓨터의 보안 정책에 의해 제어되는 방식으로 데이터를 저장할 수 있습니다. 이 방법은 특히 사용자가 주의하여 실행해야 하는 다운로드된 구성 요소에 유용합니다. 표준 I/O 메커니즘을 사용하여 파일 시스템에 액세스하는 경우, 사용 권한을 이 유형의 코드에 부여하는 경우는 거의 없습니다. 그러나 격리된 스토리지를 사용할 권한은 로컬 컴퓨터, 로컬 네트워크 또는 인터넷에서 실행되는 코드에 기본적으로 부여됩니다.

관리자는 해당 신뢰 수준에 따라 애플리케이션 또는 사용자가 가질 수 있는 격리된 스토리지 양을 제한할 수 있습니다. 또한 사용자의 지속된 데이터를 모두 제거할 수도 있습니다. 격리된 스토리지를 만들거나 액세스하려면 코드에 적절한 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 권한이 부여되어야 합니다.

격리된 스토리지에 액세스하려면 필요한 네이티브 플랫폼 운영 체제 권한이 모두 코드에 있어야 합니다. 파일 시스템을 사용할 수 있는 권한을 가진 사용자를 제어하는 ACL(액세스 제어 목록)이 충족되어야 합니다. .NET Framework 애플리케이션은 특정 플랫폼 관련 가장을 수행하는 경우를 제외하고는 격리된 스토리지에 액세스할 수 있는 운영 체제 권한을 이미 가지고 있습니다. 이런 경우 애플리케이션은 가장된 사용자 ID가 격리된 스토리지에 액세스할 수 있는 적절한 운영 체제 권한을 가지고 있는지 확인해야 합니다. 이 액세스 권한은 웹에서 실행되거나 다운로드된 코드에 특정 사용자와 관련된 스토리지 영역에서 읽고 쓸 수 있는 편리한 방법을 제공합니다.

격리된 스토리지에 대한 액세스를 제어하기 위해 공용 언어 런타임은 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 개체를 사용합니다. 각 개체에는 다음과 같은 값을 지정하는 속성이 있습니다.

- 허용 수준 - 허용된 액세스 형식을 나타내며 값은 <xref:System.Security.Permissions.IsolatedStorageContainment> 열거형의 멤버입니다. 이러한 값에 대한 자세한 내용은 다음 섹션의 표를 참조하세요.

- 이전 섹션에서 설명한 스토리지 할당량입니다.

런타임은 코드에서 처음으로 저장소를 열려고 할 때 이 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 권한을 요청합니다. 코드의 신뢰 정도에 따라 이 권한을 부여할지 여부를 결정합니다. 이 사용 권한이 부여되면 보안 정책 및 코드의 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 요청에 의해 허용되는 사용법과 스토리지 할당량 값이 결정됩니다. 보안 정책은 .NET Framework 구성 도구(Mscorcfg.msc)를 사용하여 설정됩니다. 호출 스택의 모든 호출자를 검사하여 각 호출자가 적절한 최소 허용 수준 값을 가지고 있는지 확인합니다. 또한 런타임은 파일을 저장할 저장소를 열거나 만든 코드에 부과된 할당 한도도 검사합니다. 이러한 조건을 충족하면 사용 권한이 부여됩니다. 할당 한도는 파일을 저장소에 쓸 때마다 다시 검사됩니다.

공용 언어 런타임은 보안 정책을 기반으로 적절한 모든 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 을 부여하므로 권한을 요청하는 데 애플리케이션 코드가 필요하지 않습니다. 그러나 <xref:System.Security.Permissions.IsolatedStorageFilePermission>을 포함하여 애플리케이션에서 필요로 하는 특정 사용 권한을 요청해야 하는 경우가 있습니다.

<a name="allowed_usage"></a>

## <a name="allowed-usage-and-security-risks"></a>허용 수준과 보안 위험

<xref:System.Security.Permissions.IsolatedStorageFilePermission>에 의해 지정되는 허용 사용법에 따라 코드에서 격리된 스토리지를 만들고 사용할 수 있는 정도가 결정됩니다. 다음 표에서는 사용 권한에 지정된 허용 수준이 어떤 방식으로 격리 유형에 부합하는지를 보여 주고 각 허용 수준과 관련된 보안 위험을 요약하여 설명합니다.

|허용 수준|격리 유형|보안 효과|
|-------------------|---------------------|---------------------|
|<xref:System.Security.Permissions.IsolatedStorageContainment.None>|격리된 스토리지를 사용할 수 없습니다.|보안 효과가 없습니다.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByUser>|사용자, 도메인 및 어셈블리별 격리. 각 어셈블리는 도메인 내에 별도의 하위 저장소를 가지고 있습니다. 이 권한을 사용하는 저장소는 암시적으로 컴퓨터와 별로도 격리됩니다.|이 권한을 사용하면 비록 할당 한도가 적용되어 어느 정도까지는 허가되지 않은 수준의 리소스 남용을 방지하지만 그래도 이러한 리소스 남용이 발생할 수 있습니다. 이를 서비스 거부 공격이라고 합니다.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByRoamingUser>|`DomainIsolationByUser`와 동일하지만, 로밍 사용자 프로필을 사용할 수 있고 할당량이 적용되지 않은 경우 로밍되는 위치에 저장소가 저장됩니다.|할당 한도를 사용할 수 없으므로 스토리지 리소스가 서비스 거부 공격에 노출되기 쉽습니다.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.AssemblyIsolationByUser>|사용자 및 어셈블리별 격리. 이 권한을 사용하는 저장소는 암시적으로 컴퓨터와 별로도 격리됩니다.|서비스 거부 공격 문제를 방지하기 위해 이 수준에서 할당 한도가 적용됩니다. 다른 도메인의 동일한 어셈블리가 이 저장소에 액세스할 수 있으므로 애플리케이션 간에 정보가 누출될 가능성이 있습니다.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.AssemblyIsolationByRoamingUser>|`AssemblyIsolationByUser`와 동일하지만, 로밍 사용자 프로필을 사용할 수 있고 할당량이 적용되지 않은 경우 로밍되는 위치에 저장소가 저장됩니다.|`AssemblyIsolationByUser`의 경우와 동일하지만, 할당량이 없으므로 서비스 거부 공격 위험이 증가합니다.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.AdministerIsolatedStorageByUser>|사용자별 격리. 일반적으로 관리 또는 디버깅 도구에서 이 권한 수준을 사용합니다.|이 권한으로 액세스하면 코드가 어셈블리 격리와 관계없이 사용자의 격리된 스토리지 파일 또는 디렉터리를 보거나 삭제할 수 있습니다. 정보 누출 및 데이터 손실 등의 위험이 있지만 이에 제한되지는 않습니다.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.UnrestrictedIsolatedStorage>|모든 사용자, 도메인 및 어셈블리별 격리. 일반적으로 관리 또는 디버깅 도구에서 이 권한 수준을 사용합니다.|이 권한을 사용하면 모든 사용자에 대한 모든 격리된 저장소 전체가 손상될 가능성이 있습니다.|

<a name="isolated_storage_locations"></a>

## <a name="isolated-storage-locations"></a>격리된 스토리지 위치

때때로 운영 체제의 파일 시스템을 사용하여 격리된 스토리지에 대한 변경 내용을 확인하면 도움이 됩니다. 또한 개발자는 격리된 스토리지 파일의 위치를 알고 싶을 때가 있습니다. 이 위치는 운영 체제에 따라 다릅니다. 다음 표에서는 일반적으로 사용되는 몇 가지 운영 체제에서 격리된 스토리지가 만들어지는 루트 위치를 보여 줍니다. 이 루트 위치 아래에 있는 Microsoft\IsolatedStorage 디렉터리를 찾으세요. 파일 시스템에서 격리된 스토리지를 보려면 숨김 파일과 폴더를 표시하도록 폴더 설정을 변경해야 합니다.

|운영 체제|파일 시스템에서의 위치|
|----------------------|-----------------------------|
|Windows 2000, Windows XP, Windows Server 2003(Windows NT 4.0에서 업그레이드)|로밍 가능 저장소 =<br /><br /> \<SYSTEMROOT>\Profiles\\<user\>\Application Data<br /><br /> 비로밍 저장소 =<br /><br /> \<SYSTEMROOT>\Profiles\\<user\>\Local Settings\Application Data|
|Windows 2000  - 새로 설치 및 Windows 98, Windows NT 3.51에서 업그레이드|로밍 가능 저장소 =<br /><br /> \<SYSTEMDRIVE>\Documents and Settings\\<user\>\Application Data<br /><br /> 비로밍 저장소 =<br /><br /> \<SYSTEMDRIVE>\Documents and Settings\\<user\>\Local Settings\Application Data|
|Windows XP, Windows Server 2003 - 새로 설치 및 Windows 2000, Windows 98에서 업그레이드|로밍 가능 저장소 =<br /><br /> \<SYSTEMDRIVE>\Documents and Settings\\<user\>\Application Data<br /><br /> 비로밍 저장소 =<br /><br /> \<SYSTEMDRIVE>\Documents and Settings\\<user\>\Local Settings\Application Data|
|[!INCLUDE[win8](../../../includes/win8-md.md)], Windows 7, Windows Server 2008, Windows Vista|로밍 가능 저장소 =<br /><br /> \<SYSTEMDRIVE>\Users\\<user\>\AppData\Roaming<br /><br /> 비로밍 저장소 =<br /><br /> \<SYSTEMDRIVE>\Users\\<user\>\AppData\Local|

<a name="isolated_storage_tasks"></a>

## <a name="creating-enumerating-and-deleting-isolated-storage"></a>격리된 스토리지 만들기, 열거 및 삭제

.NET Framework에서는 <xref:System.IO.IsolatedStorage> 네임스페이스의 세 가지 클래스를 제공해 격리된 스토리지와 관련된 작업을 수행할 수 있도록 해줍니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>에서 파생되는 <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=nameWithType> 은 저장된 어셈블리 및 애플리케이션 파일의 기본 관리를 제공합니다. <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 클래스 인스턴스는 파일 시스템에 있는 단일 저장소를 나타냅니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> 에서 파생되는 <xref:System.IO.FileStream?displayProperty=nameWithType> 은 저장소에 있는 파일에 대한 액세스를 제공합니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorageScope> 은 적절한 격리 유형을 사용하여 저장소를 만들고 선택할 수 있도록 하는 열거형입니다.

격리된 스토리지 클래스를 사용하여 격리된 스토리지를 만들고 열거하고 삭제할 수 있습니다. 이러한 작업을 수행하는 데 필요한 메서드는 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 개체를 통해 사용할 수 있습니다. 일부 작업을 수행하려면 격리된 스토리지를 관리할 수 있는 권한을 나타내는 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 권한을 가져야 하며 파일이나 디렉터리에 액세스할 수 있는 운영 체제 권한도 가지고 있어야 합니다.

일반적인 격리된 스토리지 작업을 보여 주는 일련의 예제는 [관련 항목](#related_topics)에 나열되어 있는 방법 항목을 참조하세요.

<a name="scenarios_for_isolated_storage"></a>

## <a name="scenarios-for-isolated-storage"></a>격리된 스토리지 시나리오

격리된 스토리지는 다음 네 가지 시나리오를 비롯하여 다양한 상황에서 유용합니다.

- 다운로드된 컨트롤. 인터넷에서 다운로드된 관리 코드 컨트롤은 일반 I/O 클래스를 통해 하드 드라이브에 쓸 수 없지만 격리된 스토리지를 사용하여 사용자 설정 및 애플리케이션 상태를 유지할 수 있습니다.

- 공유 구성 요소 스토리지. 애플리케이션 간에 공유되는 구성 요소는 격리된 스토리지를 사용하여 데이터 스토리지에 대한 제어된 액세스를 제공할 수 있습니다.

- 서버 스토리지. 서버 애플리케이션은 격리된 스토리지를 사용하여 애플리케이션을 요청하는 다수의 사용자에게 개별 스토리지를 제공할 수 있습니다. 격리된 스토리지는 항상 사용자별로 분리되어 있으므로 서버는 요청하는 사용자를 가장해야 합니다. 이런 경우 데이터는 사용자를 구분하기 위해 애플리케이션에서 사용하는 동일한 ID인 보안 주체 ID를 기반으로 격리됩니다.

- 로밍. 또한 애플리케이션에서는 격리된 스토리지를 사용하여 로밍 사용자 프로필을 저장할 수 있습니다. 따라서 사용자의 격리된 저장소는 프로필을 로밍하는 데 사용됩니다.

다음과 같은 경우 격리된 스토리지를 사용하면 안 됩니다.

- 격리된 스토리지는 충분히 신뢰할 수 있는 코드, 비관리 코드 또는 컴퓨터에서 신뢰할 수 있는 사용자로부터 보호되지 않으므로 암호화되지 않은 키 또는 암호 등의 상위 값 비밀을 저장하는 데 사용하지 마세요.

- 코드를 저장하는 데 사용하지 마세요.

- 관리자가 컨트롤하는 구성 및 배포 설정을 저장하는 데 사용하지 마세요. 사용자 기본 설정은 관리자가 제어하지 않으므로 구성 설정으로 간주되지 않습니다.

대부분의 애플리케이션은 데이터베이스를 사용하여 데이터를 저장하고 격리합니다. 이때 데이터베이스에 있는 하나 이상의 행은 특정 사용자에 대한 스토리지를 나타낼 수 있습니다. 사용자 수가 적은 경우, 데이터베이스 사용에 따른 오버헤드가 의미가 있는 경우 또는 데이터베이스 기능이 없는 경우 데이터베이스 대신 격리된 스토리지를 사용하도록 선택할 수 있습니다. 또한 데이터베이스에서 제공하는 행보다 더 융통성 있고 복잡한 스토리지가 애플리케이션에 필요한 경우에도 격리된 스토리지를 사용할 수 있습니다.

<a name="related_topics"></a>

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[격리 유형](../../../docs/standard/io/types-of-isolation.md)|다양한 유형의 격리에 대해 설명합니다.|
|[방법: 격리된 스토리지의 저장소 가져오기](../../../docs/standard/io/how-to-obtain-stores-for-isolated-storage.md)|<xref:System.IO.IsolatedStorage.IsolatedStorageFile> 클래스를 사용하여 사용자 및 어셈블리별로 격리된 저장소를 가져오는 예제를 제공합니다.|
|[방법: 격리된 스토리지의 저장소 열거](../../../docs/standard/io/how-to-enumerate-stores-for-isolated-storage.md)|<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=nameWithType> 메서드를 사용하여 사용자에 대한 모든 격리된 스토리지 크기를 계산하는 방법을 보여 줍니다.|
|[방법: 격리된 스토리지에서 저장소 삭제](../../../docs/standard/io/how-to-delete-stores-in-isolated-storage.md)|<xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%2A?displayProperty=nameWithType> 메서드를 두 가지 방법으로 사용하여 격리된 저장소를 삭제하는 방법을 보여 줍니다.|
|[방법: 격리된 스토리지의 공간 부족 상태 예상](../../../docs/standard/io/how-to-anticipate-out-of-space-conditions-with-isolated-storage.md)|격리된 저장소에서 남은 공간을 측정하는 방법을 보여 줍니다.|
|[방법: 격리된 스토리지의 파일 및 디렉터리 만들기](../../../docs/standard/io/how-to-create-files-and-directories-in-isolated-storage.md)|격리된 저장소에서 파일 및 디렉터리를 만드는 몇 가지 예제를 제공합니다.|
|[방법: 격리된 스토리지의 기존 파일 및 디렉터리 찾기](../../../docs/standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)|격리된 스토리지에서 디렉터리 구조 및 파일을 읽는 방법을 보여 줍니다.|
|[방법: 격리된 스토리지의 파일 읽기 및 쓰기](../../../docs/standard/io/how-to-read-and-write-to-files-in-isolated-storage.md)|격리된 스토리지 파일에 문자열을 쓰고 다시 문자열을 읽는 예제를 제공합니다.|
|[방법: 격리된 스토리지의 파일 및 디렉터리 삭제](../../../docs/standard/io/how-to-delete-files-and-directories-in-isolated-storage.md)|격리된 스토리지 파일 및 디렉터리를 삭제하는 방법을 보여 줍니다.|
|[파일 및 스트림 I/O](../../../docs/standard/io/index.md)|동기 및 비동기 파일과 데이터 스트림 액세스를 수행할 수 있는 방법에 대해 설명합니다.|

<a name="reference"></a>

## <a name="reference"></a>참조

- <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=nameWithType>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream?displayProperty=nameWithType>

- <xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=nameWithType>
