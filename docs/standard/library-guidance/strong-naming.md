---
title: 강력한 이름 지정 및 .NET 라이브러리
description: .NET 라이브러리에 강력한 이름을 지정하는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 10/16/2018
ms.openlocfilehash: 3a623f65d95d776e45af245a1fe241cc5ee25b93
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70968979"
---
# <a name="strong-naming"></a>강력한 이름 지정

강력한 이름 지정은 키를 사용해서 어셈블리에 서명하여 [강력한 이름의 어셈블리](../assembly/strong-named.md)를 생성하는 것을 말합니다. 어셈블리에 강력한 이름을 지정하면 이름 및 어셈블리 버전 번호를 기준으로 고유 ID가 생성되어 어셈블리 충돌을 방지하는 데 도움이 됩니다.

강력한 이름 지정의 단점은 어셈블리에 강력한 이름이 지정되고 나면 Windows의 .NET Framework에서 어셈블리를 엄격하게 로드한다는 것입니다. 강력한 이름의 어셈블리 참조는 어셈블리에서 참조하는 버전과 정확히 일치해야 하므로 개발자가 어셈블리를 사용할 때 [바인딩 리디렉션을 구성](../../framework/configure-apps/redirect-assembly-versions.md)해야 합니다.

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="neutral" />
            <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

.NET 개발자가 강력한 이름 지정에 대해 불만을 제기하는 경우 일반적으로 엄격한 어셈블리 로드와 관련이 있습니다. 다행히, 이 문제는 .NET Framework에만 한정됩니다. .NET Core, Xamarin, UWP 및 대부분의 다른 .NET 구현에서는 엄격한 어셈블리 로드가 필요하지 않으며 강력한 이름 지정의 주요 단점이 제거됩니다.

강력한 이름 지정의 한 가지 중요한 측면은 바이럴이란 것입니다. 강력한 이름의 어셈블리는 다른 강력한 이름의 어셈블리만 참조할 수 있습니다. 라이브러리에 강력한 이름을 지정하지 않은 경우, 강력한 이름 지정이 필요한 애플리케이션 또는 라이브러리를 빌드하는 개발자는 해당 라이브러리를 사용할 수 없게 됩니다.

강력한 이름 지정의 혜택은 다음과 같습니다.

1. 다른 강력한 이름의 어셈블리에서 어셈블리를 참조하고 사용할 수 있습니다.
2. GAC(전역 어셈블리 캐시)에 어셈블리를 저장할 수 있습니다.
3. 다른 어셈블리 버전과 나란히 어셈블리를 로드할 수 있습니다. 병렬 어셈블리 로드는 일반적으로 플러그 인 아키텍처를 사용하는 애플리케이션에 필요합니다.

## <a name="create-strong-named-net-libraries"></a>강력한 이름의 .NET 라이브러리 만들기

오픈 소스 .NET 라이브러리에 강력한 이름을 지정해야 합니다. 어셈블리에 강력한 이름을 지정하면 대부분의 사용자가 사용할 수 있으며, 엄격한 어셈블리 로드는 .NET Framework에만 영향을 줍니다.

> [!NOTE]
> 이 지침은 NuGet.org에 게시된 .NET 라이브러리와 같은 공개적으로 배포된 .NET 라이브러리에만 해당합니다. 대부분의 .NET 애플리케이션에는 강력한 이름 지정이 필요하지 않으므로 기본적으로 수행해서는 안 됩니다.

**✔️** 라이브러리 어셈블리에 강력한 이름을 지정합니다.

**✔️** 소스 제어 시스템에 강력한 이름 지정키를 추가합니다.

> 공개적으로 사용 가능한 키를 통해 개발자는 라이브러리 소스 코드를 수정하고 동일한 키로 다시 컴파일할 수 있습니다.
> 
> [부분 신뢰 시나리오](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)에서 특별한 사용 권한을 제공하기 위해 이전에 사용된 경우에는 강력한 이름 지정 키를 공개해서는 안 됩니다. 공개하면 기존 환경이 손상될 수 있습니다.

> [!IMPORTANT]
> 코드 게시자 ID를 원하는 경우 [Authenticode](/windows-hardware/drivers/install/authenticode) 및 [NuGet 패키지 서명](/nuget/create-packages/sign-a-package)을 사용하는 것이 좋습니다. CAS(코드 액세스 보안)를 보안 완화로 사용해서는 안 됩니다.

**✔️** 사용자가 바인딩 리디렉션 및 업데이트 빈도를 줄일 수 있도록 주 버전 변경 시에만 어셈블리 버전을 높입니다.

> [버전 관리 및 어셈블리 버전](./versioning.md#assembly-version)을 참조하세요.

**❌** 강력한 이름 지정 키를 추가, 제거 또는 변경하지 않습니다.

> 어셈블리의 강력한 이름 지정 키를 수정하면 어셈블리 ID가 변경되고, 어셈블리 ID를 사용하는 컴파일된 코드가 중단됩니다. 자세한 내용은 [호환성이 손상되는 이진 변경](./breaking-changes.md#binary-breaking-change)을 참조하세요.

**❌ 금지** 강력한 이름이 지정되고 강력하지 않은 이름이 지정된 버전의 라이브러리를 게시합니다. 예를 들어 `Contoso.Api` 및 `Contoso.Api.StrongNamed`를 지정합니다.

> 두 패키지를 게시하면 개발자 에코시스템이 포크됩니다. 또한 애플리케이션이 두 패키지에 모두 종속하게 되면 개발자가 형식 이름 충돌을 발견할 수 있습니다. 적어도 .NET의 경우 어셈블리마다 형식이 다릅니다.

>[!div class="step-by-step"]
>[이전](cross-platform-targeting.md)
>[다음](nuget.md)
