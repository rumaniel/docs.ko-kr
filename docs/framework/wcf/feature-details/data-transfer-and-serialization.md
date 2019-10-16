---
title: 데이터 전송 및 Serialization
ms.date: 03/30/2017
helpviewer_keywords:
- data serialization [WCF]
- data transfer [WCF]
ms.assetid: 0f03c635-f3e7-4c5c-9463-3cb0135e221e
ms.openlocfilehash: 1eefd82a149d0bc215ca441e92c7d737a744b1e0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61856559"
---
# <a name="data-transfer-and-serialization"></a>데이터 전송 및 Serialization
연결된 시스템에서 서비스 및 클라이언트는 데이터 교환에 의존하여 작업을 수행합니다. 서비스나 클라이언트의 개발자는 또한 Windows Communication Foundation (WCF) 효율적이 고 쉽게 유지 관리할 수 있는 응용 프로그램을 만들기 위해 데이터 및 데이터 serialization을 처리 하는 방법을 이해 해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [서비스 계약에서 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)  
 서비스에서 데이터 전송의 기본 개념에 대해 설명합니다.  
  
 [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)  
 데이터 계약의 정의와 데이터 계약을 만들고 사용하는 방법에 대해 설명합니다.  
  
 [데이터 계약 직렬 변환기](../../../../docs/framework/wcf/feature-details/data-contract-serializer.md)  
 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스 또는 <xref:System.Runtime.Serialization.XmlObjectSerializer> 클래스의 확장을 사용하여 데이터의 serialization을 수행하는 방법에 대해 설명합니다.  
  
 [XmlSerializer 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)  
 <xref:System.Xml.Serialization.XmlSerializer> 클래스 대신 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스를 사용하는 방법 및 이유에 대해 설명합니다.  
  
 [메시지 계약 사용](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)  
 메시지 계약에서 SOAP 메시지를 정밀하게 제어하는 방법에 대해 설명합니다.  
  
 [Message 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)  
 Message 클래스 기능을 사용하는 방법에 대해 설명합니다.  
  
 [필터링](../../../../docs/framework/wcf/feature-details/filtering.md)  
 여러 조건을 기반으로 메시지 전처리를 사용하는 필터링에 대해 설명합니다.  
  
 [큰 데이터 및 스트리밍](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)  
 이진 파일과 같은 큰 데이터 블록을 보내는 방법에 대해 설명합니다.  
  
 [데이터에 대한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)  
 데이터 전송 및 serialization을 프로그래밍할 때 알고 있어야 하는 항목에 대해 설명합니다.  
  
 [데이터 전송 아키텍처 개요](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)  
 WCF에서 데이터 전송의 전반적인 디자인의 뷰를 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel>  
  
 <xref:System.Runtime.Serialization.DataContractSerializer>  
  
 <xref:System.Xml.Serialization.XmlSerializer>  
  
 <xref:System.Runtime.Serialization>  
  
 <xref:System.Xml.Serialization>  
  
## <a name="related-sections"></a>관련 단원  
 [인코더 및 직렬 변환기 확장](../../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md)  
  
## <a name="see-also"></a>참고자료

- [모범 사례: 데이터 계약 버전 관리](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)
- [서비스 버전 관리](../../../../docs/framework/wcf/service-versioning.md)
