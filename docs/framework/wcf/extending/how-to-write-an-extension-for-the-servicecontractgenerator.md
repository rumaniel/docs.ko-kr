---
title: '방법: ServiceContractGenerator에 대한 확장 쓰기'
ms.date: 03/30/2017
ms.assetid: 876ca823-bd16-4bdf-9e0f-02092df90e51
ms.openlocfilehash: af23babd9255c45b9fa89b5c167de6960f0f690e
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855717"
---
# <a name="how-to-write-an-extension-for-the-servicecontractgenerator"></a>방법: ServiceContractGenerator에 대한 확장 쓰기
이 항목에서는 <xref:System.ServiceModel.Description.ServiceContractGenerator>에 대한 확장을 쓰는 방법에 대해 설명합니다. 이 작업을 수행하려면 작업 동작에 <xref:System.ServiceModel.Description.IOperationContractGenerationExtension> 인터페이스를 구현하거나 계약 동작에 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> 인터페이스를 구현합니다. 다음 항목에서는 계약 동작에서 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> 인터페이스를 구현하는 방법을 보여 줍니다.  
  
 <xref:System.ServiceModel.Description.ServiceContractGenerator>는 <xref:System.ServiceModel.Description.ServiceEndpoint>, <xref:System.ServiceModel.Description.ContractDescription> 및 <xref:System.ServiceModel.Channels.Binding> 인스턴스에서 서비스 계약, 클라이언트 형식 및 클라이언트 구성을 생성합니다. 일반적으로 서비스 메타데이터에서 <xref:System.ServiceModel.Description.ServiceEndpoint>, <xref:System.ServiceModel.Description.ContractDescription> 및 <xref:System.ServiceModel.Channels.Binding> 인스턴스를 가져온 다음 이러한 인스턴스를 사용하여 서비스를 호출할 코드를 생성합니다. 이 예제에서 <xref:System.ServiceModel.Description.IWsdlImportExtension> 구현은 생성된 코드에 주석을 생성하기 위해 WSDL 주석을 처리한 다음 가져온 계약에 코드 생성 확장을 추가하는 데 사용됩니다.  
  
### <a name="to-write-an-extension-for-the-servicecontractgenerator"></a>ServiceContractGenerator에 대한 확장을 쓰려면  
  
1. <xref:System.ServiceModel.Description.IServiceContractGenerationExtension>를 구현해야 합니다. 생성된 서비스 계약을 수정하려면 <xref:System.ServiceModel.Description.ServiceContractGenerationContext> 메서드로 전달된 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> 인스턴스를 사용합니다.  
  
    ```csharp
    public void GenerateContract(ServiceContractGenerationContext context)  
    {  
        Console.WriteLine("In generate contract.");  
    context.ContractType.Comments.AddRange(Formatter.FormatComments(commentText));  
    }  
    ```  
  
2. 같은 클래스에서 <xref:System.ServiceModel.Description.IWsdlImportExtension>을 구현합니다. <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> 메서드는 가져온 <xref:System.ServiceModel.Description.ContractDescription> 인스턴스에 코드 생성 확장을 추가하여 특정 WSDL 확장(이 경우 WSDL 주석)을 처리할 수 있습니다.  
  
    ```csharp
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
    ```  
  
3. 클라이언트 구성에 WSDL 가져오기를 추가합니다.  
  
    ```xml  
    <metadata>  
      <wsdlImporters>  
        <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
      </wsdlImporters>  
    </metadata>  
    ```  
  
4. 클라이언트 코드에 `MetadataExchangeClient`를 만들고 `GetMetadata`를 호출합니다.  
  
    ```csharp  
    MetadataExchangeClient mexClient = new MetadataExchangeClient(metadataAddress);  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet metaDocs = mexClient.GetMetadata();  
    ```  
  
5. `WsdlImporter`를 만들고 `ImportAllContracts`를 호출합니다.  
  
    ```csharp  
    WsdlImporter importer = new WsdlImporter(metaDocs);            System.Collections.ObjectModel.Collection<ContractDescription> contracts = importer.ImportAllContracts();  
    ```  
  
6. `ServiceContractGenerator`를 만들고 각 계약에 대한 `GenerateServiceContractType`을 호출합니다.  
  
    ```csharp  
    ServiceContractGenerator generator = new ServiceContractGenerator();  
    foreach (ContractDescription contract in contracts)  
    {  
       generator.GenerateServiceContractType(contract);  
    }  
    if (generator.Errors.Count != 0)  
       throw new Exception("There were errors during code compilation.");  
    ```  
  
7. <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29>는 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension>을 구현하는 제공된 계약에서 각 계약 동작에 대해 자동으로 호출됩니다. 그런 다음 이 메서드는 전달된 <xref:System.ServiceModel.Description.ServiceContractGenerationContext>를 수정할 수 있습니다. 이 예제에서는 주석이 추가되었습니다.  
  
## <a name="see-also"></a>참고자료

- [메타데이터](../feature-details/metadata.md)
- [방법: 사용자 지정 WSDL 가져오기](how-to-import-custom-wsdl.md)
