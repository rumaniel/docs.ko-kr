---
title: '방법: 사용자 지정 WSDL 가져오기'
ms.date: 03/30/2017
ms.assetid: ddc3718d-ce60-44f6-92af-a5c67477dd99
ms.openlocfilehash: 930cb92d8193ba3ffc1f62191f2012e104091190
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796997"
---
# <a name="how-to-import-custom-wsdl"></a>방법: 사용자 지정 WSDL 가져오기
이 항목에서는 사용자 지정 WSDL을 가져오는 방법에 대해 설명합니다. 사용자 지정 WSDL을 처리하려면 <xref:System.ServiceModel.Description.IWsdlImportExtension> 인터페이스를 구현해야 합니다.  
  
### <a name="to-import-custom-wsdl"></a>사용자 지정 WSDL을 가져오려면  
  
1. <xref:System.ServiceModel.Description.IWsdlImportExtension>를 구현해야 합니다. <xref:System.ServiceModel.Description.IWsdlImportExtension.BeforeImport%28System.Web.Services.Description.ServiceDescriptionCollection%2CSystem.Xml.Schema.XmlSchemaSet%2CSystem.Collections.Generic.ICollection%7BSystem.Xml.XmlElement%7D%29> 메서드를 구현하여 메타데이터를 가져오기 전에 수정합니다. <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportEndpoint%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlEndpointConversionContext%29> 및 <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> 메서드를 구현하여 메타데이터에서 가져온 계약과 엔드포인트를 수정합니다. 가져온 계약이나 엔드포인트에 액세스하려면 해당 컨텍스트 개체(<xref:System.ServiceModel.Description.WsdlContractConversionContext> 또는 <xref:System.ServiceModel.Description.WsdlEndpointConversionContext>)를 사용합니다.  
  
    ```  
    public class WsdlDocumentationImporter : IWsdlImportExtension  
       {  
          public void ImportContract(WsdlImporter importer, WsdlContractConversionContext context)  
    {  
            // Contract documentation  
         if (context.WsdlPortType.Documentation != null)  
         {  
               context.Contract.Behaviors.Add(new WsdlDocumentationImporter(context.WsdlPortType.Documentation));  
    }  
    // Operation documentation  
    foreach (Operation operation in context.WsdlPortType.Operations)  
    {  
    if (operation.Documentation != null)  
    {  
    OperationDescription operationDescription = context.Contract.Operations.Find(operation.Name);  
    if (operationDescription != null)  
    {  
                            operationDescription.Behaviors.Add(new WsdlDocumentationImporter(operation.Documentation));  
    }  
    }  
    }  
    }  
  
    public void BeforeImport(ServiceDescriptionCollection wsdlDocuments, XmlSchemaSet xmlSchemas, ICollection<XmlElement> policy)   
            {  
                Console.WriteLine("BeforeImport called.");  
            }  
  
    public void ImportEndpoint(WsdlImporter importer, WsdlEndpointConversionContext context)   
            {  
                Console.WriteLine("ImportEndpoint called.");  
            }  
       }  
    ```  
  
2. 사용자 지정 WSDL 가져오기를 사용하도록 클라이언트 애플리케이션을 구성합니다. Svcutil.exe를 사용하는 경우 Svcutil.exe(Svcutil.exe.config)의 구성 파일에 이 구성을 추가해야 합니다.  
  
    ```xml  
    <system.serviceModel>  
          <client>  
            <endpoint   
              address="http://localhost:8000/Fibonacci"   
              binding="wsHttpBinding"  
              contract="IFibonacci"  
            />  
            <metadata>  
              <wsdlImporters>  
                <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
              </wsdlImporters>  
            </metadata>  
          </client>  
        </system.serviceModel>  
    ```  
  
3. 새 <xref:System.ServiceModel.Description.WsdlImporter> 인스턴스(가져올 WSDL 문서를 포함하는 <xref:System.ServiceModel.Description.MetadataSet> 인스턴스에 전달)를 만들고 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>를 호출합니다.  
  
    ```  
    WsdlImporter importer = new WsdlImporter(metaDocs);          System.Collections.ObjectModel.Collection<ContractDescription> contracts  = importer.ImportAllContracts();  
    ```  
  
## <a name="see-also"></a>참고자료

- [메타데이터](../feature-details/metadata.md)
- [메타데이터 내보내기 및 가져오기](../feature-details/exporting-and-importing-metadata.md)
- [사용자 지정 WSDL 게시](../samples/custom-wsdl-publication.md)
