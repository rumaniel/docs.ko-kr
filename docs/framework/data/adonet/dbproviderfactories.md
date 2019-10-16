---
title: DbProviderFactories
ms.date: 03/30/2017
ms.assetid: 2a8e2640-3a49-42a1-a3a9-b43026907ae1
ms.openlocfilehash: e3ea9e3d083314f8df25f9edadbd1a18f1227293
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784096"
---
# <a name="dbproviderfactories"></a>DbProviderFactories
<xref:System.Data.Common> 네임스페이스에서는 특정 데이터 소스를 사용하기 위해 <xref:System.Data.Common.DbProviderFactory> 인스턴스를 만드는 데 필요한 클래스를 제공합니다. <xref:System.Data.Common.DbProviderFactory> 인스턴스를 만든 다음 이 인스턴스에 데이터 공급자에 대한 정보를 전달하면 `DbProviderFactory`에서 제공된 정보에 따라 반환할 강력한 형식의 올바른 연결 개체를 결정할 수 있습니다.  
  
 .NET Framework 버전 4부터는 <xref:System.Data.Odbc>, <xref:System.Data.OleDb>, <xref:System.Data.SqlClient> 및 <xref:System.Data.OracleClient> 등의 데이터 공급자는 더 이상 제공되지 않지만 사용자 지정 공급자는 계속 표시됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [팩터리 모델 개요](factory-model-overview.md)  
 팩터리 디자인 패턴 및 프로그래밍 인터페이스를 간략히 소개합니다.  
  
 [DbProviderFactory 가져오기](obtaining-a-dbproviderfactory.md)  
 설치된 데이터 공급자를 나열하고 <xref:System.Data.Common.DbConnection>에서 `DbProviderFactory`을 만드는 방법을 보여 줍니다.  
  
 [DbConnection, DbCommand 및 DbException](dbconnection-dbcommand-and-dbexception.md)  
 <xref:System.Data.Common.DbCommand> 및 <xref:System.Data.Common.DbDataReader>를 만들고 <xref:System.Data.Common.DbException>을 사용하여 데이터 오류를 처리하는 방법을 보여 줍니다.  
  
 [DbDataAdapter로 데이터 수정](modifying-data-with-a-dbdataadapter.md)  
 <xref:System.Data.Common.DbCommandBuilder>를 <xref:System.Data.Common.DbDataAdapter>와 함께 사용하여 데이터를 검색 및 수정하는 방법을 보여 줍니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [ADO.NET 개요](ado-net-overview.md)
