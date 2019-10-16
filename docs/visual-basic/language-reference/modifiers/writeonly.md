---
title: WriteOnly(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- WriteOnly
- vb.WriteOnly
helpviewer_keywords:
- write-only properties
- WriteOnly keyword [Visual Basic]
- sensitive data, protecting
- properties [Visual Basic], write-only
- sensitive data
ms.assetid: 488d2899-b09f-4cee-92f0-6f9f9fc4f944
ms.openlocfilehash: 43507ac8e9b5843e8fa9496737a3d77b3a425a7f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963764"
---
# <a name="writeonly-visual-basic"></a>WriteOnly(Visual Basic)
속성을 쓸 수 있지만 읽을 수 없도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="rules"></a>규칙  
 **선언 컨텍스트입니다.** `WriteOnly`는 모듈 수준에서만 사용할 수 있습니다. 즉, `WriteOnly` 속성에 대 한 선언 컨텍스트는 클래스, 구조체 또는 모듈 이어야 하며 소스 파일, 네임 스페이스 또는 프로시저일 수 없습니다.  
  
 속성 `WriteOnly`은 선언할 수 있지만 변수는 선언할 수 없습니다.  
  
## <a name="when-to-use-writeonly"></a>WriteOnly를 사용 하는 경우  
 소비 하는 코드에서 값을 설정할 수 있지만 해당 값을 검색 하지 않으려는 경우가 있습니다. 예를 들어 소셜 등록 번호 또는 암호와 같은 중요 한 데이터는 해당 데이터를 설정 하지 않은 구성 요소에의 한 액세스 로부터 보호 해야 합니다. 이 경우 `WriteOnly` 속성을 사용 하 여 값을 설정할 수 있습니다.  
  
> [!IMPORTANT]
> `WriteOnly` 속성을 정의 하 고 사용 하는 경우 다음과 같은 추가 보호 조치를 고려 하십시오.  
  
- **덮어쓰지.** 속성이 클래스의 멤버인 경우 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)에 대 한 기본값을 지정할 수 있으며, `Overridable` 또는 `MustOverride`로 선언 하지 않습니다. 이렇게 하면 파생 클래스가 재정의를 통해 원치 않는 액세스를 수행할 수 없습니다.  
  
- **액세스 수준입니다.** 하나 이상의 변수에 속성의 중요 한 데이터를 저장 하는 경우 다른 코드에서 액세스할 수 없도록 [Private](../../../visual-basic/language-reference/modifiers/private.md) 을 선언 합니다.  
  
- **암호화.** 모든 중요 한 데이터를 일반 텍스트가 아닌 암호화 된 형식으로 저장 합니다. 악의적인 코드가 해당 메모리 영역에 대 한 액세스 권한을 얻으면 데이터를 사용 하는 것이 더 어려워집니다. 암호화는 중요 한 데이터를 직렬화 해야 하는 경우에도 유용 합니다.  
  
- **다시 설정.** 속성을 정의 하는 클래스, 구조체 또는 모듈을 종료 하는 경우 중요 한 데이터를 기본값으로 다시 설정 하거나 다른 의미 없는 값으로 다시 설정 합니다. 이는 일반 액세스를 위해 메모리 영역을 해제할 때 추가 보호 기능을 제공 합니다.  
  
- **지.** 중요 한 데이터 (예: 디스크를 사용 하지 않는 경우)를 유지 하지 마세요. 또한 중요 한 데이터를 클립보드에 쓰지 않습니다.  
  
 이 `WriteOnly` 컨텍스트에서는 한정자를 사용할 수 있습니다.  
  
 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## <a name="see-also"></a>참고자료

- [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)
- [전용](../../../visual-basic/language-reference/modifiers/private.md)
- [C++ 키워드](../../../visual-basic/language-reference/keywords/index.md)
