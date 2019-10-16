---
title: 기본 데이터 형식
ms.date: 03/30/2017
ms.assetid: eca2c472-9548-4800-bd31-5d8d9f11752b
ms.openlocfilehash: e85adb928925bf161e6e2d6ef935a20606f8eb32
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248033"
---
# <a name="basic-data-types"></a>기본 데이터 형식
LINQ to SQL 쿼리는 Microsoft SQL Server에서 실행되기 전에 Transact-SQL로 변환됩니다. 따라서 LINQ to SQL에서는 SQL Server에서 기본 데이터 형식에 대해 지원하는 기본 제공 함수 대부분을 지원합니다.  
  
## <a name="casting"></a>캐스팅  
 SQL Server 내에 비슷한 유효한 변환이 있는 경우 암시적 또는 명시적 캐스팅을 사용하여 소스 CLR 형식에서 대상 CLR 형식으로 변환할 수 있습니다. CLR 캐스팅에 대 한 자세한 내용은 [CType 함수](../../../../../visual-basic/language-reference/functions/ctype-function.md) (Visual Basic) 및 [형식 테스트 및 캐스트 연산자](../../../../../csharp/language-reference/operators/type-testing-and-cast.md)를 참조 하세요. 변환 후 캐스팅은 CLR 식에서 수행된 작업 동작을 변경하여 기본적으로 대상 형식에 매핑되는 다른 CLR 식의 동작과 일치시킵니다. 캐스팅은 또한 상속 매핑의 컨텍스트에서 변환 가능합니다. 개체는 보다 구체적인 엔터티 하위 형식에 캐스팅되어 하위 형식의 특정 데이터에 액세스할 수 있습니다.  
  
## <a name="equality-operators"></a>같음 연산자  
 LINQ to SQL에서는 LINQ to SQL 쿼리 내의 기본 데이터 형식에 다음과 같은 같음 연산자를 지원합니다.  
  
- 같음 및 같지 않음 연산자: 숫자, <xref:System.Boolean>, <xref:System.DateTime>및 <xref:System.TimeSpan> 형식에 대해 같음 연산자와 같지 않음 연산자를 사용할 수 있습니다. Visual Basic 연산자 `=` 및 `<>`에 대 한 자세한 내용은 [비교 연산자](../../../../../visual-basic/language-reference/operators/comparison-operators.md)를 참조 하세요. 비교 연산자 C# `==` 및 `!=`에 대 한 자세한 내용은 [같음 연산자](../../../../../csharp/language-reference/operators/equality-operators.md)를 참조 하세요.
  
- Is 연산자: 상속 `IS` 매핑을 사용 하는 경우 연산자에는 지원 되는 변환이 있습니다. 개체가 특정 엔터티 형식인지 여부를 확인하기 위해 판별자 열을 직접 테스트하는 대신에 사용되어 판별자 열에 대한 확인으로 변환됩니다. Visual Basic와 C# is 연산자에 대 한 자세한 내용은 [is 연산자](../../../../../visual-basic/language-reference/operators/is-operator.md) 및 [is를](../../../../../csharp/language-reference/operators/type-testing-and-cast.md#is-operator)참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [SQL-CLR 형식 매핑](sql-clr-type-mapping.md)
- [데이터 형식 및 함수](data-types-and-functions.md)
