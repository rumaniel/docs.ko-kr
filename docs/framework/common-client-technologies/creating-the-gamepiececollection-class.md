---
title: GamePieceCollection 클래스 만들기
ms.date: 03/30/2017
ms.assetid: e4b037ee-1201-4a55-b198-0d6532ed6f35
ms.openlocfilehash: 0a39ca479e9b370b027fcec4bcf76996e6191296
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50190582"
---
# <a name="creating-the-gamepiececollection-class"></a>GamePieceCollection 클래스 만들기
**GamePieceCollection** 클래스는 제네릭 목록 클래스에서 파생되고 여러 **GamePiece** 개체를 더 쉽게 관리하도록 메서드를 도입합니다.  
  
## <a name="creating-the-code"></a>코드 만들기  
 **GamePieceCollection** 클래스의 생성자는 개인 멤버 *capturedIndex*를 초기화합니다. 이 필드는 현재 마우스 캡처가 있는 게임 부분을 추적하는 데 사용됩니다.  
  
 [!code-csharp[ManipulationXNA#_GamePieceCollection_PrivateMembersAndConstructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_privatemembersandconstructor)]  
  
 **ProcessInertia** 및 **Draw** 메서드는 컬렉션에서 모든 게임 부분을 열거하고 각 **GamePiece** 개체에서 각 메서드를 호출하여 게임 [Game.Update](https://docs.microsoft.com/previous-versions/windows/xna/bb199616%28v%3dxnagamestudio.41%29) 및 [Game.Draw](https://docs.microsoft.com/previous-versions/windows/xna/bb196422%28v%3dxnagamestudio.41%29) 메서드에 필요한 코드를 간소화합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePieceCollection_ProcessInertiaAndDraw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_processinertiaanddraw)]  
  
 게임 업데이트 중에 **UpdateFromMouse** 메서드도 호출됩니다. 먼저 현재 캡처(있는 경우)가 계속 적용되는지 확인하여 마우스 캡처가 한 게임 부분에만 포함되도록 할 수 있습니다. 그렇다면 다른 부분에 캡처가 있는지 확인할 수 없습니다.  
  
 현재 캡처가 포함된 부분이 없으면 **UpdateFromMouse** 메서드가 마지막부터 처음까지 각 게임 부분을 열거하고 해당 부분에서 마우스 캡처를 보고하는지를 확인합니다. 그렇다면 해당 부분은 현재 캡처된 부분이 되고 추가적인 처리가 수행되지 않습니다. **UpdateFromMouse** 메서드는 컬렉션의 마지막 항목을 먼저 확인하므로 두 부분이 겹치면 더 높은 Z 순서를 가진 한 부분이 캡처를 획득합니다. Z 순서는 명시적이지 않고 변경할 수 없습니다. 단순히 게임 부분이 컬렉션에 추가된 순서대로 제어됩니다.  
  
 [!code-csharp[ManipulationXNA#_GamePieceCollection_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_updatefrommouse)]  
  
## <a name="see-also"></a>참고 항목  
 [조작 및 관성](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)  
 [XNA 응용 프로그램에서 조작 및 관성 사용](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)  
 [GamePiece 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)  
 [Game1 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)  
 [전체 코드 목록](../../../docs/framework/common-client-technologies/full-code-listings.md)
