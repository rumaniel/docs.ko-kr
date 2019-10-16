---
title: Serialization 개념
ms.date: 08/07/2017
ms.assetid: e1ff4740-20a1-4c76-a8ad-d857db307054
ms.openlocfilehash: 99716a6346689ac4d3201f83b0b8204cad462e8e
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593341"
---
# <a name="serialization-concepts"></a>Serialization 개념
serialization을 사용하는 이유는 무엇입니까? 가장 중요한 두 가지 이유는 이후 단계에서 정확한 복사본을 다시 만들 수 있도록 저장 매체에 개체의 상태를 유지하는 것과 개체를 한 애플리케이션 도메인에서 다른 애플리케이션 도메인으로 값으로 전송하는 것입니다. 예를 들어 serialization을 사용하여 세션 상태를 ASP.NET에 저장하고 개체를 Windows Forms의 클립보드로 복사할 수 있습니다. 또한 Remoting에서 이를 사용하여 개체를 한 애플리케이션 도메인에서 다른 애플리케이션 도메인으로 값으로 전달할 수도 있습니다.

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

## <a name="persistent-storage"></a>영구 스토리지
개체의 필드 값을 디스크에 저장하고 나중에 이 디스크를 검색하는 것이 필요할 경우가 있습니다. serialization을 사용하지 않고 쉽게 구현할 수 있는 기능이지만 이 방식은 불편하고 오류가 발생하기 쉬우며 개체의 계층 구조를 추적해야 할 때는 점점 더 복잡해 집니다. 수천 개의 개체가 있으며 각 개체마다 필드와 속성을 디스크에 저장하고 복원하는 코드를 작성해야 하는 대규모 비즈니스 애플리케이션을 가정해 보십시오. serialization을 사용하면 이러한 목표를 편리하게 달성할 수 있습니다.

공용 언어 런타임은 개체가 메모리에 저장되는 방식을 관리하며 [리플렉션](../../../docs/framework/reflection-and-codedom/reflection.md)을 사용하여 자동화된 serialization 메커니즘을 제공합니다. 개체가 serialize될 때 클래스의 이름, 어셈블리 및 클래스 인스턴스의 모든 데이터 멤버가 스토리지에 기록됩니다. 개체는 다른 인스턴스에 대한 참조를 멤버 변수에 저장할 경우가 있습니다. 클래스가 serialize될 때 serialization 엔진은 이미 serialize된 참조되는 개체를 추적하여 동일한 개체가 두 번 이상 serialize되는 것을 방지합니다. Serialization 아키텍처는.NET Framework를 사용 하 여 올바르게 제공 핸들 개체 그래프와 순환 참조가 자동으로 합니다. 개체 그래프에 대한 유일한 요구 사항은 직렬화된 개체가 참조하는 모든 개체도 `Serializable`로 표시되어야 한다는 점입니다. 자세한 내용은 [기본 Serialization](basic-serialization.md)을 참조하세요. 이렇게 되지 않으면 serializer가 표시되지 않은 개체를 serialize하려고 시도할 때 예외가 throw됩니다.

직렬화된 클래스가 deserialize될 때는 클래스가 다시 만들어지고 모든 데이터 멤버의 값이 자동으로 복원됩니다.

## <a name="marshal-by-value"></a>값에 의한 마샬링
개체는 해당 개체가 만들어진 애플리케이션 도메인에서만 유효합니다. 개체를 매개 변수로 전달하거나 결과로 반환하려고 하는 시도는 개체가 `MarshalByRefObject`에서 파생되거나 `Serializable`로 표시된 경우 이외에는 실패합니다. 개체가 `Serializable`로 표시된 경우 개체는 자동으로 직렬화되고, 하나의 애플리케이션 도메인에서 다른 애플리케이션 도메인으로 전송된 다음, deserialize되어 두 번째 애플리케이션 도메인에서 개체의 정확한 복사본을 생성합니다. 이 프로세스를 일반적으로 값에 의한 마샬링이라고 합니다.
 
개체가 `MarshalByRefObject`에서 파생되는 경우 개체 자체가 아니라 개체 참조가 한 애플리케이션 도메인에서 다른 애플리케이션 도메인으로 전달됩니다. `MarshalByRefObject`에서 파생되는 개체를 `Serializable`로 표시할 수 있습니다. 이 개체를 Remoting에 사용하면 서로게이트 선택기(`SurrogateSelector`)로 미리 구성된 serialization 담당 포맷터가 serialization 프로세스를 제어하고, `MarshalByRefObject`에서 파생된 모든 개체를 프록시로 바꿉니다. `SurrogateSelector`가 없으면 serialization 아키텍처는 [Serialization 과정의 단계](steps-in-the-serialization-process.md)에서 설명하는 표준 serialization 규칙을 따릅니다.  

## <a name="related-sections"></a>관련 단원  
 [이진 serialization](../../../docs/standard/serialization/binary-serialization.md)  
 공용 언어 런타임에 포함된 이진 serialization 메커니즘을 설명합니다.  
  
 [.NET remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))\
 .NET Framework에서 원격 통신에 사용할 수 있는 다양한 통신 방법에 대해 설명합니다.  
  
 [XML 및 SOAP serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md)  
 공용 언어 런타임에 포함된 XML 및 SOAP serialization 메커니즘을 설명합니다.
