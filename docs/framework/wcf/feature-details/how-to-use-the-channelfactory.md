---
title: '방법: ChannelFactory 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d48f01b5-582b-4c8b-b547-8adddae7e371
ms.openlocfilehash: 7d542a3dcae514e75194b49c23a8dec5dd7e8c3b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62047258"
---
# <a name="how-to-use-the-channelfactory"></a>방법: ChannelFactory 사용
제네릭 <xref:System.ServiceModel.ChannelFactory%601> 클래스는 둘 이상의 채널을 만드는 데 사용할 수 있는 채널 팩터리를 만들어야 하는 고급 시나리오에서 사용됩니다.  
  
### <a name="to-create-and-use-the-channelfactory-class"></a>ChannelFactory 클래스를 만들고 사용하려면  
  
1. 빌드하고 Windows Communication Foundation (WCF) 서비스를 실행 합니다. 자세한 내용은 [서비스 디자인 및 구현](../../../../docs/framework/wcf/designing-and-implementing-services.md)를 [서비스 구성](../../../../docs/framework/wcf/configuring-services.md), 및 [호스팅 서비스](../../../../docs/framework/wcf/hosting-services.md)합니다.  
  
2. 사용 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 클라이언트에 대 한 계약 (인터페이스)를 생성 합니다.  
  
3. 클라이언트 코드에서 <xref:System.ServiceModel.ChannelFactory%601> 클래스를 사용하여 여러 개의 엔드포인트 수신기를 만듭니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[c_HowToUseChannelFactory#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtousechannelfactory/cs/source.cs#1)]
 [!code-vb[c_HowToUseChannelFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtousechannelfactory/vb/source.vb#1)]
