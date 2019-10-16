---
title: Null 값 처리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.openlocfilehash: 26b7e3a287c00f103129632ae8b0db882d468ef3
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71352981"
---
# <a name="handling-null-values"></a>Null 값 처리
관계형 데이터베이스에서 null 값은 열의 값이 없거나 알 수 없을 때 사용됩니다. null은 빈 문자열(문자 또는 datetime 데이터 형식의 경우)도 아니고 0 값(숫자 데이터 형식의 경우)도 아닙니다. ANSI SQL-92 사양에서는 모든 null이 일관성 있게 처리되도록 모든 데이터 형식에 대해 null이 동일해야 함을 규정하고 있습니다. <xref:System.Data.SqlTypes> 네임스페이스에서는 <xref:System.Data.SqlTypes.INullable> 인터페이스를 구현함으로써 null 의미 체계를 제공합니다. <xref:System.Data.SqlTypes>의 각 데이터 형식마다 해당 데이터 형식의 인스턴스에 할당할 수 있는 고유의 `IsNull` 속성과 `Null` 값이 있습니다.  
  
> [!NOTE]
> .NET Framework 버전 2.0에는 null을 허용하는 형식에 대한 지원 기능이 도입되었습니다. 프로그래머는 이 기능을 사용하여 값 형식이 내부 형식의 모든 값을 나타내도록 확장할 수 있습니다. 이러한 CLR null 허용 형식은 <xref:System.Nullable> 구조체의 인스턴스를 나타냅니다. 이 기능은 값 형식이 boxed 및 unboxed일 때 개체 형식과의 향상된 호환성을 제공하므로 특히 유용합니다. ANSI SQL null은 `null` 참조(Visual Basic에서는 `Nothing`)와 동일한 방식으로 동작하지 않기 때문에 CLR null 허용 형식으로 데이터베이스 null을 스토리지할 수는 없습니다. 데이터베이스 ANSI SQL null 값을 처리하려면 <xref:System.Data.SqlTypes> 대신 <xref:System.Nullable> null을 사용해야 합니다. Visual Basic에서 CLR nullable 형식을 사용 하는 방법에 대 한 자세한 내용은 [Nullable 값](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)형식 및 C# [nullable 값 형식 사용](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)을 참조 하세요.  
  
## <a name="nulls-and-three-valued-logic"></a>Null과 3중값 논리  
 열 정의에서 null 값을 허용하면 애플리케이션에 3중값 논리가 도입됩니다. 비교는 다음 세 가지 조건 중 하나로 평가할 수 있습니다.  
  
- True  
  
- False  
  
- 알 수 없음  
  
 null은 알 수 없는 상태로 간주되기 때문에 서로 비교되는 두 개의 null 값은 같은 값으로 간주되지 않습니다. 산술 연산자를 사용하는 식에서 피연산자 중 하나가 null이면 그 결과도 null입니다.  
  
## <a name="nulls-and-sqlboolean"></a>Null과 SqlBoolean  
 모든 <xref:System.Data.SqlTypes> 간의 비교는 <xref:System.Data.SqlTypes.SqlBoolean>을 반환합니다. 각 `IsNull`의 `SqlType` 함수는 <xref:System.Data.SqlTypes.SqlBoolean>을 반환하며 null 값을 검사하는 데 사용할 수 있습니다. 다음 진위표는 AND, OR 및 NOT 연산자가 null 값이 있을 때 어떻게 작용하는지 보여 줍니다. (T=true, F=false, U=unknown 또는 null)  
  
 ![Truth Table](./media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")  
  
### <a name="understanding-the-ansi_nulls-option"></a>ANSI_NULLS 옵션 이해  
 <xref:System.Data.SqlTypes>는 SQL Server에서 ANSI_NULLS 옵션이 설정되어 있을 때와 동일한 의미 체계를 제공합니다. 모든 산술 연산자 (+,-, \*,/,%), 비트 연산자 (~, &, \|) 및 대부분의 함수는 null @no__t을 반환 합니다.  
  
 ANSI SQL-92 표준은 WHERE 절에서 *columnName* = NULL을 지원 하지 않습니다. SQL Server에서는 ANSI_NULLS 옵션이 데이터베이스의 기본 null 허용 여부와 null 값에 대한 비교 평가를 모두 제어합니다. ANSI_NULLS를 사용하는 경우(기본값)에는 null 값을 테스트할 때 식에서 IS NULL 연산자를 사용해야 합니다. 예를 들어, 다음 비교는 ANSI_NULLS가 사용될 때 항상 알 수 없음 상태를 반환합니다.  
  
```  
colname > NULL  
```  
  
 null 값을 포함하는 변수와의 비교 역시 알 수 없음 상태를 반환합니다.  
  
```  
colname > @MyVariable  
```  
  
 null 값을 테스트하려면 IS NULL 또는 IS NOT NULL 조건자를 사용하세요. 그러면 WHERE 절이 복잡해질 수 있습니다. 예를 들어, AdventureWorks Customer 테이블의 TerritoryID 열에서는 null 값을 허용합니다. SELECT 문에서 다른 값은 물론 null 값도 테스트해야 하는 경우에는 다음과 같이 IS NULL 조건부가 포함되어야 합니다.  
  
```  
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
 SQL Server에서 ANSI_NULLS가 사용되지 않도록 설정하면 등호 연산자를 사용하여 null을 비교하는 식을 만들 수 있습니다. 그러나 다른 연결에서 해당 연결에 대해 null 옵션을 설정하게 될 수도 있습니다. 연결에 대한 ANSI_NULLS 설정과 상관없이 null 값을 테스트할 목적으로 IS NULL을 항상 사용할 수 있습니다.  
  
 `DataSet`에서는 null 값을 처리할 때 항상 ANSI SQL-92 표준을 따르기 때문에 <xref:System.Data.SqlTypes>에서는 ANSI_NULLS가 사용되지 않도록 설정할 수 있는 기능이 지원되지 않습니다.  
  
## <a name="assigning-null-values"></a>Null 값 할당  
 Null 값은 특수하며, 해당 스토리지 및 할당 의미 체계도 다양한 형식 시스템 및 스토리지 시스템에 따라 다릅니다. `Dataset`은 다양한 형식 및 스토리지 시스템에서 사용하도록 만들어집니다.  
  
 이 단원에서는 다양한 형식 시스템에서 null 값을 <xref:System.Data.DataColumn>의 <xref:System.Data.DataRow>에 할당하기 위한 null 의미 체계에 대해 설명합니다.  
  
 `DBNull.Value`  
 이 할당은 모든 형식의 `DataColumn`에 사용할 수 있습니다. 해당 형식에서 `INullable`을 구현하는 경우 `DBNull.Value`는 강력한 형식의 적절한 Null 값으로 강제 변환됩니다.  
  
 `SqlType.Null`  
 모든 <xref:System.Data.SqlTypes> 데이터 형식에서 INullable`INullable`을 구현합니다. 암시적 캐스트 연산자를 사용하여 강력한 형식의 null 값을 열의 데이터 형식으로 변환할 수 있는 경우에는 할당이 수행되어야 합니다. 그렇지 않으면 잘못된 캐스팅 예외가 throw됩니다.  
  
 `null`  
 주어진 `DataColumn` 데이터 형식에 대해 'null'이 올바른 값인 경우 이 값은 적절한 `DbNull.Value` 또는 `Null` 형식과 연결된 `INullable`(`SqlType.Null`)로 강제 변환됩니다.  
  
 `derivedUdt.Null`  
 UDT 열의 경우, null은 항상 `DataColumn`과 연결된 형식에 따라 저장됩니다. 하위 클래스에서 수행하는 동안 `DataColumn`을 구현하지 않는 `INullable`에 연결된 UDT의 경우를 살펴보세요. 이 경우 파생 클래스에 연결된 강력한 형식의 null 값이 할당되면 null 스토리지가 항상 DataColumn의 데이터 형식과 일관되므로 이 값은 형식화되지 않은 `DbNull.Value`로 저장됩니다.  
  
> [!NOTE]
> `Nullable<T>` 또는 <xref:System.Nullable> 구조체는 현재 `DataSet`에서 지원되지 않습니다.  
  
### <a name="multiple-column-row-assignment"></a>여러 열(행) 할당  
 `DataTable.Add`, `DataTable.LoadDataRow` 또는 행으로 매핑되는 <xref:System.Data.DataRow.ItemArray%2A>를 허용하는 그 밖의 API는 'null'을 DataColumn의 기본값으로 매핑합니다. 배열의 개체가 `DbNull.Value` 또는 이에 해당하는 강력한 형식의 값을 포함하는 경우 위에서 설명한 것과 동일한 규칙이 적용됩니다.  
  
 또한 다음 규칙은 `DataRow.["columnName"]` null 할당의 인스턴스에도 적용됩니다.  
  
1. 기본 *기본값* 은 강력한 형식의 null 열을 제외한 모든 값에 대해 `DbNull.Value`입니다. 여기에는 적절 한 강력한 형식의 null 값이 있습니다.  
  
2. Null 값은 "xsi:nil"에서와 같이 XML 파일과의 직렬화 중에는 작성되지 않습니다.  
  
3. 기본값을 포함하여 null이 아닌 모든 값은 항상 XML에 대한 직렬화 중에 기록됩니다. 이 경우는 null 값(xsi:nil)이 명시적이고 기본값이 암시적인 XSD/XML 의미 체계와는 달리, 기본값이 XML에 없으면 유효성 검사 파서가 연결된 XSD 스키마에서 해당 기본값을 가져올 수 있습니다. `DataTable`의 경우에는 이와 반대로 null 값이 암시적이고 기본값이 명시적입니다.  
  
4. XML 입력에서 읽어온 행에 대해 누락된 모든 열 값에는 NULL이 할당됩니다. <xref:System.Data.DataTable.NewRow%2A> 또는 이와 유사한 메서드를 사용하여 만들어진 행에는 DataColumn의 기본값이 할당됩니다.  
  
5. <xref:System.Data.DataRow.IsNull%2A> 메서드는 `true`와 `DbNull.Value`에 대해 모두 `INullable.Null`를 반환합니다.  
  
## <a name="assigning-null-values"></a>Null 값 할당  
 모든 <xref:System.Data.SqlTypes> 인스턴스의 기본값은 null입니다.  
  
 <xref:System.Data.SqlTypes>의 Null은 형식마다 다르며 `DbNull`과 같은 단일 값으로 표현할 수 없습니다. `IsNull` 속성을 사용하여 null을 검사합니다.  
  
 다음 코드 예제와 같이 Null 값을 <xref:System.Data.DataColumn>에 할당할 수 있습니다. 예외를 트리거하지 않고 null 값을 `SqlTypes` 변수에 직접 할당할 수 있습니다.  
  
### <a name="example"></a>예제  
 다음 코드 예제에서는 <xref:System.Data.DataTable> 및 <xref:System.Data.SqlTypes.SqlInt32>으로 정의된 두 개의 열이 포함된 <xref:System.Data.SqlTypes.SqlString>을 만듭니다. 이 코드는 값이 알려져 있는 행과 null 값의 행을 하나씩 추가한 다음 변수에 값을 할당하고 콘솔 창에 출력을 표시하여 <xref:System.Data.DataTable>을 반복합니다.  
  
 [!code-csharp[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/VB/source.vb#1)]  
  
 이 예제의 결과는 다음과 같습니다.  
  
```  
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>SqlTypes 및 CLR 형식을 사용하여 Null 값 비교  
 null 값을 비교할 때는 `Equals` 메서드가 <xref:System.Data.SqlTypes>에서 null 값을 평가하는 방식과 CLR 형식을 사용하는 방식을 비교하여 그 차이를 반드시 알아야 합니다. 모든 <xref:System.Data.SqlTypes>`Equals` 메서드에서는 null 값을 평가하는 데 데이터베이스 의미 체계를 사용합니다. 하나의 값 또는 두 값 모두 null이면 비교 결과는 null입니다. 한편, 두 `Equals`에 대해 CLR <xref:System.Data.SqlTypes> 메서드를 사용하면 둘 다 null인 경우 결과는 true입니다. 이는 CLR `String.Equals` 메서드와 같은 인스턴스 메서드 사용과 정적/공유 메서드인 `SqlString.Equals` 사용 간의 차이를 나타냅니다.  
  
 다음 예제에서는 각각의 `SqlString.Equals` 메서드와 `String.Equals` 메서드에 null 값 쌍이 전달된 후 빈 문자열 쌍이 전달될 때 두 메서드의 결과 차이를 보여 줍니다.  
  
 [!code-csharp[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/VB/source.vb#1)]  
  
 이 코드의 출력은 다음과 같습니다.  
  
```  
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="see-also"></a>참조

- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
- [ADO.NET 개요](../ado-net-overview.md)
