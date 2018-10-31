---
title: Game1 클래스 만들기
ms.date: 03/30/2017
ms.assetid: 47932ce3-2ba5-476f-a26b-3ddfd5226f27
ms.openlocfilehash: c96fa846d11947af03faec26dd6de99e0aeec052
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49452799"
---
# <a name="creating-the-game1-class"></a>Game1 클래스 만들기
모든 Microsoft XNA 프로젝트와 마찬가지로 Game1 클래스는 XNA 게임에 대한 기본 그래픽 장치 초기화, 게임 논리 및 렌더링 코드를 제공하는 [Microsoft.Xna.Framework.Game](https://docs.microsoft.com/previous-versions/windows/xna/bb197040%28v%3dxnagamestudio.41%29) 클래스에서 파생됩니다. 대부분의 작업이 GamePiece 및 GamePieceCollection 클래스에서 수행되기 때문에 Game1 클래스는 비교적 간단합니다.  
  
## <a name="creating-the-code"></a>코드 만들기  
 클래스의 private 멤버는 게임 피스를 저장할 **GamePieceCollection** 개체, [GraphicsDeviceManager](https://docs.microsoft.com/previous-versions/windows/xna/bb197317%28v%3dxnagamestudio.41%29) 개체 및 게임 피스 렌더링에 사용되는 [SpriteBatch](https://docs.microsoft.com/previous-versions/windows/xna/bb199034%28v%3dxnagamestudio.41%29) 개체로 구성됩니다.  
  
 [!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]  
  
 게임 초기화 중에 이러한 개체가 인스턴스화됩니다.  
  
 [!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]  
  
 [LoadContent](https://docs.microsoft.com/previous-versions/windows/xna/bb975766%28v%3dxnagamestudio.41%29) 메서드를 호출하면 게임 피스가 생성되고 **GamePieceCollection** 개체에 할당됩니다. 두 가지 유형의 게임 피스가 있습니다. 좀더 작은 피스와 좀더 큰 피스가 있으므로 피스에 대한 배율은 약간 변경됩니다.  
  
 [!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]  
  
 게임을 실행하는 동안 [Update](https://docs.microsoft.com/previous-versions/windows/xna/bb199616%28v%3dxnagamestudio.41%29) 메서드가 XNA Framework에서 반복적으로 호출됩니다. [Update](https://docs.microsoft.com/previous-versions/windows/xna/bb199616%28v%3dxnagamestudio.41%29) 메서드는 게임 피스 컬렉션에 대해 **ProcessInertia** 및 **UpdateFromMouse** 메서드를 호출합니다. 이러한 메서드는 [GamePieceCollection 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)에서 설명합니다.  
  
 [!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]  
  
 게임을 실행하는 동안 [Draw](https://docs.microsoft.com/previous-versions/windows/xna/bb196422%28v%3dxnagamestudio.41%29) 메서드도 XNA Framework에서 반복적으로 호출됩니다. [Draw](https://docs.microsoft.com/previous-versions/windows/xna/bb196422%28v%3dxnagamestudio.41%29) 메서드는 **GamePieceCollection** 개체의 **Draw** 메서드를 호출하여 게임 피스 렌더링을 수행합니다. 이 메서드는 [GamePieceCollection 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)에서 설명합니다.  
  
 [!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]  
  
## <a name="see-also"></a>참고 항목  
 [조작 및 관성](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)  
 [XNA 응용 프로그램에서 조작 및 관성 사용](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)  
 [GamePiece 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)  
 [GamePieceCollection 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)  
 [전체 코드 목록](../../../docs/framework/common-client-technologies/full-code-listings.md)
