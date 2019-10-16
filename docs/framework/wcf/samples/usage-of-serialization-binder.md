---
title: Serialization 바인더 사용
ms.date: 03/30/2017
ms.assetid: ab46c087-200c-45bf-9c95-5a6cda6e8b98
ms.openlocfilehash: 10900950b935b484053fe8e37263f0dfc25eba99
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348453"
---
# <a name="usage-of-serialization-binder"></a>Serialization 바인더 사용
이 샘플에서는 <xref:System.Runtime.Serialization.SerializationBinder>를 사용하여 제네릭 형식이 serialize될 때 이 형식의 버전을 변경하는 방법을 보여 줍니다.  
  
## <a name="demonstrates"></a>세부 항목  
 <xref:System.Runtime.Serialization.SerializationBinder>, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>  
  
## <a name="discussion"></a>토론  
 이 샘플은.NET Framework 수의 서로 다른 버전을 대상 통신할 수 있는지 이진 포맷터와 serialization 바인더를 사용 하 여 두 엔터티를 보여 줍니다.  
  
이 샘플은.NET Remoting을 사용 하 여 개발 되었습니다. 대상으로 하는 서버 이루어져 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)], 제네릭 형식 및 두 명의 다른 클라이언트, 하나의 대상.NET Framework 2.0 및 다른 대상으로 하는 계약을 구현 하는 [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)]합니다.  
  
 서버에서는 <xref:System.Runtime.Serialization.SerializationBinder>를 이진 포맷터에 연결하여 serialization 시 형식 버전을 적절하게 변경할 수 있도록 하므로 두 클라이언트 모두 해당 형식을 올바르게 deserialize할 수 있습니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 클라이언트를 실행 하려면 SBGenericsVTS 솔루션을 마우스 오른쪽 단추로 클릭 (6 개 프로젝트)를 선택한 **속성**합니다.  
  
2. **공용 속성**를 선택 **시작 프로젝트**을 선택한 후 **여러 개의 시작 프로젝트**합니다.  
  
3. 선택 **Server** 먼저 **Client20** 차례로 **Client40**합니다. 선택 된 **시작** 이 세 가지 프로젝트 작업과 나머지 **None**합니다.  
  
4. 클릭 **확인** 한 다음 f5 키를 눌러 샘플을 실행 합니다.
