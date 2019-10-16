---
title: <soapProcessing>
ms.date: 03/30/2017
ms.assetid: e8707027-e6b8-4539-893d-3cd7c13fbc18
ms.openlocfilehash: 0728e22205d4ac2c7674f7690e142aed51d42440
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399535"
---
# <a name="soapprocessing"></a>\<soapProcessing>

서로 다른 바인딩 형식과 메시지 버전 간에 메시지 마샬링을 위해 사용되는 클라이언트 엔드포인트 동작을 정의합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<endpointBehaviors >** ](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<soapProcessing >**
  
## <a name="syntax"></a>구문  
  
```xml  
<soapProcessing processMessages="true|false" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
  
다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|                   | Description |
| ----------------- | ----------- |
| `processMessages` | SOAP 메시지 버전 간에 메시지가 마샬링되어야 하는지 여부를 지정하는 부울 값입니다. |

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|     | Description |
| --- | ----------- |
| [ **\<behavior>** ](behavior-of-endpointbehaviors.md) | 엔드포인트 동작을 지정합니다. |

## <a name="remarks"></a>설명

SOAP 처리는 메시지 버전 간에 메시지를 변환하는 프로세스입니다.

WCF (Windows Communication Foundation) 라우팅 서비스는 한 프로토콜에서 다른 프로토콜로 메시지를 변환할 수 있습니다. 들어오는 메시지 버전과 나가는 메시지 버전이 다른 경우 올바른 버전의 새로운 메시지가 만들어집니다. 한 <xref:System.ServiceModel.Channels.MessageVersion>에서 다른 버전으로 메시지를 처리하는 작업은 들어오는 WCF 메시지의 본문 부분과 관련 헤더를 포함하는 새 WCF 메시지를 생성하는 방법으로 수행됩니다. 주소 지정에만 사용되는 헤더나 라우터 수준에서 인식되는 헤더는 새 WCF 메시지 생성 중에 사용되지 않습니다. 이러한 헤더는 서로 다른 버전(주소 지정 헤더인 경우)이거나 클라이언트와 라우터 간의 통신의 일부로 처리되었기 때문입니다.

헤더가 아웃바운드 메시지에 배치되는지 여부는 들어오는 채널 계층을 통해 전달될 때 해당 헤더가 인식된 것으로 표시되었는지 여부에 따라 결정됩니다. 사용자 지정 헤더 등과 같이 인식되지 않는 헤더는 제거되지 않고 아웃바운드 메시지에 복사되어 라우팅 서비스를 통해 전달됩니다. 메시지의 본문은 아웃바운드 메시지에 복사됩니다. 그런 다음 메시지가 아웃바운드 채널로 전송되며 이때 해당 통신 프로토콜/전송에 대한 모든 헤더와 기타 봉투 데이터가 만들어지고 추가됩니다.

이러한 처리 단계는 SOAP 처리 동작이 지정될 때 수행됩니다. [ 이\<soapProcessingExtension >](soapprocessing.md) 동작은 라우팅 서비스 시작 시 모든 클라이언트 (나가는) 끝점에 적용 되는 끝점 동작입니다. 기본적으로 [ \<라우팅 >](routing-of-servicebehavior.md) 동작은 각 클라이언트 끝점에 대해 `true` 를로 설정 하 여 `processMessages` 새 [ \<soapProcessingExtension >](soapprocessing.md) 동작을 만들고 연결 합니다. 라우팅 서비스에서 인식하지 못하는 프로토콜을 사용하거나 기본 처리 동작을 재지정하려는 경우 전체 라우팅 서비스 또는 특정 엔드포인트에 대해 SOAP 처리를 사용하지 않을 수 있습니다.  모든 끝점에서 전체 라우팅 서비스에 대해 SOAP 처리를 사용 하지 않도록 설정 `soapProcessing` 하려면 [ \<라우팅 >](routing-of-servicebehavior.md) 동작의 특성을 `false`로 설정 합니다. 특정 엔드포인트에 대해 SOAP 처리를 해제하려면 이 동작을 사용하여 `processMessages` 특성을 `false`로 설정한 다음 이 동작을 기본 처리 코드가 실행되지 않도록 할 엔드포인트에 연결합니다.  라우팅 > 동작에서 라우팅 서비스를 설정 하는 경우 끝점 동작이 이미 존재 하므로 다시 적용 하는 작업은 건너뜁니다. [ \<](routing-of-servicebehavior.md)
