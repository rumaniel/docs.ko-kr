---
title: ServiceModel Metadata 유틸리티 도구(Svcutil.exe)
ms.date: 03/30/2017
helpviewer_keywords:
- clients [WCF], building
- endpoints [WCF]
- Svcutil.exe
- clients [WCF], consuming services
ms.assetid: 1abf3d9f-b420-46f1-b628-df238751f308
ms.openlocfilehash: 0cb14bba724b50a8a2b723fe88503fafeeea3880
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959902"
---
# <a name="servicemodel-metadata-utility-tool-svcutilexe"></a>ServiceModel Metadata 유틸리티 도구(Svcutil.exe)

ServiceModel Metadata 유틸리티 도구는 메타 데이터 문서 및 서비스 모델 코드에서 메타 데이터 문서에서 서비스 모델 코드 생성에 사용 됩니다.

## <a name="svcutilexe"></a>SvcUtil.exe

Windows SDK 설치 위치에 특히 ServiceModel Metadata 유틸리티 도구를 찾을 수 있습니다 *%ProgramFiles%\Microsoft SDKs\Windows\v6.0\Bin*합니다.

### <a name="functionalities"></a>기능

다음 표에서이 도구를 사용 하는 방식을 설명 하는 해당 항목을 제공 하는 다양 한 기능을 보여 줍니다.

|작업|항목|
|----------|-----------|
|실행 중인 서비스나 정적 메타데이터 문서에서 코드를 생성합니다.|[서비스 메타데이터에서 WCF 클라이언트 생성](../../../docs/framework/wcf/feature-details/generating-a-wcf-client-from-service-metadata.md)|
|컴파일된 코드에서 메타데이터 문서를 내보냅니다.|[방법: Svcutil.exe를 사용 하 여 컴파일된 서비스 코드에서 메타 데이터를 내보내려면](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)|
|컴파일된 서비스 코드의 유효성을 검사합니다.|[방법: Svcutil.exe를 사용 하 여 컴파일된 서비스 코드 유효성 검사](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-validate-compiled-service-code.md)|
|실행 중인 서비스에서 메타데이터 문서를 다운로드합니다.|[방법: Svcutil.exe를 사용 하 여 메타 데이터 문서 다운로드](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)|
|serialization 코드를 생성합니다.|[방법: 시작 시간의 WCF 클라이언트 응용 프로그램 개선 XmlSerializer를 사용 하 여](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)|

> [!CAUTION]
> Svcutil 매개 변수로 입력 한 이름이 동일한 경우 디스크에 기존 파일을 덮어씁니다. 이 코드 파일, 구성 또는 메타 데이터 파일에 포함할 수 있습니다. 이 방지 하려면 코드 및 구성 파일을 생성할 때 사용 된 `/mergeConfig` 전환 합니다.
>
> 또한 합니다 `/r` 및 `/ct` 형식을 참조 하는 스위치는 데이터 계약을 생성 합니다. 이러한 스위치는 XmlSerializer를 사용하는 경우 작동하지 않습니다.

### <a name="timeout"></a>제한 시간

도구에는 메타 데이터를 검색 하는 경우 5 분 시간 제한입니다. 이 시간 제한은 네트워크를 통해 메타데이터를 검색하는 경우에만 적용됩니다. 해당 메타데이터를 처리하는 경우에는 적용되지 않습니다.

### <a name="multi-targeting"></a>멀티 타기팅

이 도구는 멀티 타기팅을 지원하지 않습니다. .NET 4 아티팩트를 생성 하려는 경우 *svcutil.exe*를 사용 합니다 *svcutil.exe* .NET 4 SDK에서. .NET 3.5 아티팩트를 생성하려면 .NET 3.5 SDK에서 실행 파일을 사용합니다.

### <a name="accessing-wsdl-documents"></a>WSDL 문서 액세스

Svcutil을 사용하여 STS(보안 토큰 서비스)에 대한 참조가 있는 WSDL 문서에 액세스하는 경우 Svcutil은 STS에 대해 WS-MetadataExchange 호출을 수행합니다. 그러나 서비스는 WS-MetadataExchange 또는 HTTP GET을 사용하여 해당 서비스의 WSDL 문서를 노출할 수 있습니다. 따라서 STS가 HTTP GET을 사용 하 여 WSDL 문서를 노출만, WinFX에서 작성 된 클라이언트가 실패 합니다. 으로 작성 된 클라이언트에 대 한 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)], Svcutil 모두 Ws-metadataexchange를 사용 하려고 하 고 HTTP GET STS WSDL을 가져오려고 합니다.

## <a name="using-svcutilexe"></a>SvcUtil.exe 사용

### <a name="common-usages"></a>일반적인 사용

다음 표에서 일반적으로 사용 되는 일부 옵션이 도구를 보여 줍니다.

|옵션|설명|
|------------|-----------------|
|/directory:\<directory>|파일을 만들 디렉터리입니다.<br /><br /> 기본값: 현재 디렉터리입니다.<br /><br /> 약식: `/d`|
|/help|이 도구의 명령 구문 및 옵션을 표시합니다.<br /><br /> 약식: `/?`|
|/noLogo|저작권 및 배너 메시지를 표시하지 않습니다.|
|/svcutilConfig:\<configFile>|App.config 파일 대신 사용할 사용자 지정 구성 파일을 지정합니다. 이 옵션은 도구의 구성 파일을 바꾸지 않고 system.serviceModel 확장을 등록하는 데 사용될 수 있습니다.|
|/target:\<출력 유형 >|도구에서 생성할 출력을 지정합니다.<br /><br /> 유효한 값은 코드, 메타데이터 또는 xmlSerializer입니다.<br /><br /> 약식: `/t`|

### <a name="code-generation"></a>코드 생성

Svcutil.exe를 사용하여 메타데이터 문서에서 서비스 계약, 클라이언트 및 데이터 형식에 대한 코드를 생성할 수 있습니다. 이러한 메타데이터 문서는 지속적인 스토리지에 있거나 온라인으로 검색할 수 있습니다. 온라인 검색은 WS-Metadata Exchange 프로토콜이나 DISCO 프로토콜을 따릅니다. 자세한 내용은 메타데이터 다운로드 단원을 참조하십시오.

사용할 수는 *SvcUtil.exe* 는 미리 정의 된 WSDL 문서를 기반으로 하는 서비스 및 데이터 계약을 생성 하는 도구입니다. /serviceContract 스위치를 사용하고 WSDL 문서를 다운로드하거나 찾을 수 있는 URL 또는 파일 위치를 지정합니다. 이 불만 서비스를 구현 하는 데 사용할 수 있는 WSDL 문서에 정의 된 서비스 및 데이터 계약을 생성 합니다. 자세한 내용은 [방법: 메타 데이터 검색 및 규격 서비스 구현](../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md)합니다.

BasicHttpContextBinding 끝점이 있는 서비스에 대 한 *Svcutil.exe* BasicHttpBinding을 사용 하 여 생성 된 `allowCookies` 특성이로 설정 `true` 대신 합니다. 서버의 컨텍스트에 쿠키가 사용됩니다. 서비스가 쿠키를 사용할 때 클라이언트에서 컨텍스트를 관리하려면 컨텍스트 바인딩을 사용하도록 구성을 수동으로 수정할 수 있습니다.

> [!CAUTION]
> Svcutil.exe는 WSDL을 기반으로 하는 클라이언트 또는 서비스에서 받은 정책 파일을 생성합니다. 사용자 계정 이름 (UPN) 사용자 이름, 연결 하 여 생성 됩니다 "\@" 및 정규화 된 도메인 이름 (FQDN)입니다. 그러나 Active Directory에 등록한 사용자의 경우에는 이 형식은 유효하지 않으며 도구에서 생성한 UPN으로 인해 "로그온하지 못했습니다."라는 오류 메시지와 함께 Kerberos 인증 오류가 발생합니다. 이 문제를 해결하려면 이 도구에서 생성한 클라이언트 파일을 수동으로 수정해야 합니다.

`svcutil.exe [/t:code]  <metadataDocumentPath>* | <url>* | <epr>`

|인수|설명|
|--------------|-----------------|
|`epr`|WS-Metadata Exchange를 지원하는 서비스 엔드포인트에 대한 WS-Addressing EndpointReference가 포함된 XML 파일의 경로입니다. 자세한 내용은 메타데이터 다운로드 단원을 참조하십시오.|
|`metadataDocumentPath`|메타 데이터 문서의 경로 (*wsdl* 하거나 *xsd*)로 코드 (.wsdl,.xsd,.wspolicy, 또는.wsmex)로 가져올 계약이 포함 된 합니다.<br /><br /> Svcutil은 메타데이터의 원격 URL을 지정하는 경우 import 및 include를 따릅니다. 그러나 로컬 파일 시스템의 메타데이터 파일을 처리하려면 이 인수로 모든 파일을 지정해야 합니다. 이러한 방식으로 네트워크 종속성을 사용할 수 없는 빌드 환경에서 Svcutil을 사용할 수 있습니다. 와일드 카드 (*.xsd, \*.wsdl) 이이 인수에 대 한 합니다.|
|`url`|메타데이터를 제공하는 서비스 엔드포인트의 URL 또는 온라인으로 호스팅되는 메타데이터 문서의 URL입니다. 이러한 문서를 검색하는 방법에 대한 자세한 내용은 메타데이터 다운로드 단원을 참조하십시오.|

|옵션|설명|
|------------|-----------------|
|/async|동기 및 비동기 메서드 서명을 모두 생성합니다.<br /><br /> 기본값: 동기 메서드 서명만 생성합니다<br /><br /> 약식: `/a`|
|/collectionType:\<type>|WCF 클라이언트에 대한 목록 컬렉션 형식을 지정합니다.<br/><br /> 기본값: 컬렉션 형식은 System.Array입니다. <br /><br /> 약식: `/ct`|
|/config:\<configFile>|생성된 구성 파일의 파일 이름을 지정합니다.<br /><br /> 기본값: output.config|
|/dataContractOnly|데이터 계약 형식에 대한 코드만 생성합니다. 서비스 계약 형식은 생성되지 않습니다.<br /><br /> 이 옵션에 대한 로컬 메타데이터 파일만 지정해야 합니다.<br /><br /> 약식: `/dconly`|
|/enableDataBinding|모든 데이터 계약 형식에 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현하여 데이터 바인딩을 사용할 수 있습니다.<br /><br /> 약식: `/edb`|
|/excludeType:\<type>|참조된 계약 형식에서 제외할 정규화된 형식 이름 또는 정규화된 어셈블리 형식 이름을 지정합니다.<br /><br /> 별도의 DLL에서 `/r`과 함께 이 스위치를 사용하는 경우 XSD 클래스의 전체 이름이 참조됩니다.<br /><br /> 약식: `/et`|
|/importXmlTypes|비데이터 계약 형식을 IXmlSerializable 형식으로 가져오도록 데이터 계약 serializer를 구성합니다.|
|/internal|internal로 표시된 클래스를 생성합니다. 기본값: 공용 클래스만 생성합니다.<br /><br /> 약식: `/i`|
|/language:\<language>|코드 생성에 사용할 프로그래밍 언어를 지정합니다. Machine.config 파일에 등록 된 언어 이름 또는에서 상속 되는 클래스의 정규화 된 이름을 제공 해야 <xref:System.CodeDom.Compiler.CodeDomProvider>합니다.<br /><br /> 값: C#, cs, csharp, vb, visualbasic, c++, cpp<br /><br /> 기본값: csharp<br /><br /> 약식: `/l`|
|/mergeConfig|기존 파일을 덮어쓰는 대신 생성된 구성을 기존 파일에 병합합니다.|
|/messageContract|메시지 계약 형식을 생성합니다.<br /><br /> 약식: `/mc`|
|/namespace:\<문자열, 문자열 >|WSDL 또는 XML 스키마 targetNamespace에서 CLR 네임스페이스로의 매핑을 지정합니다. 사용 하 여 '\*'의 targetNamespace CLR 네임 스페이스를 명시적으로 매핑하지 않고 모든 targetNamespaces를 매핑합니다.<br /><br /> 메시지 계약 이름이 작업 이름과 충돌하지 않도록 하려면 `::`을 사용하여 형식 참조를 한정하거나 이름이 고유한지 확인해야 합니다.<br /><br /> 기본값: 데이터 계약에 대 한 스키마 문서의 대상 네임 스페이스에서 파생 됩니다. 기본 네임스페이스는 생성된 다른 모든 형식에 사용됩니다.<br /><br /> 약식: `/n` **참고:**  XmlSerializer를 사용 하는 형식을 생성 하는 경우 단일 네임 스페이스 매핑은 사용할 수 있습니다. 기본 네임 스페이스 또는 지정 된 네임 스페이스에서 생성 된 모든 형식 일은 ' *'.|
|/noConfig|구성 파일을 생성하지 않습니다.|
|/noStdLib|표준 라이브러리를 참조하지 않습니다.<br /><br /> 기본값: Mscorlib.dll 및 System.servicemodel.dll 참조 됩니다.|
|/out:\<file>|생성된 코드에 대한 파일 이름을 지정합니다.<br /><br /> 기본값: WSDL 정의 이름에서 파생 된, WSDL 서비스 이름 또는 스키마 중 하나의 대상 네임 스페이스입니다.<br /><br /> 약식: `/o`|
|참조:\<파일 경로 >|지정한 어셈블리에서 형식을 참조합니다. 클라이언트를 생성할 때 이 옵션을 사용하여 가져오는 메타데이터를 나타내는 형식이 포함될 수 있는 어셈블리를 지정합니다.<br /><br /> 이 스위치를 사용하여 메시지 계약 및 <xref:System.Xml.Serialization.XmlSerializer> 형식을 지정할 수 없습니다.<br /><br /> <xref:System.DateTimeOffset>을 참조하는 경우 새 형식을 생성하는 대신 이 형식을 사용합니다. [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]를 사용하여 애플리케이션이 작성되는 경우 SvcUtil.exe는 <xref:System.DateTimeOffset>을 자동으로 참조합니다.<br /><br /> 약식: `/r`|
|/serializable|Serializable 특성으로 표시된 클래스를 생성합니다.<br /><br /> 약식: `/s`|
|/serviceContract|서비스 계약에만 해당하는 코드를 생성합니다. 클라이언트 클래스 및 구성이 생성되지 않습니다.<br /><br /> 약식: `/sc`|
|/serializer:Auto|Serializer를 자동으로 선택 합니다. 이 데이터 계약 serializer를 사용 하려고 하며 실패할 경우 XmlSerializer를 사용 합니다.<br /><br /> 약식: `/ser`|
|/serializer:DataContractSerializer|serialization 및 deserialization을 위해 데이터 계약 Serializer를 사용하는 데이터 형식을 생성합니다.<br /><br /> 약식: `/ser:DataContractSerializer`|
|/serializer:XmlSerializer|serialization 및 deserialization을 위해 <xref:System.Xml.Serialization.XmlSerializer>를 사용하는 데이터 형식을 생성합니다.<br /><br /> 약식: `/ser:XmlSerializer`|
|/targetClientVersion|응용 프로그램 대상.NET Framework 버전을 지정 합니다. 유효한 값은 `Version30` 및 `Version35`입니다. 기본값은 `Version30`입니다.<br /><br /> 약식: `/tcv`<br /><br /> `Version30`: 사용 하 여 `/tcv:Version30` WinFX를 사용 하는 클라이언트에 대 한 코드를 생성 하는 경우.<br /><br /> `Version35`: 사용 하 여 `/tcv:Version35` 를 사용 하는 클라이언트에 대 한 코드를 생성 하는 경우 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]합니다. `/tcv:Version35` 스위치와 함께 `/async`를 사용하면 이벤트 기반 메서드 및 콜백/대리자 기반 비동기 메서드가 모두 생성됩니다. 또한 LINQ 사용 DataSet 및 <xref:System.DateTimeOffset>을 지원하도록 설정되어 있습니다.|
|/wrapped|래핑된 매개 변수가 있는 문서 리터럴 스타일 문서에 특수 대/소문자가 사용되는지 여부를 제어합니다. 사용 하 여는 **래핑된 /** 스위치와 함께 합니다 [서비스 모델 메타 데이터 유틸리티 도구 (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 일반 대/소문자를 지정 하는 도구입니다.|

> [!NOTE]
> 서비스 바인딩이 시스템 제공 바인딩 중 하나는 경우 (참조 [System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md)), 및 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 속성이 설정 되어 `None` 또는 `Sign`, Svcutil을 사용 하 여 구성 파일을 생성 합니다 [ \<customBinding >](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) 예상 되는 시스템 제공 요소 대신 요소입니다. 예를 들어 서비스에서 `<wsHttpBinding>`이 `ProtectionLevel`으로 설정된 `Sign` 요소를 사용하는 경우 생성된 구성의 바인딩 섹션에는 `<customBinding>` 대신 `<wsHttpBinding>`이 있습니다. 보호 수준에 대 한 자세한 내용은 참조 하세요. [보호 수준을 이해](../../../docs/framework/wcf/understanding-protection-level.md)합니다.

### <a name="metadata-export"></a>메타데이터 내보내기

Svcutil.exe에서는 컴파일된 어셈블리에 있는 서비스, 계약 및 데이터 형식에 대한 메타데이터를 내보낼 수 있습니다. 서비스에 대한 메타데이터를 내보내려면 `/serviceName` 옵션을 사용하여 내보낼 서비스를 지정해야 합니다. 어셈블리 내의 모든 데이터 계약 형식을 내보내려면 `/dataContractOnly` 옵션을 사용해야 합니다. 기본적으로 입력 어셈블리에 있는 모든 서비스 계약에 대한 메타데이터가 내보내집니다.

`svcutil.exe [/t:metadata] [/serviceName:<serviceConfigName>] [/dataContractOnly] <assemblyPath>*`

|인수|설명|
|--------------|-----------------|
|`assemblyPath`|내보낼 서비스, 계약 또는 데이터 계약 형식이 포함된 어셈블리의 경로를 지정합니다. 여러 파일을 입력으로 제공하려면 표준 명령줄 와일드카드를 사용할 수 있습니다.|

|옵션|설명|
|------------|-----------------|
|/serviceName:\<serviceConfigName>|내보낼 서비스의 구성 이름을 지정합니다. 이 옵션을 사용할 경우 연결된 구성 파일이 있는 실행 가능한 어셈블리를 입력으로 전달해야 합니다. Svcutil.exe는 서비스 구성에 대한 연결된 모든 구성 파일을 검색합니다. 구성 파일에 확장명 형식이 있는 경우 이러한 형식을 포함하는 어셈블리는 GAC에 있거나 `/reference` 옵션을 사용하여 명시적으로 제공되어야 합니다.|
|참조:\<파일 경로 >|형식 참조를 확인하는 데 사용되는 어셈블리 집합에 지정된 어셈블리를 추가합니다. 구성에 등록된 타사 확장명(Behaviors, Bindings 및 BindingElements)을 사용하는 서비스를 내보내거나 유효성을 검사하는 경우 이 옵션을 사용하여 GAC에 없는 확장명 어셈블리를 찾으십시오.<br /><br /> 약식: `/r`|
|/dataContractOnly|데이터 계약 형식에 대해서만 작동합니다. 서비스 계약은 처리되지 않습니다.<br /><br /> 이 옵션에 대한 로컬 메타데이터 파일만 지정해야 합니다.<br /><br /> 약식: `/dconly`|
|/excludeType:\<type>|내보내기에서 제외할 형식의 정규화된 이름 또는 정규화된 어셈블리 이름을 지정합니다. 형식을 내보내기에서 제외하기 위해 서비스 또는 서비스 계약 집합에 대한 메타데이터를 내보내는 경우 이 옵션을 사용할 수 있습니다. 이 옵션은 `/dconly` 옵션과 함께 사용할 수 없습니다.<br /><br /> 여러 서비스가 포함된 단일 어셈블리가 있고, 각 서비스에서 XSD 이름이 같은 별도의 클래스를 사용하는 경우 이 스위치에 XSD 클래스 이름 대신 서비스 이름을 지정해야 합니다.<br /><br /> XSD 또는 데이터 계약 형식은 지원되지 않습니다.<br /><br /> 약식: `/et`|

### <a name="service-validation"></a>서비스 유효성 검사

유효성 검사는 서비스를 호스트하지 않고 서비스 구현의 오류를 검색하는 데 사용될 수 있습니다. 유효성을 검사할 서비스를 나타내려면 `/serviceName` 옵션을 사용해야 합니다.

`svcutil.exe /validate /serviceName:<serviceConfigName>  <assemblyPath>*`

|인수|설명|
|--------------|-----------------|
|`assemblyPath`|유효성을 검사할 서비스 형식이 포함된 어셈블리의 경로를 지정합니다. 서비스 구성을 제공하려면 어셈블리에 연결된 구성 파일이 있어야 합니다. 여러 어셈블리를 제공하는 데 표준 명령줄 와일드카드를 사용할 수 있습니다.|

|옵션|설명|
|------------|-----------------|
|/validate|`/serviceName` 옵션에 의해 지정된 서비스 구현의 유효성을 검사합니다. 이 옵션을 사용할 경우 연결된 구성 파일이 있는 실행 가능한 어셈블리를 입력으로 전달해야 합니다.<br /><br /> 약식: `/v`|
|/serviceName:\<serviceConfigName>|유효성을 검사할 서비스의 구성 이름을 지정합니다. Svcutil.exe는 서비스 구성에 대한 모든 입력 어셈블리의 연결된 모든 구성 파일을 검색합니다. 구성 파일에 확장명 형식이 있는 경우 이러한 형식을 포함하는 어셈블리는 GAC에 있거나 `/reference` 옵션을 사용하여 명시적으로 제공되어야 합니다.|
|참조:\<파일 경로 >|형식 참조를 확인하는 데 사용되는 어셈블리 집합에 지정된 어셈블리를 추가합니다. 구성에 등록된 타사 확장명(Behaviors, Bindings 및 BindingElements)을 사용하는 서비스를 내보내거나 유효성을 검사하는 경우 이 옵션을 사용하여 GAC에 없는 확장명 어셈블리를 찾으십시오.<br /><br /> 약식: `/r`|
|/dataContractOnly|데이터 계약 형식에 대해서만 작동합니다. 서비스 계약은 처리되지 않습니다.<br /><br /> 이 옵션에 대한 로컬 메타데이터 파일만 지정해야 합니다.<br /><br /> 약식: `/dconly`|
|/excludeType:\<type>|유효성 검사에서 제외할 형식의 정규화된 이름 또는 정규화된 어셈블리 이름을 지정합니다.<br /><br /> 약식: `/et`|

### <a name="metadata-download"></a>메타데이터 다운로드

Svcutil.exe를 사용하여 실행 중인 서비스에서 메타데이터를 다운로드하고 로컬 파일에 저장할 수 있습니다. 메타데이터를 다운로드하려면 `/t:metadata` 옵션을 지정해야 합니다. 그렇지 않으면 클라이언트 코드가 생성됩니다. HTTP 및 HTTPS URL 스키마의 경우 Svcutil.exe에서는 WS-Metadata Exchange 및 DISCO를 사용하여 메타데이터를 검색하려고 시도합니다. 기타 모든 URL 스키마의 경우 Svcutil.exe에서 WS-Metadata Exchange만 사용합니다.

Svcutil은 다음 메타데이터 요청을 생성하고 동시에 메타데이터를 검색합니다.

- 주어진 주소에 대한 MEX(WS-Transfer) 요청

- /mex가 추가된 주어진 주소에 대한 MEX 요청

- 주어진 주소에 대한 DISCO 요청(ASMX에서 DiscoveryClientProtocol 사용)

기본적으로 Svcutil.exe는 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 클래스에 정의된 바인딩을 사용하여 MEX 요청을 수행합니다. WS-Metadata Exchange에 사용되는 바인딩을 구성하려면 IMetadataExchange 계약을 사용하는 구성에서 클라이언트 엔드포인트를 정의해야 합니다. 이 끝점은 Svcutil.exe의 구성 파일 또는 `/svcutilConfig` 옵션을 사용하여 지정한 다른 구성 파일에서 정의할 수 있습니다.

`svcutil.exe /t:metadata  <url>* | <epr>`

|인수|설명|
|--------------|-----------------|
|`url`|메타데이터를 제공하는 서비스 엔드포인트의 URL 또는 온라인으로 호스팅되는 메타데이터 문서의 URL입니다.|
|`epr`|WS-Metadata Exchange를 지원하는 서비스 엔드포인트에 대한 WS-Addressing EndpointReference가 포함된 XML 파일의 경로입니다.|

### <a name="xmlserializer-type-generation"></a>XmlSerializer 형식 생성

<xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize할 수 있는 데이터 형식을 사용하는 서비스 및 클라이언트 애플리케이션은 런타임에 해당 데이터 형식에 대한 serialization 코드를 생성하고 컴파일합니다. 이로 인해 시작 시 성능이 저하될 수 있습니다.

> [!NOTE]
> 미리 생성된 serialization 코드는 서비스가 아닌 클라이언트 애플리케이션에서만 사용할 수 있습니다.

Svcutil.exe를 사용하면 애플리케이션에 대해 컴파일된 어셈블리에서 필요한 C# serialization 코드를 생성할 수 있으므로 이러한 애플리케이션의 시작 성능을 향상시킬 수 있습니다. 자세한 내용은 [방법: 시작 시간의 WCF 클라이언트 응용 프로그램 개선 XmlSerializer를 사용 하 여](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)입니다.

> [!NOTE]
> Svcutil.exe는 입력 어셈블리에 있는 서비스 계약에서 사용하는 형식의 코드만 생성합니다.

`svcutil.exe /t:xmlSerializer  <assemblyPath>*`

|인수|설명|
|--------------|-----------------|
|`assemblyPath`|서비스 계약 형식이 포함된 어셈블리의 경로를 지정합니다. Serialization 형식이 각 계약의 모든 Xml Serializable 형식에 대해 생성됩니다.|

|옵션|설명|
|------------|-----------------|
|참조:\<파일 경로 >|형식 참조를 확인하는 데 사용되는 어셈블리 집합에 지정된 어셈블리를 추가합니다.<br /><br /> 약식: `/r`|
|/excludeType:\<type>|내보내기 또는 유효성 검사에서 제외할 형식의 정규화된 이름 또는 정규화된 어셈블리 이름을 지정합니다.<br /><br /> 약식: `/et`|
|/out:\<file>|생성된 코드에 대한 파일 이름을 지정합니다. 이 옵션은 여러 어셈블리가 도구에 입력으로 전달되는 경우 무시됩니다.<br /><br /> 기본값: 어셈블리 이름에서 파생 됩니다.<br /><br /> 약식: `/o`|
|/UseSerializerForFaults|오류를 읽고 쓰는 데 기본 <xref:System.Xml.Serialization.XmlSerializer> 대신 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하도록 지정합니다.|

## <a name="examples"></a>예제

다음 명령은 실행 중인 서비스나 온라인 메타데이터 문서에서 클라이언트 코드를 생성합니다.

`svcutil http://service/metadataEndpoint`

다음 명령은 로컬 메타데이터 문서에서 클라이언트 코드를 생성합니다.

`svcutil *.wsdl *.xsd /language:C#`

다음 명령은 로컬 스키마 문서에서 Visual Basic의 데이터 계약 형식을 생성합니다.

`svcutil /dconly *.xsd /language:VB`

다음 명령은 실행 중인 서비스에서 메타데이터 문서를 다운로드합니다.

`svcutil /t:metadata http://service/metadataEndpoint`

다음 명령은 서비스 계약의 메타데이터 문서 및 연결된 형식을 어셈블리에 생성합니다.

`svcutil myAssembly.dll`

다음 명령은 서비스의 메타데이터 문서를 생성하고 연결된 모든 서비스 계약 및 데이터 형식을 어셈블리에 생성합니다.

`svcutil myServiceHost.exe /serviceName:myServiceName`

다음 명령은 데이터 형식의 메타데이터 문서를 어셈블리에 생성합니다.

`svcutil myServiceHost.exe /dconly`

다음 명령은 서비스 호스팅을 확인합니다.

`svcutil /validate /serviceName:myServiceName myServiceHost.exe`

다음 명령은 어셈블리의 모든 서비스 계약이 사용하는 <xref:System.Xml.Serialization.XmlSerializer> 형식에 대해 serialization 형식을 생성합니다.

`svcutil /t:xmlserializer myContractLibrary.exe`

## <a name="maximum-nametable-character-count-quota"></a>최대 nametable 문자 수 할당량

svcutil을 사용하여 서비스에 대해 메타데이터를 생성할 때는 다음 메시지가 나타날 수 있습니다.

오류: 메타 데이터를 가져올 수 없습니다 `http://localhost:8000/somesservice/mex` XML 데이터를 읽는 동안 최대 nametable 문자 수 할당량 (16384) 초과 합니다. nametable은 XML 처리 도중에 발견된 문자열을 저장하는 데 사용되는 데이터 구조입니다. 반복되지 않는 요소 이름, 특성 이름 및 특성 값을 가지는 긴 XML 문서로 인해 이 할당량이 트리거될 수 있습니다. XML 판독기를 만들 때 사용되는 XmlDictionaryReaderQuotas 개체에서 MaxNameTableCharCount 속성을 변경하여 이 할당량을 늘릴 수 있습니다.

이 오류는 큰 WSDL 파일의 메타데이터를 요청하면 해당 파일을 반환하는 서비스에서 발생할 수 있습니다. svcutil.exe 도구에 대한 문자 할당량이 초과되어 문제가 발생합니다. 이 값은 서비스 거부(dos) 공격을 방지하기 위해 설정됩니다. svcutil에 대해 다음 구성 파일을 지정하여 이 할당량을 늘릴 수 있습니다.

다음 구성 파일에서는 svcutil에 대한 판독기 할당량을 설정하는 방법을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.serviceModel>
        <bindings>
            <customBinding>
                <binding name="MyBinding">
                    <textMessageEncoding>
                        <readerQuotas maxDepth="2147483647" maxStringContentLength="2147483647"
                            maxArrayLength="2147483647" maxBytesPerRead="2147483647" maxNameTableCharCount="2147483647" />
                    </textMessageEncoding>
                    <httpTransport maxReceivedMessageSize="2147483647" maxBufferSize="2147483647" />
                </binding>
            </customBinding>
        </bindings>
        <client>
            <endpoint binding="customBinding" bindingConfiguration="MyBinding"
                contract="IMetadataExchange"
                name="http" />
        </client>
    </system.serviceModel>
</configuration>
```

svcutil.exe.config 파일을 새로 만들고 XML 예제 코드를 파일 안에 복사합니다. 그런 다음 이 파일을 svcutil.exe와 같은 디렉터리에 배치합니다. 다음 번에 svcutil.exe를 실행하면 새 설정이 선택됩니다.

## <a name="security-concerns"></a>보안 고려 사항

적절한 ACL(액세스 제어 목록)을 사용하여 Svcutil.exe의 설치 폴더, Svcutil.config 및 `/svcutilConfig`에서 가리키는 파일을 보호해야 합니다. 이렇게 하면 악의적인 확장이 등록되어 실행되는 것을 방지할 수 있습니다.

또한 보안이 손상 될 가능성을 최소화 하려면 신뢰할 수 없는 시스템의 일부 이거나 신뢰할 수 없는 코드 공급자를 사용 하 여 Svcutil.exe를 사용 하 여 확장 하지 추가 해야 합니다.

마지막으로 애플리케이션의 중간 계층에서 이 도구를 사용하면 현재 프로세스에 서비스 거부가 발생할 수 있으므로 사용하면 안 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [방법: 클라이언트 만들기](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)
