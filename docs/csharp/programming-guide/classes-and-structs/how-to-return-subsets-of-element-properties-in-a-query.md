---
title: '방법: 쿼리에서 요소 속성의 하위 집합 반환 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- anonymous types [C#], for subsets of element properties
ms.assetid: fabdf349-f443-4e3f-8368-6c471be1dd7b
ms.openlocfilehash: 2c9fea2189819058187020c2e67b8826659fbed4
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205438"
---
# <a name="how-to-return-subsets-of-element-properties-in-a-query-c-programming-guide"></a>방법: 쿼리에서 요소 속성의 하위 집합 반환(C# 프로그래밍 가이드)
이러한 조건이 둘 다 적용되는 경우 쿼리 식에서 무명 형식을 사용합니다.  
  
- 각 소스 요소의 속성 중 일부만 반환하려고 합니다.  
  
- 쿼리가 실행되는 메서드의 범위 외부에 쿼리 결과를 저장할 필요는 없습니다.  
  
 각 소스 요소에서 하나의 속성 또는 필드만 반환하려는 경우 `select` 절에 점 연산자만 사용할 수 있습니다. 예를 들어 각 `student`의 `ID`만 반환하려면 `select` 절을 다음과 같이 작성합니다.  
  
```csharp  
select student.ID;  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 무명 형식을 사용하여 지정된 조건과 일치하는 각 소스 요소의 속성 하위 집합만 반환하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideLINQ#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#31)]  
  
 이름이 지정되지 않은 경우 무명 형식은 소스 요소의 이름을 해당 속성에 사용합니다. 무명 형식의 속성에 새 이름을 지정하려면 `select` 문을 다음과 같이 작성합니다.  
  
```csharp  
select new { First = student.FirstName, Last = student.LastName };  
```  
  
 앞의 예제에서 이 작업을 수행하는 경우 `Console.WriteLine` 문도 변경되어야 합니다.  
  
```csharp  
Console.WriteLine(student.First + " " + student.Last);  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
이 코드를 실행하려면 System.Linq에 대한 `using` 지시문을 통해 클래스를 복사하여 C# 콘솔 애플리케이션 프로젝트에 붙여넣습니다.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [익명 형식](./anonymous-types.md)
- [LINQ 쿼리 식](../linq-query-expressions/index.md)
