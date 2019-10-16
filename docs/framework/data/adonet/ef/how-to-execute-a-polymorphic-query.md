---
title: '방법: 다형성 쿼리 실행'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2f05da1e-845b-4f14-83e4-c6353a850553
ms.openlocfilehash: 49e0a6b44af0729959fabf6278cc6d8ecf37a16b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251509"
---
# <a name="how-to-execute-a-polymorphic-query"></a>방법: 다형성 쿼리 실행

이 항목에서는 [OFTYPE](./language-reference/oftype-entity-sql.md) 연산자를 사용 하 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 여 다형 쿼리를 실행 하는 방법을 보여 줍니다.

### <a name="to-run-the-code-in-this-example"></a>이 예제의 코드를 실행하려면

1. 프로젝트에 [School 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) 을 추가 하 고 Entity Framework를 사용 하도록 프로젝트를 구성 합니다. 자세한 내용은 [방법: 엔터티 데이터 모델 마법사](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))를 사용 합니다.

2. 애플리케이션의 코드 페이지에서 다음 `using` 문(Visual Basic에서는 `Imports`)을 추가합니다.

    [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
    [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]

3. [연습의 단계를 수행 하 여 계층당 하나의 테이블 상속을 갖도록 개념적 모델을 수정 합니다. 매핑 상속-계층당](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716683(v=vs.100))하나의 테이블

## <a name="example"></a>예제

다음 예제에서는 OFTYPE 연산자를 사용하여 `OnsiteCourses` 컬렉션의 `Courses`만으로 구성된 컬렉션을 가져와서 표시합니다.

[!code-csharp[DP EntityServices Concepts#PolymorphicQuery](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#polymorphicquery)]
[!code-vb[DP EntityServices Concepts#PolymorphicQuery](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#polymorphicquery)]

## <a name="see-also"></a>참고자료

- [Entity Framework용 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)
- [Entity SQL 언어](./language-reference/entity-sql-language.md)
