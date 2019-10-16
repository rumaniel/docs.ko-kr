---
title: 서버를 사용 하지 않는 디자인 예제-서버 리스 앱
description: 서버를 사용 하지 않는 아키텍처에서 지 원하는 다양 한 시나리오를 일정 예약 및 이벤트 기반 처리에서 파일 트리거 및 스트림 프로세스로 이해 합니다.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 096dce6ef23bde5ef9c6ca65769f4dcc7e08a904
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577196"
---
# <a name="serverless-design-examples"></a>서버리스 디자인 예제

서버 리스에 대해 존재 하는 다양 한 디자인 패턴이 있습니다. 이 섹션에서는 서버 리스를 사용 하는 몇 가지 일반적인 시나리오를 캡처합니다. 모든 예제가 공통적으로 포함 하는 것은 이벤트 트리거와 비즈니스 논리의 기본적인 조합입니다.

## <a name="scheduling"></a>일정 예약

작업 예약은 일반적인 기능입니다. 다음 다이어그램에서는 적절 한 무결성 검사가 없는 레거시 데이터베이스를 보여 줍니다. 데이터베이스는 주기적으로 삭제 되어야 합니다. 서버를 사용 하지 않는 함수는 잘못 된 데이터를 찾아서 정리 합니다. 트리거는 일정에 따라 코드를 실행 하는 타이머입니다.

![서버 리스 일정](./media/serverless-scheduling.png)

## <a name="command-and-query-responsibility-segregation-cqrs"></a>명령과 쿼리의 역할 분리 (CQRS)

CQRS (명령과 쿼리의 역할 분리)는 데이터를 읽고 쿼리 하는 다른 인터페이스와 데이터를 수정 하는 작업을 제공 하는 패턴입니다. 몇 가지 일반적인 문제를 해결 합니다. 기존의 CRUD (읽기 업데이트 삭제) 기반 시스템에서 동일한 데이터 저장소에 대 한 읽기와 쓰기의 양이 많은 경우 충돌이 발생할 수 있습니다. 잠금이 자주 발생 하 고 읽기 속도가 크게 느려질 수 있습니다. 데이터는 여러 도메인 개체의 복합으로 표시 되 고 읽기 작업은 여러 엔터티의 데이터를 결합 해야 하는 경우가 많습니다.

CQRS를 사용 하 여 읽기는 사용 되는 방식으로 데이터를 모델링 하는 특수 한 "평면화 된" 엔터티를 포함할 수 있습니다. 읽기는 저장 된 방식과 다르게 처리 됩니다. 예를 들어, 데이터베이스에서 하위 주소 레코드가 있는 헤더 레코드로 연락처를 저장할 수 있지만 읽기는 헤더와 주소 속성이 모두 포함 된 엔터티를 포함할 수 있습니다. 읽기 모델을 만드는 방법에는 여러 가지가 있습니다. 뷰에서 구체화할 수 있습니다. 업데이트 작업은 격리 된 이벤트로 캡슐화 될 수 있으며, 그 후에는 두 가지 모델에 대 한 업데이트를 트리거합니다. 읽기 및 쓰기에 대 한 별도의 모델이 있습니다.

![CQRS 예제](./media/cqrs-example.png)

서버를 사용 하지 않는 경우 분리 된 끝점을 제공 하 여 CQRS 패턴을 수용할 수 있습니다. 서버를 사용 하지 않는 함수 하나는 쿼리 또는 읽기를 허용 하 고 다른 서버 리스 함수 또는 함수 집합은 업데이트 작업을 처리 합니다. 서버를 사용 하지 않는 함수는 읽기 모델을 최신 상태로 유지 하 고 데이터베이스의 [변경 피드에](https://docs.microsoft.com/azure/cosmos-db/change-feed)의해 트리거될 수 있습니다. 프런트 엔드 개발은 필요한 끝점에 연결 하기 위해 간소화 되었습니다. 백 엔드에서 이벤트 처리를 처리 합니다. 또한이 모델은 여러 팀이 서로 다른 작업을 수행할 수 있기 때문에 규모가 많은 프로젝트에 대해 잘 확장 됩니다.

## <a name="event-based-processing"></a>이벤트 기반 처리

메시지 기반 시스템에서 이벤트는 처리 될 큐 또는 게시자/구독자 항목으로 수집 되는 경우가 많습니다. 이러한 이벤트는 서버를 사용 하지 않는 함수를 트리거하여 비즈니스 논리를 실행할 수 있습니다. 이벤트 기반 처리의 예로는 이벤트 원본 시스템이 있습니다. 작업을 완료로 표시 하기 위해 "이벤트"가 발생 합니다. 이벤트에 의해 트리거되는 서버를 사용 하지 않는 함수는 적절 한 데이터베이스 문서를 업데이트 합니다. 서버를 사용 하지 않는 두 번째 함수는 이벤트를 사용 하 여 시스템에 대 한 읽기 모델을 업데이트할 수 있습니다. [Azure Event Grid](https://docs.microsoft.com/azure/event-grid/overview) 함수를 구독자로 통합 하는 방법을 제공 합니다.

> 이벤트는 정보 메시지입니다. 자세한 내용은 [이벤트 소싱 패턴](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)을 참조 하세요.

## <a name="file-triggers-and-transformations"></a>파일 트리거 및 변환

ETL (추출, 변환 및 로드)은 일반적인 비즈니스 기능입니다. 서버를 사용 하지 않는 것은 코드를 파이프라인의 일부로 트리거할 수 있으므로 ETL을 위한 훌륭한 솔루션입니다. 개별 코드 구성 요소는 다양 한 측면을 처리할 수 있습니다. 서버를 사용 하지 않는 함수는 파일을 다운로드 하 고, 다른 함수는 변환을 적용 하 고, 다른 하나는 데이터를 로드 합니다. 코드를 독립적으로 테스트 및 배포 하 여 필요한 경우 더 쉽게 유지 관리 하 고 확장할 수 있습니다.

![서버 리스 파일 트리거 및 변환](./media/serverless-file-triggers.png)

다이어그램에서 "쿨 저장소"는 [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics)에서 구문 분석 되는 데이터를 제공 합니다. 데이터 스트림에서 발생 하는 모든 문제는 변칙 문제를 해결 하기 위해 Azure 함수를 트리거합니다.

## <a name="asynchronous-background-processing-and-messaging"></a>비동기 백그라운드 처리 및 메시징

비동기 메시징 및 백그라운드 처리를 사용 하면 응용 프로그램에서 대기 하지 않고도 프로세스를 시작할 수 있습니다. 비동기 처리의 예로는 OCR 앱이 있습니다. 이미지가 전송 되 고 처리를 위해 큐에 대기 됩니다. 이미지를 검색 하 여 텍스트를 추출 하는 데 시간이 걸릴 수 있으며, 작업이 완료 되 면 알림이 전송 됩니다. 서버를 사용 하지 않는 경우이 시나리오에서 호출과 결과를 모두 처리할 수 있습니다.

## <a name="web-apps-and-apis"></a>웹 앱 및 Api

서버를 사용 하지 않는 인기 있는 시나리오는 N 계층 응용 프로그램입니다. 가장 일반적인 시나리오는 UI 계층이 웹 앱입니다. SPA (단일 페이지 응용 프로그램)의 인기는 최근 surged. SPA 앱은 단일 페이지를 렌더링 한 다음 API 호출을 사용 하 고 반환 된 데이터를 사용 하 여 전체 페이지를 다시 로드 하지 않고 새 UI를 동적으로 렌더링 합니다. 클라이언트 쪽 렌더링은 최종 사용자에 게 훨씬 더 빠르고 응답성 높은 응용 프로그램을 제공 합니다.

HTTP 호출로 트리거된 서버 리스 끝점은 API 요청을 처리 하는 데 사용할 수 있습니다. 예를 들어 ad 서비스 회사는 사용자 프로필 정보를 사용 하 여 서버 리스 함수를 호출 하 여 사용자 지정 광고를 요청할 수 있습니다. 서버를 사용 하지 않는 함수는 사용자 지정 광고를 반환 하 고 웹 페이지에서 렌더링 합니다.

![서버 리스 웹 API](./media/serverless-web-api.png)

## <a name="data-pipeline"></a>데이터 파이프라인

서버를 사용 하지 않는 함수를 사용 하 여 데이터 파이프라인을 쉽게 만들 수 있습니다. 이 예에서 파일은 CSV 파일의 데이터를 테이블의 데이터 행으로 변환 하는 함수를 트리거합니다. 구성 된 테이블을 사용 하면 Power BI 대시보드가 최종 사용자에 게 분석을 제공할 수 있습니다.

![서버를 사용 하지 않는 데이터 파이프라인](./media/serverless-data-pipeline.png)

## <a name="stream-processing"></a>스트림 처리

장치 및 센서는 실시간으로 처리 해야 하는 데이터 스트림을 생성 하는 경우가 많습니다. [Event Hubs](https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs) 및 [IoT Hub](https://docs.microsoft.com/azure/iot-hub) 에서 [Service Bus](https://docs.microsoft.com/azure/service-bus)으로 메시지와 스트림을 캡처할 수 있는 여러 기술이 있습니다. 전송 여부와 관계 없이 서버를 사용 하지 않는 데이터 및 데이터 스트림을 처리 하는 데 적합 한 메커니즘입니다. 서버 리스 서버는 대량의 데이터 수요를 충족 하기 위해 신속 하 게 확장할 수 있습니다. 서버를 사용 하지 않는 코드는 데이터를 구문 분석 하 고 작업 및 분석을 위해 구조화 된 형식으로 출력 하는 비즈니스 논리를 적용할 수 있습니다.

![서버를 사용 하지 않는 스트림 처리](./media/serverless-stream-processing.png)

## <a name="api-gateway"></a>API 게이트웨이

API 게이트웨이는 클라이언트에 대 한 단일 진입점을 제공 하 고 요청을 백 엔드 서비스로 지능적으로 라우팅합니다. 많은 서비스 집합을 관리 하는 데 유용 합니다. 또한 클라이언트를 서로 다른 환경에 쉽게 연결 하 여 버전 관리를 처리 하 고 개발을 간소화할 수 있습니다. 서버를 사용 하지 않는 경우 API 게이트웨이를 통해 단일 프런트 엔드를 제공 하는 동시에 개별 마이크로 서비스의 백 엔드 크기 조정을 처리할 수 있습니다.

![서버를 사용 하지 않는 API 게이트웨이](./media/serverless-api-gateway.png)

## <a name="recommended-resources"></a>권장 리소스

* [Azure Event Grid](https://docs.microsoft.com/azure/event-grid/overview)
* [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub)
* [분산 데이터 관리의 문제 및 솔루션](../microservices/architect-microservice-container-applications/distributed-data-management.md)
* [마이크로 서비스 디자인: 마이크로 서비스 경계 식별](https://docs.microsoft.com/azure/architecture/microservices/microservice-boundaries)
* [Event Hubs](https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs)
* [이벤트 소싱 패턴](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)
* [회로 차단기 패턴 구현](../microservices/implement-resilient-applications/implement-circuit-breaker-pattern.md)
* [IoT Hub](https://docs.microsoft.com/azure/iot-hub)
* [Service Bus](https://docs.microsoft.com/azure/service-bus)
* [Azure Cosmos DB에서 변경 피드 지원 사용](https://docs.microsoft.com/azure/cosmos-db/change-feed)

>[!div class="step-by-step"]
>[이전](serverless-architecture-considerations.md)
>[다음](azure-serverless-platform.md)
