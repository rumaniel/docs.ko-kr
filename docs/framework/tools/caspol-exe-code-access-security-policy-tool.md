---
title: Caspol.exe(코드 액세스 보안 정책 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- permission sets, modifying security policy
- security policy [.NET Framework], Code Access Security Policy tool
- enterprise security policy
- referencing code groups and permission sets
- user security policy
- Caspol.exe
- Code Access Security Policy tool
- code groups, modifying security policy
- application development [.NET Framework], security
- machine security policy
- security policy [.NET Framework], modifying
- manually editing security configuration files
ms.assetid: d2bf6123-7b0c-4e60-87ad-a39a1c3eb2e0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bc4dd2703f32f2983a207d5990a6e8e646de8c17
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044856"
---
# <a name="caspolexe-code-access-security-policy-tool"></a>Caspol.exe(코드 액세스 보안 정책 도구)
CAS(코드 액세스 보안 정책 도구)(Caspol.exe)를 사용하면 사용자나 관리자가 컴퓨터 정책 수준, 사용자 정책 수준 및 엔터프라이즈 정책 수준의 보안 정책을 수정할 수 있습니다.  
  
> [!IMPORTANT]
> .NET Framework 4부터는 Caspol.exe가 CAS 정책에 영향을 주려면 [\<legacyCasPolicy> 요소](../configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md)를 `true`로 설정해야 합니다. CasPol.exe에 의해 표시 또는 수정되는 모든 설정은 CAS 정책을 사용하도록 선택하는 애플리케이션에만 영향을 줍니다. 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조하세요.  
  
> [!NOTE]
> 64비트 컴퓨터에 64비트 및 32비트 버전의 보안 정책이 포함됩니다. 정책 변경 내용을 32비트와 64비트 애플리케이션에 적용하도록 하려면, Caspol.exe의 32비트와 64비트 버전을 모두 실행해야 합니다.  
  
 코드 액세스 보안 정책 도구는 .NET Framework와 Visual Studio와 함께 자동으로 설치됩니다. Caspol.exe는 32비트 시스템의 경우 %windir%\Microsoft.NET\Framework\\*version*에서, 64비트 시스템의 경우 %windir%\Microsoft.NET\Framework64\\*version*에서 찾을 수 있습니다. (예를 들어 위치는 64비트 시스템의 .NET Framework 4인 경우 %windir%\Microsoft.NET\Framework64\v4.030319\caspol.exe입니다.) 컴퓨터에 여러 .NET Framework 버전이 함께 실행 중인 경우 도구의 여러 버전을 설치할 수 있습니다. 설치 디렉터리에서 도구를 실행할 수 있습니다. 하지만 설치 폴더로 이동할 필요가 없는 [명령 프롬프트](developer-command-prompt-for-vs.md)를 사용하는 것이 좋습니다.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console
caspol [options]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|옵션|설명|  
|------------|-----------------|  
|**-addfulltrust** *assembly_file*<br /><br /> 또는<br /><br /> **-af** *assembly_file*|사용자 지정 보안 개체(예: 사용자 지정 권한, 사용자 지정 멤버 자격 조건 등)를 구현하는 어셈블리를 특정 정책 수준에서 완전 신뢰 어셈블리 목록에 추가합니다. *assembly_file* 인수는 추가할 어셈블리를 지정합니다. 이 파일은 [강력한 이름](../../standard/assembly/strong-named.md)으로 서명되어야 합니다. [Sn.exe(강력한 이름 도구)](sn-exe-strong-name-tool.md)를 사용하여 강력한 이름으로 어셈블리에 서명할 수 있습니다.<br /><br /> 사용자 지정 권한이 포함된 권한 집합을 정책에 추가할 때마다 해당 사용자 지정 권한을 구현하는 어셈블리를 해당 정책 수준의 완전 신뢰 목록에 추가해야 합니다. 보안 정책(예: 컴퓨터 정책)에 사용된 사용자 지정 보안 개체(예: 사용자 지정 코드 그룹, 멤버 자격 조건 등)를 구현하는 어셈블리는 항상 완전 신뢰 어셈블리 목록에 추가해야 합니다. **주의:**  사용자 지정 보안 개체를 구현하는 어셈블리가 다른 어셈블리를 참조하는 경우에는 먼저 참조되는 어셈블리를 완전 신뢰 어셈블리 목록에 추가해야 합니다. Visual Basic, C++ 및 JScript를 사용하여 만들어진 사용자 지정 보안 개체는 Microsoft.VisualBasic.dll, Microsoft.VisualC.dll 또는 Microsoft.JScript.dll을 각각 참조합니다. 이러한 어셈블리는 기본적으로 완전 신뢰 어셈블리 목록에 들어 있지 않습니다. 따라서 사용자 지정 보안 개체를 추가하기 전에 적절한 어셈블리를 완전 신뢰 목록에 추가해야 합니다. 이렇게 하지 않으면 보안 시스템이 중단되어 모든 어셈블리를 로드할 수 없게 됩니다. 이 경우 Caspol.exe **-all -reset** 옵션은 보안을 복구하지 않습니다. 보안을 복구하려면 수동으로 보안 파일을 편집하여 사용자 지정 보안 개체를 제거해야 합니다.|  
|**-addgroup** {*parent_label &#124; parent_name*} *mship pset_name* [*flags*]<br /><br /> 또는<br /><br /> **-ag** {*parent_label &#124; parent_name*} *mship pset_name* [*flags*]|코드 그룹 계층 구조에 새로운 코드 그룹을 추가합니다. *parent_label* 또는 *parent_name*을 지정할 수 있습니다. *parent_label* 인수는 추가되는 코드 그룹의 부모인 코드 그룹의 레이블(예: 1. 또는 1.1.)을 지정합니다. *parent_name* 인수는 추가되는 코드 그룹의 부모 코드 그룹의 이름을 지정합니다. *parent_label*과 *parent_name*은 서로 교환하여 사용할 수 있으므로 Caspol.exe에서 이 두 인수를 구별할 수 있어야 합니다. 따라서 *parent_name*은 숫자로 시작할 수 없습니다. 또한 *parent_name*에는 A-Z, 0-9 및 밑줄 문자만 사용할 수 있습니다.<br /><br /> *mship* 인수는 새 코드 그룹의 멤버 자격 조건을 지정합니다. 자세한 내용은 이 섹션의 뒷부분에 나오는 *mship* 인수 표를 참조하세요.<br /><br /> *pset_name* 인수는 새 코드 그룹과 연결될 권한 집합의 이름입니다. 새 그룹에 대해 *flags*를 하나 이상 설정할 수도 있습니다. 자세한 내용은 이 섹션의 뒷부분에 나오는 *flags* 인수 표를 참조하세요.|  
|**-addpset** {*psfile* &#124; *psfile* p*set_name*}<br /><br /> 또는<br /><br /> **-ap** {*named*_*psfile* &#124; *psfile* *pset_name*}|명명된 새 권한 집합을 정책에 추가합니다. 권한 집합은 XML로 작성되어 .xml 파일에 저장되어야 합니다. XML 파일에 권한 집합의 이름이 포함되어 있으면 해당 파일(*psfile*)만 지정됩니다. XML 파일에 권한 집합의 이름이 포함되어 있지 않으면 XML 파일 이름(*psfile*)과 권한 집합 이름(*pset_name*)을 모두 지정해야 합니다.<br /><br /> 권한 집합에 사용되는 모든 권한은 전역 어셈블리 캐시에 포함된 어셈블리에 정의되어 있어야 합니다.|  
|**-a**[**ll**]|이 옵션 다음의 모든 옵션이 컴퓨터 정책, 사용자 정책 및 엔터프라이즈 정책에 적용됨을 나타냅니다. **-all** 옵션은 항상 현재 로그온한 사용자의 정책을 참조합니다. 현재 사용자 이외의 사용자에 대한 사용자 정책을 참조하려면 **-customall** 옵션을 참조하세요.|  
|**-chggroup** {*label &#124;name*} {*mship* &#124; *pset_name* &#124;<br /><br /> *flags* `}`<br /><br /> 또는<br /><br /> **-cg** {*label &#124;name*} {*mship* &#124; *pset_name* &#124;<br /><br /> *flags* `}`|코드 그룹의 멤버 자격 조건, 권한 집합 또는 플래그(**exclusive**, **levelfinal**, **name** 또는 **description**)의 설정을 변경합니다. *label* 또는 *name* 중 하나를 지정할 수 있습니다. *label* 인수는 코드 그룹의 레이블(예: 1. 또는 1.1.)을 지정합니다. *name* 인수는 변경할 코드 그룹의 이름을 지정합니다. *label*과 *name*은 서로 교환하여 사용할 수 있으므로 Caspol.exe에서 이 두 인수를 구별할 수 있어야 합니다. 따라서 *name*은 숫자로 시작할 수 없습니다. 또한 *name*에는 A-Z, 0-9 및 밑줄 문자만 사용할 수 있습니다.<br /><br /> *pset_name* 인수는 코드 그룹과 연결될 권한 집합의 이름을 지정합니다. *mship* 및 *flags* 인수에 대한 내용은 이 섹션의 뒷부분에 나오는 표를 참조하세요.|  
|**-chgpset**  *psfile pset_name*<br /><br /> 또는<br /><br /> **-cp** *psfile pset_name*|명명된 권한 집합을 변경합니다. *psfile* 인수는 권한 집합을 새로 정의합니다. 즉, XML 형식의 serialize된 권한 집합 파일입니다. *pset_name* 인수는 변경할 권한 집합의 이름을 지정합니다.|  
|**-customall**  *path*<br /><br /> 또는<br /><br /> **-ca**  *path*|이 옵션 다음의 모든 옵션이 컴퓨터 정책, 엔터프라이즈 정책 및 지정된 사용자 지정 사용자 정책에 적용됨을 나타냅니다. *path* 인수를 사용하여 사용자 지정 사용자의 보안 구성 파일에 대한 위치를 지정해야 합니다.|  
|**-cu**[**stomuser**] *path*|현재 Caspol.exe가 실행되고 있는 대상 사용자에 속하지 않는 사용자 지정 사용자 정책의 관리를 허용합니다. *path* 인수를 사용하여 사용자 지정 사용자의 보안 구성 파일에 대한 위치를 지정해야 합니다.|  
|**-enterprise**<br /><br /> 또는<br /><br /> **-en**|이 옵션 다음의 모든 옵션이 엔터프라이즈 수준 정책에 적용됨을 나타냅니다. 엔터프라이즈 관리자가 아닌 사용자는 엔터프라이즈 정책을 볼 수는 있지만 수정할 수 있는 권한은 없습니다. 비엔터프라이즈 시나리오에서, 이 정책은 기본적으로 컴퓨터 및 사용자 정책과 상충되지 않습니다.|  
|**-e**[**xecution**] {**on** &#124; **off**}|코드가 실행되기 전에 권한이 실행되도록 하는 메커니즘을 설정하거나 설정 해제합니다. **참고:**  .NET Framework 4 이상 버전에서는 이 스위치가 제거되었습니다. 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조하세요.|  
|**-f**[**orce**]|도구의 자동 소멸 테스트 기능을 억제하고 해당 정책을 사용자가 지정한 대로 변경합니다. 일반적으로, Caspol.exe가 올바르게 실행되지 못하도록 하는 정책 변경 내용이 있는지 여부를 확인한 다음, 그러한 정책 변경 내용이 있으면 해당 정책 변경 내용을 저장하지 않고 오류 메시지를 인쇄합니다. 이로 인해 Caspol.exe가 실행되지 않더라도 Caspol.exe에서 강제로 정책을 변경하려면 **–force** 옵션을 사용합니다.|  
|**-h**[**elp**]|Caspol.exe의 명령 구문 및 옵션을 표시합니다.|  
|**-l**[**ist**]|지정된 컴퓨터, 사용자, 엔터프라이즈 또는 모든 정책 수준에 대한 코드 그룹 계층 구조와 권한 집합을 표시합니다. Caspol.exe를 사용하여 코드 그룹의 레이블을 먼저 표시한 다음 이름(null이 아닌 경우)을 표시합니다.|  
|**-listdescription**<br /><br /> 또는<br /><br /> **-ld**|지정된 정책 수준에 대한 모든 코드 그룹 설명을 표시합니다.|  
|**-listfulltrust**<br /><br /> 또는<br /><br /> **-lf**|지정된 정책 수준에서 완전 신뢰 어셈블리 목록의 내용을 표시합니다.|  
|**-listgroups**<br /><br /> 또는<br /><br /> **-lg**|지정된 정책 수준 또는 모든 정책 수준의 코드 그룹을 표시합니다. Caspol.exe를 사용하여 코드 그룹의 레이블을 먼저 표시한 다음 이름(null이 아닌 경우)을 표시합니다.|  
|**-listpset** 또는 **-lp**|지정된 정책 수준 또는 모든 정책 수준의 권한 집합을 표시합니다.|  
|**-m**[**achine**]|이 옵션 다음의 모든 옵션이 컴퓨터 수준 정책에 적용됨을 나타냅니다. 관리자가 아닌 사용자는 컴퓨터 정책을 볼 수는 있지만 수정할 수 있는 권한은 없습니다. 관리자의 경우 **-machine**이 기본값입니다.|  
|**-polchgprompt** {**on** &#124; **off**}<br /><br /> 또는<br /><br /> **-pp** {**on** &#124; **off**}|정책을 변경시키는 옵션을 사용하여 Caspol.exe를 실행할 때마다 표시되는 프롬프트를 활성화하거나 비활성화합니다.|  
|**-quiet**<br /><br /> 또는<br /><br /> **-q**|정책을 변경시키는 옵션에 대해 일반적으로 표시되는 프롬프트를 일시적으로 비활성화합니다. 전역 변경 프롬프트 설정은 변경되지 않습니다. 모든 Caspol.exe 명령에 대한 프롬프트가 비활성화되지 않도록 하려면 개별 명령에 대해서만 이 옵션을 사용하십시오.|  
|**-r**[**ecover**]|백업 파일에서 정책을 복구합니다. 정책이 변경될 때마다 Caspol.exe를 실행하여 기존 정책을 백업 파일에 저장합니다.|  
|**-remfulltrust** *assembly_file*<br /><br /> 또는<br /><br /> **-rf**  *assembly_file*|정책 수준의 완전 신뢰 목록에서 어셈블리를 제거합니다. 이 작업은 사용자 지정 권한이 포함된 권한 집합을 정책에서 더 이상 사용하지 않을 경우 수행해야 합니다. 그러나 사용자 지정 권한을 구현하는 어셈블리가 아직 사용되고 있는 다른 사용자 지정 권한을 구현하지 않는 경우에만 해당 어셈블리를 완전 신뢰 목록에서 제거해야 합니다. 어셈블리를 목록에서 제거할 때에는 해당 어셈블리가 종속되는 다른 어셈블리도 모두 제거해야 합니다.|  
|**-remgroup** {*label &#124;name*}<br /><br /> 또는<br /><br /> **-rg** {l*abel &#124; name*}|해당 레이블 또는 이름으로 지정된 코드 그룹을 제거합니다. 지정된 코드 그룹에 자식 코드 그룹이 있으면 자식 코드 그룹도 모두 제거됩니다.|  
|**-rempset** *pset_name*<br /><br /> 또는<br /><br /> **-rp** *pset_name*|지정된 권한 집합을 정책에서 제거합니다. *pset_name* 인수는 제거할 권한 집합을 나타냅니다. Caspol.exe를 실행하여 코드 그룹과 관련되지 않은 권한 집합만 제거합니다. 기본 제공 권한 집합은 제거할 수 없습니다.|  
|**-reset**<br /><br /> 또는<br /><br /> **-rs**|정책을 기본 상태로 되돌린 다음 디스크에 보유합니다. 이 기능은 변경된 정책을 복구할 수 없을 것 같아서 설치 기본값으로 다시 시작하려는 경우에 유용합니다. 다시 설정은 또한 기본 정책을 시작 지점으로 사용하여 특정 보안 구성 파일을 수정하려는 경우에도 유용합니다. 자세한 내용은 [직접 보안 구성 파일 편집](#cpgrfcodeaccesssecuritypolicyutilitycaspolexeanchor1)을 참조하세요.|  
|**-resetlockdown**<br /><br /> 또는<br /><br /> **-rsld**|기본 상태의 보다 제한적인 버전에 정책을 반환하고 이를 디스크에 유지시킵니다. 이전 컴퓨터 정책의 백업을 만들어 `security.config.bac`라는 이름의 파일에 유지시킵니다.  잠긴 정책은 기본 정책과 유사하지만 `Local Intranet`, `Trusted Sites` 및 `Internet` 영역에서 코드에 권한을 부여하지 않으며 해당 코드 그룹에 자식 노드 그룹이 없다는 점에서 다릅니다.|  
|**-resolvegroup** *assembly_file*<br /><br /> 또는<br /><br /> **-rsg**  *assembly_file*|특정 어셈블리(*assembly_file*)가 속한 코드 그룹을 표시합니다. 기본적으로 이 옵션은 어셈블리가 속한 컴퓨터, 사용자 및 엔터프라이즈 정책 수준을 표시합니다. 하나의 정책 수준만 보려면 **-machine**, **-user** 또는 **-enterprise** 옵션 중 하나와 함께 이 옵션을 사용합니다.|  
|**-resolveperm** *assembly_file*<br /><br /> 또는<br /><br /> **-rsp** *assembly_file*|해당 어셈블리의 실행이 가능한 경우, 지정된(또는 기본) 보안 정책 수준이 해당 어셈블리에 부여하는 모든 권한을 표시합니다. *assembly_file* 인수는 해당 어셈블리를 지정합니다. **-all** 옵션을 지정하면 Caspol.exe에서 사용자, 컴퓨터 또는 엔터프라이즈 정책에 따라 해당 어셈블리의 권한을 계산합니다. 그렇지 않으면 기본 동작 규칙이 적용됩니다.|  
|**-s**[**ecurity**] {**on** &#124; **off**}|코드 액세스 보안을 설정하거나 설정 해제합니다. **-s off** 옵션을 지정하면 역할 기반 보안을 사용하도록 설정할 수 있습니다. **참고:**  .NET Framework 4 이상 버전에서는 이 스위치가 제거되었습니다. 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조하세요. **주의:**  코드 액세스 보안을 해제하면 모든 코드 액세스 요청이 성공합니다. 그러나 코드 액세스 보안을 해제하면 시스템이 바이러스나 웜과 같은 악의적 코드를 사용한 공격에 취약해집니다. 보안을 해제하면 성능이 약간 향상되지만 다른 보안 방법을 통해 전반적인 시스템 보안을 유지한 경우에만 보안을 해제해야 합니다. 다른 보안 예방 조치의 예로 공용 네트워크에서 연결을 끊거나 컴퓨터를 물리적으로 보호하는 경우를 들 수 있습니다.|  
|**-u**[**ser**]|이 옵션 다음의 모든 옵션이 현재 Caspol.exe가 실행되고 있는 대상 사용자의 사용자 수준 정책에 적용됨을 나타냅니다. 관리자가 아닌 사용자의 경우 **-user**가 기본값입니다.|  
|**-?**|Caspol.exe의 명령 구문 및 옵션을 표시합니다.|  
  
 코드 그룹의 멤버 자격 조건을 지정하는 *mship* 인수는 **-addgroup** 및 **-chggroup** 옵션과 함께 사용할 수 있습니다. 각 *mship* 인수는 .NET Framework 클래스로 구현됩니다. *mship*을 지정하려면 다음 인수 중 하나를 사용합니다.  
  
|인수|설명|  
|--------------|-----------------|  
|**-allcode**|모든 코드를 지정합니다. 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.AllMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-appdir**|애플리케이션 디렉터리를 지정합니다. **–appdir**를 멤버 자격 조건으로 지정하면 코드의 URL 증명 정보가 해당 코드의 애플리케이션 디렉터리 증명 정보와 비교됩니다. 두 증명 정보 값이 모두 동일하면 이 멤버 자격 조건이 충족됩니다. 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.ApplicationDirectoryMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-custom**  *xmlfile*|사용자 지정 멤버 자격 조건을 추가합니다. 필수 *xmlfile* 인수는 사용자 지정 멤버 자격 조건의 XML serialization이 포함된 .xml 파일을 지정합니다.|  
|**-hash** *hashAlg* { **-hex** *hashValue* &#124; **-file** *assembly_file* }|지정된 어셈블리 해시가 포함된 코드를 지정합니다. 해시를 코드 그룹 멤버 자격 조건으로 사용하려면 해시 값 또는 어셈블리 파일 중 하나를 지정해야 합니다. 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.HashMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-pub** { **-cert** *cert_file_name* &#124;<br /><br /> **-file** *signed_file_name* &#124; **-hex**  *hex_string* }|인증서 파일, 파일의 서명 또는 X509 인증서의 16진수 표시가 나타내는 것처럼 지정된 소프트웨어 게시자가 포함된 코드를 지정합니다. 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.PublisherMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-site** *website*|지정된 원본 사이트가 포함된 코드를 지정합니다. 예:<br /><br /> `-site** www.proseware.com`<br /><br /> 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.SiteMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-strong -file** *file_name* {*name* &#124; **-noname**} {*version* &#124; **-noversion**}|파일 이름, 문자열 형식의 어셈블리 이름 및 *major*.*minor*.*build*.*revision* 형식의 어셈블리 버전으로 지정된 강력한 이름의 코드를 지정합니다. 예:<br /><br /> **-strong -file** myAssembly.exe myAssembly 1.2.3.4<br /><br /> 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.StrongNameMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-url** *URL*|지정된 URL에서 시작되는 코드를 지정합니다. URL은 `http://` 또는 `ftp://`와 같은 프로토콜을 포함해야 합니다. 또한 와일드카드 문자(\*)를 사용하여 특정 URL에서 여러 어셈블리를 지정할 수 있습니다. **참고:**  URL은 여러 이름을 사용하여 식별될 수 있으므로 URL을 멤버 자격 조건으로 사용하는 것은 코드의 ID를 정확하게 식별하기 위한 안전한 방법이 아닙니다. 가능한 경우 강력한 이름 멤버 자격 조건, 게시자 멤버 자격 조건 또는 해시 멤버 자격 조건을 사용합니다. <br /><br /> 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.UrlMembershipCondition?displayProperty=nameWithType>을 참조하세요.|  
|**-zone** *zonename*|지정된 원본 영역이 포함된 코드를 지정합니다. *zonename* 인수는 다음 값 중 하나가 될 수 있습니다. **MyComputer**, **인트라넷**, **트러스트됨**, **인터넷** 또는 **트러스트되지 않음**. 이 멤버 자격 조건에 대한 자세한 내용은 <xref:System.Security.Policy.ZoneMembershipCondition> 클래스를 참조하십시오.|  
  
 **–addgroup** 및 **–chggroup** 옵션과 함께 사용할 수 있는 *flags* 인수는 다음 중 하나를 사용하여 지정합니다.  
  
|인수|설명|  
|--------------|-----------------|  
|**-description** "*description*"|**–addgroup** 옵션과 함께 사용하는 경우 추가할 코드 그룹에 대한 설명을 지정합니다. **–chggroup** 옵션과 함께 사용하는 경우 편집할 코드 그룹에 대한 설명을 지정합니다. *description* 인수는 큰따옴표로 묶어야 합니다.|  
|**-exclusive** {**on**&#124;**off**}|**on**으로 설정하면 일부 코드가 코드 그룹의 멤버 자격 조건을 충족할 때 추가하거나 수정하는 코드 그룹과 연결된 권한 집합만 고려합니다. **off**로 설정하면 Caspol.exe는 정책 수준에서 일치하는 모든 코드 그룹의 권한 집합을 고려합니다.|  
|**-levelfinal** {**on**&#124;**off**}|**on**으로 설정하면 추가 또는 수정된 코드 그룹이 발생하는 정책 수준의 하위 수준은 고려되지 않음을 나타냅니다. 일반적으로 이 옵션은 컴퓨터 정책 수준에서 사용됩니다. 예를 들어, 컴퓨터 수준의 코드 그룹에 이 플래그를 설정하고 일부 코드가 이 코드 그룹의 멤버 자격 조건과 일치하면 이 코드에 대해 사용자 수준 정책이 계산되거나 적용되지 않습니다.|  
|**-name** "*name*"|**–addgroup** 옵션과 함께 사용하는 경우 추가할 코드 그룹의 스크립팅 이름을 지정합니다. **-chggroup** 옵션과 함께 사용하는 경우 편집할 코드 그룹의 스크립팅 이름을 지정합니다. *name* 인수는 큰따옴표로 묶어야 합니다. 또한 *name* 인수는 숫자로 시작할 수 없으며, A-Z, 0-9 및 밑줄 문자만 사용할 수 있습니다. 코드 그룹은 숫자 레이블 대신 이 *name*으로 참조될 수 있습니다. *name*은 스크립팅 용도로도 매우 유용합니다.|  
  
## <a name="remarks"></a>설명  
 보안 정책은 컴퓨터 정책, 사용자 정책 및 엔터프라이즈 정책의 세 가지 정책 수준으로 표현됩니다. 어셈블리에서 받아들이는 권한 집합은 이러한 세 가지 정책 수준에서 허용하는 권한 집합의 교집합 부분에 의해 결정됩니다. 각 정책 수준은 코드 그룹의 계층 구조로 표시됩니다. 모든 코드 그룹에는 해당 그룹의 멤버가 되는 코드를 결정하는 멤버 자격 조건이 있습니다. 또한 명명된 권한 집합이 각 코드 그룹에 연결됩니다. 이 권한 집합에서는 런타임에서 해당 멤버 자격 조건을 충족하는 코드에 허용할 권한을 지정합니다. 코드 그룹 계층 구조에서는 해당 코드 그룹에 연결된 명명된 권한 집합과 함께 보안 정책의 각 수준을 정의하고 유지합니다. **–user**, **-customuser**, **–machine** 및 **-enterprise** 옵션을 사용하여 보안 정책의 수준을 설정할 수 있습니다.  
  
 보안 정책 및 런타임에서 코드에 부여할 권한을 결정하는 방법에 대한 자세한 내용은 [보안 정책 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))를 참조하세요.  
  
## <a name="referencing-code-groups-and-permission-sets"></a>코드 그룹 및 권한 집합 참조  
 계층 구조의 코드 그룹을 쉽게 참조하려면 **-list** 옵션을 사용하여 숫자 레이블(예: 1, 1.1, 1.1.1 등)과 함께 들여쓴 코드 그룹 목록을 표시합니다. 코드 그룹을 대상으로 하는 다른 명령줄 작업에서도 숫자 레이블을 사용하여 특정 코드 그룹을 참조합니다.  
  
 명명된 권한 집합은 이름으로 참조됩니다. **-list** 옵션은 코드 그룹 목록 다음에 해당 정책에서 사용할 수 있는 명명된 권한 집합 목록을 표시합니다.  
  
## <a name="caspolexe-behavior"></a>Caspol.exe 동작  
 **-s**[**ecurity**] {**on** &#124; **off**}를 제외한 모든 옵션에서는 Caspol.exe가 설치되어 있는 .NET Framework 버전을 사용합니다. *X* 버전의 런타임과 함께 설치된 Caspol.exe를 실행하면 해당 버전에만 변경 내용이 적용됩니다. 설치된 다른 버전의 런타임(있는 경우)에는 적용되지 않습니다. 특정 런타임 버전의 디렉터리가 아닌 다른 경로에서 명령줄을 사용하여 Caspol.exe를 실행하면 이 도구는 해당 경로의 첫 번째 런타임 버전 디렉터리(대개, 최근에 설치된 런타임 버전)에서 실행됩니다.  
  
 **-s**[**ecurity**] {**on** &#124; **off**} 옵션은 컴퓨터 전체에 영향을 주는 작업입니다. 코드 액세스 보안을 해제하면 컴퓨터의 모든 관리 코드와 모든 사용자에 대한 보안 검사가 중단됩니다. .NET Framework의 side-by-side 버전이 설치된 경우 이 명령을 실행하면 컴퓨터에 설치된 모든 버전의 보안이 해제됩니다. **-list** 옵션은 해제된 보안 상태를 표시하지만, 이 방법 이외에는 다른 사용자가 보안이 해제되었음을 알 수 없습니다.  
  
 관리자 권한이 없는 사용자가 Caspol.exe를 실행할 때 **–machine** 옵션이 지정되어 있지 않으면 모든 옵션에서 사용자 수준 정책을 참조합니다. 또한 관리자가 Caspol.exe를 실행할 때 **–user** 옵션이 지정되어 있지 않으면 모든 옵션에서 컴퓨터 정책을 참조합니다.  
  
 Caspol.exe가 작동하려면 **Everything** 권한 집합과 동일한 권한 집합을 Caspol.exe에 부여해야 합니다. 이 도구에는 Caspol.exe를 실행하는 데 필요한 권한을 부여하지 않는 방식으로 정책이 수정되지 않도록 하는 보호 메커니즘이 있습니다. 즉, 변경을 시도하면 Caspol.exe는 요청한 정책 변경으로 인해 해당 도구가 중단되므로 해당 변경 내용이 거부됨을 알립니다. **–force** 옵션을 사용하여 지정된 명령에 대해 이 보호 메커니즘을 해제할 수 있습니다.  
  
<a name="cpgrfcodeaccesssecuritypolicyutilitycaspolexeanchor1"></a>   
## <a name="manually-editing-the-security-configuration-files"></a>직접 보안 구성 파일 편집  
 세 가지 보안 구성 파일은 각각 Caspol.exe로 지원되는 세 가지 정책 수준(컴퓨터 정책, 특정 사용자 정책 및 엔터프라이즈 정책)에 해당합니다. 이러한 파일은 Caspol.exe를 사용하여 컴퓨터, 사용자 또는 엔터프라이즈 정책이 변경된 경우에만 디스크에 만들어집니다. 필요한 경우 Caspol.exe의 **–reset** 옵션을 사용하여 기본 보안 정책을 디스크에 저장할 수 있습니다.  
  
 대부분의 경우에는 보안 구성 파일을 직접 편집하지 않는 것이 좋습니다. 그러나 관리자가 특정 사용자에 대해 보안 구성을 편집하려는 경우처럼 이러한 파일들을 꼭 수정해야 하는 경우도 있습니다.  
  
## <a name="examples"></a>예  
 **-addfulltrust**  
  
 사용자 지정 권한이 포함된 권한 집합이 컴퓨터 정책에 추가된 것으로 가정합니다. 이 사용자 지정 권한은 `MyPerm.exe`의 `MyPerm.exe` 및 `MyOther.exe` 참조 클래스에서 구현됩니다. 두 어셈블리는 모두 완전 신뢰 어셈블리 목록에 추가되어야 합니다. 다음 명령을 사용하여 `MyPerm.exe` 어셈블리를 컴퓨터 정책에 대해 완전 신뢰 목록에 추가합니다.  
  
```console  
caspol -machine -addfulltrust MyPerm.exe  
```  
  
 다음 명령을 사용하여 `MyOther.exe` 어셈블리를 컴퓨터 정책에 대해 완전 신뢰 목록에 추가합니다.  
  
```console  
caspol -machine -addfulltrust MyOther.exe  
```  
  
 **-addgroup**  
  
 다음 명령을 사용하여 컴퓨터 정책 코드 그룹 계층 구조의 루트에 자식 코드 그룹을 추가합니다. 새 코드 그룹은 **Internet** 영역의 멤버이며 **Execution** 권한 집합에 연결됩니다.  
  
```console  
caspol -machine -addgroup 1.  -zone Internet Execution  
```  
  
 다음 명령은 공유 \\\netserver\netshare에 로컬 인트라넷 권한을 제공하는 자식 코드 그룹을 추가합니다.  
  
```console  
caspol -machine -addgroup 1. -url \\netserver\netshare\* LocalIntranet  
```  
  
 **-addpset**  
  
 다음 명령을 사용하여 사용자 정책에 `Mypset` 권한 집합을 추가합니다.  
  
```console  
caspol -user -addpset Mypset.xml Mypset  
```  
  
 **-chggroup**  
  
 다음 명령은 1.2. 레이블이 지정된 코드 그룹의 사용자 정책에 포함된 권한 집합을 **Execution** 권한 집합으로 변경합니다.  
  
```console  
caspol -user -chggroup 1.2. Execution  
```  
  
 다음 명령은 1.2.1. 레이블이 지정된 코드 그룹의 기본 정책에 포함된 멤버 자격 조건과 **exclusive** 플래그 설정을 변경합니다. 즉 멤버 자격 조건이 **Internet**영역에서 시작하고 **exclusive** 플래그는 on으로 설정된 코드로 정의됩니다.  
  
```console  
caspol -chggroup 1.2.1. -zone Internet -exclusive on  
```  
  
 **-chgpset**  
  
 다음 명령을 사용하여 `Mypset`이라는 권한 집합을 `newpset.xml`에 포함된 권한 집합으로 변경합니다. 현재 릴리스에서는 코드 그룹 계층 구조에서 사용할 권한 집합을 변경할 수 없습니다.  
  
```console  
caspol -chgpset Mypset newpset.xml  
```  
  
 **-force**  
  
 다음 명령은 사용자 정책의 루트 코드 그룹(1 레이블 지정)이 **Nothing**으로 명명된 권한 집합에 연결되도록 합니다. 이렇게 하면 Caspol.exe가 실행되지 않습니다.  
  
```console  
caspol -force -user -chggroup 1 Nothing  
```  
  
 **-recover**  
  
 다음 명령을 사용하여 가장 최근에 저장한 컴퓨터 정책을 복구합니다.  
  
```console  
caspol -machine -recover  
```  
  
 **-remgroup**  
  
 다음 명령을 사용하여 레이블이 1.1.인 코드 그룹을 제거합니다. 이 코드 그룹에 자식 코드 그룹이 있으면 해당 그룹도 삭제됩니다.  
  
```console  
caspol -remgroup 1.1.  
```  
  
 **-rempset**  
  
 다음 명령은 사용자 정책에서 **Execution** 권한 집합을 제거합니다.  
  
```console  
caspol -user -rempset Execution  
```  
  
 다음 명령을 사용하여 사용자 정책 수준에서 `Mypset`을 제거합니다.  
  
```console  
caspol -rempset MyPset  
```  
  
 **-resolvegroup**  
  
 다음 명령은 `myassembly`가 속한 컴퓨터 정책의 모든 코드 그룹을 표시합니다.  
  
```console  
caspol -machine -resolvegroup myassembly  
```  
  
 다음 명령을 사용하여 `myassembly`가 속해 있는 컴퓨터 정책, 엔터프라이즈 정책 및 특정 사용자 지정 사용자 정책의 모든 코드 그룹을 표시합니다.  
  
```console  
caspol -customall "c:\config_test\security.config" -resolvegroup myassembly  
```  
  
 **-resolveperm**  
  
 다음 명령을 사용하여 컴퓨터 정책 수준 및 사용자 정책 수준에 따라 `testassembly`에 대한 권한을 계산합니다.  
  
```console  
caspol -all -resolveperm testassembly  
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
