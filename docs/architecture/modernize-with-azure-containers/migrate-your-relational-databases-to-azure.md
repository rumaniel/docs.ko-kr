---
title: 관계형 데이터베이스를 azure로 마이그레이션
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 관계형 데이터베이스를 azure로 마이그레이션
ms.date: 04/28/2018
ms.openlocfilehash: b2153e65a12706b97fae11c5f23846c83bcd6642
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70374105"
---
# <a name="migrate-your-relational-databases-to-azure"></a>관계형 데이터베이스를 azure로 마이그레이션

목표: Azure에서는 가장 포괄적인 데이터베이스 마이그레이션을 제공합니다.

Azure에서 IaaS VM(순수한 리프트 앤 시프트)에 직접 데이터베이스 서버를 마이그레이션하거나, 추가적인 이득을 얻기 위해 Azure SQL Database로 마이그레이션할 수 있습니다. Azure SQL Database에서는 관리되는 인스턴스와 서비스 형태의 전체 데이터베이스(DBaaS) 옵션을 제공합니다. 그림 3-1에서는 Azure에서 사용할 수 있는 다양한 관계형 데이터베이스 마이그레이션 경로를 보여 줍니다.

![Azure의 데이터베이스 마이그레이션 경로](./media/image3-1.png)

**그림 3-1.** Azure의 데이터베이스 마이그레이션 경로

## <a name="when-to-migrate-to-azure-sql-database-managed-instance"></a>Azure SQL Database Managed Instance로 마이그레이션해야 하는 경우

대부분의 경우 Azure로 데이터를 마이그레이션할 때 Azure SQL Database Managed Instance는 생각할 수 있는 가장 좋은 선택입니다. SQL Server 데이터베이스를 마이그레이션할 때 응용 프로그램을 다시 작성하거나 데이터 또는 데이터에 액세스하는 코드를 거의 변경하지 않아도 된다는 것을 100% 보장해야 하는 경우 Azure SQL Database의 Managed Instance 기능을 선택하십시오.

Azure SQL Database Managed Instance는 표준 Azure SQL 데이터베이스(단일 데이터베이스 모델)에서 제공되는 기능을 넘어선 격리 요구 사항이나 SQL Server 인스턴스 수준의 기능에 대한 추가적인 요구 사항이 있는 경우 최상의 옵션입니다. 마지막은 PaaS 중심의 선택이지만 기존 SQL 서버와 동일한 기능을 제공하지는 않습니다. 마이그레이션은 마찰을 일으킬 수 있습니다.

예를 들어 인스턴스 수준의 SQL Server 기능에 많은 투자를 한 조직은 SQL Managed Instance로 마이그레이션할 때 이점을 얻을 수 있습니다. 인스턴스 수준 SQL Server 기능의 예로는 SQL 공용 언어 런타임(CLR) 통합과 SQL Server 에이전트, 크로스 데이터베이스 쿼리가 있습니다. 이러한 기능에 대한 지원은 표준 Azure SQL 데이터베이스(단일 데이터베이스 모델)에서 사용할 수 없습니다.

규제가 엄격한 산업에서 운영되고 보안 목적으로 격리를 유지해야하는 조직은 SQL Managed Instance 모델을 선택하면 도움이 될 수 있습니다.

Azure SQL Database에서 관리되는 인스턴스는 다음과 같은 특징이 있습니다.

- Azure Virtual Network를 통한 보안 격리

- 다음 기능을 사용한 응용 프로그램 노출 호환성

  - SQL Server 에이전트 및 SQL Server Profiler

  - 크로스 데이터베이스 참조와 쿼리, SQL CLR, 복제, 변경 데이터 캡처(CDC) 및 Service Broker

- 최대 35TB 데이터베이스 크기

- 다음 기능을 사용한 최소 가동 중지 시간 마이그레이션

  - Azure Database Migration Service

  - 네이티브 백업 및 복원 및 로그 전달

이러한 기능을 사용하여, Azure SQL Database에 기존 응용 프로그램 데이터베이스를 마이그레이션하는 경우 Managed Instance 모델은 SQL Server에 대한 PaaS의 이점의 거의 100%를 제공합니다. Managed Instance는 응용 프로그램 디자인을 변경하지 않고 인스턴스 수준의 기능을 계속해서 사용할 수 있는 SQL Server 환경입니다.

Managed Instance는 현재 SQL Server를 사용 중이고 클라우드에서 네트워크 보안에 유연성이 필요한 기업에 가장 적합합니다. 이는 SQL database용 전용 가상 네트워크와 같습니다.

## <a name="when-to-migrate-to-azure-sql-database"></a>Azure SQL Database로 마이그레이션해야 하는 경우

앞서 언급했듯이 표준 Azure SQL Database는 완전히 관리되는 관계형 DBaaS입니다. SQL Database는 현재 전세계 38개의 데이터 센터에서 수백만 개의 상용 데이터베이스를 관리합니다. 간단한 트랜잭션 데이터 관리에서부터 글로벌 규모의 고급 데이터 처리를 필요로 하며 데이터를 가장 많이 사용하고 중요한 업무용 응용 프로그램에 이르기까지 광범위한 응용 프로그램과 워크로드를 지원합니다.

PaaS의 완벽한 기능, 더 나은 가격 책정(궁극적으로 저렴한 비용)으로 인해, 기본 표준 SQL 데이터베이스를 사용하는 응용 프로그램이 있고 추가 인스턴스 기능이 없는 경우 "기본적인 선택"으로 표준 Azure SQL 데이터베이스로 이동해야 합니다. 표준 Azure SQL Database에서는 SQL CLR 통합과 SQL Server 에이전트, 크로스 데이터베이스 쿼리와 같은 SQL Server 기능은 사용할 수 없습니다. 이러한 기능은 Azure SQL Database Managed Instance 모델에서만 사용할 수 있습니다.

Azure SQL Database는 앱 개발자를 위해 구축된 지능형 클라우드 데이터베이스 서비스입니다. 멀티 테넌트 앱을 효율적으로 제공하기 위해 가동 중단 시간 없이 즉석에서 크기를 조정할 수 있는 유일한 클라우드 데이터베이스 서비스입니다. 궁극적으로 Azure SQL Database를 사용하면 혁신에 더 많은 시간을 사용할 수 있고 출시를 앞당겨 줍니다. 원하는 플랫폼과 언어를 사용하여 보안 앱을 만들고 SQL database에 연결할 수 있습니다.

Azure SQL Database에서는 다음과 같은 이점을 제공합니다.

- 앱을 학습하고 적응하는 지능 내장(기계 학습)

- 온 디멘드 데이터베이스 프로비저닝

- 모든 워크로드에 대한 다양한 제품

- 가용성 99.99% SLA, 유지관리 없음

- 데이터 보호를 위한 지리적 복제 및 복원 서비스

- Azure SQL Database 시점 복원 기능

- 하이브리드 및 마이그레이션을 포함한 SQL Server 2016과의 호환성

표준 Azure SQL 데이터베이스는 Azure SQL Database Managed Instance보다 PaaS에 더 가깝습니다. 표준 Azure SQL 데이터베이스를 선호하는 이유는 관리되는 클라우드에서 더 많은 이점을 얻을 수 있기 때문입니다. 그러나 Azure SQL 데이터베이스는 일반적인 온-프레미스 SQL Server 인스턴스와 구별되는 몇 가지 주요 차이점이 존재합니다. Azure SQL 데이터베이스는 기존 애플리케이션의 데이터베이스 요구사항과 엔터프라이즈 요구사항 및 정책에 따라 클라우드로의 마이그레이션을 계획할 때 최선의 선택이 아닐 수도 있습니다.

## <a name="when-to-move-your-original-rdbms-to-a-vm-iaas"></a>원래 RDBMS를 VM(IaaS)으로 이동하는 시점

마이그레이션 옵션 중 하나는 Oracle, IBM DB2, MySQL, PostgreSQL 또는 SQL Server를 포함한 원래의 관계형 데이터베이스 관리 시스템(RDBMS)을 Azure VM에서 실행 중인 서버와 유사한 서버로 이동하는 것입니다. 전혀 변경하지 않거나 최소한의 변경만으로 가장 빠르게 클라우드로 마이그레이션을 수행해야 하는 기존 애플리케이션이 있으면 클라우드의 IaaS로 직접 마이그레이션하는 것이 적절한 옵션일 수 있습니다. 이 방법이 클라우드의 모든 이점을 활용하는 최선의 방법은 아니지만 아마도 가장 빠르게 시작하는 방법일 것입니다.

현재 Microsoft Azure에서는 IaaS Vm으로 배포되는 최대 [331개의 다양한 데이터베이스 서버](https://azuremarketplace.microsoft.com/marketplace/apps/category/databases?page=1&subcategories=databases-all)를 지원합니다. 여기에는 SQL Server와 Oracle, MySQL, PostgreSQL, IBM DB2와 같은 인기있는 RDBMS와 MongoDB, Cassandra, DataStax, MariaDB, 및 Cloudera와 같은 다양한 NoSQL 데이터베이스가 포함됩니다.

> [!NOTE]
> Azure VM으로 사용자 RDBMS 데이터를 이전하는 것이 IaaS인 클라우드로 마이그레이션하는 가장 빠른 방법일 수 있지만, 이 방법을 사용하려면 IT 팀(데이터베이스 관리자와 IT 전문가)에 많은 투자를 해야 합니다. 엔터프라이즈 팀은 SQL Server의 고가용성과 재해 복구, 패치를 설정하고 관리할 수 있어야 합니다. 또한 이 컨텍스트에는 전체 관리 권한이 있는 사용자 지정된 환경이 필요합니다.

## <a name="when-to-migrate-to-sql-server-as-a-vm-iaas"></a>VM (IaaS)으로 SQL Server로 마이그레이션해야 하는 경우

일반 VM의 SQL Server로 마이그레이션해야 하는 경우가 있습니다. 예를 들면 SQL Server Reporting Services를 사용해야하는 경우입니다. 하지만 대부분의 경우 Azure SQL Database Managed Instance는 온-프레미스 SQL 서버에서 마이그레이션하는 데 필요한 모든 것을 제공할 수 있으므로 SQL Server VM으로의 마이그레이션은 마지막 수단으로 사용해야 합니다.

## <a name="use-azure-database-migration-service-to-migrate-your-relational-databases-to-azure"></a>Azure Database Migration Service를 사용하여 Azure에 관계형 데이터베이스 마이그레이션 

대상 데이터베이스가 Azure SQL Database나 Azure SQL Database Managed Instance, Azure VM의 SQL Server 중 어느 것이든, Azure Database Migration Service를 사용하여 SQL Server와 Oracle, MySQL과 같은 관계형 데이터베이스를 Azure로 마이그레이션할 수 있습니다.

평가 보고 기능이 있는 자동화된 워크플로는 데이터베이스를 마이그레이션하기 전에 변경해야 할 사항을 안내합니다. 준비가 되면 서비스는 원본 데이터베이스를 Azure로 마이그레이션합니다.

원래의 RDBMS를 변경할 때마다 다시 테스트해야 할 수 있습니다. 테스트 결과에 따라 응용 프로그램에서 SQL 문장이나 ORM(Object-Relational Mapping) 코드를 변경해야 할 수도 있습니다.

다른 데이터베이스(예: IBM DB2)가 있고 리프트 앤 시프트 방식을 선택하는 경우, 보다 복잡한 데이터 마이그레이션을 수행하려는 경우가 아니면 Azure에서 이러한 데이터베이스를 IaaS VM으로 계속 사용할 수 있습니다. 더 복잡한 데이터 마이그레이션은 새로운 스키마와 다양한 프로그래밍 라이브러리를 사용하여 다양한 데이터베이스 유형으로 마이그레이션하기 때문에 추가적인 노력이 필요합니다.

Azure Database Migration Service를 사용하여 데이터베이스를 마이그레이션하는 방법에 알아보려면 [Azure SQL Database Managed Instance와 Azure Database Migration Service를 사용하여 클라우드로 신속하게 이동하기](https://channel9.msdn.com/Events/Build/2017/P4008)를 참조합니다.

## <a name="additional-resources"></a>추가 자료

- **클라우드 SQL Server 옵션 선택: Azure SQL Database (PaaS) 또는 Azure VM (IaaS)의 SQL Server**

    <https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas>

- **Azure SQL Database Managed Instance와 Database Migration Service를 사용하여 신속하게 클라우드 이동하기**

    <https://channel9.msdn.com/Events/Build/2017/P4008>

- **클라우드 SQL Database로 SQL Server 데이터베이스 마이그레이션**

    <https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate>

- **Azure SQL Database**

    <https://azure.microsoft.com/services/sql-database/?v=16.50>

- **가상 컴퓨터의 SQL Server**

    <https://azure.microsoft.com/services/virtual-machines/sql-server/>

> [!div class="step-by-step"]
> [이전](lift-and-shift-existing-apps-azure-iaas.md)
> [다음](modernize-existing-apps-to-cloud-optimized/index.md) <!-- Next Chapter -->
