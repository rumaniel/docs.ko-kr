---
title: JSON 웹 토큰 처리기 패키지 다운로드
ms.date: 10/10/2018
ms.assetid: d12b3f5b-f1f1-4a9d-a159-0c13e5976c90
ms.openlocfilehash: a8685a71d46778d932595965f32c0041b176bd83
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633520"
---
# <a name="download-the-json-web-token-handler-package"></a>JSON 웹 토큰 처리기 패키지 다운로드

이 항목에서는 JSON Web Token 처리기를 다운로드하고 프로젝트에서 사용하는 방법을 설명합니다.

JSON Web Token 처리기 확장은 필요한 어셈블리 및 참조를 프로젝트에 추가하는 NuGet 패키지로 사용할 수 있습니다. NuGet이 아직 설치되지 않은 경우 [nuget.org](https://nuget.org)로 이동하여 패키지를 설치합니다. NuGet의 해당 페이지를 방문 하 여 확장에 대 한 버전 관리 기록을 확인할 수 있습니다. [JSON Web Token Handler on NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/)

## <a name="use-the-package-manager-gui"></a>패키지 관리자 GUI를 사용 하 여

1. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.

2. **NuGet 패키지 관리** 창에서 검색 상자를 클릭하고 `JWT Token Handler`를 입력하고 **Enter** 키를 누릅니다.

3. [결과] 창에서 첫 번째 결과에 대한 **설치** 단추를 클릭합니다.

4. 패키지 다운로드가 시작됩니다. 프로젝트에 추가되기 전에 [라이선스 승인] 대화 상자가 나타납니다. 사용 약관에 동의하면 **동의**를 클릭합니다.

5. 최신 JSON Web Token 처리기 어셈블리가 다운로드되고 프로젝트에 추가됩니다.

## <a name="use-the-package-manager-console"></a>패키지 관리자 콘솔 사용

1. Visual Studio에서 클릭 **도구가** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.

2. **패키지 관리자 콘솔**이 나타납니다. 다음 텍스트를 입력하고 **Enter** 키를 누릅니다.

    ```powershell
    Install-Package System.IdentityModel.Tokens.Jwt
    ```

3. 최신 JSON Web Token 처리기 어셈블리가 다운로드되고 프로젝트에 추가됩니다.
