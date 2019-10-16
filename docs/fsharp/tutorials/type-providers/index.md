---
title: 형식 공급자
description: 에 대해 알아봅니다 어떻게는 F# 형식 공급자는 형식, 속성 및 프로그램에서 사용할 메서드를 제공 하는 구성 요소입니다.
ms.date: 04/02/2018
ms.openlocfilehash: 5fa9de229caa2ec3ba4a248ca5cd1c8aa5adb230
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645161"
---
# <a name="type-providers"></a>형식 공급자

F# 형식 공급자는 사용자 프로그램에서 사용할 형식, 속성 및 메서드를 제공하는 구성 요소입니다. 형식 공급자는 생성 **제공 된 형식**에서 생성 되는 F# 컴파일러 되며 외부 데이터 원본에 따라 합니다.

예를 들어는 F# SQL에 대 한 형식 공급자는 관계형 데이터베이스에서 테이블 및 열을 나타내는 형식을 생성할 수 있습니다. 이것이 사실 합니다 [SQLProvider](https://fsprojects.github.io/SQLProvider/) 형식 공급자가 있습니다.

제공 형식 입력된 매개 변수 형식 공급자에 따라 달라 집니다. 이러한 입력 (예: JSON 스키마 파일), 샘플 데이터 원본 수는 외부 서비스 또는 데이터 원본에 연결 문자열을 직접 가리키는 URL입니다. 형식 공급자 형식의 그룹을 주문형으로;만 확장을 보장할 수도 있습니다. 즉, 프로그램에서 형식을 실제로 참조 하는 경우 확장 됩니다. 따라서 강력한 형식으로 온라인 데이터 시장과 같은 대규모 정보 공간의 직접적인 주문형 통합을 허용합니다.

## <a name="generative-and-erased-type-providers"></a>인기 및 지워진 형식 공급자

형식 공급자는 두 가지 형태로 제공 합니다. 인기 및 지워진 합니다.

인기 형식 공급자는 생성 될 때 어셈블리에.NET 형식으로 작성할 수 있는 형식을 생성 합니다. 이 옵션을 사용 하면 다른 어셈블리의 코드에서 사용할 수 있도록 합니다. 이 형식화 된 데이터 원본 표현을 일반적으로 이어야 한다는 것을.NET 형식으로 나타내는 것을 의미 합니다.

지우기 형식 공급자는 어셈블리 또는 프로젝트에서 생성 됩니다만 사용할 수 있는 형식을 생성 합니다. 유형은 임시입니다. 즉, 어셈블리에 기록 되지 않으며 다른 어셈블리의 코드에서 사용할 수 없습니다. 포함할 수 있습니다 *지연* 멤버를 잠재적으로 무한 정보 공간에서 사용 하 여 제공 된 형식에 있습니다. 소수의 대규모 및 상호 연결 된 데이터 소스를 사용 하는 데 유용 합니다.

## <a name="commonly-used-type-providers"></a>일반적으로 사용 되는 형식 공급자

다양 한 용도 대 한 형식 공급자를 포함 하는 다음 널리 사용 되는 라이브러리:

- [FSharp.Data](https://fsharp.github.io/FSharp.Data/) JSON, XML, CSV 및 HTML 문서 형식 및 리소스에 대 한 형식 공급자를 포함 합니다.
- [SQLProvider](https://fsprojects.github.io/SQLProvider/) 개체 매핑을 통해 관계 데이터베이스에 대 한 강력한 형식의 액세스를 제공 하 고 F# 이러한 데이터 원본에 대 한 LINQ 쿼리 합니다.
- [FSharp.Data.SqlClient](https://fsprojects.github.io/FSharp.Data.SqlClient/) 컴파일 시간에 대 한 형식 공급자 집합을 확인 했습니다 T-SQL 포함 F#합니다.
- [Azure Storage 형식 공급자](https://fsprojects.github.io/AzureStorageTypeProvider/) Azure Blob, 테이블 및 큐, 프로그램 전체에서 문자열로 리소스 이름을 지정 하지 않고도 이러한 리소스에 액세스할 수 있도록 하기 위한 형식을 제공 합니다.
- [FSharp.Data.GraphQL](https://fsprojects.github.io/FSharp.Data.GraphQL/index.html) 포함 된 **GraphQLProvider**, URL에서 지정한 GraphQL server를 기반으로 하는 형식을 제공 하는 합니다.

필요한 경우 다음을 할 수 있습니다 [사용자 고유의 사용자 지정 형식 공급자를 만들](creating-a-type-provider.md), 또는 다른 사용자가 생성 된 형식 공급자를 참조 합니다. 예를 들어 조직에 규모가 크고 점점 더 수가 증가하는 명명된 데이터 집합(각각 자체적으로 안정적인 데이터 스키마 포함)을 제공하는 데이터 서비스가 있다고 가정합니다. 강력한 방식으로 스키마를 읽고 프로그래머에 설정된 사용할 수 있는 최신 데이터 집합을 제공하는 형식 공급자를 만들도록 선택할 수 있습니다.

## <a name="see-also"></a>참고자료

- [자습서: 형식 공급자 만들기](creating-a-type-provider.md)
- [F# 언어 참조](../../language-reference/index.md)
- [Visual F#](../../index.md)
