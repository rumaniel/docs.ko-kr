---
title: 보안 및 사용자 입력
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- security [.NET Framework], user input
- user input, security
- secure coding, user input
- code security, user input
ms.assetid: 9141076a-96c9-4b01-93de-366bb1d858bc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 832ea3c976a0a2e6bb3b4df8a2541248cfc56933
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663920"
---
# <a name="security-and-user-input"></a>보안 및 사용자 입력

웹 요청 또는 URL에서 받은 데이터와 Microsoft Windows Forms 애플리케이션의 컨트롤에 대한 입력 등을 포함하여 모든 종류의 사용자 입력 데이터는 다른 코드를 호출하는 매개 변수로 직접 사용되는 경우가 많기 때문에 코드에 악영향을 미칠 수 있습니다. 이런 상황은 이상한 매개 변수로 코드를 호출하는 악성 코드의 경우와 비슷하므로 같은 예방 조치를 취해야 합니다. 사용자 입력의 경우 신뢰할 수 없는 데이터가 있는지 여부를 추적하기 위한 스택 프레임이 없기 때문에 안전을 보장하기가 더 어렵습니다.

이러한 문제는 보안과 관련이 없어 보이는 코드에 존재할 수 있지만 실제로는 다른 코드로 올바르지 않은 데이터를 전달하는 통로가 되므로 발견하기가 가장 미묘하고 어려운 보안 버그에 속합니다. 이러한 버그를 찾으려면 모든 유형의 입력 데이터를 따라가면서 가능한 값의 범위가 될 수 있는 것을 생각해 보고 해당 데이터를 받는 코드가 이 모든 경우를 처리할 수 있는지 고려해야 합니다. 범위를 검사하고 코드가 처리할 수 없는 입력을 거부하면 이러한 버그를 해결할 수 있습니다.

사용자 데이터와 관련된 중요한 고려 사항은 다음과 같습니다.

- 서버 응답에 있는 모든 사용자 데이터는 클라이언트 쪽의 서버 사이트 컨텍스트에서 실행됩니다. 웹 서버가 사용자 데이터를 가져와서 반환된 웹 페이지에 삽입하는 경우 사용자 데이터는 **\<script>** 태그를 포함할 수도 있으며 서버에서 실행되는 것처럼 실행될 수 있습니다.

- 클라이언트는 어떤 URL이라도 요청할 수 있습니다.

- 다음과 같이 복잡하거나 잘못된 경로를 고려하세요.

  - ..\ , 매우 긴 경로

  - 와일드카드 문자(*)의 사용

  - 토큰 확장(%토큰%)

  - 특별한 의미가 있는 이상한 형식의 경로

  - 특별한 의미가 있는 이상한 형식의 경로(예: `filename::$DATA`)

  - 짧은 파일 이름(예: `longfilename`의 경우 `longfi~1`)

- Eval(userdata)은 어떤 작업이든 수행할 수 있습니다.

- 런타임에 일부 사용자 데이터를 포함하는 이름에 바인딩하는 것을 주의하세요.

- 웹 데이터를 처리하는 경우에는 다음과 같이 허용 가능한 다양한 형식의 이스케이프를 고려하세요.

  - 16진수 이스케이프(%nn)

  - 유니코드 이스케이프(%nnn)

  - 과도하게 긴 UTF-8 이스케이프(%nn%nn)

  - 배정밀도 이스케이프(%nn은 %mmnn이 됨. 여기에서 %mm은 '%'의 이스케이프)

- 둘 이상의 정규 형식이 있을 수 있는 사용자 이름에 주의하세요. 예를 들어, 종종 MYDOMAIN\\*username* 형식 또는 *username*@mydomain.example.com 형식 중 하나를 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../../docs/standard/security/secure-coding-guidelines.md)
