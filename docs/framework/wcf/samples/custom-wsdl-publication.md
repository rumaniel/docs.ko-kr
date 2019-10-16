---
title: 사용자 지정 WSDL 게시
ms.date: 03/30/2017
ms.assetid: 3b3e8103-2c95-4db3-a05b-46aa8e9d4d29
ms.openlocfilehash: 8674d852be45119b247ec10bbc639922850d5a90
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928845"
---
# <a name="custom-wsdl-publication"></a>사용자 지정 WSDL 게시
이 샘플을 통해 다음을 수행하는 방법을 알 수 있습니다.  
  
- <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType>을 사용자 지정 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> 특성에 구현하여 특성 속성을 WSDL 주석으로 내보내기.  
  
- <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType>을 구현하여 사용자 지정 WSDL 주석 가져오기.  
  
- 사용자 지정 계약 동작과 사용자 지정 작업 동작에 각각 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension?displayProperty=nameWithType> 및 <xref:System.ServiceModel.Description.IOperationContractGenerationExtension?displayProperty=nameWithType>을 구현하여 가져온 주석을 가져온 계약 및 작업의 CodeDOM에 주석으로 씁니다.  
  
- 을 사용 하 여 wsdl을 다운로드 하 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> 고,를 사용 하 여 사용자 지정 wsdl 가져오기를 사용 하 여 wsdl을 가져오고,를 사용 하 여 및에서 C# wsdl 주석이///및 ' ' ' 주석으로 Windows Communication Foundation (WCF) 클라이언트 코드를 생성 합니다 <xref:System.ServiceModel.Description.ServiceContractGenerator?displayProperty=nameWithType>. <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> Visual Basic.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
## <a name="service"></a>서비스  
 이 샘플의 서비스에는 두 개의 사용자 지정 특성이 표시되어 있습니다. 첫 특성인 `WsdlDocumentationAttribute`에서는 생성자의 문자열을 받으며 적용하면 사용을 설명하는 문자열에 계약 인터페이스 또는 작업을 제공할 수 있습니다. 둘째 특성인 `WsdlParamOrReturnDocumentationAttribute`는 적용하면 작업의 값을 설명하는 값 또는 매개 변수를 반환할 수 있습니다. 다음 예에서는 이 특성을 사용하여 설명한 서비스 계약인 `ICalculator`가 표시됩니다.  
  
```csharp  
// Define a service contract.      
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
// Document it.  
[WsdlDocumentation("The ICalculator contract performs basic calculation services.")]  
public interface ICalculator  
{  
    [OperationContract]  
    [WsdlDocumentation("The Add operation adds two numbers and returns the result.")]  
    [return:WsdlParamOrReturnDocumentation("The result of adding the two arguments together.")]  
    double Add(  
      [WsdlParamOrReturnDocumentation("The first value to add.")]double n1,   
      [WsdlParamOrReturnDocumentation("The second value to add.")]double n2  
    );  
  
    [OperationContract]  
    [WsdlDocumentation("The Subtract operation subtracts the second argument from the first.")]  
    [return:WsdlParamOrReturnDocumentation("The result of the second argument subtracted from the first.")]  
    double Subtract(  
      [WsdlParamOrReturnDocumentation("The value from which the second is subtracted.")]double n1,   
      [WsdlParamOrReturnDocumentation("The value that is subtracted from the first.")]double n2  
    );  
  
    [OperationContract]  
    [WsdlDocumentation("The Multiply operation multiplies two values.")]  
    [return:WsdlParamOrReturnDocumentation("The result of multiplying the first and second arguments.")]  
    double Multiply(  
      [WsdlParamOrReturnDocumentation("The first value to multiply.")]double n1,   
      [WsdlParamOrReturnDocumentation("The second value to multiply.")]double n2  
    );  
  
    [OperationContract]  
    [WsdlDocumentation("The Divide operation returns the value of the first argument divided by the second argument.")]  
    [return:WsdlParamOrReturnDocumentation("The result of dividing the first argument by the second.")]  
    double Divide(  
      [WsdlParamOrReturnDocumentation("The numerator.")]double n1,   
      [WsdlParamOrReturnDocumentation("The denominator.")]double n2  
    );  
}  
```  
  
 `WsdlDocumentationAttribute`에서는 <xref:System.ServiceModel.Description.IContractBehavior> 및 <xref:System.ServiceModel.Description.IOperationBehavior>를 구현하기 때문에 서비스를 열면 특성 인스턴스가 해당 <xref:System.ServiceModel.Description.ContractDescription> 또는 <xref:System.ServiceModel.Description.OperationDescription>에 추가됩니다. 특성에서는 <xref:System.ServiceModel.Description.IWsdlExportExtension>도 구현합니다. <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%28System.ServiceModel.Description.WsdlExporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29>가 호출되면 메타데이터를 내보내는 데 사용되는 <xref:System.ServiceModel.Description.WsdlExporter>와 서비스 설명 개체가 포함된 <xref:System.ServiceModel.Description.WsdlContractConversionContext>가 매개 변수로 저장되어 내보낸 메타데이터의 수정을 사용할 수 있게 됩니다.  
  
 이 샘플에서는 내보내기 컨텍스트 개체에 <xref:System.ServiceModel.Description.ContractDescription> 또는 <xref:System.ServiceModel.Description.OperationDescription>가 있는지 여부에 따라 텍스트 속성을 사용하여 주석이 추출되고 다음 코드에 표시된 것과 같이 WSDL 주석 요소에 추가됩니다.  
  
```csharp  
public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)  
{  
    if (contractDescription != null)  
    {  
        // Inside this block it is the contract-level comment attribute.  
        // This.Text returns the string for the contract attribute.  
        // Set the doc element; if this isn't done first, there is no XmlElement in the   
        // DocumentElement property.  
        context.WsdlPortType.Documentation = string.Empty;  
        // Contract comments.  
        XmlDocument owner = context.WsdlPortType.DocumentationElement.OwnerDocument;  
        XmlElement summaryElement = owner.CreateElement("summary");  
        summaryElement.InnerText = this.Text;  
        context.WsdlPortType.DocumentationElement.AppendChild(summaryElement);  
    }  
    else  
    {  
        Operation operation = context.GetOperation(operationDescription);  
        if (operation != null)  
        {  
            // We are dealing strictly with the operation here.  
            // This.Text returns the string for the operation-level attributes.  
            // Set the doc element; if this isn't done first, there is no XmlElement in the   
            // DocumentElement property.  
            operation.Documentation = String.Empty;  
  
            // Operation C# triple comments.  
            XmlDocument owner = operation.DocumentationElement.OwnerDocument;  
            XmlElement newSummaryElement = owner.CreateElement("summary");  
            newSummaryElement.InnerText = this.Text;  
            operation.DocumentationElement.AppendChild(newSummaryElement);  
```  
  
 작업을 내보내는 경우 샘플에서는 반영을 사용하여 매개 변수 및 반환 값의 `WsdlParamOrReturnDocumentationAttribute` 값을 가져온 다음 다음과 같이 해당 작업에 WSDL 주석 요소를 추가합니다.  
  
```csharp  
// Get returns information  
ParameterInfo returnValue = operationDescription.SyncMethod.ReturnParameter;  
object[] returnAttrs = returnValue.GetCustomAttributes(typeof(WsdlParamOrReturnDocumentationAttribute), false);  
if (returnAttrs.Length != 0)  
{  
    // <returns>text.</returns>  
    XmlElement returnsElement = owner.CreateElement("returns");  
    returnsElement.InnerText = ((WsdlParamOrReturnDocumentationAttribute)returnAttrs[0]).ParamComment;  
    operation.DocumentationElement.AppendChild(returnsElement);  
}  
  
// Get parameter information.  
ParameterInfo[] args = operationDescription.SyncMethod.GetParameters();  
for (int i = 0; i < args.Length; i++)  
{  
    object[] docAttrs = args[i].GetCustomAttributes(typeof(WsdlParamOrReturnDocumentationAttribute), false);  
    if (docAttrs.Length == 1)  
    {  
        // <param name="Int1">Text.</param>  
        XmlElement newParamElement = owner.CreateElement("param");  
        XmlAttribute paramName = owner.CreateAttribute("name");  
        paramName.Value = args[i].Name;  
        newParamElement.InnerText = ((WsdlParamOrReturnDocumentationAttribute)docAttrs[0]).ParamComment;  
        newParamElement.Attributes.Append(paramName);  
        operation.DocumentationElement.AppendChild(newParamElement);  
    }  
}  
```  
  
 그 후 샘플에서는 다음 구성 파일을 사용해서 메타데이터를 표준적인 방법으로 게시합니다.  
  
```xml  
<services>  
  <service   
      name="Microsoft.ServiceModel.Samples.CalculatorService"  
      behaviorConfiguration="CalculatorServiceBehavior">  
    <!-- ICalculator is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    <!-- the mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->  
    <endpoint address="mex"  
              binding="mexHttpBinding"  
              contract="IMetadataExchange" />  
  </service>  
</services>  
  
<!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="svcutil-client"></a>Svcutil 클라이언트  
 이 샘플에서는 Svcutil.exe를 사용하지 않습니다. 계약은 샘플에서 사용자 지정 WSDL 가져오기 및 코드 생성을 보여 준 후에 서비스를 호출할 수 있도록 generatedClient.cs 파일에 제공됩니다. 이 예에 다음 사용자 지정 WSDL 가져오기를 사용할 수 있도록 Svcutil.exe를 실행하고 `/svcutilConfig` 옵션을 지정하여 `WsdlDocumentation.dll` 라이브러리를 참조하며 이 샘플에 사용된 클라이언트 구성 파일의 경로를 지정할 수 있습니다. 하지만 `WsdlDocumentationImporter`를 로드하려면 Svuctil.exe에서 `WsdlDocumentation.dll` 라이브러리를 찾아 로드할 수 있어야 합니다. 즉 전역 어셈블리 캐시 또는 경로에 등록되어 있거나 Svcutil.exe와 같은 디렉터리에 있어야 합니다. 이와 같은 기본 샘플의 경우 가장 쉽게 수행할 수 있는 일은 Svcutil.exe와 클라이언트 구성 파일을 `WsdlDocumentation.dll`과 같은 디렉터리에 복사한 다음 그 위치에서 실행하는 것입니다.  
  
## <a name="the-custom-wsdl-importer"></a>사용자 지정 WSDL 가져오기  
 사용자 지정 <xref:System.ServiceModel.Description.IWsdlImportExtension> 개체 `WsdlDocumentationImporter`에서는 가져온 ServiceEndpoints에 추가할 <xref:System.ServiceModel.Description.IContractBehavior> 및 <xref:System.ServiceModel.Description.IOperationBehavior>와 계약 또는 작업 코드를 만들 때 코드 생성을 수정하기 위해 호출할 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> 및 <xref:System.ServiceModel.Description.IOperationContractGenerationExtension>도 구현합니다.  
  
 먼저, <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> 메서드에서 샘플은 WSDL 주석이 계약 수준과 작업 수준 중 어느 쪽에 있는지를 확인하고 가져온 주석 텍스트를 생성자에 전달하며 적절한 범위에서 동작을 추가합니다.  
  
```csharp  
public void ImportContract(WsdlImporter importer, WsdlContractConversionContext context)  
{  
    // Contract Documentation  
    if (context.WsdlPortType.Documentation != null)  
    {  
        // System examines the contract behaviors to see whether any implement IWsdlImportExtension.  
        context.Contract.Behaviors.Add(new WsdlDocumentationImporter(context.WsdlPortType.Documentation));  
    }  
    // Operation Documentation  
    foreach (Operation operation in context.WsdlPortType.Operations)  
    {  
        if (operation.Documentation != null)  
        {  
            OperationDescription operationDescription = context.Contract.Operations.Find(operation.Name);  
            if (operationDescription != null)  
            {  
                // System examines the operation behaviors to see whether any implement IWsdlImportExtension.  
                operationDescription.Behaviors.Add(new WsdlDocumentationImporter(operation.Documentation));  
            }  
        }  
    }  
}  
```  
  
 그런 다음, 코드가 생성되면 시스템에서 적절한 컨텍스트 정보를 전달하여 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> 및 <xref:System.ServiceModel.Description.IOperationContractGenerationExtension.GenerateOperation%28System.ServiceModel.Description.OperationContractGenerationContext%29> 메서드를 호출합니다. 샘플에서는 사용자 지정 WSDL 주석의 서식을 지정하고 CodeDOM에 주석으로 삽입합니다.  
  
```csharp  
public void GenerateContract(ServiceContractGenerationContext context)  
{  
    Debug.WriteLine("In generate contract.");  
    context.ContractType.Comments.AddRange(FormatComments(text));  
}  
  
public void GenerateOperation(OperationContractGenerationContext context)  
{  
    context.SyncMethod.Comments.AddRange(FormatComments(text));  
    Debug.WriteLine("In generate operation.");  
}  
```  
  
## <a name="the-client-application"></a>클라이언트 애플리케이션  
 클라이언트 애플리케이션에서는 애플리케이션 구성 파일에 사용자 지정 WSDL 가져오기를 지정하여 로드합니다.  
  
```xml  
<client>  
  <endpoint address="http://localhost/servicemodelsamples/service.svc"   
  binding="wsHttpBinding"   
  contract="ICalculator" />  
  <metadata>  
    <wsdlImporters>  
      <extension type="Microsoft.ServiceModel.Samples.WsdlDocumentationImporter, WsdlDocumentation"/>  
    </wsdlImporters>  
  </metadata>  
</client>  
```  
  
 사용자 지정 가져오기가 지정 된 후에는 WCF 메타 데이터 시스템에서 사용자 지정 가져오기를 해당 목적 <xref:System.ServiceModel.Description.WsdlImporter> 으로 만든에 로드 합니다. 이 샘플에서는 <xref:System.ServiceModel.Description.MetadataExchangeClient>를 사용하여 메타데이터를 다운로드하고, 올바르게 구성된 <xref:System.ServiceModel.Description.WsdlImporter>를 사용하여 샘플로 만든 사용자 지정 가져오기를 통해 메타데이터를 가져오고, <xref:System.ServiceModel.Description.ServiceContractGenerator>를 사용하여 Visual Studio에서 Intellisense 지원을 위해 사용하거나 XML 문서에 컴파일할 수 있는 Visual Basic 및 C# 클라이언트 코드로 수정된 계약 정보를 컴파일합니다.  
  
```csharp  
/// From WSDL Documentation:  
///   
/// <summary>The ICalculator contract performs basic calculation   
/// services.</summary>   
///   
[System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "3.0.0.0")]  
[System.ServiceModel.ServiceContractAttribute(Namespace="http://Microsoft.ServiceModel.Samples", ConfigurationName="ICalculator")]  
public interface ICalculator  
{  
  
    /// From WSDL Documentation:  
    ///   
    /// <summary>The Add operation adds two numbers and returns the   
    /// result.</summary><returns>The result of adding the two arguments   
    /// together.</returns><param name="n1">The first value to add.</param><param   
    /// name="n2">The second value to add.</param>   
    ///   
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Add", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/AddResponse")]  
    double Add(double n1, double n2);  
  
    /// From WSDL Documentation:  
    ///   
    /// <summary>The Subtract operation subtracts the second argument from the   
    /// first.</summary><returns>The result of the second argument subtracted from the   
    /// first.</returns><param name="n1">The value from which the second is   
    /// subtracted.</param><param name="n2">The value that is subtracted from the   
    /// first.</param>   
    ///   
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Subtract", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/SubtractResponse")]  
    double Subtract(double n1, double n2);  
  
    /// From WSDL Documentation:  
    ///   
    /// <summary>The Multiply operation multiplies two values.</summary><returns>The   
    /// result of multiplying the first and second arguments.</returns><param   
    /// name="n1">The first value to multiply.</param><param name="n2">The second value   
    /// to multiply.</param>   
    ///   
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Multiply", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/MultiplyResponse")]  
    double Multiply(double n1, double n2);  
  
    /// From WSDL Documentation:  
    ///   
    /// <summary>The Divide operation returns the value of the first argument divided   
    /// by the second argument.</summary><returns>The result of dividing the first   
    /// argument by the second.</returns><param name="n1">The numerator.</param><param   
    /// name="n2">The denominator.</param>   
    ///   
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Divide", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/DivideResponse")]  
    double Divide(double n1, double n2);  
}  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Metadata\WsdlDocumentation`  
