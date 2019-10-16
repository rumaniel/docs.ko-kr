---
title: WCF 개발자를 위한 ASP.NET Core gRPC - WCF 개발자를 위한 gRPC
description: 작성할 항목
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: dc39fc96e7154fb50acd0b65a58586b3fa12ab50
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696913"
---
# <a name="aspnet-core-grpc-for-wcf-developers"></a>WCF 개발자를 위한 ASP.NET Core gRPC

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

![표지 이미지](./media/cover.png)

게시자:

Microsoft 개발자 사업부, .NET 및 Visual Studio 제품 팀

Microsoft Corporation의 사업부

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2019 by Microsoft Corporation

All rights reserved. 이 가이드의 내용 중 어떤 부분도 게시자의 서면 허가 없이는 어떠한 형식이나 방법으로도 복제하거나 전송할 수 없습니다.

이 가이드는 작성자의 견해와 의견을 “있는 그대로” 제공하고 전달합니다. URL 및 기타 인터넷 웹 사이트 참조를 비롯하여 이 가이드에 제공된 견해, 의견 및 정보는 예고 없이 변경될 수 있습니다.

여기에 설명된 일부 예제는 예시 용도로만 제공되며 실제 데이터가 아닙니다. 실제로 연관시키거나 관련시키려고 의도하거나 추론해서는 안 됩니다.

“상표” 웹 페이지의 https://www.microsoft.com 에 나열된 Microsoft 및 상표는 Microsoft 그룹 계열사의 상표입니다.

Docker 고래 로고는 Docker, Inc.의 등록 상표로, 허가하에 사용됩니다.

기타 모든 표시와 로고는 해당 소유자의 자산입니다.

만든 이:

> **Mark Rendle** - 최고 기술 책임자 - [Visual Recode](https://visualrecode.com)
>
> **Miranda Steiner** - 기술 작성자

편집자:

> **Maira Wenzel** - 선임 콘텐츠 개발자 - Microsoft

## <a name="introduction"></a>소개

TODO

## <a name="purpose"></a>용도

TODO

## <a name="who-should-use-this-guide"></a>이 가이드의 대상 사용자

**이 항목 업데이트**

이 가이드의 대상 사용자는 gRPC 서비스를 사용하여 .NET 4 이전 버전의 WCF 솔루션을 ASP.NET Core 3.0으로 마이그레이션하려는 WCF 개발자, 개발 책임자 및 설계자입니다.

## <a name="how-you-can-use-this-guide"></a>이 가이드를 사용하는 방법

**이 항목 업데이트**

다음은 WCF에 대한 특정 참조를 유사한 플랫폼으로 사용하여 ASP.NET Core 3.0에서 gRPC 서비스를 빌드하는 방법에 대한 간략한 소개입니다. 여기서는 각 개념을 WCF의 해당 기능과 연계하여 gRPC의 원칙을 설명하고 기존 WCF 애플리케이션을 gRPC로 마이그레이션하기 위한 지침을 제공합니다. 또한 WCF를 경험하고 새 서비스를 빌드하기 위해 gRPC를 알아보려는 개발자에게 유용합니다. 애플리케이션 예제를 사용자 프로젝트를 위한 템플릿 또는 참조로 사용하고, 가이드 또는 샘플에서 코드를 복사하여 재사용할 수 있습니다.

이 가이드를 팀에서 자유롭게 공유하고 이러한 여러가지 고려 사항과 기회에 대한 이해를 도모하세요. 모든 사람이 공통적인 용어와 기본 원칙으로 작업하도록 하면 아키텍처 패턴및 사례를 일관성 있게 적용하는 데 도움이 됩니다.

## <a name="references"></a>참조

- **gRPC 웹 사이트**  
  <https://grpc.io>
- **서버 앱에 대해 .NET Core와 .NET Framework 중에 선택**  
  <https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server>

>[!div class="step-by-step"]
>[다음](introduction.md)
