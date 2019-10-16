---
title: 보안 및 원격 서비스 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- code security, remoting
- remoting, security
- security [.NET Framework], remoting
- secure coding, remoting
ms.assetid: 125d2ab8-55a4-4e5f-af36-a7d401a37ab0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2d4d3b009e5792685ea39a3bcc2a15e082e1b8de
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70206091"
---
# <a name="security-and-remoting-considerations"></a>보안 및 원격 서비스 고려 사항
원격 기능을 사용하면 애플리케이션 도메인, 프로세스 또는 컴퓨터 간에 투명한 호출을 설정할 수 있습니다. 그러나 코드 액세스 보안 스택 워크는 프로세스 또는 시스템 경계를 넘어갈 수 없습니다(동일한 프로세스의 애플리케이션 도메인 간에 적용됨).  
  
 원격으로 사용 가능한(<xref:System.MarshalByRefObject> 클래스에서 파생된) 모든 클래스는 보안을 책임져야 합니다. 호출하는 코드를 암시적으로 신뢰할 수 있는 폐쇄된 환경에서만 코드를 사용해야 하거나, 악의적으로 사용될 수 있는 외부 입력이 보호된 코드에 적용되지 않도록 원격 호출을 설계해야 합니다.  
  
 일반적으로 선언적 [LinkDemand](link-demands.md) 및 <xref:System.Security.Permissions.SecurityAction.InheritanceDemand> 보안 검사로 보호 되는 메서드, 속성 또는 이벤트를 노출 하면 안 됩니다. 원격 기능에서는 이러한 검사가 적용되지 않습니다. <xref:System.Security.Permissions.SecurityAction.Demand>, [Assert](using-the-assert-method.md)등의 다른 보안 검사는 프로세스 내의 응용 프로그램 도메인 간에는 작동 하지만 크로스 프로세스 또는 크로스 시스템 시나리오에서는 작동 하지 않습니다.  
  
## <a name="protected-objects"></a>보호되는 개체  
 일부 개체는 그 자체에 보안 상태를 포함합니다. 고유한 권한 이상의 보안 권한이 부여되지 않도록 신뢰할 수 없는 코드에는 이러한 개체를 전달하면 안 됩니다.  
  
 한 가지 예로 <xref:System.IO.FileStream> 개체 만들기가 있습니다. 생성 시 <xref:System.Security.Permissions.FileIOPermission>이 요구되며, 성공하면 파일 개체가 반환됩니다. 그러나 이 개체 참조가 파일 권한이 없는 코드에 전달되면 개체가 이 특정 파일을 읽고 쓸 수 있습니다.  
  
 이러한 개체에 대 한 가장 간단한 방어는 공용 API 요소를 통해 개체 참조를 가져오도록 하는 코드와 동일한 **FileIOPermission** 을 요구 하는 것입니다.  
  
## <a name="application-domain-crossing-issues"></a>애플리케이션 도메인을 넘을 때의 문제  
 관리되는 호스팅 환경에서 코드를 격리하려면 다양한 어셈블리에 대한 권한 수준을 축소하는 명시적 정책을 사용하여 여러 자식 애플리케이션 도메인을 생성하는 것이 일반적입니다. 그러나 해당 어셈블리에 대한 정책은 기본 애플리케이션 도메인에 변경되지 않고 유지됩니다. 자식 애플리케이션 도메인 중 하나가 기본 애플리케이션 도메인에서 어셈블리를 로드하도록 강제할 수 있는 경우 코드 격리 효과가 손실되며 강제로 로드된 어셈블리의 형식이 상위 신뢰 수준으로 코드를 실행할 수 있습니다.  
  
 애플리케이션 도메인은 다른 애플리케이션 도메인에서 어셈블리를 로드하도록 강제하고 다른 애플리케이션 도메인에 호스트된 개체에 대한 프록시를 호출하여 포함된 코드를 실행할 수 있습니다. 애플리케이션 도메인 간 프록시를 가져오려면 개체를 호스트하는 애플리케이션 도메인이 메서드 호출 매개 변수나 반환 값을 통해 프록시를 배포해야 합니다. 또는 애플리케이션 도메인이 방금 만들어진 경우 기본적으로 작성자에게 <xref:System.AppDomain> 개체에 대한 프록시가 있습니다. 따라서 코드 격리 손상을 방지하려면 상위 신뢰 수준의 애플리케이션 도메인이 해당 도메인의 참조 방식 마샬링 개체에 대한 참조(<xref:System.MarshalByRefObject>에서 파생된 클래스 인스턴스)를 하위 신뢰 수준의 애플리케이션 도메인에 배포하면 안 됩니다.  
  
 일반적으로 기본 애플리케이션 도메인은 각각 컨트롤 개체가 있는 자식 애플리케이션 도메인을 만듭니다. 컨트롤 개체는 새 애플리케이션 도메인을 관리하고 때때로 기본 애플리케이션 도메인에서 주문을 받지만 실제로 도메인에 직접 연결할 수 없습니다. 때로는 기본 애플리케이션 도메인이 컨트롤 개체에 대한 프록시를 호출합니다. 그러나 컨트롤 개체가 기본 애플리케이션 도메인을 다시 호출해야 하는 경우도 있을 수 있습니다. 이러한 경우 기본 애플리케이션 도메인은 참조 방식 마샬링 콜백 개체를 컨트롤 개체의 생성자에 전달합니다. 이 프록시를 보호하는 것은 컨트롤 개체의 책임입니다. 컨트롤 개체가 공용 클래스의 public 정적 필드에 프록시를 배치하거나 달리 프록시를 공개적으로 노출하는 경우 다른 코드가 기본 애플리케이션 도메인에 콜백하는 위험한 메커니즘이 개방됩니다. 이런 이유로, 컨트롤 개체는 프록시를 비공개로 유지하기 위해 항상 암시적으로 신뢰됩니다.  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)
