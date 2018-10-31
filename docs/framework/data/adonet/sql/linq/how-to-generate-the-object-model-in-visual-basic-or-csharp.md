---
title: '방법: Visual Basic 또는 C#에서 개체 모델 생성'
ms.date: 03/30/2017
ms.assetid: a0c73b33-5650-420c-b9dc-f49310c201ee
ms.openlocfilehash: 21266ca2d1230a1afc903734d1b4c53b259e50e1
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200929"
---
# <a name="how-to-generate-the-object-model-in-visual-basic-or-c"></a>방법: Visual Basic 또는 C#에서 개체 모델 생성 #
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 사용자 프로그래밍 언어의 개체 모델은 관계형 데이터베이스에 매핑됩니다. 두 가지 도구는 자동으로 생성 되는 Visual Basic에 사용할 수 있는 또는 C# 기존 데이터베이스의 메타 데이터에서 모델입니다.  
  
-   Visual Studio를 사용 하는 경우 사용할 수 있습니다는 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 개체 모델을 생성 합니다. [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 개체 모델을 생성하는 데 도움이 되는 다양한 사용자 인터페이스를 제공합니다. 자세한 내용은 참조 하십시오 [Linq to SQL 도구 Visual Studio에서](https://docs.microsoft.com/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)합니다.
  
-   SQLMetal 명령줄 도구. 자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요.  
  
    > [!NOTE]
    >  기존 데이터베이스가 없는 경우 개체 모델에서 데이터베이스를 만들려면 코드 편집기와 <xref:System.Data.Linq.DataContext.CreateDatabase%2A>를 사용하여 개체 모델을 만들 수 있습니다. 자세한 내용은 [방법: 동적으로 데이터베이스를 만들](../../../../../../docs/framework/data/adonet/sql/linq/how-to-dynamically-create-a-database.md)합니다.  
  
 에 대 한 설명서는 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] Visual Basic을 생성 하는 방법의 예제를 제공 또는 C# 를 사용 하 여 개체 모델을 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]합니다. 다음 정보에서는 SQLMetal 명령줄 도구를 사용하는 방법에 대한 예제를 제공합니다. 자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제의 SQLMetal 명령줄 Northwind 샘플 데이터베이스의 특성 기반 개체 모델과 같은 Visual Basic 코드를 생성 합니다. 또한 저장 프로시저와 함수가 렌더링됩니다.  
  
```  
sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions  
```  
  
## <a name="example"></a>예제  
 다음 예제의 SQLMetal 명령줄에서는 Northwind 샘플 데이터베이스의 특성 기반 개체 모델과 같은 C# 코드를 생성합니다. 또한 저장 프로시저와 함수가 렌더링되며 테이블 이름은 자동으로 복수화됩니다.  
  
```  
sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize  
```  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 가이드](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)  
 [LINQ to SQL 개체 모델](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)  
 [연습으로 학습](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)  
 [방법: 코드 편집기를 사용하여 엔터티 클래스 사용자 지정](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)  
 [특성 기반 매핑](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md)  
 [SqlMetal.exe(코드 생성 도구)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)  
 [외부 매핑](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md)  
 [샘플 데이터베이스 다운로드](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)  
 [개체 모델 만들기](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)
