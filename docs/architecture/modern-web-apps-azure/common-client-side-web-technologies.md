---
title: 일반 클라이언트측 웹 기술
description: ASP.NET Core 및 Azure를 사용하여 현대식 웹 애플리케이션 설계 | 일반 클라이언트측 웹 기술
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 4dd747293fba4c18c2d10738d36f4d98cfd3f5b9
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926496"
---
# <a name="common-client-side-web-technologies"></a>일반 클라이언트측 웹 기술

> “웹 사이트는 안팎으로 보기에 좋아야 합니다.”  
> _- Paul Cookson_

ASP.NET Core 애플리케이션은 웹 애플리케이션이며 일반적으로 HTML, CSS 및 JavaScript와 같은 클라이언트측 웹 기술에 의존합니다. 레이아웃과 스타일(CSS), 동작(JavaScript를 통해)에서 페이지(HTML)의 콘텐츠를 분리하면 복잡한 웹앱에서 관심사 분리 원칙을 활용할 수 있습니다. 이러한 관심사가 긴밀히 연결되어 있지 않으면 향후에 애플리케이션의 구조, 디자인 또는 동작을 더 쉽게 변경할 수 있습니다.

HTML 및 CSS는 상대적으로 안정적인 반면, JavaScript는 웹 기반 애플리케이션 빌드를 위해 애플리케이션 프레임워크와 유틸리티 개발자가 함께 일하는 덕분에 빠른 속도로 발전하고 있습니다. 이 장에서는 Angular 및 React 클라이언트측 라이브러리의 간단한 개요를 제공하면서 웹 개발자가 애플리케이션 개발의 일환으로 JavaScript를 사용하는 몇 가지 방법에 대해 살펴봅니다.

## <a name="html"></a>HTML

HTML(HyperText Markup Language)은 웹 페이지 및 웹 애플리케이션을 만드는 데 사용되는 표준 표시 언어입니다. 해당 요소는 서식 있는 텍스트, 이미지, 입력 구성 및 다른 구조를 나타내는 페이지의 구성 요소를 형성합니다. 브라우저가 URL에 대한 요청을 만들 때 페이지나 애플리케이션을 페치하는지 상관 없이 가장 먼저 반환되는 것은 HTML 문서입니다. 이 HTML 문서는 CSS 양식의 모양과 레이아웃에 대한 추가 정보 또는 JavaScript 양식의 동작을 참조하거나 포함할 수 있습니다.

## <a name="css"></a>CSS

CSS(CSS 스타일시트)는 HTML 요소의 모양과 레이아웃을 제어하는 데 사용됩니다. CSS 스타일은 HTML 요소에 직접 적용되고, 동일한 페이지에서 별도로 정의되거나 개별 파일로 정의되며, 페이지별로 참조될 수 있습니다. 스타일은 주어진 HTML 요소를 선택하는 데 사용되는 방식에 따라 계단식으로 배열됩니다. 예를 들어 스타일은 전체 문서에 적용될 수도 있지만 특정 요소에 적용되는 스타일에 의해 재정의됩니다. 마찬가지로, 요소 관련 스타일은 요소에 적용된 CSS 클래스에 적용되는 스타일에 의해 재정의됩니다. 그 다음으로 해당 요소의 특정 인스턴스를 대상으로 하는 스타일에 의해 재정의됩니다(해당 ID를 통해). 그림 6-1

![CSS 특이성 규칙](./media/image6-1.png)

**그림 6-1.** 순서 대로 CSS 특이성 규칙

자체 개별 스타일시트의 스타일을 유지하고 선택 영역 기반 계단식 배열을 사용하여 애플리케이션 내에서 스타일의 일관성 및 재사용을 구현하는 것이 가장 좋습니다. HTML 내에 스타일 규칙을 배치하지 말아야 하며, 스타일을 특정 개별 요소(요소의 전체 클래스 또는 특정 CSS 클래스가 적용되어 있는 요소 아님)에 적용하는 것은 규칙이 아닌 예외여야 합니다.

### <a name="css-preprocessors"></a>CSS 프로세서

CSS 스타일시트에는 조건부 논리, 변수 및 다른 프로그래밍 언어의 기능에 대한 지원이 부족합니다. 따라서 같은 색, 글꼴 또는 기타 설정이 HTML 요소 및 CSS 클래스의 여러 다른 변형에 적용되는 것처럼 큰 스타일 시트에는 종종 많은 반복이 포함됩니다. CSS 프로세서는 변수 및 논리에 대한 지원을 추가하여 [DRY 원칙](https://deviq.com/don-t-repeat-yourself/)을 따르는 사용자의 스타일시트에 도움이 될 수 있습니다.

가장 인기 있는 CSS 프로세서는 Sass와 LESS입니다. 둘 다 CSS를 확장하며 이전 버전과 호환됩니다. 즉, 일반 CSS 파일은 유효한 Sass 또는 LESS 파일입니다. Sass는 Ruby를 기반으로 하며, LESS는 JavaScript를 기반으로 합니다. 일반적으로 둘 다 로컬 개발 프로세스의 일환으로 실행합니다. 둘 다 Gulp 또는 Grunt 작업을 사용하여 실행할 수 있도록 Visual Studio의 기본 제공 지원뿐만 아니라 사용 가능한 명령줄 도구가 있습니다.

## <a name="javascript"></a>JavaScript

JavaScript는 ECMAScript 언어 사양에 표준화된 동적이고 해석된 프로그래밍 언어이며, 웹의 프로그래밍 언어입니다. CSS와 마찬가지로 JavaScript는 페이지 내 또는 개별 파일의 스크립트 차단과 같이 HTML 요소 내 특성으로 정의될 수 있습니다. CSS와 마찬가지로, 일반적으로 JavaScript를 개별 웹 페이지나 애플리케이션 뷰에 있는 HTML로부터 최대한 분리하여 별도 파일에 구성하는 것이 좋습니다.

웹 애플리케이션에서 JavaScript를 작업할 때 일반적으로 수행해야 하는 다음과 같은 몇 가지 작업이 있습니다.

- HTML 요소를 선택하고 해당 값을 검색 및/또는 업데이트.

- 데이터에 대한 Web API 쿼리.

- Web API에 대한 명령 전송(및 해당 결과가 포함된 콜백에 응답).

- 유효성 검사 수행.

이러한 작업은 모두 JavaScript만 사용하여 수행할 수도 있지만, 이러한 작업을 쉽게 수행할 수 있도록 해주는 다양한 라이브러리가 있습니다. 이러한 라이브러리 중 첫 번째이자 가장 성공적인 것은 jQuery로, 웹 페이지에서 이러한 작업을 간소화하는 데 꾸준히 많이 사용됩니다. SPA(단일 페이지 애플리케이션)의 경우 jQuery는 Angular 및 React가 제공하는 원하는 기능을 많이 제공하지 않습니다.

### <a name="legacy-web-apps-with-jquery"></a>jQuery를 사용한 레거시 웹앱

JavaScript 프레임워크 표준에서 유래되었음에도 jQuery는 여전히 HTML/CSS로 작업하고 웹 API에 대한 AJAX 호출을 수행하는 애플리케이션을 빌드하기 위해 매우 일반적으로 사용되는 라이브러리입니다. 그러나 jQuery는 브라우저 DOM(문서 개체 모델)의 수준에서 작동하며, 기본적으로 선언적이 아닌 명령적 모델을 제공합니다.

예를 들어 텍스트 상자의 값이 10을 초과하는 경우 페이지에 요소가 표시되어야 합니다. jQuery에서는 일반적으로 텍스트 상자의 값을 검사하고 해당 값에 따라 대상 요소의 표시 여부를 설정하는 코드를 사용하여 이벤트 처리기를 작성하면 이를 구현할 수 있습니다. 이는 명령형 코드 기반 방법입니다. 대신 다른 프레임워크가 데이터 바인딩을 사용하여 텍스트 상자의 값에 따라 요소의 표시 여부를 선언적으로 바인딩할 수 있습니다. 코드를 작성할 필요는 없으나, 대신 데이터 바인딩 특성이 포함된 요소를 데코레이팅해야 합니다. 클라이언트측 동작이 더 복잡해짐에 따라 데이터 바인딩 방식은 코드 및 조건부 복잡성이 덜한 더 간단한 솔루션이 됩니다.

### <a name="jquery-vs-a-spa-framework"></a>jQuery 대 SPA 프레임워크

| **요소** | **jQuery** | **Angular**|
|--------------------------|------------|-------------|
| DOM 추상화 | **예** | **예** |
| AJAX 지원 | **예** | **예** |
| 선언적 데이터 바인딩 | **No** | **예** |
| MVC 스타일 라우팅 | **No** | **예** |
| 템플릿 | **No** | **예** |
| 딥 링크 라우팅 | **No** | **예** |

대부분의 jQuery 기능 부족은 본질적으로 다른 라이브러리를 추가하여 채울 수 있습니다. 그러나 Angular와 같은 SPA 프레임워크는 이러한 기능을 더 통합된 방식으로 제공합니다. 처음부터 이러한 사항 모두를 고려하여 설계되었기 때문입니다. 또한 jQuery는 매우 명령적 라이브러리입니다. 즉, jQuery를 사용한 작업을 수행하려면 jQuery 함수를 호출해야 합니다. SPA 프레임워크가 제공하는 많은 작업과 기능은 실제 코드를 작성할 필요 없이 선언적으로 수행될 수 있습니다.

데이터 바인딩은 이에 대한 좋은 예입니다. jQuery에서는 일반적으로 단 한 줄의 코드로 DOM 요소의 값을 가져오거나 요소의 값을 설정합니다. 단, 이 코드는 요소의 값을 변경해야 때마다 작성해야 하며, 경우에 따라 이는 페이지의 여러 기능에서 발생됩니다. 또 다른 일반적인 예제는 요소 표시 유형입니다. jQuery에서는 여러 다른 위치에서 특정 요소를 표시할지 여부를 제어하는 코드를 작성해야 할 수 있습니다. 이러한 각각의 경우에서 데이터 바인딩을 사용할 때 코드를 작성할 필요가 없습니다. 문제의 값 또는 요소의 표시 여부를 페이지의 *viewmodel*에 바인딩하기만 하면 해당 viewmodel에 대한 변경 사항이 자동으로 바인딩된 요소에 반영됩니다.

### <a name="angular-spas"></a>Angular SPA

AngularJS는 빠르게 세계에서 가장 인기 있는 JavaScript 프레임워크 중 하나가 되었습니다. Angular 2를 사용하면 팀이 처음부터 프레임워크를 다시 빌드하고([TypeScript](https://www.typescriptlang.org/) 사용) AngularJS에서 간단히 Angular로 브랜드를 변경할 수 있습니다. 버전 4인 현재 Angular는 여전히 단일 페이지 애플리케이션을 빌드하기 위한 강력한 프레임워크입니다.

Angular 애플리케이션은 구성 요소에서 빌드됩니다. 구성 요소는 특정 개체와 HTML 템플릿을 결합하고 페이지의 일부를 제어합니다. Angular 문서의 간단한 구성 요소는 다음과 같습니다.

```js
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<h1>Hello {{name}}</h1>`
})

export class AppComponent { name = 'Angular'; }
```

구성 요소는 @Component 데코레이터 함수를 사용하여 정의되며 구성 요소에 대한 메타데이터에 위치합니다. 선택기 속성은 이 구성 요소가 표시되는 페이지에서 요소의 ID를 식별합니다. 템플릿 속성은 마지막 줄에 정의되는 구성 요소의 이름 속성에 해당하는 자리 표시자를 포함하는 간단한 HTML 템플릿입니다.

DOM 요소 대신 구성 요소 및 템플릿을 사용하면 Angular 앱은 추상화의 상위 수준에서 작업할 수 있으며 JavaScript만(“바닐라 JS”라고 함) 또는 jQuery를 사용하여 작성된 앱보다 전체 코드가 더 적습니다. 또한 Angular는 클라이언트 쪽 스크립트 파일을 구성하는 방식에 몇 가지 순서를 적용합니다. 규칙에 따라 Angular 앱은 앱 폴더에 모듈 및 구성 요소 스크립트 파일이 포함된 일반적인 폴더 구조를 사용합니다. 앱의 빌드, 배포 및 테스트와 관련된 Angular 스크립트는 일반적으로 상위 폴더에 위치합니다.

또한 Angular는 CLI(명령줄 인터페이스) 도구를 적절히 사용합니다. 로컬에서 Angular 개발을 시작하면(이미 git 및 npm이 설치되어 있다고 가정) 바로 GitHub에서 리포지토리 복제가 구성되고 `npm install` 및 `npm start`가 실행됩니다. 이 외에 Angular는 프로젝트를 만들고, 파일을 추가하고, 테스트, 묶음 및 배포 작업을 지원할 수 있는 자체 CLI 도구를 함께 제공합니다. 이 CLI 도구 친화성 덕분에 Angular는 특별히 탁월한 CLI 지원이 특징인 ASP.NET Core와 호환됩니다.

Microsoft는 Angular SPA 구현을 포함하는 [eShopOnContainers](https://aka.ms/MicroservicesArchitecture)라는 참조 애플리케이션을 개발했습니다. 이 앱에는 온라인 상점의 장바구니를 관리하고, 해당 카탈로그의 항목을 로드 및 표시하며, 주문 생성을 처리하는 Angular 모듈이 포함됩니다. [GitHub](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Web/WebSPA)에서 샘플 애플리케이션을 보고 다운로드할 수 있습니다.

### <a name="react"></a>React

전체 모델-뷰-컨트롤러 패턴 구현을 제공하는 Angular와 달리, React는 오직 뷰와 관련이 있습니다. 프레임워크가 아닌 라이브러리일 뿐이므로 SPA를 빌드하려면 추가 라이브러리를 활용해야 합니다.

React의 가장 중요한 기능 중 하나는 가상 DOM을 사용하는 것입니다. 가상 DOM은 React에 성능(가상 DOM은 업데이트가 필요한 실제 DOM의 부분을 최적화할 수 있음) 및 테스트 용이성(React와 해당 가상 DOM과의 상호 작용을 테스트하기 위해 브라우저가 필요하지 않음)을 포함한 여러 장점을 제공합니다.

또한 React는 HTML과 작동하는 방식 작동 방식이 특이합니다. 코드 및 표시 사이를 엄격히 구분하지 않으면서(아마 HTML 특성에 표시되는 JavaScript에 대한 참조 사용) React는 HTML을 직접 해당 JavaScript 코드 내에 JSX로 추가합니다. JSX는 순수 JavaScript로 컴파일 다운할 수 있는 HTML 스타일의 구문입니다. 예:

```js
<ul>
{ authors.map(author =>
    <li key={author.id}>{author.name}</li>
)}
</ul>
```

JavaScript에 대해 이미 알고 있다면 React는 이해하기 쉬울 것입니다. Angular 또는 다른 인기 있는 라이브러리를 사용하는 것만큼 곡선이나 특수 구문이 거의 포함되어 있지 않습니다.

React는 전체 프레임워크가 아니므로 라우팅, 웹 API 호출 및 종속성 관리와 같은 작업을 처리하기 위해 일반적으로 다른 라이브러리가 필요할 수도 있습니다. 장점은 이러한 각 작업에 최선의 라이브러리를 사용자가 고를 수 있다는 점이며, 단점은 이러한 모든 결정을 사용자가 내려야 하며, 작업을 완료했을 때 함께 제대로 작동하는지 선택한 모든 라이브러리의 유효성을 검사해야 한다는 점입니다. 시작점을 찾고 있다면, 일련의 호환 가능한 라이브러리를 React와 함께 패키지로 묶은 React Slingshot 같은 시작키트를 사용해 보세요.

### <a name="choosing-a-spa-framework"></a>SPA 프레임워크 선택

SPA를 지원하기에 어떤 JavaScript 프레임워크가 최선인지를 고려할 때는 다음 고려 사항을 염두에 두어야 합니다.

- 팀이 프레임워크 및 해당 종속성에 대해 잘 알고 있는가(일부 경우에 TypeScript 포함)?

- 프레임워크는 얼마나 독단적인가? 그리고 그러한 작업을 수행하는 기본 방식에 동의하는가?

- 프레임워크(또는 도우미 라이브러리)에 앱에 필요한 모든 기능이 포함되어 있는가?

- 문서화가 잘 되어 있는가?

- 해당 커뮤니티는 얼마나 활발한가? 해당 프레임워크를 사용하여 새 프로젝트가 빌드되고 있는가?

- 해당 코어 팀은 얼마나 활발한가? 문제가 해결되고 있는가? 또 새 버전이 정기적으로 제공되는가?

JavaScript 프레임워크는 지속적으로 매우 빠르게 발전하고 있습니다. 나중에 종속된 것을 후회하게 될 프레임워크의 선택 위험을 완화하는 데 도움을 받으려면 위에 나열된 고려 사항을 사용하세요. 특히 안전 주의자인 경우 상용 지원을 제공하고 또는 대기업에서 개발되는 프레임워크를 고려하세요.

> ### <a name="references--client-web-technologies"></a>참조 - 클라이언트 웹 기술
>
> - **HTML 및 CSS**  
> <https://www.w3.org/standards/webdesign/htmlcss>
> - **Sass 대 LESS**  
> <https://www.keycdn.com/blog/sass-vs-less/>
> - **LESS, Sass 및 Font Awesome을 사용하여 ASP.NET Core 앱 스타일 지정**  
> <https://docs.microsoft.com/aspnet/core/client-side/less-sass-fa>
> - **ASP.NET Core의 클라이언트측 개발**  
> <https://docs.microsoft.com/aspnet/core/client-side/>
> - **jQuery**  
> <https://jquery.com/>
> - **jQuery 대 AngularJS**  
> <https://www.airpair.com/angularjs/posts/jquery-angularjs-comparison-migration-walkthrough>
> - **Angular**  
> <https://angular.io/>
> - **React**  
> <https://facebook.github.io/react/>
> - **React Slingshot**  
> <https://github.com/coryhouse/react-slingshot>
> - **React 대 Angular 2 비교**  
> <https://www.codementor.io/codementorteam/react-vs-angular-2-comparison-beginners-guide-lvz5710ha>
> - **2017년 최고 JavaScript 프레임워크 5위**  
> <https://hackernoon.com/5-best-javascript-frameworks-in-2017-7a63b3870282>

>[!div class="step-by-step"]
>[이전](common-web-application-architectures.md)
>[다음](develop-asp-net-core-mvc-apps.md)
