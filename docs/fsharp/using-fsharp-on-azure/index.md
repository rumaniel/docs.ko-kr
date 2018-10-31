---
title: Azure에서 F# 사용
description: 'F #을 사용 하 여 Azure 서비스 사용에 대 한 가이드'
author: sylvanc
ms.date: 09/22/2016
ms.openlocfilehash: 1fbb85a07fc057c1b89a4c4a1ad356066cebf2b8
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201506"
---
# <a name="using-f-on-azure"></a>Azure에서 F# 사용

F#은 클라우드 프로그래밍의 뛰어난 언어이며 웹 응용 프로그램, 클라우드 서비스, 클라우드 호스티드 마이크로 서비스를 작성하는 데 자주 사용되고 확장 가능한 데이터 처리에도 사용됩니다.

다음 섹션에서 F#과 함께 다양한 Azure 서비스를 사용하는 방법에 대한 리소스를 찾아볼 수 있습니다.

> [!NOTE]
> 특정 Azure 서비스가 이러한 설명서 집합에 소개되지 않은 경우 해당 서비스에 대한 Azure Functions 또는 .NET 설명서를 참조하세요. 일부 Azure 서비스는 언어의 구애를 받지 않으며 언어와 관련된 설명서를 요구하지 않고 여기에 나열되지도 않습니다.

## <a name="using-azure-virtual-machines-with-f"></a>F #을 사용 하 여 Azure Virtual Machines를 사용 하 여 #

Azure는 다양한 VM(가상 머신) 구성을 지원합니다. [Linux 및 Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/)를 참조하세요.

가상 머신에서 F#을 실행하고 컴파일하거나 스크립팅하도록 설치하려면 [Using F# on Linux](https://fsharp.org/use/linux)(Linux에서 F# 사용) 및 [Using F# on Windows](https://fsharp.org/use/windows)(Windows에서 F# 사용)를 참조하세요.


## <a name="using-azure-functions-with-f"></a>Azure Functions F # 사용 #

[Azure Functions](https://azure.microsoft.com/services/functions/)는 클라우드에서 소량의 코드 또는 "함수"를 쉽게 실행하기 위한 솔루션입니다. 전체 응용 프로그램 또는 이를 실행하는 인프라에 대해 걱정하지 않고, 당면한 문제에 필요한 코드만 작성할 수 있습니다. 함수는 Azure 저장소 및 기타 클라우드에 호스트된 리소스의 이벤트에 연결됩니다. 데이터는 함수 인수를 통해 F# 함수로 흐릅니다. Azure는 필요에 따라 크기를 조정할 수 있으므로 안심하고 선택한 개발 언어를 사용할 수 있습니다.

Azure Functions는 F# 코드의 효율적이고 반응적이며 확장 가능한 실행을 통해 F#을 최고의 언어로 지원합니다. Azure Functions와 함께 F#을 사용하는 방법에 대한 참조 설명서는 [Azure Functions F# 개발자 참조](/azure/azure-functions/functions-reference-fsharp)를 참조하세요.

Azure Functions 및 F# 사용에 대한 기타 리소스:

* [Suave를 사용하여 F#에서 Azure Functions 확장](https://blog.tamizhvendan.in/blog/2016/09/19/scale-up-azure-functions-in-f-number-using-suave/)
* [F#으로 Azure 함수를 만드는 방법](https://mnie.github.io/2016-09-08-AzureFunctions/)
* [Azure Functions를 사용 하 여 Azure 형식 공급자를 사용 하 여](https://compositional-it.com/blog/2017/08-30-using-the-azure-type-provider-with-azure-functions/index.html)

## <a name="using-azure-storage-with-f"></a>F #을 사용 하 여 Azure Storage를 사용합니다. #

Azure Storage는 내구성, 가용성, 확장성을 활용하여 고객의 요구 사항을 충족하는 최신 응용 프로그램을 위한 저장소 서비스의 기본 레이어입니다. F#프로그램은 다음 문서에서 설명한 기술을 사용 하 여 Azure 저장소 서비스에 직접 상호 작용할 수 있습니다.

* [F#을 사용하여 Azure Blob Storage 시작](blob-storage.md)
* [F#을 사용하여 Azure File Storage 시작](file-storage.md)
* [F#을 사용하여 Azure Queue Storage 시작](queue-storage.md)
* [F#을 사용하여 Azure Table Storage 시작](table-storage.md)

명시적 API 호출이 아닌 선언적 구성을 통해 Azure Functions와 함께 Azure Storage를 사용할 수도 있습니다. F# 예제를 포함하는 [Azure Storage를 위한 Azure Functions 트리거 및 바인딩](/azure/azure-functions/functions-bindings-storage)을 참조하세요.

## <a name="using-azure-app-service-with-f"></a>F #을 사용 하 여 Azure App Service를 사용 하 여 #

[Azure App Service](https://azure.microsoft.com/services/app-service/)는 클라우드 또는 온-프레미스 내 어디서든 데이터에 연결되는 강력한 웹 및 모바일 앱을 빌드하는 클라우드 플랫폼입니다.

* [F# Azure 웹 API 예제](https://github.com/fsprojects/azure-webapi-example)
* [Azure의 웹 응용 프로그램에서 F# 호스트](https://github.com/isaacabraham/fsharp-demonstrator)

## <a name="using-apache-spark-with-f-with-azure-hdinsight"></a>F#을 사용한 Apache Spark와 함께 Azure HDInsight 사용

[Azure HDInsight용 Apache Spark](https://azure.microsoft.com/services/hdinsight/apache-spark/)는 대규모 데이터 분석 응용 프로그램을 실행하는 오픈 소스 처리 프레임워크입니다. Azure는 배포하기에 간단하고 비용 효과적인 Apache Spark를 만듭니다. Spark용 .NET API인 [Mobius](https://github.com/Microsoft/Mobius)를 사용하여 F#으로 Spark 응용 프로그램을 개발합니다.

* [Mobius를 사용하여 F#으로 Spark 앱 구현](https://github.com/Microsoft/Mobius/blob/master/notes/spark-fsharp-mobius.md)
* [Mobius를 사용하는 예제 F# Spark 앱](https://github.com/Microsoft/Mobius/tree/master/examples/fsharp)

## <a name="using-azure-cosmos-db-with-f"></a>F #을 사용 하 여 Azure Cosmos DB를 사용 하 여 #

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db) 는 가용성이 뛰어나고 전역으로 분산 된 앱에 대 한 NoSQL 서비스입니다.

두 가지 방법으로 F #을 사용 하 여 azure Cosmos DB은 사용할 수 있습니다.

1. F # Azure Functions 생성을 통해 반응 하는 또는 Azure Cosmos DB 컬렉션을 변경 합니다. 참조 [Azure Functions의 Azure Cosmos DB 바인딩](/azure/azure-functions/functions-bindings-cosmosdb), 또는
2. 사용 하 여 합니다 [SQL API에 대 한 Azure Cosmos DB.NET SDK](/azure/cosmos-db/sql-api-sdk-dotnet)합니다. 관련된 샘플 C#의 경우

## <a name="using-azure-event-hubs-with-f"></a>F #을 사용 하 여 Azure Event Hubs를 사용 하 여 #

[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/)는 웹 사이트, 앱 및 장치에서 클라우드 규모의 원격 분석 수집을 제공합니다.

Azure Event Hubs는 다음과 같은 두 가지 방법으로 F#과 함께 사용할 수 있습니다.

1. 이벤트에 의해 트리거되는 F# Azure Functions의 생성을 통해. [Event Hubs에 대한 Azure Function 트리거](/azure/azure-functions/functions-bindings-event-hubs)를 참조하세요.
2. [Azure용 .NET SDK](/azure/event-hubs/event-hubs-csharp-ephcs-getstarted)를 사용하여. 이러한 예제는 C#으로 작성됩니다.

## <a name="using-azure-notification-hubs-with-f"></a>F #을 사용 하 여 Azure Notification Hubs를 사용 하 여 #

[Azure Notification Hubs](/azure/notification-hubs/)는 백 엔드(클라우드 또는 온-프레미스)에서 임의의 모바일 플랫폼으로 모바일 푸시 알림을 보낼 수 있도록 지원하는 다중 플랫폼의 확장된 푸시 인프라입니다.

Azure Notification Hubs는 다음과 같은 두 가지 방법으로 F#과 함께 사용할 수 있습니다.

1. 알림 허브로 결과를 보내는 F# Azure Functions 생성을 통해. [Notification Hubs에 대한 Azure Function 출력 트리거](/azure/azure-functions/functions-bindings-notification-hubs)를 참조하세요.
2. [Azure용 .NET SDK](https://blogs.msdn.microsoft.com/azuremobile/2014/04/08/push-notifications-using-notification-hub-and-net-backend/)를 사용하여. 이러한 예제는 C#으로 작성됩니다.


## <a name="implementing-webhooks-on-azure-with-f"></a>F #을 사용 하 여 Azure에서 Webhook 구현 #

[Webhook](https://en.wikipedia.org/wiki/Webhook)는 웹 요청을 통해 트리거되는 콜백입니다. Webhook는 신호 이벤트에 대한 GitHub와 같은 사이트에 사용됩니다. 

Webhook은 [F#의 Azure Function 및 Webhook 바인딩](/azure/azure-functions/functions-bindings-http-webhook)을 통해 Azure에서 F#으로 구현하고 호스트할 수 있습니다.

## <a name="using-webjobs-with-f"></a>F #과 함께 Webjobs 사용 #

[WebJobs](/azure/app-service-web/web-sites-create-web-jobs)는 주문형, 지속형, 예약형의 세 가지 방법으로 App Service 웹앱에서 실행할 수 있는 프로그램입니다.

[예제 F# WebJobs](https://github.com/jrr/webjob-project-examples)

## <a name="implementing-timers-on-azure-with-f"></a>F #을 사용 하 여 Azure에서 타이머 구현 #

타이머는 일정, 한 번 또는 되풀이에 따라 호출 함수를 트리거합니다.

타이머는 [F#의 Azure Function 및 타이머 트리거](/azure/azure-functions/functions-bindings-timer)를 통해 Azure에서 F#으로 구현하고 호스트할 수 있습니다.

## <a name="deploying-and-managing-azure-resources-with-f-scripts"></a>F# 스크립트를 통해 Azure 리소스 배포 및 관리 #

Azure VM은 Microsoft.Azure.Management 패키지 및 API를 사용하여 프로그래밍 방식으로 배포하고 관리할 수 있습니다. 예를 들어 [.NET용 관리 라이브러리 시작](https://msdn.microsoft.com/library/dn722415.aspx) 및 [Azure Resource Manager 사용](/azure/azure-resource-manager/resource-manager-deployment-model)을 참조하세요.

마찬가지로, 동일한 구성 요소를 사용하여 F# 스크립트에서 다른 Azure 리소스를 배포하고 관리할 수 있습니다. 예를 들어 저장소 계정을 만들고, Azure Cloud Services 배포, Azure Cosmos DB 인스턴스를 만들 하 수 F # 스크립트에서 Azure Notifcation Hubs를 프로그래밍 방식으로 관리 합니다.

F# 스크립트를 사용하여 리소스를 배포하고 관리하는 작업은 일반적으로 필요하지 않습니다. 예를 들어 Azure 리소스는 JSON 템플릿 설명에서 직접 배포할 수도 있습니다(매개 변수화할 수 있음). [Azure 퀵 스타트 템플릿](https://azure.microsoft.com/resources/templates/)과 같은 예제를 비롯하여 [Azure Resource Manager 템플릿](/azure/azure-resource-manager/resource-manager-template-best-practices)을 참조하세요.

## <a name="other-resources"></a>기타 리소스

* [모든 Azure 서비스에 대한 전체 설명서](/azure/)
