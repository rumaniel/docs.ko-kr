---
title: 메타데이터 내보내기 및 가져오기
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], exporting and importing
ms.assetid: 614a75bb-e0b0-4c95-b6d8-02cb5e5ddb38
ms.openlocfilehash: 692382de81459ad52d306ca7fd05546b4e36294d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963661"
---
# <a name="exporting-and-importing-metadata"></a>메타데이터 내보내기 및 가져오기
WCF (Windows Communication Foundation)에서 메타 데이터 내보내기는 서비스 끝점을 설명 하 고 클라이언트가 서비스를 사용 하는 방법을 이해 하는 데 사용할 수 있는 병렬, 표준화 된 표현으로 프로젝션 하는 프로세스입니다. 서비스 메타데이터 가져오기는 서비스 메타데이터에서 <xref:System.ServiceModel.Description.ServiceEndpoint> 인스턴스 또는 부분을 생성하는 프로세스입니다.  
  
## <a name="exporting-metadata"></a>메타데이터 내보내기  
 <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> 인스턴스에서 메타데이터를 내보내려면 <xref:System.ServiceModel.Description.MetadataExporter> 추상 클래스 구현을 사용합니다. 합니다 <xref:System.ServiceModel.Description.WsdlExporter> 형식은 구현의 <xref:System.ServiceModel.Description.MetadataExporter> 추상 WCF에 포함 된 클래스입니다.  
  
 <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> 형식은 <xref:System.ServiceModel.Description.MetadataSet> 인스턴스에서 캡슐화된 연결된 정책 식을 사용하여 WSDL(웹 서비스 기술 언어) 메타데이터를 생성합니다. <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> 인스턴스를 사용하여 <xref:System.ServiceModel.Description.ContractDescription> 개체 및 <xref:System.ServiceModel.Description.ServiceEndpoint> 개체에 대한 메타데이터를 반복적으로 내보낼 수 있습니다. <xref:System.ServiceModel.Description.ServiceEndpoint> 개체의 컬렉션을 내보내고, 해당 컬렉션을 특정 서비스 이름과 연결할 수도 있습니다.  
  
> [!NOTE]
> `WsdlExporter`는 CLR(공용 언어 런타임) 형식 정보를 포함하는 `ContractDescription` 인스턴스(예: `ContractDescription` 메서드를 사용하여 만들어지거나 `ContractDescription.GetContract` 인스턴스에 대한 `ServiceDescription`의 일부로 만들어진 `ServiceHost` 인스턴스)에서 메타데이터를 내보내는 경우에만 사용할 수 있습니다. 서비스 메타데이터에서 가져왔거나 형식 정보 없이 생성된 `WsdlExporter` 인스턴스에서 메타데이터를 내보낼 경우에는 `ContractDescription`를 사용할 수 없습니다.  
  
## <a name="importing-metadata"></a>메타데이터 가져오기  
  
### <a name="importing-wsdl-documents"></a>WSDL 문서 가져오기  
 WCF에서 서비스 메타 데이터를 가져오려면 <xref:System.ServiceModel.Description.MetadataImporter> 추상 클래스의 구현을 사용 합니다. 합니다 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> 형식은 구현의 <xref:System.ServiceModel.Description.MetadataImporter> 추상 WCF에 포함 된 클래스입니다. <xref:System.ServiceModel.Description.WsdlImporter> 형식은 <xref:System.ServiceModel.Description.MetadataSet> 개체에 번들로 제공되는 연결된 정책과 함께 WSDL 메타데이터를 가져옵니다.  
  
 <xref:System.ServiceModel.Description.WsdlImporter> 형식을 사용하여 메타데이터를 가져오는 방식을 제어할 수 있습니다. 엔드포인트, 바인딩 또는 계약을 모두 가져올 수 있습니다. 특정 WSDL 서비스, 바인딩 또는 포트 종류와 관련된 모든 엔드포인트를 가져올 수 있습니다. 특정 WSDL 포트에 대한 엔드포인트, 특정 WSDL 바인딩에 대한 바인딩 또는 특정 WSDL 포트 종류에 대한 계약을 가져올 수도 있습니다.  
  
 <xref:System.ServiceModel.Description.WsdlImporter>는 가져올 필요가 없는 계약 집합을 지정할 수 있는 <xref:System.ServiceModel.Description.MetadataImporter.KnownContracts%2A> 속성도 노출합니다. <xref:System.ServiceModel.Description.WsdlImporter>는 메타데이터로부터 정규화된 동일한 이름이 있는 계약을 가져오지 않고 <xref:System.ServiceModel.Description.MetadataImporter.KnownContracts%2A> 속성의 계약을 사용합니다.  
  
### <a name="importing-policies"></a>정책 가져오기  
 <xref:System.ServiceModel.Description.WsdlImporter> 형식은 메시지, 작업 및 끝점 정책 주체에 연결된 정책 식을 수집하고 <xref:System.ServiceModel.Description.IPolicyImportExtension> 컬렉션에서 <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> 구현을 사용하여 정책 식을 가져옵니다.  
  
 정책 가져오기 논리는 동일한 WSDL 문서에 있는 정책 식에 대한 정책 참조를 처리하며, `wsu:Id` 또는 `xml:id` 특성으로 식별됩니다. 정책 가져오기 논리는 정책 식의 크기를 4096개의 노드로 제한하여 순환 정책 참조로부터 애플리케이션을 보호합니다. 여기서 노드는 `wsp:Policy`, `wsp:All`, `wsp:ExactlyOne`, `wsp:policyReference` 요소 중 하나입니다.  
  
 이 정책 가져오기 논리는 정책 식을 자동으로 정규화합니다. 중첩된 정책 식과 `wsp:Optional` 특성은 정규화되지 않습니다. 수행되는 정규화 처리 양은 4096 단계로 제한됩니다. 여기서 각 단계는 정책 어설션 또는 `wsp:ExactlyOne` 요소의 하위 요소를 생성합니다.  
  
 <xref:System.ServiceModel.Description.WsdlImporter> 형식은 여러 WSDL 정책 주체에 연결된 정책 대안의 조합을 최대 32개까지 시도합니다. 완전히 가져오는 조합이 없는 경우, 첫 번째 조합을 사용하여 부분 사용자 지정 바인딩을 생성합니다.  
  
## <a name="error-handling"></a>오류 처리  
 <xref:System.ServiceModel.Description.MetadataExporter> 및 <xref:System.ServiceModel.Description.MetadataImporter> 형식은 각각 도구를 구현할 때 사용할 수 있는 내보내기 및 가져오기 프로세스 중에 발생한 오류 및 경고 메시지의 컬렉션이 포함될 수 있는 `Errors` 속성을 노출합니다.  
  
 일반적으로 <xref:System.ServiceModel.Description.WsdlImporter> 형식은 가져오기 프로세스 중에 catch된 예외에 대해 예외를 throw하고, 해당 오류를 해당 `Errors` 속성에 추가합니다. 그러나 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>, <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A>, <xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A><xref:System.ServiceModel.Description.WsdlImporter.ImportEndpoints%2A> 메서드는 이러한 예외를 throw하지 않으므로 `Errors` 속성을 확인하여 이러한 메서드를 호출할 때 문제가 발생하는지 확인합니다.  
  
 <xref:System.ServiceModel.Description.WsdlExporter> 형식은 내보내기 프로세스 중에 catch된 예외를 다시 throw합니다. 이러한 예외는 `Errors` 속성에서 오류로 캡처되지 않습니다. <xref:System.ServiceModel.Description.WsdlExporter>가 예외를 throw하면 오류 상태에 있게 되므로 다시 사용할 수 없습니다. 작업에서 와일드카드 동작을 사용해서 작업을 내보낼 수 없는 경우와 중복 바인딩 이름이 발생하는 경우, <xref:System.ServiceModel.Description.WsdlExporter>가 경고를 해당 `Errors` 속성에 추가합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 서비스 끝점으로 메타 데이터 가져오기](../../../../docs/framework/wcf/feature-details/how-to-import-metadata-into-service-endpoints.md)  
 다운로드한 메타데이터를 설명 개체로 가져오는 방법에 대해 설명합니다.  
  
 [방법: 서비스 끝점에서 메타 데이터 내보내기](../../../../docs/framework/wcf/feature-details/how-to-export-metadata-from-service-endpoints.md)  
 설명 개체를 메타데이터로 내보내는 방법에 대해 설명합니다.  
  
 [ServiceDescription 및 WSDL 참조](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)  
 설명 개체와 WSDL 간 매핑에 대해 설명합니다.  
  
 [방법: Svcutil.exe를 사용 하 여 컴파일된 서비스 코드에서 메타 데이터 내보내기](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)  
 Svcutil.exe를 사용하여 컴파일된 어셈블리에 있는 서비스, 계약 및 데이터 형식에 대한 메타데이터를 내보내는 방법에 대해 설명합니다.  
  
 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)  
 XML serialization에 대한 CLR(공용 언어 런타임) 형식을 설명하기 위해 <xref:System.Runtime.Serialization.DataContractSerializer>에서 사용하는 XSD(XML 스키마) 하위 집합에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel.Description.WsdlExporter>  
  
 <xref:System.ServiceModel.Description.WsdlImporter>  
  
## <a name="see-also"></a>참고자료

- [WCF 확장에 대한 사용자 지정 메타데이터 내보내기](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md)
- [WCF 확장에 대한 사용자 지정 메타데이터 가져오기](../../../../docs/framework/wcf/extending/importing-custom-metadata-for-a-wcf-extension.md)
