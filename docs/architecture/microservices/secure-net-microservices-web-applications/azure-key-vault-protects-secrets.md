---
title: Azure Key Vault를 사용하여 프로덕션 시 비밀 보호
description: .NET 마이크로 서비스 및 웹 애플리케이션의 보안 - Azure Key Vault는 관리자가 완전히 제어하는 애플리케이션 비밀을 처리하는 뛰어난 방법입니다. 개발자가 처리하지 않고도 관리자가 개발 값을 할당하고 철회할 수도 있습니다.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 63bf357c95b82a820b6dfb6a2d24a5d89f66de72
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675670"
---
# <a name="use-azure-key-vault-to-protect-secrets-at-production-time"></a>Azure Key Vault를 사용하여 프로덕션 시 비밀 보호

환경 변수로 저장되거나 비밀 관리자 도구로 저장된 비밀은 여전히 로컬로 저장되고 컴퓨터에서 암호화되지 않습니다. 비밀을 저장하기 위한 더 안전한 옵션은 키 및 비밀을 저장하기 위해 안전한 중앙 위치를 제공하는 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)입니다.

**Microsoft.Extensions.Configuration.AzureKeyVault** 패키지를 통해 ASP.NET Core 애플리케이션에서 Azure Key Vault의 구성 정보를 읽을 수 있습니다. Azure Key Vault에서 암호 사용을 시작하려면 다음 단계를 수행합니다.

1. 애플리케이션을 Azure AD 애플리케이션으로 등록합니다. (키 자격 증명 모음에 대한 액세스는 Azure AD에 의해 관리됩니다.) Azure 관리 포털을 통해 이 작업을 수행할 수 있습니다.\

   또는 암호나 클라이언트 암호 대신 인증서를 사용하여 애플리케이션을 인증하려는 경우 [New-AzADApplication](/powershell/module/az.resources/new-azadapplication) PowerShell cmdlet을 사용할 수 있습니다. Azure Key Vault로 등록하는 인증서는 공개 키만 필요합니다. 애플리케이션은 프라이빗 키를 사용합니다.

2. 새 서비스 주체를 만들어 등록된 애플리케이션에 키 자격 증명 모음에 대한 액세스를 제공합니다. 다음 PowerShell 명령을 사용하여 이를 수행할 수 있습니다.

   ```powershell
   $sp = New-AzADServicePrincipal -ApplicationId "<Application ID guid>"
   Set-AzKeyVaultAccessPolicy -VaultName "<VaultName>" -ServicePrincipalName $sp.ServicePrincipalNames[0] -PermissionsToSecrets all -ResourceGroupName "<KeyVault Resource Group>"
   ```

3. <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> 인스턴스를 만들 때 <xref:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault%2A?displayProperty=nameWithType> 확장 메서드를 호출하여 애플리케이션에 키 자격 증명 모음을 구성 소스로 포함합니다. `AddAzureKeyVault`를 호출하려면 이전 단계에서 등록되었으며 키 자격 증명 모음에 대한 액세스 권한이 부여된 애플리케이션 ID가 필요합니다.

   [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) 패키지에 대한 참조만 포함하여 클라이언트 암호 대신 인증서를 사용하는 `AddAzureKeyVault`의 오버로드를 사용할 수도 있습니다.

> [!IMPORTANT]
> Azure Key Vault를 마지막 구성 공급자로 등록하는 것이 좋습니다. 이렇게 하면 이전 공급자의 구성 값을 재정의할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **Azure Key Vault를 사용하여 애플리케이션 비밀 보호** \
  [https://docs.microsoft.com/azure/guidance/guidance-multitenant-identity-keyvault](/azure/guidance/guidance-multitenant-identity-keyvault)

- **개발 중 안전한 앱 비밀 스토리지** \
  [https://docs.microsoft.com/aspnet/core/security/app-secrets](/aspnet/core/security/app-secrets)

- **데이터 보호 구성** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/overview](/aspnet/core/security/data-protection/configuration/overview)

- **ASP.NET Core에서 데이터 보호 키 관리 및 수명** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/default-settings](/aspnet/core/security/data-protection/configuration/default-settings)

- **Microsoft.Extensions.Configuration.KeyPerFile** GitHub 리포지토리 \
  <https://github.com/aspnet/Configuration/tree/master/src/Config.KeyPerFile>

>[!div class="step-by-step"]
>[이전](developer-app-secrets-storage.md)
>[다음](../key-takeaways.md)
