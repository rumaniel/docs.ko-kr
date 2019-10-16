---
title: '연습: 간단한 개체 모델 및 쿼리(C#)'
ms.date: 03/30/2017
ms.assetid: 419961cc-92d6-45f5-ae8a-d485bdde3a37
ms.openlocfilehash: a9b3b57e37331cd13f2cd30b8a7663f2fb39d8c1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792135"
---
# <a name="walkthrough-simple-object-model-and-query-c"></a>연습: 간단한 개체 모델 및 쿼리(C#)

이 연습에서는 간단한 기본 엔드투엔드 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 시나리오에 대해 설명합니다. 샘플 Northwind 데이터베이스의 Customers 테이블을 모델링하는 엔터티 클래스를 만듭니다. 그런 다음 단순 쿼리를 만들어 London에 있는 고객을 나열합니다.

이 연습은 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 개념을 보여 주기 위한 코드를 중심으로 디자인되었습니다. 일반적으로 개체 관계형 디자이너를 사용 하 여 개체 모델을 만듭니다.

[!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]

이 연습은 Visual C# 개발 설정을 사용하여 작성했습니다.

## <a name="prerequisites"></a>필수 구성 요소

- 이 연습에서는 전용 폴더("c:\linqtest5")를 사용하여 파일을 저장합니다. 연습을 시작하기 전에 먼저 이 폴더를 만듭니다.

- 이 연습을 수행하려면 Northwind 샘플 데이터베이스가 있어야 합니다. 이 데이터베이스가 개발 컴퓨터에 없는 경우 Microsoft 다운로드 사이트에서 다운로드할 수 있습니다. 지침은 [샘플 데이터베이스 다운로드](downloading-sample-databases.md)를 참조 하세요. 이 데이터베이스를 다운로드한 후 파일을 c:\linqtest5 폴더에 복사합니다.

## <a name="overview"></a>개요

이 연습은 다음과 같은 여섯 가지 주요 작업으로 구성됩니다.

- Visual Studio에서 솔루션 만들기 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]

- 데이터베이스 테이블에 클래스 매핑

- 데이터베이스 열을 나타내도록 클래스의 속성 지정

- Northwind 데이터베이스에 대한 연결 지정

- 데이터베이스에 대해 실행할 단순 쿼리 만들기

- 쿼리 실행 및 결과 검토

## <a name="creating-a-linq-to-sql-solution"></a>LINQ to SQL 솔루션 만들기

이 첫 번째 작업에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 프로젝트를 빌드하고 실행 하는 데 필요한 참조를 포함 하는 Visual Studio 솔루션을 만듭니다.

### <a name="to-create-a-linq-to-sql-solution"></a>LINQ to SQL 솔루션을 만들려면

1. Visual Studio **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭 합니다.

2. **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **C#시각적 개체**를 클릭 합니다.

3. **템플릿** 창에서 **콘솔 애플리케이션**을 클릭합니다.

4. **이름** 상자에 **linqconsoleapp 입력**을 입력 합니다.

5. **위치** 상자에서 프로젝트 파일을 저장할 위치를 확인 합니다.

6. **확인**을 클릭합니다.

## <a name="adding-linq-references-and-directives"></a>LINQ 참조 및 지시문 추가

이 연습에서는 프로젝트에 기본적으로 설치되어 있지 않을 수 있는 어셈블리를 사용합니다. System.object가 프로젝트에 참조로 나열 되지 않은 경우 ( **솔루션 탐색기**의 **참조** 노드 확장) 다음 단계에 설명 된 대로 추가 합니다.

### <a name="to-add-systemdatalinq"></a>System.Data.Linq를 추가하려면

1. **솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭 한 다음 **참조 추가**를 클릭 합니다.

2. **참조 추가** 대화 상자에서 **.net**을 클릭 하 고 system.xml 어셈블리를 클릭 한 다음 **확인**을 클릭 합니다.

     어셈블리가 프로젝트에 추가됩니다.

3. **Program.cs**의 맨 위에 다음 지시문을 추가 합니다.

     [!code-csharp[DLinqWalk1CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#1)]

## <a name="mapping-a-class-to-a-database-table"></a>데이터베이스 테이블에 클래스 매핑

이 단계에서는 클래스를 생성하여 데이터베이스 테이블에 매핑합니다. 이러한 클래스를 *엔터티 클래스*라고 합니다. 매핑을 수행하려면 <xref:System.Data.Linq.Mapping.TableAttribute> 특성을 추가하면 됩니다. <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> 속성은 데이터베이스의 테이블 이름을 지정합니다.

### <a name="to-create-an-entity-class-and-map-it-to-a-database-table"></a>엔터티 클래스를 만들어 데이터베이스 테이블에 매핑하려면

- 다음 코드를 Program.cs에서 `Program` 클래스 선언 바로 위에 입력하거나 붙여넣습니다.

     [!code-csharp[DLinqWalk1CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#2)]

## <a name="designating-properties-on-the-class-to-represent-database-columns"></a>데이터베이스 열을 나타내도록 클래스의 속성 지정

이 단계에서는 다음과 같은 몇 가지 작업을 수행합니다.

- <xref:System.Data.Linq.Mapping.ColumnAttribute> 특성을 사용하여 데이터베이스 테이블의 열을 나타내도록 엔터티 클래스의 `CustomerID` 및 `City` 속성을 지정합니다.

- 데이터베이스의 기본 키 열을 나타내도록 `CustomerID` 속성을 지정합니다.

- 전용 스토리지에 `_CustomerID` 및 `_City` 필드를 지정합니다. 그러면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 비즈니스 논리가 포함된 공용 접근자를 사용하는 대신 값을 직접 저장하고 검색할 수 있습니다.

### <a name="to-represent-characteristics-of-two-database-columns"></a>두 데이터베이스 열의 특징을 나타내려면

- 다음 코드를 Program.cs에서 `Customer` 클래스의 중괄호 내에 입력하거나 붙여넣습니다.

     [!code-csharp[DLinqWalk1CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#3)]

## <a name="specifying-the-connection-to-the-northwind-database"></a>Northwind 데이터베이스에 대한 연결 지정

이 단계에서는 <xref:System.Data.Linq.DataContext> 개체를 사용하여 코드 기반 데이터 구조체와 데이터베이스 자체 간의 연결을 설정할 수 있습니다. <xref:System.Data.Linq.DataContext>는 데이터베이스에서 개체를 검색하고 변경 내용을 전송할 때 사용하는 기본 채널입니다.

또한 `Table<Customer>`이 데이터베이스의 Customers 테이블에 대한 쿼리에 대해 형식화된 논리적 테이블로 사용되도록 선언합니다. 이후 단계에서 이러한 쿼리를 만들고 실행합니다.

### <a name="to-specify-the-database-connection"></a>데이터베이스 연결을 지정하려면

- 다음 코드를 `Main` 메서드에 입력하거나 붙여넣습니다.

     `northwnd.mdf` 파일이 linqtest5 폴더 내에 있는 것으로 가정합니다. 자세한 내용은 이 연습 앞부분의 사전 요구 사항 단원을 참조하세요.

     [!code-csharp[DLinqWalk1CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#4)]

## <a name="creating-a-simple-query"></a>단순 쿼리 작성

이 단계에서는 데이터베이스 Customers 테이블에서 London에 있는 고객을 찾는 쿼리를 만듭니다. 이 단계의 쿼리 코드는 쿼리를 설명하기만 하고 실행하지는 않습니다. 이 방법을 *지연 된 실행*이라고 합니다. 자세한 내용은 [LINQ 쿼리 소개(C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)를 참조하세요.

또한 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 생성하는 SQL 명령을 보여 주는 로그 출력을 만듭니다. <xref:System.Data.Linq.DataContext.Log%2A>를 사용하는 이 로깅 기능은 디버깅할 때와 데이터베이스로 전송되는 명령이 쿼리를 정확히 나타내는지 확인할 때 유용합니다.

### <a name="to-create-a-simple-query"></a>단순 쿼리를 작성하려면

- 다음 코드를 `Main` 메서드에서 `Table<Customer>` 선언 뒤에 입력하거나 붙여넣습니다.

     [!code-csharp[DLinqWalk1ACS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#5)]

## <a name="executing-the-query"></a>쿼리 실행

이 단계에서는 실제로 쿼리를 실행합니다. 앞의 단계에서 만든 쿼리 식은 결과가 필요할 때까지 계산되지 않습니다. `foreach` 반복을 시작하면 데이터베이스에 대해 SQL 명령이 실행되고 개체가 구체화됩니다.

### <a name="to-execute-the-query"></a>쿼리를 실행하려면

1. 다음 코드를 `Main` 메서드의 끝(쿼리 설명 뒤)에 입력하거나 붙여넣습니다.

     [!code-csharp[DLinqWalk1ACS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#6)]

2. F5 키를 눌러 애플리케이션을 디버깅합니다.

    > [!NOTE]
    > 응용 프로그램에서 런타임 오류를 생성 하는 경우 [연습에서 학습](learning-by-walkthroughs.md)의 문제 해결 섹션을 참조 하세요.

     콘솔 창의 쿼리 결과는 다음과 같습니다.

     `ID=AROUT, City=London`

     `ID=BSBEV, City=London`

     `ID=CONSH, City=London`

     `ID=EASTC, City=London`

     `ID=NORTS, City=London`

     `ID=SEVES, City=London`

3. 콘솔 창에서 Enter 키를 눌러 애플리케이션을 닫습니다.

## <a name="next-steps"></a>다음 단계

[연습: 관계 간 쿼리 (C#)](walkthrough-querying-across-relationships-csharp.md) 토픽은이 연습을 종료 하는 위치에서 계속 됩니다. 관계 간 쿼리 연습에서는에서 관계형 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 데이터베이스의 *조인과* 유사 하 게 테이블을 쿼리 하는 방법을 보여 줍니다.

관계 간 쿼리 연습을 수행하려면 방금 완료한 연습의 솔루션을 저장해야 합니다.

## <a name="see-also"></a>참고자료

- [연습으로 학습](learning-by-walkthroughs.md)
