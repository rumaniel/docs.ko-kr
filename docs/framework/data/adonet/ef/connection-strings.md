---
title: ADO.NET Entity Framework의 연결 문자열
ms.date: 10/15/2018
ms.assetid: 78d516bc-c99f-4865-8ff1-d856bc1a01c0
ms.openlocfilehash: 8c583d74dd3b1b8322fa8ea884092f8eb893af6a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251648"
---
# <a name="connection-strings-in-the-adonet-entity-framework"></a>ADO.NET Entity Framework의 연결 문자열

연결 문자열에는 데이터 공급자에서 데이터 소스에 매개 변수로 전달되는 초기화 정보가 있습니다. 연결 문자열 구문은 데이터 공급자에 따라 다르며 연결을 여는 동안 연결 문자열이 구문 분석됩니다. Entity Framework에서 사용하는 연결 문자열에는 Entity Framework를 지원하는 기본 ADO.NET 데이터 공급자에 연결하는 데 사용되는 정보가 들어 있습니다. 또한 필요한 모델 및 매핑 파일에 대한 정보도 들어 있습니다.

연결 문자열은 EntityClient 공급자가 모델 및 매핑 메타데이터에 액세스하고 데이터 소스에 연결할 때 사용됩니다. <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A>의 <xref:System.Data.EntityClient.EntityConnection> 속성을 통해 연결 문자열에 액세스하거나 설정할 수 있습니다. <xref:System.Data.EntityClient.EntityConnectionStringBuilder> 클래스를 사용하여 프로그래밍 방식으로 연결 문자열의 매개 변수를 생성하거나 액세스할 수 있습니다. 자세한 내용은 [방법: EntityConnection 연결 문자열](how-to-build-an-entityconnection-connection-string.md)을 작성 합니다.

[엔터티 데이터 모델 도구](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100)) 는 응용 프로그램의 구성 파일에 저장 되는 연결 문자열을 생성 합니다. <xref:System.Data.Objects.ObjectContext>는 개체 쿼리를 만들 때 이 연결 정보를 자동으로 검색합니다. <xref:System.Data.EntityClient.EntityConnection> 인스턴스에서 사용하는 <xref:System.Data.Objects.ObjectContext>은 <xref:System.Data.Objects.ObjectContext.Connection%2A> 속성에서 액세스할 수 있습니다. 자세한 내용은 [트랜잭션과 연결 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))합니다.

## <a name="connection-string-syntax"></a>연결 문자열 구문

연결 문자열의 일반적인 구문에 대 한 자세한 내용은 [연결 문자열 구문을 참조 하세요. ADO.NET의 연결 문자열](../connection-strings.md#connection-string-syntax)입니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수

다음 표에는 <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A>에 포함되는 키워드 값의 올바른 이름이 정리되어 있습니다.

|키워드|설명|
|-------------|-----------------|
|`Provider`|`Name` 키워드를 지정하지 않은 경우에 필요합니다. 기본 공급자의 <xref:System.Data.Common.DbProviderFactory> 개체를 검색하는 데 사용되는 공급자 이름입니다. 이 값은 상수입니다.<br /><br /> `Name` 키워드가 엔터티 연결 문자열에 포함되어 있지 않은 경우 `Provider` 키워드에 대해 비어 있지 않은 값이 필요합니다. 이 키워드는 `Name` 키워드와 함께 사용할 수 없습니다.|
|`Provider Connection String`|선택 사항입니다. 기본 데이터 소스에 전달되는 공급자별 연결 문자열을 지정합니다. 이 연결 문자열에는 데이터 공급자에 대 한 유효한 키워드/값 쌍이 포함 되어 있습니다. `Provider Connection String`이 올바르지 않으면 데이터 소스에서 해당 문자열을 평가할 때 런타임 오류가 발생합니다.<br /><br /> 이 키워드는 `Name` 키워드와 함께 사용할 수 없습니다.<br /><br /> [ADO.NET 연결 문자열](../connection-strings.md)의 일반 구문에 따라 값을 이스케이프 해야 합니다. 예를 들어 다음 연결 문자열 `Server=serverName; User ID = userID`을 고려해 보십시오. 세미콜론을 포함 하기 때문에 이스케이프 해야 합니다. 큰따옴표를 포함 하지 않기 때문에 이스케이프에 사용 될 수 있습니다.<br /><br /> `Provider Connection String ="Server=serverName; User ID = userID";`|
|`Metadata`|`Name` 키워드를 지정하지 않은 경우에 필요합니다. 메타데이터와 매핑 정보를 검색할 대상 디렉터리, 파일 및 리소스 위치에 대한 파이프로 구분된 목록입니다. 예를 들면 다음과 같습니다.<br /><br /> `Metadata=`<br /><br /> `c:\model &#124; c:\model\sql\mapping.msl;`<br /><br /> 파이프 구분 기호 양쪽의 공백은 무시됩니다.<br /><br /> 이 키워드는 `Name` 키워드와 함께 사용할 수 없습니다.|
|`Name`|애플리케이션에서는 필수 키워드/값 연결 문자열 값을 제공하는 애플리케이션 구성 파일에 연결 이름을 선택적으로 지정할 수 있습니다. 이 경우에는 연결 문자열에 이름을 직접 지정할 수 없습니다. `Name` 키워드는 구성 파일에 사용할 수 없습니다.<br /><br /> `Name` 키워드가 엔터티 연결 문자열에 포함되어 있지 않은 경우 Provider 키워드에 대해 비어 있지 않은 값이 필요합니다.<br /><br /> 이 키워드는 다른 모든 연결 문자열 키워드와 함께 사용할 수 없습니다.|

다음은 응용 프로그램 구성 파일에 저장 된 [AdventureWorks Sales 모델](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 에 대 한 연결 문자열의 예입니다.

## <a name="model-and-mapping-file-locations"></a>모델 및 매핑 파일 위치

`Metadata` 매개 변수에는 `EntityClient` 공급자가 모델 및 매핑 파일을 검색할 위치 목록이 포함됩니다. 모델 및 매핑 파일은 응용 프로그램 실행 파일과 동일한 디렉터리에 배포되는 경우가 많습니다. 이러한 파일을 특정 위치에 배포하거나 응용 프로그램에 포함 리소스로 포함할 수도 있습니다.

포함 리소스는 다음과 같이 지정됩니다.

```
Metadata=res://<assemblyFullName>/<resourceName>.
```

다음 옵션을 사용하여 포함 리소스의 위치를 정의할 수 있습니다.

|옵션|설명|
|-|-|
|`assemblyFullName`|포함 리소스가 있는 어셈블리의 전체 이름입니다. 이 이름에는 다음과 같이 단순한 이름, 버전 이름, 지원되는 문화권 및 공개 키가 포함됩니다.<br /><br /> `ResourceLib, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`<br /><br /> 응용 프로그램이 액세스할 수 있는 모든 어셈블리에 리소스를 포함할 수 있습니다.<br /><br /> 에 대해\* `assemblyFullName`와일드 카드 ()를 지정 하는 경우 Entity Framework 런타임은 다음 위치의 리소스를이 순서로 검색 합니다.<br /><br /> 1.  호출 어셈블리<br />2.  참조된 어셈블리입니다.<br />3.  응용 프로그램의 bin 디렉터리에 있는 어셈블리<br /><br /> 파일이 이러한 위치 중 하나에 없으면 예외가 throw됩니다. **참고:**  와일드카드(*)를 사용하면 Entity Framework는 모든 어셈블리에서 올바른 이름을 가진 리소스를 검색해야 합니다. 성능을 향상시키려면 와일드카드 대신 어셈블리 이름을 지정합니다.|
|`resourceName`|포함 된 리소스의 이름 (예: Adventureworksmodel.edmx)입니다. 메타데이터 서비스는 확장명이 .csdl, .ssdl 또는 .msl 중 하나인 파일 또는 리소스만 찾습니다. `resourceName`을 지정하지 않으면 모든 메타데이터 리소스가 로드됩니다. 리소스 이름은 어셈블리 내에서 고유해야 합니다. 같은 이름을 가진 여러 파일이 어셈블리의 서로 다른 디렉터리에 정의되어 있으면 `resourceName`에서 리소스 이름 앞에 폴더 구조가 포함되어야 합니다(예: FolderName.FileName.csdl).<br /><br /> `resourceName`에 와일드카드(*)를 지정한 경우에는 `assemblyFullName`이 필요하지 않습니다.|

> [!NOTE]
> 성능을 향상시키려면 호출 어셈블리에 기본 매핑 및 메타데이터 파일에 대한 참조가 없는 웹이 아닌 시나리오를 제외하고 호출 어셈블리에 리소스를 포함합니다.

다음 예제에서는 호출 어셈블리, 참조된 어셈블리 및 응용 프로그램의 bin 디렉터리에 있는 기타 어셈블리의 모든 모델 및 매핑 파일을 로드합니다.

```
Metadata=res://*/
```

다음 예제에서는 AdventureWorks 어셈블리의 model.csdl 파일을 로드하고, 실행 중인 응용 프로그램의 기본 디렉터리에서 model.ssdl 및 model.msl 파일을 로드합니다.

```
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|model.ssdl|model.msl
```

다음 예제에서는 특정 어셈블리의 지정된 리소스 세 개를 로드합니다.

```
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.ssdl|
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.msl
```

다음 예제에서는 확장명이 .csdl, .msl 및 .ssdl인 어셈블리의 모든 포함 리소스를 로드합니다.

```
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/
```

다음 예제에서는 로드 된 어셈블리 위치에서 상대 파일 경로의 모든 리소스와 "\\datadir\metadata"를 로드 합니다.

```
Metadata=datadir\metadata\
```

다음 예제에서는 로드된 어셈블리 위치의 상대 파일 경로에 있는 모든 리소스를 로드합니다.

```
Metadata=.\
```

## <a name="support-for-the-124datadirectory124-substitution-string-and-the-web-application-root-operator-"></a>&#124;DataDirectory&#124; 대체 문자열 및 웹 응용 프로그램 루트 연산자 (~) 지원

`DataDirectory`및 ~ 연산자는 <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> `Metadata` 및 `Provider Connection String` 키워드의 일부로에서 사용 됩니다. <xref:System.Data.EntityClient.EntityConnection>은 `DataDirectory` 및 ~ 연산자를 각각 <xref:System.Data.Metadata.Edm.MetadataWorkspace> 및 저장소 공급자에 전달합니다.

|용어|설명|
|----------|-----------------|
|`&#124;DataDirectory&#124;`|매핑 및 메타데이터 파일에 대한 상대 경로로 확인됩니다. 이 값은 `AppDomain.SetData("DataDirectory", objValue)` 메서드를 통해 설정됩니다. 대체 `DataDirectory` 문자열은 파이프 문자로 묶어야 하며, 이름 및 파이프 문자 사이에 공백이 있을 수 없습니다. `DataDirectory` 이름은 대/소문자를 구분하지 않습니다.<br /><br /> "DataDirectory" 라는 실제 디렉터리를 메타 데이터 경로 목록의 멤버로 전달 해야 하는 경우 이름의 양쪽 또는 양쪽에 공백을 추가 합니다. 예: `Metadata="DataDirectory1 &#124; DataDirectory &#124; DataDirectory2"` ASP.NET 응용 프로그램은 &#124;"&#124; \<응용 프로그램 루트 >/app_data" 폴더로 DataDirectory를 확인 합니다.|
|~|웹 응용 프로그램 루트로 확인됩니다. 선행 위치에 있는 ~ 문자는 항상 웹 응용 프로그램 루트 연산자(~)로 해석되지만, 유효한 로컬 하위 디렉터리를 나타낼 수도 있습니다. 이러한 로컬 하위 디렉터리를 참조하려면 사용자가 명시적으로 `./~`를 전달해야 합니다.|

`DataDirectory` 및 ~ 연산자는 경로의 시작 부분에만 지정해야 하며, 다른 위치에 있으면 확인되지 않습니다. Entity Framework에서 `~/data`를 확인하려고 하지만 `/data/~`를 실제 경로로 처리합니다.

`DataDirectory` 또는 ~ 연산자로 시작하는 경로는 `DataDirectory` 및 ~ 연산자 분기 외부의 실제 경로로 확인할 수 없습니다. 예를 들어 `~` , `~/data`, `~/bin/Model/SqlServer` 경로는 확인됩니다. 하지만 `~/..`, `~/../other` 경로는 확인되지 않습니다.

`DataDirectory` 및 ~ 연산자를 확장하여 `|DataDirectory|\Model`, `~/bin/Model`와 같은 하위 디렉터리를 포함할 수 있습니다.

`DataDirectory` 대체 문자열 및 ~ 연산자 확인은 비재귀적입니다. 예를 들어 `DataDirectory`에 `~` 문자가 포함되어 있으면 예외가 발생합니다. 이 동작은 무한 재귀를 방지합니다.

## <a name="see-also"></a>참고자료

- [데이터 공급자 작업](working-with-data-providers.md)
- [배포 고려 사항](deployment-considerations.md)
- [연결 및 트랜잭션 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [연결 문자열](../connection-strings.md)
