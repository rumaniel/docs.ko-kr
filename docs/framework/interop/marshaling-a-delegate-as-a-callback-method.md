---
title: 콜백 메서드로 대리자 마샬링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data marshaling, Callback sample
- marshaling, Callback sample
ms.assetid: 6ddd7866-9804-4571-84de-83f5cc017a5a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 579bc56a538707fd19d6d089c7f3c0c0561ea9eb
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49454423"
---
# <a name="marshaling-a-delegate-as-a-callback-method"></a>콜백 메서드로 대리자 마샬링
이 샘플에서는 함수 포인터가 필요한 관리되지 않는 함수에 대리자를 전달하는 방법을 보여 줍니다. 대리자는 메서드에 대한 참조를 보유할 수 있는 클래스이고 형식이 안전한 함수 포인터나 콜백 함수에 해당합니다.  
  
> [!NOTE]
>  호출에서 대리자를 사용하면 공용 언어 런타임에서 대리자가 해당 호출 기간 동안 가비지 수집되지 않게 보호합니다. 그러나 관리되지 않는 함수에서 호출이 완료된 후 사용하기 위해 대리자를 저장하는 경우 관리되지 않는 함수가 대리자를 완료할 때까지 직접 가비지 수집이 수행되지 않게 처리해야 합니다. 자세한 내용은 [HandleRef 샘플](https://msdn.microsoft.com/library/ab23b04e-1d53-4ec7-b27a-e892d9298959(v=vs.100)) 및 [GCHandle 샘플](https://msdn.microsoft.com/library/6acce798-0385-4ded-a790-77da842c113f(v=vs.100))을 참조하세요.  
  
 Callback 샘플에서는 원래 함수 선언과 함께 표시되는 다음과 같은 관리되지 않는 함수를 사용합니다.  
  
-   PinvokeLib.dll에서 내보낸 **TestCallBack**.  
  
    ```  
    void TestCallBack(FPTR pf, int value);  
    ```  
  
-   PinvokeLib.dll에서 내보낸 **TestCallBack2**.  
  
    ```  
    void TestCallBack2(FPTR2 pf2, char* value);  
    ```  
  
 [PinvokeLib.dll](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as6wyhwt(v=vs.100))은 앞에 나열된 함수의 구현을 포함하는 관리되지 않는 사용자 지정 라이브러리입니다.  
  
 이 샘플에서 `LibWrap` 클래스에는 `TestCallBack` 및 `TestCallBack2` 메서드의 관리되는 프로토타입이 포함됩니다. 두 메서드 모두 대리자를 매개 변수로 콜백 함수에 전달합니다. 대리자의 시그니처는 대리자가 참조하는 메서드의 시그니처와 일치해야 합니다. 예를 들어 `FPtr` 및 `FPtr2` 대리자는 `DoSomething` 및 `DoSomething2` 메서드에 동일한 시그니처가 있습니다.  
  
## <a name="declaring-prototypes"></a>프로토타입 선언  
 [!code-cpp[Conceptual.Interop.Marshaling#37](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/callback.cpp#37)]
 [!code-csharp[Conceptual.Interop.Marshaling#37](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/callback.cs#37)]
 [!code-vb[Conceptual.Interop.Marshaling#37](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/callback.vb#37)]  
  
## <a name="calling-functions"></a>함수 호출  
 [!code-cpp[Conceptual.Interop.Marshaling#38](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/callback.cpp#38)]
 [!code-csharp[Conceptual.Interop.Marshaling#38](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/callback.cs#38)]
 [!code-vb[Conceptual.Interop.Marshaling#38](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/callback.vb#38)]  
  
## <a name="see-also"></a>참고 항목  
 [기타 마샬링 샘플](https://msdn.microsoft.com/library/a915c948-54e9-4d0f-a525-95a77fd8ed70(v=vs.100))  
 [플랫폼 호출 데이터 형식](https://msdn.microsoft.com/library/16014d9f-d6bd-481e-83f0-df11377c550f(v=vs.100))  
 [관리 코드에서 프로토타입 만들기](creating-prototypes-in-managed-code.md)
