---
title: 부분 신뢰를 위한 최선의 방법
ms.date: 03/30/2017
ms.assetid: 0d052bc0-5b98-4c50-8bb5-270cc8a8b145
ms.openlocfilehash: 7d5bcc7f9f179553188b4ce90c724dc0bd839670
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663030"
---
# <a name="partial-trust-best-practices"></a>부분 신뢰를 위한 최선의 방법

이 항목에서는 부분 신뢰 환경에서 Windows Communication Foundation (WCF)를 실행 하는 경우 모범 사례를 설명 합니다.

## <a name="serialization"></a>Serialization

부분 신뢰 애플리케이션에서 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용할 때 다음 방법을 적용합니다.

- serialize할 수 있는 모든 형식은 명시적으로 `[DataContract]` 특성으로 표시해야 합니다. 다음 기술은 부분 신뢰 환경에서 지원되지 않습니다.

- serialize할 클래스를 <xref:System.SerializableAttribute>로 표시하는 기술

- 클래스가 serialization 프로세스를 제어할 수 있도록 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하는 기술

### <a name="using-datacontractserializer"></a>DataContractSerializer 사용

- `[DataContract]` 특성으로 표시된 형식은 모두 public이어야 합니다. public이 아닌 형식은 부분 신뢰 환경에서 serialize할 수 없습니다.

- serialize할 수 있는 `[DataContract]` 형식의 모든 `[DataContract]` 멤버는 public이어야 합니다. public이 아닌 `[DataMember]`가 있는 형식은 부분 신뢰 환경에서 serialize할 수 없습니다.

- `OnSerializing`, `OnSerialized`, `OnDeserializing` 및 `OnDeserialized`와 같은 serialization 이벤트를 처리하는 메서드는 public으로 선언해야 합니다. 그러나 <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%28System.Object%29>의 명시적 구현과 암시적 구현이 모두 지원됩니다.

- `[DataContract]`가 deserialization을 수행하는 동안 새로 인스턴스화된 개체의 생성자를 호출하지 않으므로 <xref:System.Security.AllowPartiallyTrustedCallersAttribute>로 표시된 어셈블리에서 구현한 <xref:System.Runtime.Serialization.DataContractSerializer> 형식은 형식 생성자에서 보안 관련 작업을 수행해서는 안 됩니다. 특히 다음과 같은 일반적인 보안 기술은 `[DataContract]` 형식에 사용해서는 안 됩니다.

- 형식 생성자를 internal 또는 private으로 설정하여 부분 신뢰 액세스를 제한하려고 시도하는 보안 기술

- `[LinkDemand]`를 형식 생성자에 추가하여 형식에 대한 액세스를 제한하는 보안 기술

- 개체가 인스턴스화되었기 때문에 생성자가 적용한 유효성 검사가 확인되었다고 가정하는 보안 기술

### <a name="using-ixmlserializable"></a>IXmlSerializable 사용

다음 최선의 방법은 <xref:System.Xml.Serialization.IXmlSerializable>을 구현하고 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하여 serialize되는 형식에 적용됩니다.

- <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> 정적 메서드 구현에서는 `public`여야 합니다.

- <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 인스턴스 메서드는 `public`여야 합니다.

## <a name="using-wcf-from-fully-trusted-platform-code-that-allows-calls-from-partially-trusted-callers"></a>부분적으로 신뢰하는 호출자의 호출을 허용하는 완전히 신뢰할 수 있는 플랫폼 코드에서 WCF 사용

WCF 부분 신뢰 보안 모델을 WCF 공용 메서드 또는 속성의 모든 호출자가 호스팅 응용 프로그램의 코드 액세스 보안 (CA) 컨텍스트에서 실행 되 고 있는지를 가정 합니다. WCF는 하나의 응용 프로그램 보안 컨텍스트만 존재 각각에 대해 가정 <xref:System.AppDomain>, 및이 컨텍스트의에 설치 된 <xref:System.AppDomain> 신뢰할 수 있는 호스트에서 만든 시간 (호출 하 여 예를 들어 <xref:System.AppDomain.CreateDomain%2A> 또는 ASP.NET 응용 프로그램 관리자가).

이 보안 모델은 보통 신뢰 ASP.NET 애플리케이션에서 실행되는 사용자 코드와 같은 추가 CAS 권한을 어설션할 수 없는 사용자가 작성한 애플리케이션에 적용됩니다. 그러나 완전히 신뢰할 수 있는 플랫폼 코드 (예: 전역 어셈블리 캐시에 설치 되 고 부분적으로 신뢰할 수 있는 코드에서 호출을 수락 하는 타사 어셈블리) 주의 해야는 부분적으로 신뢰할 수 있는 응용 프로그램을 대신 하 여 WCF를 호출 하는 경우 응용 프로그램 수준 보안 취약점으로 인 한 않도록 해야 합니다.

완전 신뢰 코드는 현재 스레드의 CAS 권한 집합을 변경 하지 않아야 (호출 하 여 <xref:System.Security.PermissionSet.Assert%2A>하십시오 <xref:System.Security.PermissionSet.PermitOnly%2A>, 또는 <xref:System.Security.PermissionSet.Deny%2A>) 부분적으로 신뢰할 수 있는 코드를 대신 하 여 WCF Api를 호출 하기 전에 합니다. 애플리케이션 수준 보안 컨텍스트와 독립적인 스레드 관련 권한 컨텍스트를 어설션하거나 거부하거나 만들면 예기치 않은 동작이 발생할 수 있습니다. 애플리케이션에 따라 이 동작으로 인해 애플리케이션 수준의 보안이 취약해질 수 있습니다.

스레드 관련 권한 컨텍스트를 사용 하 여 WCF에 대 한 호출은 발생할 수 있는 다음 상황을 처리할 준비가 되어 있어야 하는 코드:

- 작업을 수행하는 동안 스레드 관련 보안 컨텍스트가 유지되지 않을 수 있으며, 이로 인해 잠재적인 보안 예외가 발생할 수 있습니다.

- 내부 WCF 코드 뿐만 아니라 모든 사용자가 제공한 콜백은 원래 시작 된 호출 중인 것 보다 다른 보안 컨텍스트에서 실행할 수 있습니다. 이러한 컨텍스트는 다음과 같습니다.

  - 애플리케이션 권한 컨텍스트

  - 현재 실행 중인 동안 WCF를 호출 하는 데는 다른 사용자 스레드가 이전에 만든 모든 스레드 관련 권한 컨텍스트 <xref:System.AppDomain>합니다.

WCF 보장 부분적으로 신뢰할 수 있는 코드는 WCF 공용 Api 코드로 호출 하기 전에 완전히 신뢰할 수 있는 구성 요소에서 이러한 권한을 어설션 하지 않는 한 완전 신뢰 권한이 가져올 수 없습니다. 그러나 완전 신뢰 권한의 어설션 결과가 특정 스레드, 작업 또는 사용자 작업에만 적용되는 것은 아닙니다.

가장 좋은 방법은 <xref:System.Security.PermissionSet.Assert%2A>, <xref:System.Security.PermissionSet.PermitOnly%2A> 또는 <xref:System.Security.PermissionSet.Deny%2A>를 호출하여 스레드 관련 권한 컨텍스트를 만들지 않는 것입니다. 대신 애플리케이션 자체에 권한을 부여하거나 거부하면 <xref:System.Security.PermissionSet.Assert%2A>, <xref:System.Security.PermissionSet.Deny%2A> 또는 <xref:System.Security.PermissionSet.PermitOnly%2A>가 필요하지 않습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.IXmlSerializable>
