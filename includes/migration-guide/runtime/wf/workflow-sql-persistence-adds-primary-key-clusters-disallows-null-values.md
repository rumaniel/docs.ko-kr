---
ms.openlocfilehash: 9e98d3bca645cf82bf4fe99160dd096b0e274ef7
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802467"
---
### <a name="workflow-sql-persistence-adds-primary-key-clusters-and-disallows-null-values-in-some-columns"></a>워크플로 SQL 지속성은 기본 키 클러스터를 추가하고 일부 열에서 null 값을 허용하지 않습니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7부터 SqlWorkflowInstanceStoreSchema.sql 스크립트로 SQL 워크플로 인스턴스 저장소(SWIS)용으로 만든 테이블은 클러스터된 기본 키를 사용합니다. 이로 인해 ID는 <code>null</code> 값을 지원하지 않습니다. SWIS 작업은 이 변경의 영향을 받지 않습니다. SQL Server 트랜잭션 복제를 지원하도록 업데이트되었습니다.|
|제안|이 변경 내용을 적용하려면 SQL 파일 SqlWorkflowInstanceStoreSchemaUpgrade.sql을 기존 설치에 적용해야 합니다. 새 데이터베이스 설치는 자동으로 변경됩니다.|
|범위|Microsoft Edge|
|버전|4.7|
|Type|런타임|

