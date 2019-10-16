---
title: Azure Functions 서버 리스 앱
description: Azure 함수는 여러 언어 (C#, JavaScript, Java) 및 플랫폼에서 서버 리스 기능을 제공 하 여 이벤트 중심의 즉시 확장 코드를 제공 합니다.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 4febcc01eebf3efce3fc1eb42e19c2ec6c0baa52
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577606"
---
# <a name="azure-functions"></a>Azure Functions

Azure 함수는 서버를 사용 하지 않는 계산 환경을 제공 합니다. 함수는 *트리거* (예: HTTP 끝점 또는 타이머에 대 한 액세스)에 의해 호출 되며, 코드 블록 또는 비즈니스 논리를 실행 합니다. 또한 함수는 저장소 및 큐와 같은 리소스에 연결 하는 특수 *바인딩을* 지원 합니다.

![Azure 함수 로고](./media/azure-functions-logo.png)

Azure Functions 프레임 워크에는 두 가지 버전이 있습니다. 레거시 버전은 전체 .NET Framework을 지원 하 고 새 런타임은 플랫폼 간 .NET Core 응용 프로그램을 지원 합니다. JavaScript, F#및 C# Java와 같은 추가 언어를 사용할 수 있습니다. 포털에서 만든 함수는 풍부한 스크립팅 구문을 제공 합니다. 독립 실행형 프로젝트로 만들어진 함수는 전체 플랫폼 지원 및 기능을 사용 하 여 배포할 수 있습니다.

자세한 내용은 [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions)를 참조 하세요.

## <a name="functions-v1-vs-v2"></a>함수 v1 및 v2

Azure Functions 런타임에는 다음과 같은 두 가지 버전이 있습니다. 1.x 및 2.x. 버전 1.x를 일반적으로 사용할 수 있습니다 (GA). 포털 또는 Windows 컴퓨터에서 .NET 개발을 지원 하 고 .NET Framework를 사용 합니다. 1.x는 Python C#, PHP, TypeScript F#, Batch, Bash 및 PowerShell에 대 한 실험적 지원으로, JavaScript 및를 지원 합니다.

[버전 2.x는 이제 일반적으로 사용할 수](https://azure.microsoft.com/blog/introducing-azure-functions-2-0/)있습니다. .NET Core를 활용 하 고 Windows, macOS 및 Linux 컴퓨터에서 플랫폼 간 개발을 지원 합니다. 2.x는 Java에 대 한 첫 번째 클래스 지원을 추가 하지만 실험적 언어를 아직 직접 지원 하지는 않습니다. 버전 2.x는 플랫폼에 대 한 타사 확장, 바인딩의 독립적인 버전 관리 및 보다 간소화 된 실행 환경을 가능 하 게 하는 새로운 바인딩 확장성 모델을 사용 합니다.

> **바인딩과 관련 된 알려진 문제는 [바인딩 리디렉션 지원](https://github.com/Azure/azure-functions-host/issues/992)입니다.** 이 문제는 .NET 개발과 관련 된 것입니다. 런타임에 포함 된 라이브러리와 다른 버전의 라이브러리에 대 한 종속성이 있는 프로젝트는 영향을 받습니다. 함수 팀은 문제를 구체적으로 진행 하기 위해 최선을 다하고 있습니다. 팀은 일반 공급으로 전환 하기 전에 2.x의 바인딩 리디렉션을 처리 합니다. 제안 된 수정 사항 및 해결 방법을 제공 하는 공식 팀 명세서는 여기에서 제공 됩니다. [Azure Functions의 어셈블리 해상도](https://github.com/Azure/azure-functions-host/wiki/Assembly-Resolution-in-Azure-Functions)입니다.

자세한 내용은 1.x 및 2.x [비교](https://docs.microsoft.com/azure/azure-functions/functions-versions)를 참조 하세요.

## <a name="programming-language-support"></a>프로그래밍 언어 지원

GA (일반 공급), 미리 보기 또는 실험적에서 지원 되는 언어는 다음과 같습니다.

|언어      |1.x         |2.x      |
|--------------|------------|---------|
|**C#**        |GA          |Preview  |
|**JavaScript**|GA          |Preview  |
|**F#**        |GA          |         |
|**Java**      |            |Preview  |
|**Python**    |실험적|         |
|**PHP**       |실험적|         |
|**TypeScript**|실험적|         |
|**일괄 처리**     |실험적|         |
|**Bug**      |실험적|         |
|**PowerShell**|실험적|         |

자세한 내용은 [지원 언어](https://docs.microsoft.com/azure/azure-functions/supported-languages)를 참조하세요.

## <a name="app-service-plans"></a>App service 계획

함수는 *app service 계획*에 의해 지원 됩니다. 계획은 함수 앱에서 사용 하는 리소스를 정의 합니다. 지역에 계획을 할당 하 고, 사용 되는 가상 머신의 크기와 수를 결정 하 고, 가격 책정 계층을 선택할 수 있습니다. 서버를 사용 하지 않는 방식의 경우 함수 앱은 **소비** 계획을 사용할 수 있습니다. 소비 계획은 부하에 따라 백 엔드를 자동으로 확장 합니다.

자세한 내용은 [App service 계획](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)을 참조 하세요.

## <a name="create-your-first-function"></a>첫 번째 함수 만들기

세 가지 일반적인 방법으로 함수 앱을 만들 수 있습니다.

* 포털에서 함수를 스크립팅 합니다.
* Azure CLI (명령줄 인터페이스)를 사용 하 여 필요한 리소스를 만듭니다.
* 즐겨 사용 하는 IDE를 사용 하 여 함수를 로컬로 빌드하고 Azure에 게시 합니다.

포털에서 스크립팅된 함수를 만드는 방법에 대 한 자세한 내용은 [Azure Portal에서 첫 번째 함수 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)를 참조 하세요.

Azure CLI에서 빌드하려면 [Azure CLI를 사용 하 여 첫 번째 함수 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli)를 참조 하세요.

Visual Studio에서 함수를 만들려면 [Visual studio를 사용 하 여 첫 번째 함수 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio)를 참조 하세요.

## <a name="understand-triggers-and-bindings"></a>트리거 및 바인딩 이해

함수는 *트리거에서* 호출 하며 정확히 하나의 함수를 포함할 수 있습니다. 함수를 호출 하는 것 외에도 특정 트리거는 바인딩으로 사용 됩니다. 트리거와 함께 여러 바인딩을 정의할 수도 있습니다. *바인딩은* 데이터를 코드에 연결 하는 선언적 방법을 제공 합니다. 이러한 데이터는 (입력)에 전달 되거나 데이터를 받을 수 있습니다 (출력). 트리거 및 바인딩을 사용 하면 함수를 쉽게 사용할 수 있습니다. 바인딩은 데이터베이스 또는 파일 시스템 연결을 수동으로 만드는 오버 헤드를 제거 합니다. 바인딩에 필요한 모든 정보는 스크립트를 위한 json 파일 또는 코드에서 특성으로 선언 된 특수 한 함수에 포함 되어 *있습니다.*

몇 가지 일반적인 트리거는 다음과 같습니다.

* Blob Storage: 파일이 나 폴더가 저장소에서 업로드 또는 변경 될 때 함수를 호출 합니다.
* HTTP: REST API 처럼 함수를 호출 합니다.
* Queue: 큐에 항목이 있을 때 함수를 호출 합니다.
* Timer: 일반 흐름에서 함수를 호출 합니다.

바인딩의 예는 다음과 같습니다.

* CosmosDB: 데이터베이스에 쉽게 연결 하 여 파일을 로드 하거나 저장할 수 있습니다.
* Table Storage: 함수 앱에서 키/값 저장소로 작업 합니다.
* Queue Storage: 큐에서 항목을 쉽게 검색 하거나 새 항목을 큐에 넣습니다.

다음 예의 *함수 json* 파일은 트리거와 바인딩을 정의 합니다.

```json
{
  "bindings": [
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "$return",
      "type": "queue",
      "direction": "out",
      "queueName": "images",
      "connection": "AzureWebJobsStorage"
    }
  ],
  "disabled": false
}
```

이 예제에서 함수는 `images` 컨테이너의 blob 저장소에 대 한 변경 내용에 의해 트리거됩니다. 파일에 대 한 정보는 전달 되기 때문에 트리거도 바인딩 역할을 합니다. 라는 `images`큐에 정보를 넣는 또 다른 바인딩이 있습니다.

다음은 함수 C# 에 대 한 스크립트입니다.

```csharp
public static string Run(Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
    return name;
}
```

예제는 blob 저장소에 수정 또는 업로드 된 파일의 이름을 사용 하 고 나중에 처리할 수 있도록 큐에 배치 하는 간단한 함수입니다.

트리거와 바인딩의 전체 목록은 [Azure Functions 트리거 및 바인딩 개념](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)을 참조 하세요.

## <a name="proxies"></a>프록시

프록시는 응용 프로그램에 대 한 리디렉션 기능을 제공 합니다. 프록시는 끝점을 노출 하 고 해당 끝점을 다른 리소스에 매핑합니다. 프록시를 사용 하 여 다음을 수행할 수 있습니다.

* 들어오는 요청을 다른 끝점으로 경로 바꾸기
* 들어오는 요청을 전달 하기 전에 수정 합니다.
* 응답을 수정 하거나 제공 합니다.

프록시는 다음과 같은 시나리오에 사용 됩니다.

* URL을 단순화, 단축 또는 변경 합니다.
* 여러 백 엔드 서비스에 일관 된 API 접두사 제공
* 개발 중인 끝점에 대 한 응답을 모의 합니다.
* 잘 알려진 끝점에 정적 응답을 제공 합니다.
* 백 엔드를 이동 하거나 마이그레이션하는 동안 API 끝점을 일관 되 게 유지 합니다.

프록시는 JSON 정의로 저장 됩니다. 다음 예를 참조하세요.

```json
{
  "$schema": "http://json.schemastore.org/proxies",
  "proxies": {
    "Domain Redirect": {
      "matchCondition": {
        "route": "/{shortUrl}"
      },
      "backendUri": "http://%WEBSITE_HOSTNAME%/api/UrlRedirect/{shortUrl}"
    },
    "Root": {
      "matchCondition": {
        "route": "/"
      },
      "responseOverrides": {
        "response.statusCode": "301",
        "response.statusReason": "Moved Permanently",
        "response.headers.location": "https://docs.microsoft.com/"
      }
    }
  }
}
```

프록시 `Domain Redirect` 는 약식 경로를 사용 하 여 더 긴 함수 리소스에 매핑합니다. 변환은 다음과 같습니다.

`https://--shorturl--/123` -> `https://--longurl--.azurewebsites.net/api/UrlRedirect/123`

프록시 `Root` 는 루트 URL (`https://--shorturl--/`)로 전송 된 모든 항목을 가져와서 설명서 사이트로 리디렉션합니다.

프록시를 사용 하는 예는 비디오 [Azure에 나와 있습니다. 서버를 사용 하지 않는 Azure Functions](https://channel9.msdn.com/events/Connect/2017/E102)를 사용 하 여 앱을 클라우드로 가져옵니다. 실시간으로 로컬 SQL Server에서 실행 되는 ASP.NET Core 응용 프로그램은 Azure 클라우드로 마이그레이션됩니다. 프록시는 함수를 사용 하기 위해 기존 Web API 프로젝트를 리팩터링 하는 데 사용 됩니다.

프록시에 대 한 자세한 내용은 [Azure Functions 프록시 사용](https://docs.microsoft.com/azure/azure-functions/functions-proxies)을 참조 하세요.

>[!div class="step-by-step"]
>[이전](azure-serverless-platform.md)
>[다음](application-insights.md)
