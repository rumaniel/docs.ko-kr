---
title: GamePiece 클래스 만들기
ms.date: 03/30/2017
ms.assetid: 37a27a86-ac1c-47be-b477-cb4b819459d3
ms.openlocfilehash: f9f08437cda685d2ec1d2d0c8d54d370d9d38341
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50195881"
---
# <a name="creating-the-gamepiece-class"></a>GamePiece 클래스 만들기
**GamePiece** 클래스는 Microsoft XNA 게임 피스 이미지를 로드하고 게임 피스와 관련된 마우스 상태를 추적하고, 마우스를 캡처하고, 조작 및 관성 처리를 제공하고, 게임 피스가 뷰포트의 제한에 도달할 경우 바운스되는 기능을 제공하는 데 필요한 모든 기능을 캡슐화합니다.  
  
## <a name="private-members"></a>private 멤버  
 **GamePiece** 클래스의 맨 위에서 여러 개의 private 멤버가 선언됩니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_privatemembers)]  
  
## <a name="public-properties"></a>Public 속성  
 이러한 private 멤버 중 3개는 public 속성을 통해 노출됩니다. **Scale** 및 **PieceColor** 속성을 통해 응용 프로그램은 피스의 배율과 색을 각각 지정할 수 있습니다. **Bounds** 속성은 한 피스가 다른 피스를 오버레이해야 하는 경우와 같이 한 피스가 렌더링되기 위해 다른 피스의 범위를 사용할 수 있도록 노출됩니다. 다음 코드에서는 public 속성의 선언을 보여 줍니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PublicProperties](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_publicproperties)]  
  
## <a name="class-constructor"></a>클래스 생성자  
 **GamePiece** 클래스에 대한 생성자는 다음 매개 변수를 수락합니다.  
  
-   [SpriteBatch](https://docs.microsoft.com/previous-versions/windows/xna/bb199034%28v%3dxnagamestudio.41%29) 형식. 여기에 전달된 참조는 private 멤버 `spriteBatch`에 할당되고, 게임 피스가 렌더링될 때 [SpriteBatch.Draw](https://docs.microsoft.com/previous-versions/windows/xna/bb196426%28v%3dxnagamestudio.41%29) 메서드에 액세스하는 데 사용됩니다. 또한 [GraphicsDevice](https://docs.microsoft.com/previous-versions/windows/xna/bb197338%28v%3dxnagamestudio.41%29) 속성은 게임 피스와 연결된 [Texture](https://docs.microsoft.com/previous-versions/windows/xna/bb199375%28v%3xnagamestudio.41%29) 개체를 만들고, 피스가 바운드될 수 있도록 게임 피스가 창 경계에 도달한 경우를 감지하기 위해 뷰포트의 크기를 가져오는 데 사용됩니다.  
  
-   게임 피스에 사용할 이미지의 파일 이름을 지정하는 문자열입니다.  
  
 또한 생성자는 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D> 개체와 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D> 개체를 만들고 해당 이벤트에 대한 이벤트 처리기를 설정합니다.  
  
 다음 코드에서는 **GamePiece** 클래스에 대한 생성자를 보여 줍니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_Constructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_constructor)]  
  
## <a name="capturing-mouse-input"></a>마우스 입력 캡처  
 **UpdateFromMouse** 메서드는 마우스가 게임 피스의 경계 내에 있는 동안 마우스 단추를 누른 경우와 마우스 단추를 놓은 경우를 감지해야 합니다.  
  
 마우스가 피스 경계 내에 있는 상태에서 마우스 왼쪽 단추를 누르면 이 메서드는 이 게임 피스가 마우스를 캡처했음을 나타내는 플래그를 설정하고, 조작 처리를 시작합니다.  
  
 조작 처리는 <xref:System.Windows.Input.Manipulations.Manipulator2D> 개체의 배열을 만들고 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D> 개체에 전달하여 시작됩니다. 그러면 조작 프로세서가 조작자(이 경우 단일 조작자)를 평가하고 조작 이벤트를 발생시킵니다.  
  
 또한 끌기가 발생하는 지점이 저장됩니다. 이 정보는 나중에 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Delta> 이벤트 중 게임 피스가 끌기 지점 뒤의 줄로 회전할 수 있도록 델타 변환 값을 조정하는 데 사용됩니다.  
  
 끝으로, 이 메서드는 마우스 캡처의 상태를 반환합니다. 이 상태를 통해 [GamePieceCollection](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) 개체는 여러 개의 게임 피스가 있을 때 캡처를 관리할 수 있습니다.  
  
 다음 코드에서는 **UpdateFromMouse** 메서드를 보여 줍니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_updatefrommouse)]  
  
## <a name="processing-manipulations"></a>조작 처리  
 조작이 시작되면 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Started> 이벤트가 발생합니다. 이 이벤트 처리기는 관성 처리가 발생할 경우 이를 중지하고 *processInertia* 플래그를 `false`로 설정합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationStarted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationstarted)]  
  
 조작과 연결된 값이 변경되면 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Delta> 이벤트가 발생합니다. 이 이벤트 처리기는 이벤트 인수에 전달된 델타 값을 사용하여 게임 피스의 위치 및 회전 값을 변경합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationDelta](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationdelta)]  
  
 조작과 연결된 모든 조작자(이 경우 단일 조작자)가 제거되면 조작자 프로세서에서 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Completed> 이벤트를 발생시킵니다. 이 이벤트 처리기는 관성 프로세서의 초기 속도를 이벤트 인수에서 보고된 값으로 설정하여 관성 처리를 시작하고 *processInertia* 플래그를 `true`로 설정합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationCompleted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationcompleted)]  
  
## <a name="processing-inertia"></a>관성 처리  
 관성 처리에서 각도 및 선형 속도, 위치(변환) 좌표 및 회전에 대한 새 값을 추정하면 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta> 이벤트가 발생합니다. 이 이벤트 처리기는 이벤트 인수에 전달된 델타 값을 사용하여 게임 피스의 위치 및 회전을 수정합니다.  
  
 새 좌표로 인해 게임 피스가 뷰포트 경계를 넘어가는 경우 관성 처리의 속도가 반대로 바뀝니다. 그러면 게임 피스가 도달한 뷰포트 경계에서 바운스됩니다.  
  
 추정을 실행하는 동안에는 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D> 개체의 속성을 변경할 수 없습니다. 따라서 X 또는 Y 속도를 반대로 하는 경우 이벤트 처리기에서 먼저 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Complete%2A> 메서드를 호출하여 관성을 중지합니다. 그런 다음 새 초기 속도 값을 현재 속도 값(스폰지 동작을 위해 조정됨)으로 할당하고 *processInertia* 플래그를 `true`로 설정합니다.  
  
 다음 코드에서는 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta> 이벤트에 대한 이벤트 처리기를 보여 줍니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnInertiaDelta](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_oninertiadelta)]  
  
 관성 처리가 완료되면 관성 프로세서에서 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Completed> 이벤트를 발생시킵니다. 이 이벤트 처리기는 *processInertia* 플래그를 `false`로 설정합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnInertiaCompleted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_oninertiacompleted)]  
  
 지금까지 제공한 논리에서는 실제로 관성 추정이 발생하지 않습니다. 이 작업은 **ProcessInertia** 메서드에서 수행됩니다. 게임 업데이트 루프([Game.Update](https://docs.microsoft.com/previous-versions/windows/xna/bb199616%28v%3dxnagamestudio.41%29) 메서드)에서 반복적으로 호출되는 이 메서드는 *processInertia* 플래그가 `true`로 설정되었는지 확인하고, 설정된 경우 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Process%2A> 메서드를 호출합니다. 이 메서드를 호출하면 추정이 수행되고 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta> 이벤트가 발생합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_ProcessInertia](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_processinertia)]  
  
 Draw 메서드 오버로드 중 하나가 호출될 때까지 게임 피스는 실제로 렌더링되지 않습니다. 이 메서드의 첫 번째 오버로드는 게임 그리기 루프([Game.Draw](https://docs.microsoft.com/previous-versions/windows/xna/bb196422%28v%3dxnagamestudio.41%29) 메서드)에서 반복적으로 호출됩니다. 이 오버로드는 현재 위치, 회전 및 배율로 게임 피스를 렌더링합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_Draw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_draw)]  
  
## <a name="additional-properties"></a>추가 속성  
 **GamePiece** 클래스는 세 개의 private 속성을 사용합니다.  
  
1.  **Timestamp** - 조작 및 관성 프로세서에서 사용할 타임스탬프 값을 가져옵니다.  
  
2.  **X** - 게임 피스의 X 좌표를 가져오거나 설정합니다. 설정할 때 적중 테스트와 조작 프로세서의 피벗 위치에 사용되는 범위를 조정합니다.  
  
3.  **Y** - 게임 피스의 Y 좌표를 가져오거나 설정합니다. 설정할 때 적중 테스트와 조작 프로세서의 피벗 위치에 사용되는 범위를 조정합니다.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PrivateProperties](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_privateproperties)]  
  
## <a name="see-also"></a>참고 항목  
 [조작 및 관성](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)  
 [XNA 응용 프로그램에서 조작 및 관성 사용](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)  
 [GamePieceCollection 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)  
 [Game1 클래스 만들기](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)
