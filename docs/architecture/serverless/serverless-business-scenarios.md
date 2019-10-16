---
title: 서버를 사용 하지 않는 앱에 대 한 샘플 비즈니스 시나리오 및 사용 사례
description: 이미지 처리에서 모바일 백 엔드 및 ETL 파이프라인에 이르는 샘플에 액세스 하 여 실습 방식으로 서버 리스를 알아보세요.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 7024a33f8a7fccd6afa51c126454afedd87cceee
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834291"
---
# <a name="serverless-business-scenarios-and-use-cases"></a>서버리스 비즈니스 시나리오 및 사용 사례

서버를 사용 하지 않는 응용 프로그램에는 다양 한 사용 사례 및 시나리오가 있습니다. 이 장에서는 다양 한 시나리오를 보여 주는 샘플이 포함 되어 있습니다. 시나리오에는 관련 설명서 및 공용 소스 코드 리포지토리에 대 한 링크가 포함 되어 있습니다. 이 챕터의 샘플을 사용 하면 서버 리스 솔루션을 직접 빌드하고 구현할 수 있습니다.

## <a name="analyze-and-archive-images"></a>이미지 분석 및 보관

이 샘플에서는 서버 리스 이벤트 (Event Grid), 워크플로 (논리 앱) 및 코드 (Azure Functions)를 보여 줍니다. 또한 다른 리소스와 통합 하는 방법을 보여 줍니다 .이 경우에는 이미지 분석에 Cognitive Services 합니다.

콘솔 응용 프로그램을 사용 하면 웹의 URL에 대 한 링크를 전달할 수 있습니다. 앱은 URL을 event grid 메시지로 게시 합니다. 동시에 서버 리스 함수 앱과 논리 앱은 메시지를 구독 합니다. 서버를 사용 하지 않는 함수 앱은 blob 저장소에 이미지를 직렬화 합니다. 또한 Azure Table Storage에 정보를 저장 합니다. 메타 데이터에는 원래 이미지 URL과 blob 이미지 이름이 저장 됩니다. 논리 앱은 Custom Vision API와 상호 작용 하 여 이미지를 분석 하 고 컴퓨터 생성 캡션을 만듭니다. 캡션은 메타 데이터 테이블에 저장 됩니다.

![이미지 아키텍처 분석 및 보관](./media/image-processing-example.png)

별도의 SPA (단일 페이지 응용 프로그램)는 서버를 사용 하지 않는 함수를 호출 하 여 이미지 및 메타 데이터 목록을 가져옵니다. 각 이미지에 대해 보관 파일에서 이미지 데이터를 배달 하는 또 다른 함수를 호출 합니다. 최종 결과는 자동 캡션이 있는 갤러리입니다.

![자동화 된 이미지 갤러리](./media/automated-image-gallery.png)

논리 앱을 빌드하는 전체 리포지토리와 지침은 여기에서 사용할 수 있습니다. [Event grid 붙이기](https://github.com/JeremyLikness/Event-Grid-Glue).

## <a name="cross-platform-mobile-client-using-xamarinforms-and-functions"></a>Xamarin.ios 및 함수를 사용 하는 플랫폼 간 모바일 클라이언트

Azure 웹 포털 또는 Visual Studio에서 간단한 서버를 사용 하지 않는 Azure 함수를 구현 하는 방법을 참조 하세요. Android, iOS 및 Windows에서 실행 되는 Xamarin 양식이 있는 클라이언트를 빌드합니다. 그런 다음 응용 프로그램은 서버와 모바일 클라이언트 사이에서 서버를 사용 하지 않는 백 엔드를 사용 하는 통신 매체로 JavaScript Object Notation (JSON)를 사용 하도록 구체화 됩니다.

자세한 내용은 [Xamarin Forms 클라이언트를 사용 하 여 간단한 Azure 함수 구현](https://azure.microsoft.com/resources/samples/functions-xamarin-getting-started/)을 참조 하세요.

## <a name="generate-a-photo-mosaic-with-serverless-image-recognition"></a>서버 리스 이미지 인식을 사용 하 여 사진 모자이크 생성

이 샘플에서는 Azure Functions 및 Microsoft Cognitive Services Custom Vision Service를 사용 하 여 입력 이미지에서 사진 모자이크를 생성 합니다. 모델은 이미지를 인식 하도록 학습 됩니다. 이미지를 업로드 하면 이미지를 인식 하 고 Bing으로 검색 합니다. 원본 이미지는 검색 결과를 사용 하 여 재작성 됩니다.

![올랜도 눈 사진 및 모자이크](./media/orlando-eye-both.png)

예를 들어 올랜도 눈동자와 같은 올랜도 랜드마크를 사용 하 여 모델을 학습 시킬 수 있습니다. Custom Vision는 올랜도 눈동자 이미지를 인식 하 고 함수는 "올랜도 눈동자"에 대해 Bing 이미지 검색 결과로 구성 된 사진 모자이크를 만듭니다.

자세한 내용은 [Azure Functions photo 모자이크 생성기](https://azure.microsoft.com/resources/samples/functions-dotnet-photo-mosaic/)를 참조 하세요.

## <a name="migrate-an-existing-application-to-the-cloud"></a>기존 응용 프로그램을 클라우드로 마이그레이션

이전 단원에서 설명한 대로 온-프레미스 응용 프로그램을 호스트 하는 N 계층 아키텍처를 도입 하는 것이 일반적입니다. 가상 컴퓨터를 사용 하 여 리소스를 "있는 그대로" 마이그레이션하는 것은 클라우드로 가장 위험한 경로 이지만 많은 회사에서 응용 프로그램을 리팩터링할 수 있는 기회를 사용 하도록 선택 합니다. 다행히 리팩터링은 "모두" 또는 아무 작업도 수행할 필요가 없습니다. 실제로 앱을 마이그레이션한 다음 구성 요소를 클라우드 네이티브 대응으로 증분 수 있습니다.

응용 프로그램은 Azure Functions의 프록시 기능을 사용 하 여 레거시 온-프레미스 코드에서 서버를 사용 하지 않는 끝점으로 끝점을 리팩터링할 수 있습니다.

![마이그레이션 아키텍처](./media/migration-architecture.png)

프록시는 서버를 사용 하지 않는 함수로 이동할 때 개별 요청을 다시 라우팅하도록 업데이트 되는 단일 API 끝점을 제공 합니다.

전체 마이그레이션 과정을 안내 하는 비디오를 볼 수 있습니다. [서버를 사용 하지 않는 Azure 함수를 리프트 앤 시프트](https://channel9.msdn.com/Events/Connect/2017/E102)합니다. 샘플 코드에 액세스 합니다. 사용자 [고유의 앱을 가져옵니다](https://github.com/JeremyLikness/bring-own-app-connect-17).

## <a name="parse-a-csv-file-and-insert-into-a-database"></a>CSV 파일의 구문을 분석 하 고 데이터베이스에 삽입

ETL (추출, 변환 및 로드)은 서로 다른 시스템을 통합 하는 일반적인 비즈니스 기능입니다. 일반적인 방법으로는 전용 FTP 서버를 설정한 후 파일을 구문 분석 하 고 비즈니스를 위해 변환 하는 예약 된 작업을 배포 하는 경우가 많습니다. 서버를 사용 하지 않는 아키텍처는 파일이 업로드 될 때 트리거를 실행할 수 있기 때문에 작업을 더 쉽게 수행할 수 있습니다. Azure Functions는 특정 문제에 초점을 맞춘 작은 코드 조각의 이상적인 컴퍼지션을 통해 ETL과 같은 작업을 있는지 합니다.

![Csv 구문 분석 프로세스를 보여 주는 스크린샷](./media/serverless-business-scenarios/csv-parse-database-import.png)

원본 코드 및 실습 랩의 경우 [CSV 가져오기 랩](https://github.com/JeremyLikness/azure-fn-file-process-hol)을 참조 하세요.

## <a name="shorten-links-and-track-metrics"></a>링크를 줄이고 메트릭 추적

링크 단축 도구는 원래 짧은 twitter 게시물에서 140 문자 제한을 수용할 수 있도록 Url을 인코딩하는 데 도움이 되었습니다. 분석에 대 한 클릭을 추적 하는 데 가장 일반적으로 사용 되는 여러 가지 용도로 사용 됩니다. 링크 단축 시나리오는 링크 및 보고서 메트릭을 관리 하는 완전히 서버를 사용 하지 않는 응용 프로그램입니다.

Azure Functions는 긴 URL을 붙여 넣고 짧은 Url을 생성할 수 있도록 하는 SPA (단일 페이지 응용 프로그램)를 제공 하는 데 사용 됩니다. Url에는 캠페인 (토픽) 및 미디어 (링크를 게시 하는 소셜 네트워크)와 같은 항목을 추적 하도록 태그가 지정 되어 있습니다. 짧은 코드는 Azure Table Storage에 키로 저장 되 고 long URL은 값으로 저장 됩니다. Short 링크를 클릭 하면 다른 함수는 긴 URL을 조회 하 고, 리디렉션을 전송 하 고, 이벤트에 대 한 정보를 큐에 넣습니다. 다른 Azure 함수는 큐를 처리 하 고 Azure Cosmos DB에 정보를 저장 합니다.

![단축 아키텍처 링크](./media/link-shortener-architecture.png)

그런 다음 Power BI 대시보드를 만들어 수집 된 데이터에 대 한 정보를 수집할 수 있습니다. 백 엔드에서 Application Insights는 중요 한 메트릭을 제공 합니다. 원격 분석에는 평균 사용자가 리디렉션하는 데 소요 되는 시간과 Azure Table Storage에 액세스 하는 데 걸리는 시간이 포함 됩니다.

![Power BI 예제](./media/power-bi-example.png)

지침이 있는 전체 링크 단축 리포지토리는 여기에서 사용할 수 있습니다. [서버 리스 URL 단축](https://github.com/jeremylikness/serverless-url-shortener). 다음에서 간소화 된 버전을 읽을 수 있습니다. [몇 분 내에 서버 리스 .net 앱에 대 한 Azure Storage](https://devblogs.microsoft.com/aspnet/azure-storage-for-serverless-net-apps-in-minutes/)입니다.

## <a name="verify-device-connectivity-using-a-ping"></a>Ping을 사용 하 여 장치 연결 확인

이 샘플은 Azure IoT Hub 및 Azure 함수로 구성 됩니다. IoT Hub의 새 메시지는 Azure Function을 트리거합니다. 서버를 사용 하지 않는 코드는 동일한 메시지 콘텐츠를 전송 된 장치로 다시 보냅니다. 프로젝트에는 솔루션에 필요한 모든 코드 및 배포 구성이 있습니다.

자세한 내용은 [ping Azure IoT Hub](https://azure.microsoft.com/resources/samples/iot-hub-node-ping/)를 참조 하세요.

## <a name="recommended-resources"></a>권장 리소스

* [Azure Functions photo 모자이크 생성기](https://azure.microsoft.com/resources/samples/functions-dotnet-photo-mosaic/)
* [Azure IoT Hub ping](https://azure.microsoft.com/resources/samples/iot-hub-node-ping/)
* [몇 분 내에 서버 리스 .NET 앱에 대 한 Azure Storage](https://devblogs.microsoft.com/aspnet/azure-storage-for-serverless-net-apps-in-minutes/)
* [사용자 고유의 앱 가져오기](https://github.com/JeremyLikness/bring-own-app-connect-17)
* [CSV 가져오기 랩](https://github.com/JeremyLikness/azure-fn-file-process-hol)
* [Event grid 붙이기](https://github.com/JeremyLikness/Event-Grid-Glue)
* [Xamarin Forms 클라이언트를 사용 하 여 간단한 Azure 함수 구현](https://azure.microsoft.com/resources/samples/functions-xamarin-getting-started/)
* [서버를 사용 하지 않는 Azure 함수로 리프트 앤 시프트](https://channel9.msdn.com/Events/Connect/2017/E102)
* [서버 리스 URL 단축](https://github.com/jeremylikness/serverless-url-shortener)

>[!div class="step-by-step"]
>[이전](orchestration-patterns.md)
>[다음](serverless-conclusion.md)
