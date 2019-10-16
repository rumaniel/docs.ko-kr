---
title: SqlMetal.exe(코드 생성 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- SQLMetal [LINQ to SQL]
- code generation tool
- SQLMetal.exe
- LINQ to SQL, serialization
- LINQ to SQL, DBML files
- LINQ to SQL, SQLMetal
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
ms.openlocfilehash: d5b4c2b59b585b3d3a3584ef9055e70c9d998e85
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044084"
---
# <a name="sqlmetalexe-code-generation-tool"></a>SqlMetal.exe(코드 생성 도구)
SqlMetal 명령줄 도구는 .NET Framework의 [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] 구성 요소에 사용할 코드 및 매핑을 생성합니다. 이 항목의 뒷부분에 나오는 옵션을 적용하면 SqlMetal을 통해 다음을 포함하는 다양한 작업을 수행할 수 있습니다.  
  
- 데이터베이스에서 소스 코드 및 매핑 특성이나 매핑 파일 생성  
  
- 데이터베이스에서 사용자 지정에 사용할 중간 데이터베이스 태그 언어(.dbml) 파일 생성  
  
- .dbml 파일에서 코드 및 매핑 특성이나 매핑 파일 생성  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 기본적으로 이 파일은 `drive`:\Program Files\Microsoft SDKs\Windows\v`n.nn`\bin에 있습니다. Visual Studio를 설치하지 않으면 [Windows SDK](https://go.microsoft.com/fwlink/?LinkId=142225)를 다운로드하여 SQLMetal 파일도 가져올 수 있습니다.  
  
> [!NOTE]
> Visual Studio를 사용하는 개발자는 개체 관계형 디자이너를 사용하여 엔터티 클래스를 생성할 수도 있습니다. 명령줄 방식을 사용하면 대규모 데이터베이스에 대해 효율적으로 크기를 조정할 수 있습니다. SqlMetal은 명령줄 도구이므로 빌드 프로세스에서 사용할 수 있습니다.  
  
 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요. 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
sqlmetal [options] [<input file>]  
```  
  
## <a name="options"></a>옵션  
 최신 옵션 목록을 보려면 설치한 위치의 명령 프롬프트에서 `sqlmetal /?` 를 입력합니다.  
  
 **연결 옵션**  
  
|옵션|설명|  
|------------|-----------------|  
|**/server:** *\<name>*|데이터베이스 서버 이름을 지정합니다.|  
|**/database:** *\<name>*|서버의 데이터베이스 카탈로그를 지정합니다.|  
|**/user:** *\<name>*|로그온 사용자 ID를 지정합니다. 기본값: Windows 인증 사용.|  
|**/password:** *\<password>*|로그온 암호를 지정합니다. 기본값: Windows 인증 사용.|  
|**/conn:** *\<connection string>*|데이터베이스 연결 문자열을 지정합니다. **/server**, **/database**, **/user**또는 **/password** 옵션과 함께 사용할 수 없습니다.<br /><br /> 연결 문자열에 파일 이름을 포함하지 마세요. 대신 파일 이름을 명령줄에 입력 파일로 추가합니다. 예를 들어 **sqlmetal /code:"c:\northwind.cs" /language:csharp "c:\northwnd.mdf"** 에서는 "c:\northwnd.mdf"를 입력 파일로 지정합니다.|  
|**/timeout:** *\<seconds>*|SqlMetal이 데이터베이스에 액세스할 때의 시간 제한 값을 지정합니다. 기본값: 0(시간 제한 없음).|  
  
 **추출 옵션**  
  
|옵션|설명|  
|------------|-----------------|  
|**/views**|데이터베이스 뷰를 추출합니다.|  
|**/functions**|데이터베이스 기능을 추출합니다.|  
|**/sprocs**|저장 프로시저를 추출합니다.|  
  
 **출력 옵션**  
  
|옵션|설명|  
|------------|-----------------|  
|**/dbml** *[:file]*|출력을 .dbml로 보냅니다. **/map** 옵션과 함께 사용할 수 없습니다.|  
|**/code** *[:file]*|출력을 소스 코드로 보냅니다. **/dbml** 옵션과 함께 사용할 수 없습니다.|  
|**/map** *[:file]*|특성 대신 XML 매핑 파일을 생성합니다. **/dbml** 옵션과 함께 사용할 수 없습니다.|  
  
 **기타**  
  
|옵션|설명|  
|------------|-----------------|  
|**/language:** *\<language>*|소스 코드 언어를 지정합니다.<br /><br /> 유효한 *\<language>* : vb, csharp.<br /><br /> 기본값: 코드 파일 이름의 확장명에서 파생됩니다.|  
|**/namespace:** *\<name>*|생성된 코드의 네임스페이스를 지정합니다. 기본적으로는 네임스페이스가 없습니다.|  
|**/context:** *\<type>*|데이터 컨텍스트 클래스의 이름을 지정합니다. 기본값: 데이터베이스 이름에서 파생됩니다.|  
|**/entitybase:** *\<type>*|생성된 코드에서 엔터티 클래스의 기본 클래스를 지정합니다. 기본값: 엔터티에 기본 클래스가 없습니다.|  
|**/pluralize**|클래스 및 멤버 이름을 자동으로 복수 및 단수로 지정합니다.<br /><br /> 이 옵션은 미국에서만 사용할 수 있습니다. 영어 버전입니다.|  
|**/serialization:** *\<option>*|serialize 가능한 클래스를 생성합니다.<br /><br /> Valid *\<option>* : None, Unidirectional. 기본값: 없음<br /><br /> 자세한 내용은 [Serialization](../data/adonet/sql/linq/serialization.md)을 참조하세요.|  
  
 **입력 파일**  
  
|옵션|설명|  
|------------|-----------------|  
|**\<input file>**|SQL Server Express .mdf 파일, SQL Server Compact 3.5 .sdf 파일 또는 .dbml 중간 파일을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 실제로 SqlMetal 기능에는 다음과 같은 두 단계가 포함됩니다.  
  
- 데이터베이스의 메타데이터를 .dbml 파일에 추출  
  
- 코드 출력 파일 생성  
  
     적절한 명령줄 옵션을 사용하면 Visual Basic 또는 C# 소스 코드를 생성하거나 XML 매핑 파일을 생성할 수 있습니다.  
  
 .mdf 파일에서 메타데이터를 추출하려면 다른 모든 옵션 뒤에 .mdf 파일 이름을 지정해야 합니다.  
  
 **/server** 가 지정되어 있지 않으면 **localhost/sqlexpress** 로 간주됩니다.  
  
 Microsoft SQL Server 2005는 다음 조건 중 하나 이상이 true이면 예외를 throw합니다.  
  
- SqlMetal이 자기 자신을 호출하는 저장 프로시저의 추출을 시도합니다.  
  
- 저장 프로시저, 함수 또는 뷰의 중첩 수준이 32를 초과합니다.  
  
     SqlMetal이 이 예외를 catch하여 경고로 보고합니다.  
  
 입력 파일 이름을 지정하려면 이름을 명령줄에 입력 파일로 추가합니다. **/conn** 옵션을 사용하여 연결 문자열에 파일 이름을 포함할 수는 없습니다.  
  
## <a name="examples"></a>예  
 추출된 SQL 메타데이터를 포함하는 .dbml 파일을 생성합니다.  
  
 **sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml**  
  
 SQL Server Express를 사용하여 .mdf 파일에서 추출한 SQL 메타데이터를 포함하는 .dbml 파일을 생성합니다.  
  
 **sqlmetal /dbml:mymeta.dbml mydbfile.mdf**  
  
 SQL Server Express에서 추출한 SQL 메타데이터를 포함하는 .dbml 파일을 생성합니다.  
  
 **sqlmetal /server:.\sqlexpress /dbml:mymeta.dbml /database:northwind**  
  
 .dbml 메타데이터 파일에서 소스 코드를 생성합니다.  
  
 **sqlmetal /namespace:nwind /code:nwind.cs /language:csharp mymetal.dbml**  
  
 SQL 메타데이터에서 직접 소스 코드를 생성합니다.  
  
 **sqlmetal /server:myserver /database:northwind /namespace:nwind /code:nwind.cs /language:csharp**  
  
> [!NOTE]
> Northwind 샘플 데이터베이스에 **/pluralize** 옵션을 사용하는 경우에는 다음 동작에 유의하세요. SqlMetal이 테이블에 대해 행 형식 이름을 만들면 테이블 이름은 단수가 됩니다. 그리고 테이블에 대해 <xref:System.Data.Linq.DataContext> 속성을 만드는 경우에는 테이블 이름이 복수가 됩니다. 이와 동시에 Northwind 샘플 데이터베이스의 테이블은 미리 복수로 지정되어 있습니다. 그러므로 이러한 작업이 실제로 수행되는지 확인할 수는 없습니다. 일반적으로는 데이터베이스 테이블 이름을 단수로 지정하지만 .NET에서는 컬렉션 이름을 복수로 지정하는 경우도 많습니다.  
  
## <a name="see-also"></a>참고 항목

- [방법: Visual Basic 또는 C#에서 개체 모델 생성](../data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)
- [LINQ to SQL에서 코드 생성](../data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [외부 매핑](../data/adonet/sql/linq/external-mapping.md)
