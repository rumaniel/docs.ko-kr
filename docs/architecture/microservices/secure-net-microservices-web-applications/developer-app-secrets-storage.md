---
title: 개발하는 동안 애플리케이션 비밀 저장
description: .NET 마이크로 서비스 및 웹 애플리케이션의 보안 - 암호, 연결 문자열 또는 API 키와 같은 애플리케이션 비밀을 소스 제어에 저장하지 마세요. ASP.NET Core에서 사용할 수 있는 옵션, 특히 “사용자 비밀”을 처리하는 방법을 이해하고 있어야 합니다.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: fe8e7fa11c9a4f4cae133c2e09f9e4b4dd40a546
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675700"
---
# <a name="store-application-secrets-safely-during-development"></a>개발 중에 애플리케이션 비밀을 안전하게 저장

보호된 리소스 및 기타 서비스에 연결하려면 ASP.NET Core 애플리케이션은 일반적으로 연결 문자열, 암호 또는 중요한 정보를 포함하는 다른 자격 증명을 사용해야 합니다. 이러한 정보의 중요한 부분을 *암호*라고 합니다. 소스 코드에 비밀을 포함하지 않고 소스 제어에 비밀을 저장하지 않는 것이 좋습니다. 대신 ASP.NET Core 구성 모델을 사용하여 보다 안전한 위치에서 암호를 읽어야 합니다.

개인마다 다른 비밀 집합에 액세스해야 하기 때문에 프로덕션 리소스에 액세스할 때 사용되는 비밀과 개발 및 준비 리소스에 액세스할 때 사용되는 비밀을 분리해야 합니다. 개발 중에 사용되는 암호를 저장하는 일반적인 방법은 환경 변수에서 암호를 저장하거나 ASP.NET Core 암호 관리자 도구를 사용하는 것입니다. 프로덕션 환경에 있는 보다 안전한 스토리지의 경우 마이크로 서비스는 Azure Key Vault에 암호를 저장할 수 있습니다.

## <a name="store-secrets-in-environment-variables"></a>환경 변수에 비밀 저장

소스 코드에서 암호를 유지하는 한 가지 방법은 개발자가 해당 개발 컴퓨터에서 [환경 변수](/aspnet/core/security/app-secrets#environment-variables)로 문자열 기반 암호를 설정하는 것입니다. 환경 변수를 사용하여 계층적 이름(예: 구성 섹션에서 중첩된 이름)으로 비밀을 저장하는 경우 해당 섹션의 전체 계층 구조를 콜론(:)으로 구분해서 포함하도록 변수의 이름을 지정해야 합니다.

예를 들어 `Logging:LogLevel:Default` 환경 변수를 `Debug`로 설정하는 작업은 다음과 같은 JSON 파일의 구성 값에 해당합니다.

```json
{
    "Logging": {
        "LogLevel": {
            "Default": "Debug"
        }
    }
}
```

환경 변수의 이러한 값에 액세스하려면 애플리케이션이 IConfigurationRoot 개체를 생성할 때 해당 ConfigurationBuilder에서 AddEnvironmentVariables를 호출해야 합니다.

대체로 환경 변수는 일반 텍스트로 저장됩니다. 따라서 환경 변수를 포함하는 머신 또는 프로세스가 손상된 경우 환경 변수 값이 표시됩니다.

## <a name="store-secrets-with-the-aspnet-core-secret-manager"></a>ASP.NET Core 비밀 관리자를 사용하여 비밀 저장

ASP.NET Core [암호 관리자](/aspnet/core/security/app-secrets#secret-manager) 도구는 소스 코드에서 암호를 유지하는 또 다른 방법을 제공합니다. 비밀 관리자 도구를 사용하려면 **Microsoft.Extensions.Configuration.SecretManager** 패키지를 프로젝트 파일에 설치합니다. 해당 종속성이 표시되고 복원되면 `dotnet user-secrets` 명령을 사용하여 명령줄에서 비밀 값을 설정할 수 있습니다. 이러한 암호는 소스 코드와 다르게 사용자의 프로필 디렉터리에 있는 JSON 파일에 저장됩니다(세부 정보는 운영 체제에 따라 다름).

비밀 관리자 도구에 의해 설정된 비밀은 비밀을 사용하는 프로젝트의 `UserSecretsId` 속성으로 구성됩니다. 따라서 아래 코드 조각과 같이 프로젝트 파일에서 UserSecretsId 속성을 설정해야 합니다. 기본값은 Visual Studio에서 할당된 GUID이지만 컴퓨터에서 고유하기만 하면 실제 문자열은 중요하지 않습니다.

```xml
<PropertyGroup>
    <UserSecretsId>UniqueIdentifyingString</UserSecretsId>
</PropertyGroup>
```

애플리케이션에서 비밀 관리자를 통해 저장된 비밀을 사용하려면 ConfigurationBuilder 인스턴스에서 `AddUserSecrets<T>`를 호출하여 애플리케이션의 비밀을 해당 구성에 포함해야 합니다. 제네릭 매개 변수 T는 UserSecretId를 적용할 어셈블리의 형식이어야 합니다. 일반적으로 `AddUserSecrets<Startup>`을 사용해도 됩니다.

*Program.cs*의 `CreateDefaultBuilder` 메서드를 사용하는 경우 개발 환경의 기본 옵션에 `AddUserSecrets<Startup>()`이 포함됩니다.

>[!div class="step-by-step"]
>[이전](authorization-net-microservices-web-applications.md)
>[다음](azure-key-vault-protects-secrets.md)
