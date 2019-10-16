---
title: '방법: 쿼리에서 모델 정의 함수 호출'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6c804e4d-f348-4afd-9f63-d3f0f24bc6a9
ms.openlocfilehash: 33f26896dd0d4ff08beb4a011fa6bd468cba7207
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250750"
---
# <a name="how-to-call-model-defined-functions-in-queries"></a>방법: 쿼리에서 모델 정의 함수 호출
이 항목에서는 LINQ to Entities 쿼리 내에서 개념적 모델에 정의 된 함수를 호출 하는 방법에 대해 설명 합니다.  
  
 다음 절차에서는 LINQ to Entities 쿼리 내에서 모델 정의 함수를 호출 하는 방법에 대 한 개략적인 개요를 제공 합니다. 절차 다음에 나오는 예제에서는 절차의 단계를 보다 자세히 설명합니다. 이 절차에서는 사용자가 개념적 모델에서 함수를 정의했다고 가정합니다. 자세한 내용은 [방법: 개념적 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))에서 사용자 지정 함수를 정의 합니다.  
  
### <a name="to-call-a-function-defined-in-the-conceptual-model"></a>개념적 모델에 정의된 함수를 호출하려면  
  
1. 개념적 모델에 정의된 함수로 매핑되는 CLR(공용 언어 런타임) 메서드를 애플리케이션에 추가합니다. 메서드를 매핑하려면 메서드에 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>를 적용해야 합니다. 특성의 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 및 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 매개 변수는 각각 개념적 모델의 네임스페이스 이름과 함수 이름입니다. LINQ에서 함수 이름을 확인할 때는 대/소문자가 구분됩니다.  
  
2. LINQ to Entities 쿼리에서 함수를 호출합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 LINQ to Entities 쿼리 내에서 개념적 모델에 정의 된 함수를 호출 하는 방법을 보여 줍니다. 이 예제에서는 School 모델을 사용합니다. School 모델에 대 한 자세한 내용은 [School 샘플 데이터베이스 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100)) 및 [School .edmx 파일 생성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399739(v=vs.100))을 참조 하세요.  
  
 다음의 개념적 모델 함수는 강사가 고용된 이후 경과된 년 수를 반환합니다. 개념적 모델 [에 함수를 추가 하는 방법에 대 한 자세한 내용은 방법: 개념적 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))에서 사용자 지정 함수를 정의 합니다.  
  
 [!code-xml[DP ConceptualModelFunctions#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp conceptualmodelfunctions/xml/school.edmx#1)]
  
## <a name="example"></a>예제  
 다음에는 애플리케이션에 아래 메서드를 추가하고 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>를 사용하여 이 메서드를 개념적 모델 함수에 매핑합니다.  
  
 [!code-csharp[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#2)]
 [!code-vb[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#2)]  
  
## <a name="example"></a>예제  
 이제 LINQ to Entities 쿼리 내에서 개념적 모델 함수를 호출할 수 있습니다. 다음 코드에서는 고용된 지 10년이 넘은 모든 강사를 표시하는 메서드를 호출합니다.  
  
 [!code-csharp[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#3)]
 [!code-vb[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#3)]  
  
## <a name="see-also"></a>참고자료

- [.edmx 파일 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [LINQ to Entities에서 쿼리](queries-in-linq-to-entities.md)
- [LINQ to Entities 쿼리에서 함수 호출](calling-functions-in-linq-to-entities-queries.md)
- [방법: 모델 정의 함수를 개체 메서드로 호출](how-to-call-model-defined-functions-as-object-methods.md)
