---
title: ASP.NET Web Forms용 Blazor 개발자
description: Blazor 및 .NET Core를 사용하여 .NET을 통해 전체 스택 웹앱을 빌드하는 간단하고 친숙한 방법을 알아보세요.
author: danroth27
ms.author: daroth
ms.date: 09/11/2019
ms.openlocfilehash: 936f85d4fda9c5396a6586810735877488226157
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696928"
---
# <a name="blazor-for-aspnet-web-forms-developers"></a>ASP.NET Web Forms용 Blazor 개발자

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

![서버리스 앱 eBook 표지를 보여주는 스크린샷.](./media/index/blazor-for-web-forms-developers-cover.png)

> 다운로드 위치: <https://aka.ms/blazor-ebook>

게시자:

Microsoft 개발자 사업부, .NET 및 Visual Studio 제품 팀

Microsoft Corporation의 사업부

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2019 by Microsoft Corporation

All rights reserved. 이 가이드의 내용 중 어떤 부분도 게시자의 서면 허가 없이는 어떠한 형식이나 방법으로도 복제하거나 전송할 수 없습니다.

이 가이드는 작성자의 견해와 의견을 "있는 그대로" 제공하고 전달합니다. URL 및 기타 인터넷 웹 사이트 참조를 비롯하여 이 가이드에 제공된 견해, 의견 및 정보는 예고 없이 변경될 수 있습니다.

여기에 설명된 일부 예제는 예시 용도로만 제공되며 실제 데이터가 아닙니다. 실제로 연관시키거나 관련시키려고 의도하거나 추론해서는 안 됩니다.

"상표" 웹 페이지의 <https://www.microsoft.com>에 나열된 Microsoft 및 상표는 Microsoft 그룹 계열사의 상표입니다.

Mac 및 macOS는 Apple Inc.의 상표입니다.

기타 모든 표시와 로고는 해당 소유자의 자산입니다.

작성자:

> **[Daniel Roth](https://github.com/danroth27)** , 수석 프로그램 관리자, Microsoft Corp.

> **[Jeff Fritz](https://github.com/csharpfritz)** , 선임 프로그램 관리자, Microsoft Corp.

> **[Taylor Southwick](https://github.com/twsouthwick)** , 수석 소프트웨어 엔지니어, Microsoft Corp.

> **[Scott Addie](https://github.com/scottaddie)** , 수석 콘텐츠 개발자, Microsoft Corp.

## <a name="introduction"></a>소개

.NET은 모든 종류의 웹앱을 빌드할 수 있는 포괄적인 프레임워크 및 도구 집합인 ASP.NET을 통해 수많은 웹앱의 개발을 지원해 왔습니다. ASP.NET에는 클래식 ASP(Active Server Page)를 사용하여 완전히 다시 시작하는 웹 프레임워크 및 기술의 고유한 계보가 있습니다. ASP.NET Web Forms, ASP.NET MVC, ASP.NET 웹 페이지, 최신 ASP.NET Core 등과 같은 프레임워크는 *서버에서 렌더링된* 웹앱을 빌드하는 생산적이고 강력한 방법을 제공합니다. 여기서 UI 콘텐츠는 HTTP 요청에 응답하여 서버에서 동적으로 생성됩니다. ASP.NET 프레임워크마다 사용 대상과 앱 빌드 철학이 다릅니다. ASP.NET Web Forms는 .NET Framework의 원본 릴리스와 함께 제공되며, 간단한 이벤트 처리를 지원하는 재사용 가능한 UI 컨트롤과 같이 데스크톱 개발자에게 익숙한 많은 패턴을 사용하여 웹 개발을 지원합니다. 하지만 ASP.NET 제품에서는 사용자의 브라우저에서 실행되는 코드를 실행할 수 없습니다. 이렇게 하려면 JavaScript를 작성하고 jQuery, Knockout, Angular, React 등과 같은 다양한 JavaScript 프레임워크 및 도구를 사용해야 합니다.

[Blazor](https://blazor.net)는 .NET을 사용하여 웹앱을 빌드할 때 가능한 항목을 변경하는 새로운 웹 프레임워크입니다. Blazor는 JavaScript 대신 C#을 기반으로 하는 클라이언트 쪽 웹 UI 프레임워크입니다. Blazor를 사용하면 C#으로 클라이언트 쪽 논리 및 UI 구성 요소를 작성하여 일반 .NET 어셈블리로 컴파일한 다음 WebAssembly라는 새로운 개방형 웹 표준을 사용하여 브라우저에서 직접 실행할 수 있습니다. 또는 Blazor가 서버에서 .NET UI 구성 요소를 실행하고 브라우저를 사용하여 실시간 연결을 통해 모든 UI 상호 작용을 유동적으로 처리할 수 있습니다. 서버에서 실행되는 .NET과 연결된 경우 Blazor는 .NET을 통해 전체 스택 웹 개발을 지원할 수 있습니다. Blazor는 ASP.NET Web Forms와 많은 공통점을 공유하고(예: 재사용 가능한 구성 요소 모델 사용, 사용자 이벤트를 처리하는 간단한 방법), .NET Core를 기반으로 빌드되어 최신의 고성능 웹 개발 환경을 제공합니다.

이 책에서는 ASP.NET Web Forms 개발자에게 친숙하고 편리한 방식으로 Blazor를 소개합니다. Blazor 개념을 ASP.NET Web Forms의 유사 개념과 함께 소개하는 한편, 친숙하지 않은 새로운 개념도 설명합니다. 구성 요소 제작, 라우팅, 레이아웃, 구성, 보안 등 광범위한 항목과 문제를 다룹니다. 이 책의 내용은 주로 새로운 개발을 지원하기 위한 것이지만, 기존 앱을 현대화하려는 경우에 사용할 수 있도록 기존 ASP.NET Web Forms를 Blazor로 마이그레이션하기 위한 지침과 전략에 대해서도 설명합니다.

## <a name="who-should-use-the-book"></a>이 책의 대상 사용자

이 책은 기존 지식 및 기술과 관련된 Blazor를 도입하려는 ASP.NET Web Forms 개발자를 위한 것입니다. 이 책을 활용하여 새 Blazor 기반 프로젝트를 신속하게 시작하거나 기존 ASP.NET Web Forms 애플리케이션의 현대화를 위한 로드맵 차트를 작성할 수 있습니다.

## <a name="how-to-use-the-book"></a>책 사용 방법

이 책의 1부에서는 Blazor가 무엇인지를 설명하고 ASP.NET Web Forms를 통한 웹앱 개발과 비교합니다. 그런 다음 다양한 Blazor 항목을 장별로 설명하고 각 Blazor 개념을 ASP.NET Web Forms의 해당 개념과 연결하거나 완전히 새로운 개념을 설명합니다. 또한 이 책에서는 ASP.NET Web Forms 및 Blazor 모두에 구현된 전체 샘플 앱을 정기적으로 참조하여 Blazor 기능을 시연하고 ASP.NET Web Forms에서 Blazor로 마이그레이션하기 위한 사례 연구를 제공합니다. [GitHub](https://github.com/dotnet-architecture/eshoponblazor)에서 두 가지 샘플 앱(ASP.NET Web Forms 및 Blazor 버전) 구현을 모두 확인할 수 있습니다.

## <a name="what-this-book-doesnt-cover"></a>이 책에서 다루지 않는 내용

이 책은 Blazor를 소개하지만 포괄적인 마이그레이션 가이드가 아닙니다. ASP.NET Web Forms에서 Blazor로 프로젝트를 마이그레이션하는 방법에 대한 지침을 포함하고 있지만 미묘한 차이나 세부 사항에 대해서는 다루지 않습니다. ASP.NET에서 ASP.NET Core로 마이그레이션하는 방법에 대한 일반적인 지침은 ASP.NET Core 설명서의 [마이그레이션 지침](https://docs.microsoft.com/aspnet/core/migration/proper-to-2x/)을 참조하세요.

### <a name="additional-resources"></a>추가 자료

<https://blazor.net>에서 공식 Blazor 홈페이지 및 설명서를 확인할 수 있습니다.

## <a name="send-your-feedback"></a>피드백 보내기

이 책과 관련 샘플은 지속적으로 진화합니다. 여러분의 피드백을 기다리고 있습니다! 이 책을 향상시킬 수 있는 방법에 대한 의견이 있으면 [GitHub 문제](https://github.com/dotnet/docs/issues)에 빌드된 페이지의 맨 아래에서 피드백 섹션을 사용하세요.

>[!div class="step-by-step"]
>[다음](introduction.md)
