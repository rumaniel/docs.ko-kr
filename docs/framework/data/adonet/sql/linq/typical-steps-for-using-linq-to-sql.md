---
title: LINQ to SQL 사용을 위한 일반 단계
ms.date: 03/30/2017
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
ms.openlocfilehash: c7964c821a838e027302cddce704d86cc6a34f66
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792337"
---
# <a name="typical-steps-for-using-linq-to-sql"></a>LINQ to SQL 사용을 위한 일반 단계
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 애플리케이션을 구현하려면 이 항목에 설명된 단계를 따릅니다. 대부분의 단계는 선택 사항이며 고유한 개체 모델을 기본 상태에서 사용할 수 있습니다.  
  
 매우 빠른 시작을 위해 개체 관계형 디자이너를 사용 하 여 개체 모델을 만들고 쿼리 코딩을 시작 합니다.  
  
## <a name="creating-the-object-model"></a>개체 모델 만들기  
 첫 번째 단계는 기존 관계형 데이터베이스의 메타데이터에서 개체 모델을 만드는 것입니다. 개체 모델은 개발자의 프로그래밍 언어에 따라 데이터베이스를 나타냅니다. 자세한 내용은 [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)을 참조 하세요.  
  
### <a name="1-select-a-tool-to-create-the-model"></a>1. 모델을 만들기 위한 도구를 선택합니다.  
 모델을 만들기 위한 세 가지 도구를 사용할 수 있습니다.  
  
- 개체 관계형 디자이너  
  
     이 디자이너는 기존 데이터베이스에서 개체 모델을 만들기 위한 풍부한 사용자 인터페이스를 제공합니다. 이 도구는 Visual Studio IDE의 일부 이며 중소 규모의 데이터베이스에 가장 적합 합니다.  
  
- SQLMetal 코드 생성 도구  
  
     이 명령줄 유틸리티는 O/R 디자이너와 약간 다른 옵션 집합을 제공 합니다. 대규모 데이터베이스 모델링에는 이 도구를 사용하는 것이 가장 좋습니다. 자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요.  
  
- 코드 편집기  
  
     Visual Studio code 편집기나 다른 편집기를 사용 하 여 사용자 고유의 코드를 작성할 수 있습니다. 기존 데이터베이스를 사용 하 고 O/R 디자이너나 SQLMetal 도구를 사용할 수 있는 경우 오류가 발생할 수 있는이 방법은 사용 하지 않는 것이 좋습니다. 단, 다른 도구를 사용하여 이미 생성한 코드를 구체화하거나 수정하려는 경우 코드 편집기가 유용할 수 있습니다. 자세한 내용은 [방법: 코드 편집기](how-to-customize-entity-classes-by-using-the-code-editor.md)를 사용 하 여 엔터티 클래스를 사용자 지정 합니다.  
  
### <a name="2-select-the-kind-of-code-you-want-to-generate"></a>2. 생성할 코드의 종류를 선택합니다.  
  
- 특성 C# 기반 매핑의 또는 Visual Basic 소스 코드 파일입니다.  
  
     그런 다음 Visual Studio 프로젝트에이 코드 파일을 포함 합니다. 자세한 내용은 [특성 기반 매핑](attribute-based-mapping.md)을 참조 하세요.  
  
- 외부 매핑을 위한 XML 파일  
  
     이 방법을 사용하면 애플리케이션 코드 외부에 매핑 메타데이터를 둘 수 있습니다. 자세한 내용은 [외부 매핑](external-mapping.md)을 참조 하세요.  
  
    > [!NOTE]
    > O/R 디자이너는 외부 매핑 파일의 생성을 지원 하지 않습니다. SQLMetal 도구를 사용하여 이 기능을 구현해야 합니다.  
  
- 최종 코드 파일을 생성하기 전에 수정할 수 있는 DBML 파일  
  
     이는 고급 기능에 해당합니다.  
  
### <a name="3-refine-the-code-file-to-reflect-the-needs-of-your-application"></a>3. 응용 프로그램의 요구 사항을 반영하도록 코드 파일을 구체화합니다.  
 이러한 목적을 위해 O/R 디자이너 또는 코드 편집기를 사용할 수 있습니다.  
  
## <a name="using-the-object-model"></a>개체 모델 사용  
 다음 그림에서는 2계층 시나리오에서 개발자와 데이터 간의 관계를 보여 줍니다. 다른 시나리오의 경우 [LINQ to SQL를 사용 하는 N 계층 및 원격 응용 프로그램](n-tier-and-remote-applications-with-linq-to-sql.md)을 참조 하세요.  
  
 ![Linq 개체 모델을 보여 주는 스크린샷](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 이제 개체 모델이 있으므로 해당 모델 내에서 정보 요청을 설명하고 데이터를 조작할 차례입니다. 데이터베이스의 행과 열이 아니라 개체 모델의 개체와 속성을 고려합니다. 데이터베이스를 직접 다루지는 않습니다.  
  
 설명한 쿼리를 실행하거나 조작한 데이터에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]를 호출하도록 `SubmitChanges()`에 지시할 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 데이터베이스 언어로 데이터베이스와 통신합니다.  
  
 만들어진 개체 모델을 사용하기 위한 일반적인 단계는 다음과 같습니다.  
  
### <a name="1-create-queries-to-retrieve-information-from-the-database"></a>1. 데이터베이스에서 정보를 검색하기 위해 쿼리를 만듭니다.  
 자세한 내용은 [쿼리 개념](query-concepts.md) 및 [쿼리 예제](query-examples.md)를 참조 하세요.  
  
### <a name="2-override-default-behaviors-for-insert-update-and-delete"></a>2. Insert, Update 및 Delete의 기본 동작을 재정의합니다.  
 이 단계는 선택 사항입니다. 자세한 내용은 [삽입, 업데이트 및 삭제 작업 사용자 지정](customizing-insert-update-and-delete-operations.md)을 참조 하세요.  
  
### <a name="3-set-appropriate-options-to-detect-and-report-concurrency-conflicts"></a>3. 동시성 충돌을 탐지 및 보고하기 위해 적절한 옵션을 설정합니다.  
 모델에서 동시성 충돌을 처리하기 위한 기본값을 유지하거나 원하는 목적에 맞게 변경할 수 있습니다. 자세한 내용은 [방법: 동시성 충돌](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) 에 대해 테스트할 멤버를 지정 하 [고 다음을 수행 합니다. 동시성 예외가 Throw](how-to-specify-when-concurrency-exceptions-are-thrown.md)되는 시기를 지정 합니다.  
  
### <a name="4-establish-an-inheritance-hierarchy"></a>4. 상속 계층 구조를 설정합니다.  
 이 단계는 선택 사항입니다. 자세한 내용은 [상속 지원](inheritance-support.md)을 참조 하세요.  
  
### <a name="5-provide-an-appropriate-user-interface"></a>5. 적절한 사용자 인터페이스를 제공합니다.  
 이 단계는 선택 사항이며 애플리케이션이 사용될 방법에 따라 달라집니다.  
  
### <a name="6-debug-and-test-your-application"></a>6. 응용 프로그램을 디버깅 및 테스트합니다.  
 자세한 내용은 [디버깅 지원](debugging-support.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [시작](getting-started.md)
- [개체 모델 만들기](creating-the-object-model.md)
- [저장 프로시저](stored-procedures.md)
