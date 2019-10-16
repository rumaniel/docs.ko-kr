---
title: Serialization(C#)
ms.date: 04/26/2018
ms.openlocfilehash: 638fdbd31912ffeb284d734e1f8ce2ecd879b540
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61680109"
---
# <a name="serialization-c"></a>Serialization(C#)

Serialization은 개체를 저장하거나 메모리, 데이터베이스 또는 파일로 전송하기 위해 개체를 바이트 스트림으로 변환하는 프로세스입니다. 주 목적은 필요할 때 다시 개체로 만들 수 있도록 개체의 상태를 저장하는 것입니다. 역 프로세스는 deserialization입니다.

## <a name="how-serialization-works"></a>Serialization 작동 방법

아래 그림에서는 serialization의 전체 프로세스 과정을 보여 줍니다:

![Serialization 그래픽](./media/index/serialization-process.gif)

개체는 스트림으로 serialize되어 데이터 뿐만 아니라 버전, 문화권 및 어셈블리 이름과 같은 개체 형식에 대한 정보를 운반합니다. 해당 스트림에서 데이터베이스, 파일 또는 메모리에 저장될 수 있습니다.

### <a name="uses-for-serialization"></a>Serialization 용도

Serialization은 개발자에게 개체의 상태를 스토리지하고 필요할 때 다시 만들 수 있도록 해줍니다. 또한 데이터를 교환하는 기능뿐만 아니라 개체를 스토리지하는 기능도 제공합니다. Serialization을 통해 개발자는 웹 서비스를 통해 원격 애플리케이션에 개체를 전송하거나, 한 도메인에서 다른 도메인으로 개체를 전달하거나, 방화벽을 통과해 XML 문자열로 개체를 전달하거나, 애플리케이션 간에 보안을 유지하거나 또는 사용자별 정보를 관리하는 등의 작업을 수행할 수 있습니다.

### <a name="making-an-object-serializable"></a>개체를 Serialize 가능하게 만들기

개체를 직렬화하려면 직렬화할 개체, 직렬화된 개체를 포함할 스트림 및 <xref:System.Runtime.Serialization.Formatter>가 필요합니다. <xref:System.Runtime.Serialization>은 개체를 직렬화하거나 deserialize하는 데 사용할 수 있는 클래스를 포함합니다.

형식에 <xref:System.SerializableAttribute> 특성을 적용하여 이 형식의 인스턴스를 직렬화할 수 있음을 나타냅니다. 형식에 <xref:System.SerializableAttribute> 특성이 없는 경우 직렬화하려고 하면 예외가 throw됩니다.

클래스 내의 필드를 직렬화가 불가능하게 하려면 <xref:System.NonSerializedAttribute> 특성을 적용합니다. serialize 가능한 형식의 필드에 특정 환경과 관련된 포인터, 핸들 또는 다른 데이터 구조가 포함되어 있고 필드를 다른 환경에서 의미 있게 재구성할 수 없으면 serialize할 수 없게 만들 수 있습니다.

직렬화된 클래스에 <xref:System.SerializableAttribute>가 표시된 다른 클래스의 개체에 대한 참조가 포함된 경우 해당 개체도 직렬화됩니다.

## <a name="binary-and-xml-serialization"></a>이진 및 XML Serialization

이진 또는 XML Serialization을 사용할 수 있습니다. 이진 Serialization에서 멤버가 읽기 전용이더라도 모든 멤버가 Serialize되고 성능이 향상됩니다. XML Serialization은 상호 운용성을 위한 보다 읽기 쉬운 코드 및 보다 유연한 개체 공유 및 사용을 제공합니다.

### <a name="binary-serialization"></a>이진 Serialization

이진 serialization은 이진 인코딩을 사용하여 스토리지 또는 소켓 기반 네트워크 스트림과 같은 용도에서 사용할 수 있는 압축된 serialization을 생성합니다.

### <a name="xml-serialization"></a>XML serialization

XML serialization은 개체의 public 필드와 속성 또는 메서드의 매개 변수와 반환 값을 특정 XSD(XML 스키마 정의 언어) 문서와 일치하는 XML 스트림으로 serialize합니다. XML serialization을 사용하면 XML로 변환되는 public 속성 및 필드가 있는 강력한 형식의 클래스가 만들어집니다. <xref:System.Xml.Serialization>은 XML을 직렬화하거나 deserialize하는 데 사용할 수 있는 클래스를 포함합니다.

<xref:System.Xml.Serialization.XmlSerializer>가 클래스 인스턴스를 직렬화 또는 deserialize하는 방법을 제어하기 위해 클래스 및 클래스 멤버에 특성을 적용합니다.

## <a name="basic-and-custom-serialization"></a>기본 및 사용자 지정 Serialization

serialization은 기본 및 사용자 지정의 두 가지 방법으로 수행할 수 있습니다. 기본 serialization은 .NET Framework를 사용하여 개체를 자동으로 serialize합니다.

### <a name="basic-serialization"></a>기본 serialization

기본 serialization의 유일한 요구 사항은 개체에 <xref:System.SerializableAttribute> 특성이 적용되어야 한다는 것입니다. <xref:System.NonSerializedAttribute>는 특정 필드가 직렬화되지 않도록 하는 데 사용할 수 있습니다.

기본 Serialization을 사용하면 개체의 버전 관리에 문제가 발생할 수 있습니다. 버전 관리 문제가 중요하면 사용자 지정 Serialization을 사용합니다. 기본 serialization은 serialization을 수행하는 가장 쉬운 방법이지만 프로세스를 강력하게 제어하기는 어렵습니다.

### <a name="custom-serialization"></a>사용자 지정 serialization

사용자 지정 serialization에서는 serialize될 개체 및 수행 방법을 정확하게 지정할 수 있습니다. 클래스에 <xref:System.SerializableAttribute>가 표시되어야 하고 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현해야 합니다.

개체를 사용자 지정 방식으로 deserialize하려면 사용자 지정 생성자를 사용해야 합니다.

## <a name="designer-serialization"></a>디자이너 Serialization

디자이너 Serialization은 개발 도구와 관련해서 개체 지속성이 적용되는 특수한 형태의 Serialization입니다. 디자이너 serialization은 개체 그래프를 소스 파일로 변환하여 나중에 개체 그래프를 복구하는 데 사용할 수 있도록 하는 프로세스입니다. 소스 파일에는 코드, 태그 또는 심지어 SQL 테이블 정보도 포함될 수 있습니다.

## <a name="BKMK_RelatedTopics"></a> 관련 항목 및 예제  
[연습: Visual Studio에서 개체 유지(C#)](walkthrough-persisting-an-object-in-visual-studio.md)  
serialization을 사용하여 인스턴스 간에 개체의 데이터를 유지함으로써 다음에 개체를 인스턴스화할 때 값을 저장하고 검색하는 방식을 보여 줍니다.

[방법: XML 파일에서 개체 데이터 읽기(C#)](how-to-read-object-data-from-an-xml-file.md)  
 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 이전에 XML 파일에 기록된 개체 데이터를 읽는 방법을 보여 줍니다.

[방법: XML 파일에 개체 데이터 쓰기(C#)](how-to-write-object-data-to-an-xml-file.md)  
<xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 클래스의 개체를 XML 파일에 쓰는 방법을 보여 줍니다.
