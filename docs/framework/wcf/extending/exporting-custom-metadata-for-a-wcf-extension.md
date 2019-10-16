---
title: WCF 확장에 대한 사용자 지정 메타데이터 내보내기
ms.date: 03/30/2017
ms.assetid: 53c93882-f8ba-4192-965b-787b5e3f09c0
ms.openlocfilehash: 540dd9011be83d349495a0b05283b83f3d55dc2c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797184"
---
# <a name="exporting-custom-metadata-for-a-wcf-extension"></a>WCF 확장에 대한 사용자 지정 메타데이터 내보내기
WCF (Windows Communication Foundation)에서 메타 데이터 내보내기는 서비스 끝점을 설명 하 고 클라이언트가 서비스를 사용 하는 방법을 이해 하는 데 사용할 수 있는 병렬, 표준화 된 표현으로 프로젝션 하는 프로세스입니다. 사용자 지정 메타데이터는 시스템에서 제공한 메타데이터 내보내기에서 내보낼 수 없는 XML 요소로 구성됩니다. 일반적으로 여기에는 사용자 정의 동작 및 바인딩 요소에 대한 사용자 지정 WSDL 요소를 비롯하여 바인딩 및 계약의 기능과 요구 사항에 대한 정책 어설션이 포함됩니다.  
  
 이 단원에서는 사용자 지정 WSDL 또는 정책 어설션 내보내기에 대해 설명하지만 내보내기 프로세스 자체를 중점적으로 설명하지는 않습니다. 메타 데이터가 사용자 지정 인지 또는 시스템 생성 인지에 관계 없이 메타 데이터를 내보내고 가져오는 형식을 사용 하는 방법에 대 한 자세한 내용은 [메타 데이터 내보내기 및 가져오기](../feature-details/exporting-and-importing-metadata.md)를 참조 하세요.  
  
## <a name="overview"></a>개요  
 를 사용 하 여 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType>메타 데이터를 게시 하면 <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType> 가 검사 되 고, WCF가 시스템 제공 특성 및 바인딩을 사용 하 여 지원할 수 있는 모든 계약과 바인딩에 대해 XSD 및 WSDL (정책 어설션 포함)이 생성 됩니다. 그러나 메타데이터를 올바르게 내보내려면 먼저 사용자 지정 동작 특성 또는 바인딩 요소가 지원되어야 합니다.  
  
 이 단원의 내용은 다음과 같습니다.  
  
1. WSDL을 게시하기 전에 WSDL 생성 데이터를 공개하는 <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> 인터페이스를 구현하고 사용하는 방법  
  
2. WSDL 데이터에서 정책 어설션을 내보내기 전에 정책 데이터를 공개하는 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> 인터페이스를 구현하고 사용하는 방법  
  
 사용자 지정 WSDL 및 정책 어설션을 가져오는 방법에 대 한 자세한 내용은 [WCF 확장에 대 한 사용자 지정 메타 데이터 가져오기](importing-custom-metadata-for-a-wcf-extension.md)를 참조 하세요.  
  
## <a name="exporting-custom-wsdl-elements"></a>사용자 지정 WSDL 요소 내보내기  
 작업 동작, 계약 동작, 엔드포인트 동작 또는 바인딩 요소(각각 <xref:System.ServiceModel.Description.IWsdlExportExtension>, <xref:System.ServiceModel.Description.IOperationBehavior>, <xref:System.ServiceModel.Description.IContractBehavior>, <xref:System.ServiceModel.Description.IEndpointBehavior>)에서 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>을 구현하고, 내보낼 서비스에 대한 설명에 동작 또는 바인딩 요소를 삽입합니다. (동작 삽입에 대 한 자세한 내용은 [동작을 사용 하 여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md))을 참조 하세요. 각 엔드포인트에 대해 <xref:System.ServiceModel.Description.IWsdlExportExtension>이 호출되고 각 엔드포인트에서 계약을 먼저 내보냅니다(아직 내보내지 않은 경우). 필요에 따라 내보내기 프로세스에 참여할 수 있습니다.  
  
- <xref:System.ServiceModel.Description.WsdlContractConversionContext> 메서드에서 내보낸 메타데이터를 수정하려면 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A>를 사용합니다.  
  
- <xref:System.ServiceModel.Description.WsdlEndpointConversionContext> 메서드에서 엔드포인트에 대해 내보낸 메타데이터를 수정하려면 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A>를 사용합니다.  
  
 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A> 메서드는 내보낼 <xref:System.ServiceModel.Description.IWsdlExportExtension> 인스턴스 내의 모든 <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType> 구현에 대해 호출됩니다.  <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> 메서드는 내보낼 <xref:System.ServiceModel.Description.IWsdlExportExtension> 인스턴스가 있는 모든 <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> 구현에 대해 호출됩니다.  
  
 자세한 내용은 [방법: 사용자 지정 wsdl](how-to-export-custom-wsdl.md) 및 샘플 [사용자 지정 wsdl 게시](../samples/custom-wsdl-publication.md)를 내보냅니다.  
  
## <a name="exporting-custom-policy-assertions"></a>사용자 지정 정책 어설션 내보내기  
 <xref:System.ServiceModel.Description.IPolicyExportExtension>에서 <xref:System.ServiceModel.Channels.BindingElement>을 구현하고 바인딩에 바인딩 요소를 추가하여 바인딩 지원 및 계약 기능에 대한 사용자 지정 정책 어설션을 WSDL로 작성합니다. <xref:System.ServiceModel.Description.IPolicyExportExtension>은 바인딩에서 구현된 바인딩 요소를 내보낼 때 호출되어 <xref:System.ServiceModel.Description.PolicyConversionContext>를 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A> 메서드에 전달합니다. <xref:System.ServiceModel.Description.PolicyConversionContext> 인스턴스의 메서드를 사용하여 메시지, 작업 또는 엔드포인트 주체에서 WSDL 바인딩에 연결된 정책 어설션에 추가할 수 있습니다.  
  
 자세한 내용은 [방법: 사용자 지정 정책 어설션을](how-to-export-custom-policy-assertions.md)내보냅니다.  
  
## <a name="see-also"></a>참고자료

- [방법: 사용자 지정 WSDL 내보내기](how-to-export-custom-wsdl.md)
- [방법: 사용자 지정 정책 어설션 내보내기](how-to-export-custom-policy-assertions.md)
- [WCF 확장에 대한 사용자 지정 메타데이터 가져오기](importing-custom-metadata-for-a-wcf-extension.md)
