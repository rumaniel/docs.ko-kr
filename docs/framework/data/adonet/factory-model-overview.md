---
title: 팩터리 모델 개요
ms.date: 03/30/2017
ms.assetid: b5dc81c4-7554-44b9-b513-769bd61e2e7b
ms.openlocfilehash: 7d50ddd3b02b66a5b2be41eaba5cf9a497b5f1b3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795079"
---
# <a name="factory-model-overview"></a>팩터리 모델 개요
ADO.NET 2.0에서는 <xref:System.Data.Common> 네임스페이스에 새로운 기본 클래스가 추가되었습니다. 이러한 기본 클래스는 추상적이기 때문에 직접 인스턴스화할 수 없습니다. 여기에는 <xref:System.Data.Common.DbConnection>, <xref:System.Data.Common.DbCommand> 및 <xref:System.Data.Common.DbDataAdapter>가 포함되며 세 클래스 모두 <xref:System.Data.SqlClient> 및 <xref:System.Data.OleDb>와 같은 .NET Framework 데이터 공급자에서 공유됩니다. 기본 클래스를 사용하면 새 인터페이스를 만들 필요 없이 .NET Framework 데이터 공급자에 기능을 간편하게 추가할 수 있습니다.  
  
 또한 ADO.NET 2.0에서는 추상 기본 클래스가 도입되어 개발자가 특정 데이터 공급자에 한정되지 않는 제네릭 데이터 액세스 코드를 작성할 수 있습니다.  
  
## <a name="the-factory-design-pattern"></a>팩터리 디자인 패턴  
 공급자에 독립적인 코드를 작성하기 위한 프로그래밍 모델은 단일 API를 사용하여 여러 공급자의 데이터베이스에 액세스하는 "팩터리" 디자인 패턴을 기본적으로 사용합니다. 이 패턴은 이름에서 알 수 있듯이 실제 팩터리와 마찬가지로 다른 개체를 만들기 위해서만 특수 개체를 사용해야 합니다. 팩터리 디자인 패턴에 대 한 자세한 설명은 [ASP.NET 2.0 및 ADO.NET 2.0에서 일반 데이터 액세스 코드 작성](https://go.microsoft.com/fwlink/?LinkId=55915)을 참조 하세요.
  
 ADO.NET 2.0부터 <xref:System.Data.Common.DbProviderFactories> 클래스는 `static` 인스턴스를 만드는 `Shared`(Visual Basic의 경우 <xref:System.Data.Common.DbProviderFactory>) 메서드를 제공합니다. 그러면 이 인스턴스는 런타임에 제공되는 공급자 정보와 연결 문자열을 기반으로 강력한 형식의 개체를 반환합니다.  
  
## <a name="see-also"></a>참고자료

- [DbProviderFactory 가져오기](obtaining-a-dbproviderfactory.md)
- [DbConnection, DbCommand 및 DbException](dbconnection-dbcommand-and-dbexception.md)
- [DbDataAdapter로 데이터 수정](modifying-data-with-a-dbdataadapter.md)
- [ADO.NET 개요](ado-net-overview.md)
