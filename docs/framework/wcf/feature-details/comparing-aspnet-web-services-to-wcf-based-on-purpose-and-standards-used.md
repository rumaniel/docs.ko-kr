---
title: 용도와 사용되는 표준을 기반으로 ASP.NET 웹 서비스와 WCF 비교
ms.date: 03/30/2017
ms.assetid: d3890278-fa9b-4902-91ea-8da73b7143cc
ms.openlocfilehash: f57e895680b5cc043dad365b9f25f32477f42e72
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62048064"
---
# <a name="comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used"></a>용도와 사용되는 표준을 기반으로 ASP.NET 웹 서비스와 WCF 비교
ASP.NET Web 서비스는 HTTP에서 SOAP(Simple Object Access Protocol)를 사용하여 메시지를 보내고 받는 애플리케이션을 빌드하기 위해 개발되었습니다. 메시지 구조는 XML 스키마를 사용하여 정의할 수 있으며 메시지를 .NET Framework 개체로 또는 그 반대로 쉽게 serialize하기 위한 도구가 제공됩니다. 이 기술은 자동으로 메타데이터를 생성하여 WSDL(웹 서비스 기술 언어)로 웹 서비스를 설명할 수 있으며 WSDL에서 웹 서비스용 클라이언트를 생성하기 위한 두 번째 도구가 제공됩니다.  
  
 WCF는 다른 소프트웨어 엔터티와 메시지를 교환 하는.NET Framework 응용 프로그램입니다. 기본적으로 SOAP가 사용되지만 메시지는 임의의 형식일 수 있으며 모든 전송 프로토콜을 사용하여 전달할 수 있습니다. 메시지 구조는 XML 스키마를 사용하여 정의할 수 있으며 메시지를 .NET Framework 개체로 또는 그 반대로 쉽게 serialize하기 위한 다양한 옵션이 제공됩니다. WCF wsdl에서 기술을 사용 하 여 빌드된 응용 프로그램을 설명 하는 메타 데이터를 자동으로 생성할 수 있습니다. 또한 WSDL에서 이러한 응용 프로그램에 대 한 클라이언트를 생성 하기 위한 도구를 제공 하며  
  
 ASP.NET 웹 서비스에서 지 원하는 표준에 설명 되어 있습니다 [XML Web Services Created Using ASP.NET](https://go.microsoft.com/fwlink/?LinkId=94872)합니다. 표준 WCF에서 지 원하는 더 광범위 한 목록에 나열 됩니다 [웹 서비스 프로토콜에서 지 원하는 시스템 제공 상호 운용성 바인딩에서](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [개발을 기반으로 ASP.NET 웹 서비스와 WCF 비교](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)
