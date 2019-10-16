---
title: MissingMetadataException 클래스(.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: 408f25c4-6d60-475c-92b1-7b52b777c6db
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 251d63fe8e025fe73b148c7deb368ab95ca3b1f7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049476"
---
# <a name="missingmetadataexception-class-net-native"></a>MissingMetadataException 클래스(.NET 네이티브)

**Windows 10 용 Windows 앱 용 .NET, .NET 네이티브만**

리플렉션을 사용하여 존재하지 않는 메타데이터를 검색하면 throw되는 예외입니다.

**네임스페이스:** System.Reflection

> [!IMPORTANT]
> 클래스 `MissingMetadataException` 는 .NET 네이티브 도구 체인에서 내부용 으로만 사용 됩니다. 이 클래스는 타사 코드에서 사용하면 안 되고 응용 프로그램 코드에서 예외를 처리하면 안 됩니다. 대신, [런타임 지시문 파일](runtime-directives-rd-xml-configuration-file-reference.md)에 항목을 추가하여 예외를 제거합니다. 자세한 내용은 설명 섹션을 참조하세요.

## <a name="syntax"></a>구문

[!code-csharp[ProjectN#4](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingmetadataexception_syntax1.cs#4)]

`MissingMetadataException` 클래스가 <xref:System.TypeAccessException>에서 파생되는지 확인합니다.

`MissingMetadataException` 클래스의 멤버는 다음과 같습니다.

## <a name="constructors"></a>생성자

|생성자|설명|
|-----------------|-----------------|
|`public MissingMetadataException()`|오류를 설명하는 시스템 제공 메시지를 사용하여 `MissingMetadataException` 클래스의 새 인스턴스를 초기화합니다.<br /><br /> 이 생성자는 .NET 네이티브 도구 체인에서 내부용 으로만 사용 됩니다.|
|`public MissingMetadataException(String message)`|지정된 오류 메시지를 사용하여 `MissingMetadataException` 클래스의 새 인스턴스를 초기화합니다.<br /><br /> 이 생성자는 .NET 네이티브 도구 체인에서 내부용 으로만 사용 됩니다.|

## <a name="properties"></a>속성

|속성|설명|
|--------------|-----------------|
|`public IDictionary Data { get; }`|예외에 대한 사용자 정의 추가 정보를 제공하는 키/값 쌍의 컬렉션을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public string HelpLink { get; set; }`|이 예외와 연결된 도움말 파일에 대한 링크를 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public int HResult { get; protected set; }`|특정 예외에 할당되는 코딩된 숫자 값인 `HRESULT`를 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public Exception InnerException { get; }`|현재 예외를 발생시킨 예외를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public string Message { get; }`|현재 예외를 설명하는 메시지를 가져옵니다. <xref:System.TypeLoadException>에서 상속됩니다.|
|`public string Source { get; set; }`|오류를 발생시킨 응용 프로그램 또는 개체의 이름을 가져오거나 설정합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public string StackTrace { get; }`|호출 스택의 직접 실행 프레임 문자열 표현을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public MethodBase TargetSite { get; }`|현재 예외가 throw된 메서드를 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public string TypeName { get; ]`|메타데이터가 누락된 형식의 정규화된 이름을 가져옵니다. <xref:System.TypeLoadException>에서 상속됩니다.|

## <a name="methods"></a>메서드

|메서드|설명|
|------------|-----------------|
|`public bool Equals(Object obj)`|지정한 개체와 현재 개체가 같은지 여부를 확인합니다.  <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`protected void Finalize()`|가비지 수집기가 회수하기 전에 개체가 리소스를 해제하고 다른 정리 작업을 수행할 수 있게 합니다. <xref:System.Object>에서 상속됩니다.|
|`public Exception GetBaseException()`|후속 예외 하나 이상의 근본 원인이 되는 예외를 반환합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`public int GetHashCode()`|`MissingMetadataException` 인스턴스의 해시 코드를 반환합니다.   <xref:System.Object>에서 상속됩니다.|
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|예외에 대한 정보를 사용하여 <xref:System.Runtime.Serialization.SerializationInfo> 개체를 설정합니다.  <xref:System.TypeLoadException>에서 상속됩니다.|
|`public Type GetType()`|현재 인스턴스의 런타임 형식을 가져옵니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|
|`protected Object MemberwiseClone()`|현재 개체의 부분 복사본을 만듭니다. <xref:System.Object>에서 상속됩니다.|
|`public string ToString()`|현재 예외의 문자열 표현을 반환합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|

## <a name="events"></a>이벤트

|이벤트(event)|설명|
|-----------|-----------------|
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|예외에 대한 serialize된 데이터를 포함하는 예외 상태 개체를 만들기 위해 예외를 serialize할 때 발생합니다. <xref:System.Exception?displayProperty=nameWithType>에서 상속됩니다.|

## <a name="usage-details"></a>자세한 용도

리플렉션을 사용하여 어셈블리에서 제공되지 않는 메타데이터에 액세스하면 `MissingMetadataException` 예외가 throw됩니다.

런타임에 응용 프로그램에 사용할 수 있는 메타 데이터는 런타임 지시문 (xml 구성) 파일 \*(app.config)에 의해 정의 됩니다. 앱에서 이 예외가 throw되지 않도록 하려면 런타임에 존재해야 하는 메타데이터를 정의하도록 \*.rd.xml을 수정해야 합니다. \*.rd.xml 파일의 형식에 대한 자세한 내용은 [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)를 확인하세요.

> [!IMPORTANT]
> 이 예외는 애플리케이션에 필요한 메타데이터를 런타임에 사용할 수 없음을 나타내므로 `try`/`catch` 블록에서 이 예외를 처리하면 안 됩니다. 대신 예외의 원인을 진단하고 런타임 지시문 파일을 사용하여 예외를 방지해야 합니다. 예외를 제거하는 런타임 지시문 파일에 추가할 수 있는 항목을 가져오려면 두 문제 해결사 중 하나를 사용할 수 있습니다.
>
> - 형식의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/type.html) 입니다.
> - 메서드의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/method.html) 입니다.

`MissingMetadataException` 클래스는 고유한 멤버를 포함하지 않으며 모든 멤버는 <xref:System.TypeAccessException>에서 상속됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Exception?displayProperty=nameWithType>
- <xref:System.TypeAccessException>
- [MissingInteropDataException 클래스](missinginteropdataexception-class-net-native.md)
- [MissingRuntimeArtifactException 클래스](missingruntimeartifactexception-class-net-native.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
