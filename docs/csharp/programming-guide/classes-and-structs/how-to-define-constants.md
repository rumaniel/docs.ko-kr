---
title: '방법: C#에서 상수 정의'
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, constants
- constants [C#]
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
ms.openlocfilehash: ba5bc3d03dcaf5c8be94936a453a439670e8dc1f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924483"
---
# <a name="how-to-define-constants-in-c"></a>방법: C\#에서 상수 정의
상수는 해당 값이 컴파일 시간에 설정되며 변경할 수 없는 필드입니다. 상수를 사용하여 특수 값에 대해 숫자 리터럴(“매직 넘버”) 대신 의미 있는 이름을 제공할 수 있습니다.  
  
> [!NOTE]
> C#에서는 [#define](../../language-reference/preprocessor-directives/preprocessor-define.md) 전처리기 지시문을 사용하여 일반적으로 C와 C++에서 사용되는 방식으로 상수를 정의할 수 없습니다.  
  
 정수 형식(`int`, `byte` 등)의 상수 값을 정의하려면 열거 형식을 사용합니다. 자세한 내용은 [enum](../../language-reference/keywords/enum.md)을 참조하세요.  
  
 정수가 아닌 상수를 정의하는 한 가지 방법은 `Constants`라는 단일 정적 클래스로 그룹화하는 것입니다. 이 경우 다음 예제와 같이 상수에 대한 모든 참조 앞에 클래스 이름이 와야 합니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csProgGuideObjects#89](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#89)]  
  
 클래스 이름 한정자를 통해 사용자와 상수를 사용하는 다른 사용자가 상수이며 수정할 수 없음을 쉽게 파악할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [클래스 및 구조체](./index.md)
