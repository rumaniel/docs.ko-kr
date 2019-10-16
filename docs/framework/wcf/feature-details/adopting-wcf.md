---
title: Windows Communication Foundation 채택
ms.date: 03/30/2017
ms.assetid: 49ba71e2-9468-4082-84c5-cf8daf95e34a
ms.openlocfilehash: 58a51f7ea0db2297c7151a752de3f54307e0c5fd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857716"
---
# <a name="adopting-windows-communication-foundation"></a>Windows Communication Foundation 채택

ASP.NET을 사용 하 여 개발을 계속 기존 응용 프로그램을 유지 하는 동안 새로운 개발에 대 한 Windows Communication Foundation (WCF)를 사용 하도록 선택할 수 있습니다. 이기 때문에 WCF는 모든 시나리오에서.NET Framework로 빌드된 응용 프로그램을 사용 하 여 통신을 용이 하는 데 가장 적합을 제공할 수 있습니다. 다양 한 방식으로 소프트웨어 통신 문제를 해결 하기 위한 표준 도구로 ASP.NET 수 없습니다.

새 WCF 응용 프로그램은 기존 ASP.NET 웹 서비스와 동일한 컴퓨터에 배포할 수 있습니다. 기존 ASP.NET 웹 서비스의.NET Framework 버전 2.0 이전 버전을 사용 하는 경우 선택적으로 호스트 해야 하는 새 WCF 응용 프로그램에는 IIS 응용 프로그램에.NET Framework 2.0을 배포 하려면 ASP.NET IIS 등록 도구를 사용할 수 있습니다. 해당 도구에 설명 되어 있습니다 [ASP.NET IIS Registration Tool (Aspnet_regiis.exe)](https://go.microsoft.com/fwlink/?LinkId=94687), IIS 6.0 관리 콘솔에 사용자 인터페이스를 작성 합니다.

WCF는 IIS의 기존 ASP.NET 웹 서비스 응용 프로그램에 ASP.NET 호환 모드에서 실행 되도록 구성 하는 WCF 서비스를 추가 하 여 기존 ASP.NET 웹 서비스에 새 기능을 추가 하려면 사용할 수 있습니다. ASP.NET 호환성 모드로 인해 새 WCF 서비스에 대 한 코드 액세스를 사용 하 여 기존 ASP.NET 코드와 동일한 응용 프로그램 상태 정보를 업데이트 합니다 <xref:System.Web.HttpContext> 클래스입니다. 또한 애플리케이션은 동일한 클래스 라이브러리를 공유할 수도 있습니다.

WCF 클라이언트는 ASP.NET 웹 서비스를 사용할 수 있습니다. 구성 된 WCF 서비스는 <xref:System.ServiceModel.BasicHttpBinding> ASP.NET 웹 서비스 클라이언트에서 사용할 수 있습니다. ASP.NET 웹 서비스는 WCF 응용 프로그램과 공존할 수 있습니다 및 WCF을 사용 하 여 기존 ASP.NET 웹 서비스에 기능을 추가할 수도 있습니다. 모든는 WCF 및 ASP.NET 웹 서비스 함께 사용할 수 있는 다음과 같은 방법이으로, 있습니다 싶을 WCF 및 없습니다 ASP.NET 웹 서비스에서 제공 하는 기능을 사용 해야 하는 경우에 ASP.NET 웹 서비스를 WCF로 마이그레이션하려면입니다.

필요한 경우 몇 가지 경우에도 다른 기술 간에 코드를 마이그레이션하는 올바른 방법은 거의 없습니다. 새 기술을 채택하는 이유는 이전 기술로는 충족할 수 없는 새 요구 사항을 충족하기 위한 것이며, 이러한 경우 올바른 수행 작업은 새롭게 확장된 요구 사항 집합을 충족할 새 해결 방법을 디자인하는 것입니다. 새롭게 디자인할 경우 기존 시스템에 대한 사용자 경험과 시스템이 디자인된 이후 얻은 지식을 활용할 수 있습니다. 또한 새 플랫폼에서 기존 디자인을 재현하지 않고 새 기술의 전체 기능을 사용할 수도 있습니다. 새 디자인의 주요 요소를 프로토타입화하면 새 시스템 내에서 기존 시스템의 코드를 쉽게 다시 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [방법: 메타 데이터 검색 및 규격 서비스 구현](../../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md)
