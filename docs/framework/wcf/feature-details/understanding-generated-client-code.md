---
title: 생성된 클라이언트 코드 이해
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c3f6e4b0-1131-4c94-aa39-a197c5c2f2ca
ms.openlocfilehash: 6bc921355e54023ead3a308a7877ab609f868221
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968631"
---
# <a name="understanding-generated-client-code"></a>생성된 클라이언트 코드 이해
[ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 는 클라이언트 응용 프로그램을 빌드하는 데 사용할 클라이언트 응용 프로그램 구성 파일과 클라이언트 코드를 생성합니다. 이 항목에서는 표준 서비스 계약 시나리오를 위해 생성된 코드 예제를 간략히 살펴 봅니다. 생성 된 코드를 사용 하 여 클라이언트 응용 프로그램을 빌드하는 방법에 대 한 자세한 내용은 [WCF 클라이언트 개요](../../../../docs/framework/wcf/wcf-client-overview.md)를 참조 하세요.  
  
## <a name="overview"></a>개요  
 Visual Studio를 사용 하 여 프로젝트에 대 한 WCF (Windows Communication Foundation) 클라이언트 형식을 생성 하는 경우 일반적으로 생성 된 클라이언트 코드를 검사할 필요가 없습니다. 동일한 서비스를 수행하는 개발 환경을 사용하지 않는 경우 Svcutil.exe 같은 도구를 사용하여 클라이언트 코드를 생성한 다음 해당 코드를 사용하여 클라이언트 애플리케이션을 개발할 수 있습니다.  
  
 Svcutil.exe에는 생성된 형식 정보를 수정하는 많은 옵션이 있으므로 이 항목에서 모든 시나리오에 대해 설명하지는 않습니다. 그러나 다음 표준 작업에는 생성된 코드를 찾는 과정이 포함됩니다.  
  
- 서비스 계약 인터페이스 식별  
  
- WCF 클라이언트 클래스를 식별 합니다.  
  
- 데이터 형식 식별  
  
- 이중 서비스에 대한 콜백 계약 식별  
  
- 도우미 서비스 계약 채널 인터페이스 식별  
  
### <a name="finding-service-contract-interfaces"></a>서비스 계약 인터페이스 찾기  
 서비스 계약을 모델링하는 인터페이스를 찾으려면 <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType> 특성으로 표시된 인터페이스를 검색합니다. 다른 특성이 있고 특성 자체에 명시적 속성이 설정되어 있어 빠른 읽기로 이 특성을 찾기 어려울 수 있습니다. 서비스 계약 인터페이스와 클라이언트 계약 인터페이스는 두 가지 다른 형식입니다. 다음 코드 예제에서는 원래 서비스 계약을 보여 줍니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#22](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#22)]  
  
 다음 코드 예제에서는 Svcutil.exe에서 생성된 것과 동일한 서비스 계약을 보여 줍니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#12)]  
  
 생성 된 서비스 계약 인터페이스를 <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> 클래스와 함께 사용 하 여 서비스 작업을 호출 하는 데 사용할 WCF 채널 개체를 만들 수 있습니다. 자세한 내용은 [방법: ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)를 사용 합니다.  
  
### <a name="finding-wcf-client-classes"></a>WCF 클라이언트 클래스 찾기  
 사용할 서비스 계약을 구현 하는 WCF 클라이언트 클래스를 찾으려면 형식 매개 변수가 이전에 찾아서 해당 인터페이스를 <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>확장 하는 서비스 계약 인터페이스인의 확장을 검색 합니다. 다음 코드 예제에서는 <xref:System.ServiceModel.ClientBase%601> 형식의 `ISampleService`클래스를 보여 줍니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#14)]  
  
 이 WCF 클라이언트 클래스의 새 인스턴스를 만들고이 클래스에서 구현 하는 메서드를 호출 하 여이 클래스를 사용할 수 있습니다. 이러한 메서드는 상호 작용하도록 디자인 및 구성된 서비스 작업을 호출합니다. 자세한 내용은 [WCF 클라이언트 개요](../../../../docs/framework/wcf/wcf-client-overview.md)를 참조 하세요.  
  
> [!NOTE]
> SvcUtil.exe는 WCF 클라이언트 클래스를 생성할 때 디버거가 WCF 클라이언트 클래스를 단계별로 실행하지 못하도록 하는 <xref:System.Diagnostics.DebuggerStepThroughAttribute> 를 클라이언트 클래스에 추가합니다.  
  
### <a name="finding-data-types"></a>데이터 형식 찾기  
 생성된 코드에서 데이터 형식을 찾으려는 경우 가장 기본적인 메커니즘은 계약에 지정된 형식 이름을 식별하고 해당 형식 선언에 대해 코드를 검색하는 것입니다. 예를 들어 다음 계약은 `SampleMethod` 에서 `microsoft.wcf.documentation.SampleFault`형식의 SOAP 오류를 반환할 수 있도록 지정합니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#11)]  
  
 `SampleFault` 를 검색하면 다음 형식 선언을 찾습니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#30](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#30)]  
  
 이 경우 데이터 형식은 클라이언트의 특정 예외인 <xref:System.ServiceModel.FaultException%601> 에서 throw되는 세부 유형이며, 여기서 세부 유형 매개 변수는 `microsoft.wcf.documentation.SampleFault`입니다. 데이터 형식에 대 한 자세한 내용은 [서비스 계약의 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)을 참조 하세요. 클라이언트에서 예외를 처리 하는 방법에 대 한 자세한 내용은 [오류 보내기 및 받기](../../../../docs/framework/wcf/sending-and-receiving-faults.md)를 참조 하십시오.  
  
### <a name="finding-callback-contracts-for-duplex-services"></a>이중 서비스에 대한 콜백 계약 찾기  
 계약 인터페이스가 <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=nameWithType> 속성 값을 지정하는 서비스 계약을 찾으면 해당 계약이 이중 계약을 지정합니다. 이중 계약에서는 클라이언트 응용 프로그램이 콜백 계약을 구현하는 콜백 클래스를 만들고 해당 클래스의 인스턴스를 서비스와의 통신에 사용되는 <xref:System.ServiceModel.DuplexClientBase%601?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=nameWithType>로 전달해야 합니다. 이중 클라이언트 [에 대 한 자세한 내용은 방법: 이중 계약](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)을 사용 하 여 서비스에 액세스 합니다.  
  
 다음 계약에서는 `SampleDuplexHelloCallback`형식의 콜백 계약을 지정합니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/duplexproxycode.cs#2)]
 [!code-vb[C_GeneratedCodeFiles#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_generatedcodefiles/vb/duplexproxycode.vb#2)]  
  
 해당 콜백 계약을 검색하면 클라이언트 애플리케이션이 구현해야 하는 다음 인터페이스를 찾습니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/duplexproxycode.cs#4)]
 [!code-vb[C_GeneratedCodeFiles#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_generatedcodefiles/vb/duplexproxycode.vb#4)]  
  
### <a name="finding-service-contract-channel-interfaces"></a>서비스 계약 채널 인터페이스 찾기  
 <xref:System.ServiceModel.ChannelFactory> 클래스를 서비스 계약 인터페이스와 함께 사용하면 채널을 명시적으로 열고, 닫고, 중단할 수 있도록 <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType> 인터페이스로 캐스팅해야 합니다. 더 편리하게 작업할 수 있도록 Svcutil.exe 도구에서는 서비스 계약 인터페이스와 <xref:System.ServiceModel.IClientChannel> 을 모두 구현하는 도우미 인터페이스도 생성되므로 캐스팅하지 않고도 클라이언트 채널 인프라와 상호 작용할 수 있습니다. 다음 코드에서는 이전의 서비스 계약을 구현하는 도우미 클라이언트 채널에 대한 정의를 보여 줍니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#13)]  
  
## <a name="see-also"></a>참고자료

- [WCF 클라이언트 개요](../../../../docs/framework/wcf/wcf-client-overview.md)
