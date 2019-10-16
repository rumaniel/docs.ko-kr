---
title: 명령 트리의 모양
ms.date: 03/30/2017
ms.assetid: 2215585e-ca47-45f8-98d4-8cb982f8c1d3
ms.openlocfilehash: 8368354049a77a56a5aa54ab500619576f41b0dc
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854268"
---
# <a name="the-shape-of-the-command-trees"></a>명령 트리의 모양

SQL 생성 모듈은 지정된 입력 쿼리 명령 트리 식을 기반으로 특정 백엔드 SQL 쿼리를 생성하는 작업을 담당합니다. 이 단원에서는 쿼리 명령 트리의 특성, 속성 및 구조에 대해 설명합니다.

## <a name="query-command-trees-overview"></a>쿼리 명령 트리 개요

쿼리 명령 트리는 쿼리의 개체 모델 표현입니다. 쿼리 명령 트리는 다음 두 가지 용도로 사용됩니다.

- Entity Framework에 대해 지정 된 입력 쿼리를 나타내려면입니다.

- 공급자에 제공되고 백엔드에 대한 쿼리를 설명하는 출력 쿼리를 표현하기 위해

쿼리 명령 트리는 SQL:1999 규격 쿼리보다 다양한 의미 체계를 지원합니다. 예를 들어, 엔터티가 특정 형식인지 확인하거나 형식을 기반으로 집합을 필터링하는 등의 형식 작업 및 중첩 컬렉션 작업을 지원합니다.

DBQueryCommandTree.Query 속성은 쿼리 논리를 설명하는 식 트리의 루트입니다. DBQueryCommandTree.Parameters 속성에는 쿼리에서 사용되는 매개 변수의 목록이 포함되어 있습니다. 식 트리는 DbExpression 개체로 구성됩니다.

DbExpression 개체는 특정 계산을 나타냅니다. 상수, 변수, 함수, 생성자 및 표준 관계형 연산자 (예: 필터 및 조인)를 비롯 한 쿼리 식을 작성 하기 위해 Entity Framework에서 제공 하는 여러 종류의 식이 제공 됩니다. 모든 DbExpression 개체에는 해당 식에서 생성 되는 결과의 형식을 나타내는 ResultType 속성이 있습니다. 이 형식은 TypeUsage로 표현됩니다.

## <a name="shapes-of-the-output-query-command-tree"></a>출력 쿼리 명령 트리의 모양

출력 쿼리 명령 트리는 관계형(SQL) 쿼리를 유사하게 나타내며 쿼리 명령 트리에 적용되는 것보다 훨씬 엄격한 규칙을 따릅니다. 일반적으로 출력 쿼리 명령 트리에는 SQL로 쉽게 변환되는 구문이 포함되어 있습니다.

입력 명령 트리는 탐색 속성, 엔터티 간의 연결 및 상속을 지원하는 개념적 모델에 대해 표현됩니다. 출력 명령 트리는 스토리지 모델에 대해 표현됩니다. 입력 명령 트리는 중첩 컬렉션을 프로젝션할 수 있도록 하지만 출력 명령 트리는 그렇지 않습니다.

출력 쿼리 명령 트리는 사용 가능한 DbExpression 개체의 하위 집합을 사용하여 작성되며 해당 하위 집합의 일부 식은 제한적으로 사용됩니다.

지정된 식이 특정 형식인지 확인하거나 형식을 기반으로 집합을 필터링하는 등의 형식 작업은 출력 명령 트리에 없습니다.

출력 명령 트리에서는 부울 값을 반환하는 식만 프로젝션에 사용되며 필터 또는 CASE 문과 같은 조건자가 필요한 식에서 조건자에만 사용됩니다.

출력 쿼리 명령 트리의 루트는 DbProjectExpression 개체입니다.

### <a name="expression-types-not-present-in-output-query-command-trees"></a>출력 쿼리 명령 트리에 없는 식 형식

다음 식 형식은 출력 쿼리 명령 트리에서 유효하지 않으며 공급자가 처리할 필요가 없습니다.

- DbDerefExpression

- DbEntityRefExpression

- DbRefKeyExpression

- DbIsOfExpression

- DbOfTypeExpression

- DbRefExpression

- DbRelationshipNavigationExpression

- DbTreatExpression

### <a name="expression-restrictions-and-notes"></a>식 제한 사항 및 참고 정보

출력 쿼리 명령 트리에서 제한된 방식으로만 사용할 수 있는 식이 많이 있습니다.

#### <a name="dbfunctionexpression"></a>DbFunctionExpression

다음 함수 형식이 전달될 수 있습니다.

- Edm 네임스페이스에서 인식되는 정식 함수

- BuiltInAttribute에서 인식되는 기본 제공(저장소) 함수

- 사용자 정의 함수

정식 함수 (자세한 내용은 [정식 함수](./language-reference/canonical-functions.md) 참조)는 Entity Framework 일부로 지정 되며, 공급자는 해당 사양에 따라 정식 함수에 대 한 구현을 제공 해야 합니다. 저장소 함수는 해당 공급자 매니페스트에 지정된 사항을 기반으로 합니다. 사용자 정의 함수는 SSDL에서 지정된 사항을 기반으로 합니다.

또한 NiladicFunction 특성이 있는 함수에는 인수가 없으며 끝에 괄호 없이 변환되어야 합니다.  즉  *\<* *, \<functionName > ()* 대신 functionName > 합니다.

#### <a name="dbnewinstanceexpression"></a>DbNewInstanceExpression

DbNewInstanceExpression은 다음 두 경우에만 발생할 수 있습니다.

- DbProjectExpression의 Projection 속성으로.  이렇게 사용되는 경우 다음 제한 사항이 적용됩니다.

  - 결과 형식이 행 형식이어야 합니다.

  - 각 인수가 기본 형식을 사용하여 결과를 생성하는 식입니다. 일반적으로 각 인수는 DbVariableReferenceExpression을 통한 PropertyExpression과 같은 스칼라 식, 함수 호출 또는 DbVariableReferenceExpression을 통한 DbPropertyExpression 또는 함수 호출의 산술 계산입니다. 그러나 스칼라 하위 쿼리를 나타내는 식은 DbNewInstanceExpression의 인수 목록에서도 발생할 수 있습니다. 스칼라 하위 쿼리를 나타내는 식은 DbElementExpression 개체 root를 사용 하 여 정확히 한 개의 행과 기본 형식의 열 하나를 반환 하는 하위 쿼리를 나타내는 식 트리입니다.

- 컬렉션 반환 형식과 함께. 이 경우 DbNewInstanceExpression은 인수로 제공된 식의 새 컬렉션을 정의합니다.

#### <a name="dbvariablereferenceexpression"></a>DbVariableReferenceExpression

DbVariableReferenceExpression은 DbPropertyExpression 노드의 자식이어야 합니다.

#### <a name="dbgroupbyexpression"></a>DbGroupByExpression

DbGroupByExpression의 Aggregates 속성에는 DbFunctionAggregate 형식의 요소만 포함될 수 있습니다. 다른 집계 형식은 없습니다.

#### <a name="dblimitexpression"></a>DbLimitExpression

Limit 속성은 DbConstantExpression 또는 DbParameterReferenceExpression일 수만 있습니다. 또한 WithTies 속성은 .NET Framework 버전 3.5부터 항상 false입니다.

#### <a name="dbscanexpression"></a>DbScanExpression

출력 명령 트리에서 사용 되는 경우 DbScanExpression은 EntitySetBase:: Target으로 표시 되는 테이블, 뷰 또는 저장소 쿼리에 대 한 검색을 효과적으로 나타냅니다.

대상의 메타 데이터 속성 "정의 쿼리"가 null이 아닌 경우 쿼리를 나타내고,에 대 한 쿼리 텍스트는 저장소 스키마 정의에 지정 된 공급자의 특정 언어 (또는 언어)에서 해당 메타 데이터 속성에 제공 됩니다.

대상의 메타데이터 속성 “정의 쿼리”가 null이면 대상은 테이블 또는 뷰를 나타냅니다. 해당 스키마 접두사는 "Schema" 메타 데이터 속성에서 null이 아닌 경우이 고, 그렇지 않으면 엔터티 컨테이너 이름입니다.  테이블이 나 뷰 이름은 "Table" 메타 데이터 속성 (null이 아닌 경우)이 고, 그렇지 않으면 엔터티 집합 기본의 Name 속성입니다.

이러한 모든 속성은 저장소 스키마 정의 파일(SSDL)에 있는 해당 EntitySet의 정의에서 제공됩니다.

### <a name="using-primitive-types"></a>기본 형식 사용

기본 형식이 출력 명령 트리에서 참조되는 경우 일반적으로 개념적 모델의 기본 형식에서 참조됩니다. 그러나 특정 식의 경우 공급자에 해당 저장소 기본 형식이 필요합니다. 이러한 식에는 DbCastExpression, DbNullExpression(공급자가 null을 해당 형식으로 캐스팅해야 하는 경우) 등이 있습니다. 이러한 경우에 공급자는 기본 형식 종류와 해당 패싯에 따라 공급자 형식으로 매핑해야 합니다.

## <a name="see-also"></a>참고자료

- [SQL 생성](sql-generation.md)
