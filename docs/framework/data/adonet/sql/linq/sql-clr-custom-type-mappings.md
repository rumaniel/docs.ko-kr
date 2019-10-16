---
title: SQL-CLR 사용자 지정 대/소문자 매핑
ms.date: 03/30/2017
ms.assetid: d916c7fb-4b56-4214-acbe-5e23365047b2
ms.openlocfilehash: 8901998533ec14e733ea072dd1a69b465e596328
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781077"
---
# <a name="sql-clr-custom-type-mappings"></a>SQL-CLR 사용자 지정 대/소문자 매핑
SQL Server와 CLR(공용 언어 런타임) 간의 형식 매핑은 SQLMetal 명령줄 도구 또는 개체 관계형 디자이너(O/R 디자이너)를 사용할 때 자동으로 지정됩니다.  
  
 사용자 지정 된 매핑이 수행 되지 않는 경우 이러한 도구는 [SQL CLR 형식 매핑](sql-clr-type-mapping.md)에 설명 된 대로 기본 형식 매핑을 할당 합니다. 기본 매핑과 다른 형식 매핑을 사용하려는 경우에는 해당 형식 매핑을 사용자 지정해야 합니다.  
  
 형식 매핑을 사용자 지정할 때는 중간 DBML 파일을 변경하는 것이 좋습니다. 그런 다음 SQLMetal 또는 O/R 디자이너에서 코드 및 매핑 파일을 만들 때 사용자 지정된 DBML 파일을 사용해야 합니다.  
  
 코드 및 매핑 파일에서 <xref:System.Data.Linq.DataContext> 개체를 인스턴스화하면 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드는 지정된 형식 매핑을 기반으로 데이터베이스를 생성합니다. 매핑에 CLR `type` 특성이 지정되지 않은 경우에는 기본 형식 매핑이 사용됩니다.  
  
## <a name="customization-with-sqlmetal-or-or-designer"></a>SQLMetal 또는 O/R 디자이너 사용자 지정  
 SQLMetal 및 O/R 디자이너를 사용할 때 코드 파일 내부 또는 외부의 형식 매핑 정보를 포함하는 개체 모델을 자동으로 만들 수 있습니다. 이러한 파일은 SQLMetal 또는 O/R 디자이너에서 덮어쓰므로 매핑을 다시 만들 때마다 DBML 파일을 사용자 지정하여 사용자 형식 매핑을 지정하는 것이 좋습니다.  
  
 SQLMetal 또는 O/R 디자이너를 사용하여 형식 매핑을 사용자 지정하려면 먼저 DBML 파일을 생성합니다. 그런 다음 코드 파일 또는 매핑 파일을 생성하기 전에 DBML 파일을 수정하여 원하는 형식 매핑을 확인합니다. SQLMetal을 사용하는 경우 DBML 파일에서 `Type` 및 `DbType` 특성을 직접 변경하여 형식 매핑을 사용자 지정해야 합니다. O/R 디자이너를 사용하는 경우에는 디자이너 내부에서 변경할 수 있습니다. O/R 디자이너를 사용 하는 방법에 대 한 자세한 내용은 [LINQ to SQL Tools In Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)를 참조 하세요.  
  
> [!NOTE]
> 일부 형식 매핑의 경우 데이터베이스 관련 변환 과정에서 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다. 사용자 지정을 수행 하기 전에 [SQL-CLR 형식 매핑의](sql-clr-type-mapping.md) 형식 매핑 런타임 동작 매트릭스를 신중 하 게 검토 합니다.  
  
 SQLMetal 또는 O/R 디자이너에서 형식 매핑 사용자 지정을 인식하게 하려면 코드 파일 또는 외부 매핑 파일을 생성할 때 사용자 지정 DBML 파일에 대한 경로가 이러한 도구에 제공되어야 합니다. 형식 매핑 사용자 지정을 위해 반드시 필요한 것은 아니지만, 항상 형식 매핑 정보를 코드 파일과 분리하고 추가 외부 형식 매핑 파일을 생성하는 것이 좋습니다. 이렇게 하면 유연성이 개선되어 코드 파일 재컴파일의 필요성이 줄어듭니다.  
  
## <a name="incorporating-database-changes"></a>데이터베이스 변경 내용 통합  
 데이터베이스를 변경할 경우 이러한 변경 내용이 반영되도록 DBML 파일을 업데이트해야 합니다. DBML 파일을 업데이트하는 한 가지 방법은 자동으로 새 DBML 파일이 만들어지면 형식 매핑 사용자 지정을 다시 수행하는 것입니다. 또는 새 DBML 파일과 사용자 지정된 DBML 파일 간의 차이점을 비교하여 데이터베이스 변경 내용이 반영되도록 사용자 지정 DBML 파일을 수동으로 업데이트할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [SQL-CLR 형식 매핑](sql-clr-type-mapping.md)
- [LINQ to SQL에서 코드 생성](code-generation-in-linq-to-sql.md)
