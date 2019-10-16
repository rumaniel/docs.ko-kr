---
title: XMLSerializer 샘플
ms.date: 03/30/2017
ms.assetid: 7d134453-9a35-4202-ba77-9ca3a65babc3
ms.openlocfilehash: ae8e4f7c9be427ec5107318443816c8ade6c5085
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044479"
---
# <a name="xmlserializer-sample"></a>XMLSerializer 샘플
이 샘플에서는 <xref:System.Xml.Serialization.XmlSerializer>와 호환되는 형식을 serialize 및 deserialize하는 방법을 보여 줍니다. WCF (기본 Windows Communication Foundation) 포맷터 <xref:System.Runtime.Serialization.DataContractSerializer> 는 클래스입니다. <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용할 수 없는 경우 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스를 사용하여 형식을 serialize 및 deserialize할 수 있습니다. 이는 XML에 대한 정밀한 제어가 필요한 경우(예: 데이터의 일부가 XML 요소가 아닌 XML 특성이어야 하는 경우)에 자주 발생합니다. <xref:System.Xml.Serialization.XmlSerializer> 또한 WCF가 아닌 서비스에 대해 클라이언트를 만들 때가 자동으로 선택 됩니다.  
  
 이 샘플에서 클라이언트는 콘솔 응용 프로그램(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 다음 샘플 코드에서 보여 주는 것처럼 <xref:System.ServiceModel.ServiceContractAttribute> 및 <xref:System.ServiceModel.XmlSerializerFormatAttribute>가 인터페이스에 적용되어야 합니다.  
  
```csharp  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"), XmlSerializerFormat]  
public interface IXmlSerializerCalculator  
{  
    [OperationContract]  
    ComplexNumber Add(ComplexNumber n1, ComplexNumber n2);  
    [OperationContract]  
    ComplexNumber Subtract(ComplexNumber n1, ComplexNumber n2);  
    [OperationContract]  
    ComplexNumber Multiply(ComplexNumber n1, ComplexNumber n2);  
    [OperationContract]  
    ComplexNumber Divide(ComplexNumber n1, ComplexNumber n2);  
}  
```  
  
 `ComplexNumber` 클래스의 public 멤버는 <xref:System.Xml.Serialization.XmlSerializer>에 의해 XML 특성으로 serialize됩니다. 이러한 종류의 XML 인스턴스를 만들 때는 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용할 수 없습니다.  
  
```csharp  
public class ComplexNumber  
{  
    private double real;  
    private double imaginary;  
  
    [XmlAttribute]  
    public double Real  
    {  
        get { return real; }  
        set { real = value; }  
    }  
  
    [XmlAttribute]  
    public double Imaginary  
    {  
        get { return imaginary; }  
        set { imaginary = value; }  
    }  
  
    public ComplexNumber(double real, double imaginary)  
    {  
        this.Real = real;  
        this.Imaginary = imaginary;  
    }  
    public ComplexNumber()  
    {  
        this.Real = 0;  
        this.Imaginary = 0;  
    }  
  
}  
```  
  
 서비스 구현은 적절한 결과를 계산하여 반환합니다. 즉, `ComplexNumber` 형식의 값을 수락하고 반환합니다.  
  
```csharp  
public class XmlSerializerCalculatorService : IXmlSerializerCalculator  
{  
    public ComplexNumber Add(ComplexNumber n1, ComplexNumber n2)  
    {  
        return new ComplexNumber(n1.Real + n2.Real, n1.Imaginary +  
                                                      n2.Imaginary);  
    }  
    …  
}  
```  
  
 클라이언트 구현에서도 복소수가 사용됩니다. 서비스 계약과 데이터 형식은 모두 서비스 메타 데이터에서 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 에 의해 생성 된 generatedClient.cs 소스 파일에 정의 됩니다. Svcutil.exe는 계약이 <xref:System.Runtime.Serialization.DataContractSerializer>에 의해 serialize될 수 없는 경우를 감지할 수 있으며, 이 경우 `XmlSerializable` 형식 내보내기로 되돌아갑니다. 강제로 <xref:System.Xml.Serialization.XmlSerializer>를 사용하려는 경우 /serializer:XmlSerializer(XmlSerializer 사용) 명령 옵션을 Svcutil.exe 도구에 전달할 수 있습니다.  
  
```csharp  
// Create a client.  
XmlSerializerCalculatorClient client = new  
                         XmlSerializerCalculatorClient();  
  
// Call the Add service operation.  
ComplexNumber value1 = new ComplexNumber();  
value1.Real = 1;  
value1.Imaginary = 2;  
ComplexNumber value2 = new ComplexNumber();  
value2.Real = 3;  
value2.Imaginary = 4;  
ComplexNumber result = client.Add(value1, value2);  
Console.WriteLine("Add({0} + {1}i, {2} + {3}i) = {4} + {5}i",  
    value1.Real, value1.Imaginary, value2.Real, value2.Imaginary,   
    result.Real, result.Imaginary);  
    …  
}  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Add(1 + 2i, 3 + 4i) = 4 + 6i  
Subtract(1 + 2i, 3 + 4i) = -2 + -2i  
Multiply(2 + 3i, 4 + 7i) = -13 + 26i  
Divide(3 + 7i, 5 + -2i) = 0.0344827586206897 + 1.41379310344828i  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\Interop\XmlSerializer`  
