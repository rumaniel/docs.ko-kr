---
title: ServiceHost 및 서비스 모델 계층 확장
ms.date: 03/30/2017
helpviewer_keywords:
- extending service models [WCF]
ms.assetid: 954c138a-1cd0-45a0-8abe-e4d2b8ff5400
ms.openlocfilehash: e370316cd121f49953e00e83dfc9d2aec17de1e8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795728"
---
# <a name="extending-servicehost-and-the-service-model-layer"></a>ServiceHost 및 서비스 모델 계층 확장
서비스 모델 계층은 기본 채널에서 들어오는 메시지를 끌어와서 애플리케이션 코드에서 이를 메서드 호출로 변환하여 결과를 다시 호출자에게 보내는 역할을 합니다. 서비스 모델 확장은 클라이언트 또는 디스패처 기능, 사용자 지정 동작, 메시지 및 매개 변수 가로채기 그리고 다른 확장명 기능이 포함된 통신 동작 및 기능 또는 실행을 수정하거나 구현합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [클라이언트 확장](extending-clients.md)  
 사용자 지정 확장을 클라이언트 애플리케이션에 삽입할 수 있는 클래스뿐 아니라 클라이언트 런타임을 가로채고 수정할 수 있는 인터페이스에 대해 설명합니다. 예를 들어, 사용자 지정 클라이언트 메시지 로깅, 사용자 지정 메시지 serialization 등을 수행할 수 있습니다.  
  
 [디스패처 확장](extending-dispatchers.md)  
 사용자 지정 확장을 서비스 애플리케이션에 삽입할 수 있는 클래스뿐 아니라 서비스 런타임을 가로채고 수정할 수 있는 인터페이스에 대해 설명합니다. 예를 들어, 사용자 지정 서비스 로깅, 서비스 측 메시지 유효성 검사, 사용자 지정 디스패치 등을 수행할 수 있습니다.  
  
 [확장 가능한 개체](extensible-objects.md)  
 5개의 확장 가능한 개체 및 <xref:System.ServiceModel.IExtensibleObject%601> 패턴에 대해 설명합니다. 새 기능과 함께 기존 런타임 클래스를 확장하거나 새 상태를 개체에 추가하기 위해 확장명 가능한 개체 패턴이 사용됩니다. 확장명 가능한 개체 중 하나에 연결된 확장은 이 개체에서 액세스할 수 있는 확장명 가능한 일반 개체에 연결된 공유 상태 및 기능에 액세스하는 처리 시에 매우 다른 단계에서 동작을 활성화합니다.  
  
 [동작을 사용하여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)  
 WCF 런타임에서 설정을 변경 하거나 확장을 삽입 하려면 동작을 사용 합니다. WCF에는 스로틀, 인스턴스 만들기 그리고 서비스 및 작업의 여러 사항을 제어하기 위한 시스템 구현 동작이 포함되어 있습니다. 이 단원에서는 사용자 지정 동작을 만드는 방법 및 프로그램 방식과 구성 파일을 사용하여 해당 동작을 사용하는 방법에 대해 설명합니다.  
  
 [ServiceHostFactory를 사용하여 호스팅 확장](extending-hosting-using-servicehostfactory.md)  
 <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType>와 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType>를 확장하는 방법 및 <xref:System.ServiceModel.Activation.ServiceHostFactory?displayProperty=nameWithType> 클래스를 사용하여 호스트 환경을 사용자 지정하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
  
## <a name="related-sections"></a>관련 단원
