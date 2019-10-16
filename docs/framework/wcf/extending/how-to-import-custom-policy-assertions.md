---
title: '방법: 사용자 지정 정책 어설션 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f41d787-accb-4a10-bfc6-a807671d1581
ms.openlocfilehash: 4510eac2d9c1b3bb64420b0678b3a47a90887188
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795613"
---
# <a name="how-to-import-custom-policy-assertions"></a>방법: 사용자 지정 정책 어설션 가져오기
정책 어설션은 서비스 엔드포인트의 기능 및 요구 사항에 대해 설명합니다.  클라이언트 애플리케이션은 서비스 메타데이터에서 정책 어설션을 사용하여 서비스 엔드포인트에 대해 서비스 계약을 사용자 지정하거나 클라이언트 바인딩을 구성할 수 있습니다.  
  
 <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> 인터페이스를 구현하고 해당 개체를 메타데이터 시스템에 전달하거나 애플리케이션 구성 파일에 구현 형식을 등록하면 사용자 지정 정책 어설션을 가져올 수 있습니다.  <xref:System.ServiceModel.Description.IPolicyImportExtension> 인터페이스 구현에서는 매개 변수가 없는 생성자를 제공 해야 합니다.  
  
### <a name="to-import-custom-policy-assertions"></a>사용자 지정 정책 어설션을 가져오려면  
  
1. 클래스에서 <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> 인터페이스를 구현합니다. 다음 절차를 참조하십시오.  
  
2. 다음 중 하나를 사용하여 사용자 지정 정책 가져오기를 삽입합니다.  
  
3. 구성 파일 사용 다음 절차를 참조하십시오.  
  
4. [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)를 사용 하 여 구성 파일을 사용 합니다. 다음 절차를 참조하십시오.  
  
5. 정책 가져오기를 프로그래밍 방식으로 삽입 다음 절차를 참조하십시오.  
  
### <a name="to-implement-the-systemservicemodeldescriptionipolicyimportextension-interface-on-any-class"></a>클래스에서 System.ServiceModel.Description.IPolicyImportExtension 인터페이스를 구현하려면  
  
1. <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType> 메서드에서 원하는 각 정책 주체에 대해, 이 메서드에 전달된 <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=nameWithType> 개체에서 원하는 어설션 범위에 따라 적절한 메서드를 호출하여 가져올 정책 어설션을 찾습니다. 다음 코드 예제에서는 <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=nameWithType> 메서드를 사용하여 사용자 지정 정책 어설션을 찾고 컬렉션에서 이를 한 번에 제거하는 방법을 보여 줍니다. remove 메서드를 사용하여 어설션을 찾아 제거하면 4단계를 수행할 필요가 없습니다.  
  
     [!code-csharp[CustomPolicySample#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyimporter.cs#9)]
     [!code-vb[CustomPolicySample#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyimporter.vb#9)]  
  
2. 정책 어설션을 처리합니다. 정책 시스템은 중첩된 정책 및 `wsp:optional`을 정규화하지 않습니다. 따라서 정책 가져오기 확장 구현에서 이러한 구문을 처리해야 합니다.  
  
3. 정책 어설션에 의해 지정된 기능 또는 요구 사항을 지원하는 바인딩 또는 계약에 대해 사용자 지정을 수행합니다. 일반적으로 어설션은 바인딩에 특정 구성 또는 특정 바인딩 요소가 필요함을 나타냅니다. <xref:System.ServiceModel.Description.PolicyConversionContext.BindingElements%2A?displayProperty=nameWithType> 속성에 액세스하여 이러한 사항을 수정하십시오. 다른 어설션을 사용하려면 계약을 수정해야 합니다.  <xref:System.ServiceModel.Description.PolicyConversionContext.Contract%2A?displayProperty=nameWithType> 속성을 사용하여 계약에 액세스하고 이를 수정할 수 있습니다.  정책 가져오기는 동일한 바인딩 및 계약에 대해 여러 번 호출될 수 있지만 정책 대안을 가져오는 데 실패하면 다른 정책으로 대체됩니다. 사용자 코드는 이 동작에 대해 유연해야 합니다.  
  
4. 어설션 컬렉션에서 사용자 지정 정책 어설션을 제거합니다. 어설션 Windows Communication Foundation 제거 하지 않으면 (WCF) 정책 가져오기가 실패 했다고 가정 하 고 연결 된 바인딩을 가져오지 않습니다. <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=nameWithType> 메서드를 사용하여 사용자 지정 정책 어설션을 찾고 컬렉션에서 이를 한 번에 제거했다면 이 단계를 수행할 필요가 없습니다.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-a-configuration-file"></a>구성 파일을 사용하여 사용자 지정 정책 가져오기를 메타데이터 시스템에 삽입하려면  
  
1. 클라이언트 구성 파일에서 `<extensions>` [ \<policyimporters >](../../configure-apps/file-schema/wcf/policyimporters.md) 요소 내의 요소에 가져오기 형식을 추가 합니다.  
  
     [!code-xml[CustomPolicySample#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.exe.config#7)]   
  
2. 클라이언트 애플리케이션에서 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType>를 사용하여 메타데이터를 확인하면 해당 가져오기가 자동으로 호출됩니다.  
  
     [!code-csharp[CustomPolicySample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.cs#10)]
     [!code-vb[CustomPolicySample#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.vb#10)]  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-svcutilexe"></a>Svcutil.exe를 사용하여 사용자 지정 정책 가져오기를 메타데이터 시스템에 삽입하려면  
  
1. Svcutil.exe 구성 파일의 `<extensions>` [ \<policyimporters >](../../configure-apps/file-schema/wcf/policyimporters.md) 요소 내에 있는 요소에 가져오기 형식을 추가 합니다. 또한 `/svcutilConfig` 옵션을 사용하여 다른 구성 파일에서 등록된 정책 가져오기 형식을 로드하도록 Svcutil.exe를 지정할 수 있습니다.  
  
2. [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 메타 데이터를 가져오고, 가져오기가 자동으로 호출 됩니다.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-programmatically"></a>프로그래밍 방식으로 사용자 지정 정책 가져오기를 메타데이터 시스템에 삽입하려면  
  
1. 메타데이터를 가져오기 전에 가져오기를 <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A?displayProperty=nameWithType> 속성(예를 들어 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType>를 사용 중인 경우)에 추가합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>
- [메타데이터 시스템 확장](extending-the-metadata-system.md)
