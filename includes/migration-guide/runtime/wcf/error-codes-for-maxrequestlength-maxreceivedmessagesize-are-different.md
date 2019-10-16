---
ms.openlocfilehash: c9d6111edcfeec6852f23cc0768833de32e61022
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235551"
---
### <a name="error-codes-for-maxrequestlength-or-maxreceivedmessagesize-are-different"></a>maxRequestLength 또는 maxReceivedMessageSize의 오류 코드가 다릅니다.

|   |   |
|---|---|
|세부 정보|IIS(인터넷 정보 서비스) 또는 ASP.NET 개발 서버에서 호스팅되는 WCF 웹 서비스의 메시지가 maxRequestLength(ASP.NET의 경우) 또는 maxReceivedMessageSize(WCF의 경우)를 초과할 경우 오류 코드가 변경됩니다. HTTP 상태 코드가 400(잘못된 요청)에서 413(요청 엔터티가 너무 큼)으로 변경되었으며, maxRequestLength 또는 maxReceivedMessageSize 설정을 초과하는 메시지가 <xref:System.ServiceModel.ProtocolException?displayProperty=name> 예외를 throw합니다. 이는 전송 모드가 스트리밍 상태인 경우를 포함합니다.|
|제안 해결 방법|이러한 변경은 메시지 길이가 ASP.NET 또는 WCF에서 허용한 한계를 초과하는 경우에 디버깅을 용이하게 합니다. HTTP 400 상태 코드에 따라 처리를 수행하는 모든 코드를 수정해야 합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
