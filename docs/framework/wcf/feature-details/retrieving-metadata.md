---
title: 메타데이터 검색
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], retrieving
ms.assetid: 18d8ba4c-af0f-4827-a50b-4202d767bacc
ms.openlocfilehash: bb415d88c2bae75cb16aa137bdf867eb463afa63
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61748306"
---
# <a name="retrieving-metadata"></a>메타데이터 검색
메타데이터 검색은 WS-MEX(WS-MetadataExchange) 메타데이터 엔드포인트 또는 HTTP/GET 메타데이터 엔드포인트 같은 메타데이터 엔드포인트에서 메타데이터를 요청 및 검색하는 프로세스입니다.  
  
## <a name="retrieving-metadata-from-the-command-line-using-svcutilexe"></a>Svcutil.exe를 사용하여 명령줄에서 메타데이터 검색  
 사용 하 여 Ws-metadataexchange 또는 HTTP/GET 요청을 사용 하 여 서비스 메타 데이터를 검색할 수 있습니다는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 도구 및 전달 된 `/target:metadata` 스위치와 주소입니다. Svcutil.exe는 지정된 주소의 메타데이터를 다운로드하고 파일을 디스크에 저장합니다. Svcutil.exe는 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 인스턴스를 내부적으로 사용하고, 구성에서 Svcutil.exe에 입력으로 전달된 주소 스키마와 이름이 같은 <xref:System.ServiceModel.Description.IMetadataExchange> 엔드포인트 구성을 로드합니다.  
  
## <a name="retrieving-metadata-programmatically-using-the-metadataexchangeclient"></a>MetadataExchangeClient를 사용하여 프로그래밍 방식으로 메타데이터 검색  
 Windows Communication Foundation (WCF) Ws-metadataexchange 및 HTTP/GET 요청과 같은 표준화 된 프로토콜을 사용 하 여 서비스 메타 데이터를 검색할 수 있습니다. 이러한 프로토콜은 모두 <xref:System.ServiceModel.Description.MetadataExchangeClient> 형식에서 지원합니다. 메타데이터 엔드포인트의 주소와 선택적인 바인딩을 제공하여 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 형식을 통해 서비스 메타데이터를 검색합니다. <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 인스턴스에서 사용되는 바인딩은 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 정적 클래스의 기본 바인딩, 사용자 제공 바인딩 또는 `IMetadataExchange` 계약의 엔드포인트 구성에서 로드된 바인딩 중 하나입니다. <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType>는 <xref:System.Net.HttpWebRequest> 형식을 통해 메타데이터에 대한 HTTP URL 참조를 확인할 수도 있습니다.  
  
 기본적으로 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 인스턴스는 하나의 <xref:System.ServiceModel.ChannelFactory> 인스턴스에 연결됩니다. <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> 가상 메서드를 재정의하여 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType>에서 사용하는 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A> 인스턴스를 변경하거나 바꿀 수 있습니다. 마찬가지로 <xref:System.Net.HttpWebRequest> 가상 메서드를 재정의하여 HTTP/GET 요청을 만들기 위해 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType>에서 사용하는 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=nameWithType> 인스턴스를 변경하거나 바꿀 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: Svcutil.exe를 사용 하 여 메타 데이터 문서 다운로드](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)  
 Svcutil.exe를 사용하여 메타데이터 문서를 다운로드하는 방법을 보여 줍니다.  
  
 [방법: MetadataResolver를 사용 하 여 동적으로 바인딩 메타 데이터를 가져오려면](../../../../docs/framework/wcf/feature-details/how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)  
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>를 사용하여 바인딩 메타데이터를 런타임에 동적으로 가져오는 방법을 보여 줍니다.  
  
 [방법: MetadataExchangeClient를 사용 하 여 메타 데이터를 검색 합니다.](../../../../docs/framework/wcf/feature-details/how-to-use-metadataexchangeclient-to-retrieve-metadata.md)  
 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 클래스를 사용하여 파일에 기록하거나 다른 용도로 사용할 <xref:System.ServiceModel.Description.MetadataSet?displayProperty=nameWithType> 개체가 있는 <xref:System.ServiceModel.Description.MetadataSection?displayProperty=nameWithType> 개체에 메타데이터 파일을 다운로드하는 방법을 보여 줍니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.MetadataExchangeClient>
