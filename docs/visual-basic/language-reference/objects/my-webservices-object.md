---
title: WebServices 개체 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- My.WebServices
- My.MyProject.WebServices
helpviewer_keywords:
- My.WebServices object
ms.assetid: f188dc05-2c75-41b6-bb68-122d1c3110a2
ms.openlocfilehash: c887f9b7c5a41c0aa02016354c46d5507b103d25
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918176"
---
# <a name="mywebservices-object"></a>My.WebServices 개체
현재 프로젝트에서 참조 하는 각 XML Web services의 단일 인스턴스를 만들고 액세스 하기 위한 속성을 제공 합니다.  
  
## <a name="remarks"></a>설명  
 `My.WebServices` 개체는 현재 프로젝트에서 참조하는 각 웹 서비스의 인스턴스를 제공합니다. 필요에 따라 각 인스턴스가 인스턴스화됩니다. `My.WebServices` 개체의 속성을 통해 이러한 웹 서비스에 액세스할 수 있습니다. 속성 이름은 속성이 액세스하는 웹 서비스의 이름과 같습니다. <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>에서 상속되는 모든 클래스는 웹 서비스입니다. 프로젝트에 웹 서비스를 추가 하는 방법에 대 한 자세한 내용은 [응용 프로그램 웹 서비스 액세스](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)를 참조 하세요.  
  
 개체 `My.WebServices` 는 현재 프로젝트와 연결 된 웹 서비스만 노출 합니다. 참조 된 Dll에 선언 된 웹 서비스에 대 한 액세스는 제공 하지 않습니다. DLL이 제공 하는 웹 서비스에 액세스 하려면 웹 서비스의 정규화 된 이름을 *DllName*형식으로 사용 해야 합니다. *Webservicename*. 자세한 내용은 [응용 프로그램 웹 서비스 액세스](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)를 참조 하세요.  
  
 개체와 해당 속성은 웹 응용 프로그램에 사용할 수 없습니다.  
  
## <a name="properties"></a>속성  
 `My.WebServices` 개체의 각 속성은 현재 프로젝트에서 참조 하는 웹 서비스의 인스턴스에 대 한 액세스를 제공 합니다. 속성의 이름은 속성이 액세스 하는 웹 서비스의 이름과 동일 하며, 속성 형식이 웹 서비스의 형식과 동일 합니다.  
  
> [!NOTE]
> 이름 충돌이 있는 경우 웹 서비스에 액세스 하기 위한 속성 이름은 *RootNamespace*_*Namespace*\_*ServiceName*입니다. 예를 들어 라는 `Service1`두 개의 웹 서비스를 가정 합니다. 이러한 서비스 중 하나가 루트 네임 `WindowsApplication1` 스페이스 및 네임 스페이스 `Namespace1`에 있는 경우를 사용 `My.WebServices.WindowsApplication1_Namespace1_Service1`하 여 해당 서비스에 액세스 합니다.  
  
 `My.WebServices` 개체의 속성 중 하나에 처음으로 액세스 하는 경우 웹 서비스의 새 인스턴스를 만들어 저장 합니다. 해당 속성에 대 한 후속 액세스는 웹 서비스의 인스턴스를 반환 합니다.  
  
 웹 서비스의 속성에를 할당 `Nothing` 하 여 웹 서비스를 삭제할 수 있습니다. 속성 setter는 저장 `Nothing` 된 값에을 할당 합니다. 속성 `Nothing` 에 이외의 값을 할당 하면 setter가 <xref:System.ArgumentException> 예외를 throw 합니다.  
  
 또는 `My.WebServices` `Is` 연산자를 사용 하 여 개체의 속성이 웹 서비스의 인스턴스를 저장 하는지 여부를 테스트할 수 있습니다. `IsNot` 이러한 연산자를 사용 하 여 속성 값이 인지 `Nothing`확인할 수 있습니다.  
  
> [!NOTE]
> 일반적으로 또는 `Is` `IsNot` 연산자는 비교를 수행 하기 위해 속성의 값을 읽어야 합니다. 그러나 속성이 현재 저장 `Nothing`된 경우 속성은 웹 서비스의 새 인스턴스를 만든 다음 해당 인스턴스를 반환 합니다. 그러나 Visual Basic 컴파일러는 `My.WebServices` 개체의 속성을 특수 하 게 처리 하 고 `Is` 또는 `IsNot` 연산자가 해당 값을 변경 하지 않고 속성의 상태를 확인할 수 있도록 허용 합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 `TemperatureConverter` XML `FahrenheitToCelsius` Web services의 메서드를 호출 하 고 결과를 반환 합니다.  
  
 [!code-vb[VbVbalrMyWebService#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyWebService/VB/Form1.vb#1)]  
  
 이 예제가 작동 하려면 프로젝트가 이라는 `Converter`웹 서비스를 참조 해야 하 고 웹 서비스에서 메서드를 `ConvertTemperature` 노출 해야 합니다. 자세한 내용은 [응용 프로그램 웹 서비스 액세스](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)를 참조 하세요.  
  
 이 코드는 웹 응용 프로그램 프로젝트에서 작동 하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
  
### <a name="availability-by-project-type"></a>프로젝트 형식에 따라 가용성  
  
|프로젝트 형식|사용 가능|  
|---|---|  
|Windows 애플리케이션|**예**|  
|클래스 라이브러리|**예**|  
|콘솔 애플리케이션|**예**|  
|Windows 컨트롤 라이브러리|**예**|  
|웹 컨트롤 라이브러리|**예**|  
|Windows 서비스|**예**|  
|웹 사이트|아니요|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>
- <xref:System.ArgumentException>
- [응용 프로그램 웹 서비스 액세스](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)
