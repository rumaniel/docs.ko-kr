---
title: Serialization-.NET
ms.date: 09/02/2019
helpviewer_keywords:
- JSON serialization
- XML serialization, defined
- binary serialization
- serializing objects
- serialization
- objects, serializing
ms.assetid: 4d1111c0-9447-4231-a997-96a2b74b3453
ms.openlocfilehash: e6db24326c79ab6509b253c45c27f87a2aacd73c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053355"
---
# <a name="serialization-in-net"></a>.NET의 Serialization

serialization은 지속시키거나 전송할 수 있는 형태로 개체 상태를 변환하는 프로세스입니다. serialization과 짝을 이루는 것은 스트림을 개체로 변환하는 deserialization입니다. 이러한 프로세스를 함께 사용 하면 데이터를 저장 하 고 전송할 수 있습니다.  
  
.NET은 다음과 같은 serialization 기술을 제공 합니다.  
  
- [이진 serialization](binary-serialization.md) 은 응용 프로그램의 여러 호출 간에 개체 상태를 유지 하는 데 유용한 형식 충실도를 유지 합니다. 예를 들어, 개체를 클립보드로 serialize하면 여러 애플리케이션 간에 개체를 공유할 수 있습니다. 개체를 스트림, 디스크, 메모리, 네트워크 등으로 serialize할 수 있습니다. Remoting에서는 serialization을 사용하여 한 컴퓨터 또는 애플리케이션 도메인의 개체를 다른 컴퓨터 또는 애플리케이션 도메인으로 &quot;값으로&quot; 전달합니다.  
  
- [XML 및 SOAP serialization](xml-and-soap-serialization.md) 은 public 속성과 필드만 serialize 하며 형식 충실도를 유지 하지 않습니다. 데이터를 사용하는 애플리케이션을 제한하지 않고 데이터를 제공하거나 사용하려고 할 때 유용합니다. XML은 공개 표준이기 때문에 웹을 통해 정보를 공유할 때 적합합니다. SOAP도 마찬가지로 공개 표준이어서 적합한 선택입니다.  
  
- [JSON serialization](system-text-json-overview.md) 은 public 속성만 serialize 하며 형식 충실도를 유지 하지 않습니다. JSON은 웹을 통해 데이터를 공유 하는 데 적합 한 개방형 표준입니다.

## <a name="reference"></a>참조

<xref:System.Runtime.Serialization>  
개체를 serialize하거나 deserialize하는 데 사용할 수 있는 클래스를 포함합니다.
  
<xref:System.Xml.Serialization>  
개체를 XML 형식 문서 또는 스트림으로 serialize하는 데 사용할 수 있는 클래스를 포함합니다.

<xref:System.Text.Json>  
개체를 JSON 형식 문서 또는 스트림으로 serialize 하는 데 사용할 수 있는 클래스를 포함 합니다.
