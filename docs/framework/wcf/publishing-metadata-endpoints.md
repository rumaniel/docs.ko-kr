---
title: 메타데이터 엔드포인트 게시
ms.date: 03/30/2017
ms.assetid: 29cd8a60-dfb7-460c-bf5a-c2b31b782671
ms.openlocfilehash: 143a46ce18a0d9dee89bbbffac9be9a467e951df
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61955159"
---
# <a name="publishing-metadata-endpoints"></a>메타데이터 엔드포인트 게시
Windows Communication Foundation (WCF) 서비스는 하나 이상의 메타 데이터 끝점을 게시 하 여 메타 데이터를 게시 합니다. 서비스 메타데이터를 게시하면 WS-MetadataExchange(MEX) 및 HTTP/GET 요청과 같이 표준화된 프로토콜을 통해 메타데이터를 사용할 수 있습니다. 메타데이터 엔드포인트는 주소, 바인딩 및 계약에 포함된 다른 서비스 엔드포인트와 유사하며 구성 또는 코드를 통해 서비스 호스트에 추가할 수 있습니다. 메타데이터 엔드포인트 게시를 사용하도록 설정하려면 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 서비스 동작을 서비스에 추가해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 구성 파일을 사용 하는 서비스의 메타 데이터 게시](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 클라이언트는 Ws-metadataexchange 또는 사용 하 여 HTTP/GET 요청을 사용 하 여 메타 데이터를 검색할 수 있도록 메타 데이터를 게시할 WCF 서비스를 구성 하는 방법에 설명 합니다 `?wsdl` 쿼리 문자열입니다.  
  
 [방법: 코드를 사용 하는 서비스의 메타 데이터 게시](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 클라이언트는 Ws-metadataexchange 또는 사용 하 여 HTTP/GET 요청을 사용 하 여 메타 데이터를 검색할 수 있도록 코드에서 WCF 서비스에 대 한 메타 데이터 게시를 사용 하도록 설정 하는 방법에 설명 합니다 `?wsdl` 쿼리 문자열입니다.  
  
## <a name="see-also"></a>참고자료

- [메타데이터 게시](../../../docs/framework/wcf/feature-details/publishing-metadata.md)
