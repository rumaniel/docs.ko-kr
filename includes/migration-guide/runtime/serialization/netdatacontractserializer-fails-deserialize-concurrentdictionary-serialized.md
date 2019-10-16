---
ms.openlocfilehash: 380f662349a8dcd04e5bf445e1479d0a32d5861f
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235607"
---
### <a name="netdatacontractserializer-fails-to-deserialize-a-concurrentdictionary-serialized-with-a-different-net-version"></a>NetDataContractSerializer가 다른 .NET 버전으로 직렬화된 ConcurrentDictionary를 역직렬화하지 못합니다.

|   |   |
|---|---|
|세부 정보|기본적으로 직렬화 측과 역직렬화 측이 모두 동일한 CLR 형식을 공유하는 경우에만 <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=name>을 사용할 수 있습니다. 따라서 한 버전의 .NET Framework를 사용하여 직렬화된 개체를 다른 버전으로 역직렬화할 수 있다고 보장할 수 없습니다.<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=name> .NET Framework 4.5 또는 이전 버전으로 직렬화되고 .NET Framework 4.5.1 이상으로 역직렬화되면 올바르게 역직렬화하지 않는 것으로 알려진 형식입니다.|
|제안 해결 방법|이 문제에 대한 해결 방법에는 여러 가지가 있습니다.<ul><li>.NET Framework 4.5.1도 사용하도록 직렬화 컴퓨터를 업그레이드합니다.</li><li>직렬화 및 역직렬화 측 모두에서 정확히 동일한 CLR 형식이 필요하지 않으므로 <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=name> 대신 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=name>을 사용합니다.</li><li>이 특정 4.5-&gt;4.5.1 문제가 발생하지 않으므로 <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=name> 대신 <xref:System.Collections.Generic.Dictionary%602?displayProperty=name>을 사용합니다.</li></ul>|
|범위|부|
|버전|4.5.1|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Runtime.Serialization.NetDataContractSerializer.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li></ul>|
