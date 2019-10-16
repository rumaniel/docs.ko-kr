---
title: '연습: BatchBlock 및 BatchedJoinBlock을 사용하여 효율성 향상'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, improving efficiency
ms.assetid: 5beb4983-80c2-4f60-8c51-a07f9fd94cb3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 32255c988397853c4b38e4ab723c7261a8999899
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929211"
---
# <a name="walkthrough-using-batchblock-and-batchedjoinblock-to-improve-efficiency"></a>연습: BatchBlock 및 BatchedJoinBlock을 사용하여 효율성 향상

TPL 데이터 흐름 라이브러리는 하나 이상의 소스에서 데이터를 검색 및 버퍼링한 다음, 해당 버퍼링된 데이터를 하나의 컬렉션으로 전파할 수 있도록 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602?displayProperty=nameWithType> 클래스를 제공합니다. 이 일괄 처리 메커니즘은 하나 이상의 소스에서 데이터를 수집한 다음, 여러 데이터 요소를 일괄 처리할 때 유용합니다. 예를 들어 데이터 흐름을 사용하여 레코드를 데이터베이스에 삽입하는 애플리케이션을 고려합니다. 이 작업은 순차적으로 한 번에 하나가 아니라 동시에 여러 항목이 삽입되는 경우 더 효율적일 수 있습니다. 이 문서에서는 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 클래스를 사용하여 이러한 데이터베이스 삽입 작업의 효율성을 개선하는 방법을 설명합니다. 또한 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> 클래스를 사용하여 프로그램이 데이터베이스에서 읽을 때 발생하는 모든 예외와 결과를 둘 다 캡처하는 방법을 설명합니다.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="prerequisites"></a>전제 조건

1. 이 연습을 시작하기 전에 [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) 문서의 조인 블록 섹션을 읽어 보세요.

2. 컴퓨터에서 Northwind 데이터베이스 복사본인 Northwind.sdf를 사용할 수 있는지 확인하세요. 이 파일은 일반적으로 %Program Files%\Microsoft SQL Server Compact Edition\v3.5\Samples\\ 폴더에 있습니다.

    > [!IMPORTANT]
    > 일부 Windows 버전에서는 Visual Studio가 비관리자 모드로 실행 중인 경우 Northwind.sdf에 연결할 수 없습니다. Northwind.sdf에 연결하거나 Visual Studio 또는 Visual Studio용 개발자 명령 프롬프트를 **관리자 권한으로 실행** 모드에서 시작합니다.

이 연습에는 다음과 같은 섹션이 있습니다.

- [콘솔 애플리케이션 만들기](#creating)

- [Employee 클래스 정의](#employeeClass)

- [직원 데이터베이스 작업 정의](#operations)

- [버퍼링을 사용하지 않고 직원 데이터를 데이터베이스에 추가](#nonBuffering)

- [버퍼링을 사용하여 직원 데이터를 데이터베이스에 추가](#buffering)

- [버퍼링된 조인을 사용하여 데이터베이스에서 직원 데이터 읽기](#bufferedJoin)

- [전체 예제](#complete)

<a name="creating"></a>

## <a name="creating-the-console-application"></a>콘솔 애플리케이션 만들기

1. Visual Studio에서 Visual C# 또는 Visual Basic **콘솔 애플리케이션** 프로젝트를 만듭니다. 이 문서에서 프로젝트 이름은 `DataflowBatchDatabase`입니다.

2. 프로젝트에서 System.Data.SqlServerCe.dll에 대한 참조와 System.Threading.Tasks.Dataflow.dll에 대한 참조를 추가합니다.

3. Form1.cs(Visual Basic에서는 Form1.vb)에 다음 `using`(Visual Basic에서는 `Imports`) 명령문이 포함되어 있는지 확인합니다.

    [!code-csharp[TPLDataflow_BatchDatabase#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#1)]
    [!code-vb[TPLDataflow_BatchDatabase#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#1)]

4. `Program` 클래스에 다음 데이터 멤버를 추가합니다.

    [!code-csharp[TPLDataflow_BatchDatabase#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#2)]
    [!code-vb[TPLDataflow_BatchDatabase#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#2)]

<a name="employeeClass"></a>

## <a name="defining-the-employee-class"></a>Employee 클래스 정의

`Program` 클래스에 `Employee` 클래스를 추가합니다.

[!code-csharp[TPLDataflow_BatchDatabase#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#3)]
[!code-vb[TPLDataflow_BatchDatabase#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#3)]

`Employee` 클래스에는 세 가지 속성 `EmployeeID` , `LastName` 및 `FirstName`이 포함되어 있습니다. 이러한 속성은 Northwind 데이터베이스의 `Employees` 테이블에 있는 `Employee ID`, `Last Name` 및 `First Name` 열에 해당합니다. 이 데모에서 `Employee` 클래스는 해당 속성에 대한 임의 값을 가지는 `Employee` 개체를 만드는 `Random` 메서드도 정의합니다.

<a name="operations"></a>

## <a name="defining-employee-database-operations"></a>직원 데이터베이스 작업 정의

`Program` 클래스에 `InsertEmployees`, `GetEmployeeCount` 및 `GetEmployeeID` 메서드를 추가합니다.

[!code-csharp[TPLDataflow_BatchDatabase#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#4)]
[!code-vb[TPLDataflow_BatchDatabase#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#4)]

`InsertEmployees` 메서드는 새 직원 레코드를 데이터베이스에 추가합니다. `GetEmployeeCount` 메서드는 `Employees` 테이블의 항목 수를 검색합니다. `GetEmployeeID` 메서드는 제공된 이름이 있는 첫 번째 직원의 식별자를 검색합니다. 이러한 각 메서드는 Northwind 데이터베이스에 대한 연결 문자열을 사용하고 `System.Data.SqlServerCe` 네임스페이스의 기능을 사용하여 데이터베이스와 통신합니다.

<a name="nonBuffering"></a>

## <a name="adding-employee-data-to-the-database-without-using-buffering"></a>버퍼링을 사용하지 않고 직원 데이터를 데이터베이스에 추가

`Program` 클래스에 `AddEmployees` 및 `PostRandomEmployees` 메서드를 추가합니다.

[!code-csharp[TPLDataflow_BatchDatabase#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#5)]
[!code-vb[TPLDataflow_BatchDatabase#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#5)]

`AddEmployees` 메서드는 데이터 흐름을 사용하여 데이터베이스에 임의 직원 데이터를 추가합니다. 데이터베이스에 직원 항목을 추가하기 위해 `InsertEmployees` 메서드를 호출하는 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체를 만듭니다. 그런 다음, `AddEmployees` 메서드는 `PostRandomEmployees` 메서드를 호출하여 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체에 여러 `Employee` 개체를 게시합니다. 그런 다음, `AddEmployees` 메서드는 모든 삽입 작업이 완료될 때까지 대기합니다.

<a name="buffering"></a>

## <a name="using-buffering-to-add-employee-data-to-the-database"></a>버퍼링을 사용하여 직원 데이터를 데이터베이스에 추가

`Program` 클래스에 `AddEmployeesBatched` 메서드를 추가합니다.

[!code-csharp[TPLDataflow_BatchDatabase#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#6)]
[!code-vb[TPLDataflow_BatchDatabase#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#6)]

이 메서드는 `AddEmployees`와 유사합니다. 단, 이 메서드는 해당 개체를 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체에 보내기 전에 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 클래스를 사용하여 여러 `Employee` 개체를 버퍼링합니다. <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 클래스는 여러 요소를 컬렉션으로 전파하므로 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체는 `Employee` 개체 배열에서 작동하도록 수정됩니다. `AddEmployees` 메서드처럼 `AddEmployeesBatched`는 `PostRandomEmployees` 메서드를 호출하여 여러 `Employee` 개체를 게시합니다. 그러나 `AddEmployeesBatched`는 이러한 개체를 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 개체에 게시합니다. 또한 `AddEmployeesBatched` 메서드는 모든 삽입 작업이 완료될 때까지 대기합니다.

<a name="bufferedJoin"></a>

## <a name="using-buffered-join-to-read-employee-data-from-the-database"></a>버퍼링된 조인을 사용하여 데이터베이스에서 직원 데이터 읽기

`Program` 클래스에 `GetRandomEmployees` 메서드를 추가합니다.

[!code-csharp[TPLDataflow_BatchDatabase#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#7)]
[!code-vb[TPLDataflow_BatchDatabase#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#7)]

이 메서드는 임의 직원에 대한 정보를 콘솔에 인쇄합니다. 여러 개의 임의 `Employee` 개체를 만들고 `GetEmployeeID` 메서드를 호출하여 각 개체의 고유 식별자를 검색합니다. 지정된 이름 및 성이 일치하는 직원이 없는 경우 `GetEmployeeID` 메서드가 예외를 throw하므로 `GetRandomEmployees` 메서드는 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> 클래스를 사용하여 `GetEmployeeID` 호출 성공 시 `Employee` 개체를 저장하고 호출 실패 시 <xref:System.Exception?displayProperty=nameWithType> 개체를 저장합니다. 이 예제의 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체는 `Employee` 개체 목록과 <xref:System.Exception> 개체 목록을 포함하는 <xref:System.Tuple%602> 개체에서 작동합니다. 수신된 `Employee` 및 <xref:System.Exception> 개체의 합계가 일괄 처리 크기와 같을 경우 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> 개체는 이 데이터를 전파합니다.

<a name="complete"></a>

## <a name="the-complete-example"></a>전체 예제

다음 예제에서는 전체 코드를 보여 줍니다. `Main` 메서드는 일괄 처리된 데이터베이스 삽입을 수행하는 데 필요한 시간과 일괄 처리되지 않은 데이터베이스 삽입을 수행하는 데 필요한 시간을 비교합니다. 또한 버퍼링된 조인을 사용하여 데이터베이스에서 직원 데이터를 읽고 오류를 보고하는 작업도 보여줍니다.

[!code-csharp[TPLDataflow_BatchDatabase#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#100)]
[!code-vb[TPLDataflow_BatchDatabase#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#100)]

## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
