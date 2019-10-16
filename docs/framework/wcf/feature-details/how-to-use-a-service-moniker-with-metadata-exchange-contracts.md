---
title: '방법: 메타데이터 교환 계약을 통해 서비스 모니커 사용'
ms.date: 03/30/2017
ms.assetid: c41a07e5-cb9d-45d6-9ea4-34511e227faf
ms.openlocfilehash: e114bc2c046ba7145a91121ce23c82912680a048
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70968956"
---
# <a name="how-to-use-a-service-moniker-with-metadata-exchange-contracts"></a>방법: 메타데이터 교환 계약을 통해 서비스 모니커 사용
몇 가지 새로운 WCF 서비스를 개발한 후 스크립트나 Visual Basic 6.0 응용 프로그램에서 이러한 서비스를 호출할 수 있도록 결정할 수 있습니다. 한 가지 방법은 WCF 클라이언트 어셈블리를 생성 하 고, 어셈블리를 COM에 등록 하 고, GAC에 어셈블리를 설치한 다음 Visual Basic 코드에서 COM 형식을 참조 하는 것입니다. 응용 프로그램을 배포 하는 경우 WCF 클라이언트 어셈블리도 함께 배포 해야 합니다. 사용자는 WCF 클라이언트 어셈블리를 COM에 등록하고 GAC에 배치해야 합니다. Wcf COM Interop를 사용 하면 WCF 클라이언트 어셈블리에 의존 하지 않고 동일한 서비스 호출을 수행할 수도 있습니다. WCF 모니커를 사용 하면 서비스 모니커가 형식을 추출 하는 데 사용 하는 Mex (metadata exchange) 끝점 URI를 지정 하 여 COM 호환 언어 (Visual Basic, VBScript, Visual Basic for Applications (VBA) 등)에서 WCF 서비스를 호출할 수 있습니다. 서비스에 대 한 정보입니다. 이 항목에서는 Mex 끝점을 지정 하는 WCF 모니커를 사용 하 여 WCF 시작 샘플을 호출 하는 방법을 설명 합니다.  
  
> [!NOTE]
> WCF 클라이언트 어셈블리에 의해 정의 된 형식은 실제로 인스턴스화되지 않습니다. 어셈블리는 메타데이터에만 사용됩니다.  
  
### <a name="using-the-service-moniker-with-a-mex-address"></a>서비스 모니커에 Mex 주소 사용  
  
1. 시작 샘플을 빌드하고 Internet Explorer를 사용 하 여 해당 URL http://localhost/ServiceModelSamples/Service.svc) 로 이동 하 여 서비스가 작동 하는지 확인 합니다.  
  
2. 다음 코드가 포함된 Visual Basic 스크립트 또는 Visual Basic 애플리케이션을 만듭니다.  
  
    ```vb
    monString = "service:mexaddress=http://localhost/ServiceModelSamples/Service.svc/MEX"  
    monString = monString + ", address=http://localhost/ServiceModelSamples/Service.svc"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set calc = GetObject(monString)  
    MsgBox calc.Add(3, 4)  
    ```  
  
3. Visual Basic 애플리케이션 또는 스크립트를 실행합니다.  
  
    > [!NOTE]
    > 모니커가 서비스에서 메타데이터를 읽을 수 있도록 하려면 호출 중인 서비스가 Mex 엔드포인트를 노출해야 합니다. 자세한 내용은 [방법: 구성 파일](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)을 사용 하 여 서비스에 대 한 메타 데이터를 게시 합니다.  
  
    > [!NOTE]
    > 모니커의 형식이 잘못되었거나 서비스를 사용할 수 없는 경우 `GetObject`를 호출하면 "구문이 잘못되었습니다."라는 오류가 반환됩니다.  이 오류가 발생하면 사용하고 있는 모니커가 올바르고 서비스를 사용할 수 있는지 확인하세요.  
  
## <a name="see-also"></a>참고자료

- [방법: 등록 하지 않고 Windows Communication Foundation 서비스 모니커 사용](../../../../docs/framework/wcf/feature-details/use-the-wcf-service-moniker-without-registration.md)
- [방법: WSDL 계약을 통해 서비스 모니커 사용](../../../../docs/framework/wcf/feature-details/how-to-use-a-service-moniker-with-wsdl-contracts.md)
