---
title: MissingInteropDataException 클래스(.NET 네이티브)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: eab4bcf8-9f5f-4731-87d8-842748a6062a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8d916aa5e19b8ce583984d9a8e9708d34cf0adfb
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049539"
---
# <a name="missinginteropdataexception-class-net-native"></a>MissingInteropDataException 클래스(.NET 네이티브)
**Windows 10 용 Windows 앱 용 .NET, .NET 네이티브만**  
  
 수동 마샬링 메서드를 호출했는데 정적 분석 또는 런타임 지시문 파일에서 형식의 메타데이터를 찾을 수 없을 때 throw되는 예외입니다.  
  
 **네임스페이스:** System.Runtime.CompilerServices  
  
> [!IMPORTANT]
> 클래스 `MissingInteropDataException` 는 .NET 네이티브 도구 체인에서 내부용 으로만 사용 됩니다. 이 클래스는 타사 코드에서 사용하면 안 되고 응용 프로그램 코드에서 예외를 처리하면 안 됩니다. 대신, [런타임 지시문 파일](runtime-directives-rd-xml-configuration-file-reference.md)에 항목을 추가하여 예외를 제거합니다. 자세한 내용은 설명 섹션을 참조하세요.  
  
## <a name="syntax"></a>구문  
 [!code-csharp[ProjectN#21](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missinginteropdataexception_syntax1.cs#21)]
 [!code-vb[ProjectN#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/projectn/vb/missinginteropdataexception_syntax1.vb#21)]  
  
 `MissingInteropDataException` 클래스의 멤버는 다음과 같습니다.  
  
## <a name="constructors"></a>생성자  
  
|생성자|설명|  
|-----------------|-----------------|  
|`public MissingInteropDataException(String resourceId, Type pertinentType)`|오류를 설명하는 시스템 제공 메시지의 ID와 데이터가 누락된 형식을 사용하여 `MissingInteropDataException` 클래스의 새 인스턴스를 초기화합니다. 이 생성자는 .NET 네이티브 도구 체인에서 내부용 으로만 사용 됩니다.|  
  
## <a name="properties"></a>속성  
  
|속성|설명|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|예외에 대한 사용자 정의 추가 정보를 제공하는 키/값 쌍의 컬렉션을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string HelpLink { get; set; }`|이 예외와 연결된 도움말 파일에 대한 링크를 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public int HResult { get; protected set; }`|특정 예외에 할당되는 코딩된 숫자 값인 `HRESULT`를 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public Exception InnerException { get; }`|현재 예외를 발생시킨 예외를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string Message { get; }`|현재 예외를 설명하는 메시지를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public Type MissingType { get; private set; }`|데이터가 누락된 형식을 가져오거나 설정합니다.|  
|`public string Source { get; set; }`|오류를 발생시킨 앱 또는 개체의 이름을 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public string StackTrace { get; }`|호출 스택의 직접 실행 프레임 문자열 표현을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public MethodBase TargetSite { get; }`|현재 예외가 throw된 메서드를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|지정한 개체와 현재 개체가 같은지 여부를 확인합니다.  <xref:System.Object>에서 상속됩니다.|  
|`protected void Finalize()`|가비지 수집기가 회수하기 전에 개체가 리소스를 해제하고 다른 정리 작업을 수행할 수 있게 합니다. <xref:System.Object>에서 상속됩니다.|  
|`public Exception GetBaseException()`|후속 예외 하나 이상의 근본 원인이 되는 예외를 반환합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public int GetHashCode()`|`MissingInteropDataException` 인스턴스의 해시 코드를 반환합니다.   <xref:System.Object>에서 상속됩니다.|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|예외에 대한 정보를 사용하여 <xref:System.Runtime.Serialization.SerializationInfo> 개체를 설정합니다.  <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`public Type GetType()`|현재 인스턴스의 런타임 형식을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
|`protected Object MemberwiseClone()`|현재 개체의 부분 복사본을 만듭니다. <xref:System.Object>에서 상속됩니다.|  
|`public string ToString()`|현재 예외의 문자열 표현을 반환합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
  
## <a name="events"></a>이벤트  
  
|이벤트(event)|설명|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|예외에 대한 serialize된 데이터를 포함하는 예외 상태 개체를 만들기 위해 예외를 serialize할 때 발생합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|  
  
## <a name="usage-details"></a>자세한 용도  
 형식 정보를 사용할 수 없어 COM 또는 Windows 런타임 구성 요소에 대한 메서드 호출을 정상적으로 수행할 수 없으면 `MissingInteropDataException` 예외가 throw됩니다.  
  
 런타임에 응용 프로그램에 사용할 수 있는 메타 데이터는 런타임 지시문 (xml 구성) 파일 \*(app.config)에 의해 정의 됩니다. 앱에서 이 예외가 throw되지 않도록 하려면 런타임에 존재해야 하는 메타데이터를 정의하도록 이 파일을 수정해야 합니다. 런타임 지시문 파일에서 해당 프로그램 요소에 `MarshalObject`, `MarshalDelegate` 또는 `MarshalStructure` 특성을 추가하여 이 오류를 해결하는 방식이 가장 일반적으로 사용됩니다. 이 파일 형식에 대한 자세한 내용은 [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)를 확인하세요.  
  
> [!IMPORTANT]
> 이 예외는 애플리케이션에 필요한 메타데이터를 런타임에 사용할 수 없음을 나타내므로 `try`/`catch` 블록에서 이 예외를 처리하면 안 됩니다. 대신 예외의 원인을 진단하고 런타임 지시문 파일에 적절한 항목을 추가하여 예외를 제거해야 합니다.  
  
 `MissingInteropDataException` 클래스는 메서드를 정상적으로 호출하려면 해당 메타데이터가 필요한 형식을 나타내는 고유한 멤버 하나(`MissingType` 속성)를 포함합니다. 나머지 모든 멤버는 기본 클래스인 <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Exception?displayProperty=nameWithType>
- [MissingMetadataException 클래스](missingmetadataexception-class-net-native.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
