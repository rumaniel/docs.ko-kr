---
title: ASP.NET을 사용하는 LINQ to SQL N 계층
ms.date: 03/30/2017
ms.assetid: f6cc863a-d6a6-4281-ba8b-197c01cf6c6f
ms.openlocfilehash: 1770d84053b57e05d1a4e41919a3eb4122dc73a3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793027"
---
# <a name="linq-to-sql-n-tier-with-aspnet"></a>ASP.NET을 사용하는 LINQ to SQL N 계층
을 사용 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]하는 ASP.NET 응용 프로그램에서 <xref:System.Web.UI.WebControls.LinqDataSource> 웹 서버 컨트롤을 사용 합니다. 이 컨트롤은 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 대해 쿼리하는 데 필요한 대부분의 논리를 처리하고, 데이터를 브라우저에 전달하고 검색하며, 최종적으로 데이터베이스를 업데이트할 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.DataContext> 에 데이터를 제출합니다. 컨트롤을 태그에 구성하기만 하면 컨트롤이 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 과 브라우저 사이의 모든 데이터 전송을 처리합니다. 컨트롤은 프레젠테이션 계층과의 상호 작용을 처리 하 고 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 데이터 계층과의 통신을 처리 하기 때문에 ASP.NET 다계층 응용 프로그램의 주요 초점은 사용자 지정 비즈니스 논리를 작성 하는 것입니다.  
  
 에 대 한 `LINQDataSource`자세한 내용은 [LinqDataSource 웹 서버 컨트롤 개요](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL을 사용한 N 계층 및 원격 응용 프로그램](n-tier-and-remote-applications-with-linq-to-sql.md)
