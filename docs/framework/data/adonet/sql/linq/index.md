---
title: LINQ to SQL
ms.date: 03/30/2017
ms.assetid: 73d13345-eece-471a-af40-4cc7a2f11655
ms.openlocfilehash: fbb2f8cf37bd05864dc93b8ebbd33466a9a2c55e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793088"
---
# <a name="linq-to-sql"></a>LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]는 관계형 데이터를 개체로 관리 하는 데 필요한 런타임 인프라를 제공 하는 .NET Framework 버전 3.5의 구성 요소입니다.  
  
> [!NOTE]
> 관계형 데이터는 테이블 간에 서로 관계된 공통 열이 있는 이차원 테이블(*관계* 또는 *플랫 파일*)의 컬렉션으로 표시됩니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 효율적으로 사용하려면 관계형 데이터베이스의 기본 원리에 대해 조금은 알고 있어야 합니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 관계형 데이터베이스의 데이터 모델은 개발자의 프로그래밍 언어로 표현되는 개체 모델에 매핑됩니다. 애플리케이션을 실행하면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 개체 모델의 SQL 언어 통합 쿼리를 변환하여 실행을 위해 데이터베이스로 전송합니다. 데이터베이스에서 결과를 반환하면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 해당 결과를 사용자의 프로그래밍 언어로 작업할 수 있는 개체로 다시 변환합니다.  
  
 Visual Studio를 사용 하는 개발자는 일반적으로의 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]많은 기능을 구현 하기 위한 사용자 인터페이스를 제공 하는 개체 관계형 디자이너을 사용 합니다.  
  
 이 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 릴리스에 포함된 설명서에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 애플리케이션을 빌드하는 데 필요한 기본 빌드 블록, 프로세스 및 기술에 대해 설명합니다. 또한 특정 문제에 대 한 Microsoft Docs 검색할 수 있으며, 전문가와 함께 보다 복잡 한 항목을 자세히 논의할 수 있는 [LINQ 포럼](https://go.microsoft.com/fwlink/?LinkId=76488)에 참여할 수 있습니다. 마지막으로 [LINQ to SQL: 관계형 데이터에 대 한 .net 언어 통합 쿼리](https://go.microsoft.com/fwlink/?LinkId=93205) 백서 세부 정보 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 기술에 대 한 자세한 내용은 C# Visual Basic 및 코드 예제를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [시작](getting-started.md)  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하는 방법에 대한 정보와 함께 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 대한 간략한 개요를 제공합니다.  
  
 [프로그래밍 가이드](programming-guide.md)  
 매핑, 쿼리, 업데이트, 디버깅 및 유사한 작업에 대한 단계를 제공합니다.  
  
 [참조](reference.md)  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 일부 측면에 대한 참조 정보를 제공합니다. 항목에는 SQL-CLR 형식 매핑, 표준 쿼리 연산자 변환 등이 포함됩니다.  
  
 [샘플](samples.md)  
 Visual Basic 및 C# 샘플에 대 한 링크를 제공 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [LINQ (통합 언어 쿼리)-C#](../../../../../csharp/programming-guide/concepts/linq/index.md)\
 의 C#LINQ 기술에 대 한 개요를 제공 합니다.
 
 [LINQ(Language-Integrated Query) - Visual Basic](../../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 Visual Basic의 LINQ 기술에 대 한 개요를 제공 합니다.
  
 [LINQ](../../../../../visual-basic/programming-guide/language-features/linq/index.md)  
 Visual Basic [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 사용자를 위한 기술에 대해 설명 합니다.  
  
 [LINQ 및 ADO.NET](../../linq-and-ado-net.md)  
 ADO.NET 포털에 대 한 링크입니다.  
  
 [LINQ to SQL 연습](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bb386295(v=vs.90))  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 대한 연습을 제공합니다.  
  
 [샘플 데이터베이스 다운로드](downloading-sample-databases.md)  
 설명서에 사용되는 샘플 데이터베이스를 다운로드하는 방법에 대해 설명합니다.  
  
 [LinqDataSource 웹 서버 컨트롤 개요](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))  
 <xref:System.Web.UI.WebControls.LinqDataSource> 컨트롤이 ASP.NET 데이터 소스 제어 아키텍처를 통해 웹 개발자에 게 노출 [!INCLUDE[vbteclinqext](../../../../../../includes/vbteclinqext-md.md)] 하는 방법을 설명 합니다.
