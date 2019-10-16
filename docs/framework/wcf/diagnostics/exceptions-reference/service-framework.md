---
title: 서비스 프레임워크
ms.date: 03/30/2017
ms.assetid: 75f60b87-f80e-4377-ba7c-8e6becaa2b28
ms.openlocfilehash: 859e718a56ab63c8e012e1851c0730f53cb707be
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61780759"
---
# <a name="service-framework"></a>서비스 프레임워크
이 항목에서는 서비스 프레임워크 데이터에 의해 생성된 모든 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|ABindingInstanceHasAlreadyBeenAssociatedTo1|바인딩 인스턴스가 지정된 URI(Uniform Resource Identifier)에 이미 연결되어 있습니다. 두 엔드포인트에서 동일한 ListenUniform 리소스 식별자를 공유하려면 동일한 바인딩 개체 인스턴스를 공유해야 합니다. 충돌하는 두 개의 엔드포인트가 AddServiceEndpoint() 호출, 구성 파일 또는 AddServiceEndpoint()와 구성의 조합에 지정되었습니다.|  
|AChannelServiceEndpointIsNull0|채널 또는 서비스 엔드포인트가 null입니다.|  
|AChannelServiceEndpointSContractSNameIsNull0|채널/서비스 엔드포인트의 계약 이름이 null이거나 비어 있습니다.|  
|AChannelServiceEndpointSContractSNamespace0|채널/서비스 엔드포인트의 계약 네임스페이스가 null입니다.|  
|BaseAddressCannotHaveFragment|기본 주소는 URI(Uniform Resource Identifier) 단편을 포함할 수 없습니다.|  
|BaseAddressCannotHaveQuery|기본 주소는 URI(Uniform Resource Identifier) 쿼리 문자열을 포함할 수 없습니다.|  
|BaseAddressCannotHaveUserInfo|기본 주소는 URI(Uniform Resource Identifier) 사용자 정보 섹션을 포함할 수 없습니다.|  
|BaseAddressDuplicateScheme|이 컬렉션에는 지정된 스키마를 가진 주소가 이미 있습니다. 이 컬렉션의 각 스키마에는 하나의 주소만 허용됩니다.|  
|BaseAddressMustBeAbsolute|절대 URI(Uniform Resource Identifier)만 기본 주소로 사용할 수 있습니다.|  
|BindingDoesnTSupportAnyChannelTypes1|지정된 바인딩이 채널 형식 만들기를 지원하지 않습니다. 사용자 지정 바인딩의 바인딩 요소가 올바르지 않게 스택되었거나 순서가 잘못되었습니다. 전송이 스택의 맨 아래에 와야 합니다. 바인딩 요소에 대 한 권장 되는 순서는 다음과 같습니다. TransactionFlow, ReliableSession, Security, CompositeDuplex, OneWay, StreamSecurity, MessageEncoding, 전송 합니다.|  
|BindingDoesnTSupportDuplexButContractRequires1|계약에 Duplex가 필요하지만 지정된 바인딩이 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|BindingDoesnTSupportOneWayButContractRequires1|계약에 OneWay가 필요하지만 지정된 바인딩이 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|BindingDoesnTSupportRequestReplyButContract1|계약에 Request/Reply가 필요하지만 지정된 바인딩이 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|BindingDoesnTSupportSessionButContractRequires1|계약에 Session이 필요하지만  지정된 바인딩이 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|BindingDoesnTSupportTwoWayButContractRequires1|계약에 Two-Way(Request-Reply 또는 Duplex)가 필요하지만 지정된 바인딩이 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|BindingRequirementsAttributeDisallowsQueuedDelivery1|DeliveryRequirementsAttribute에 QueuedDelivery를 사용할 수 없습니다. 지정된 계약을 가진 엔드포인트에 대한 바인딩이 이를 지원합니다.|  
|BindingRequirementsAttributeRequiresQueuedDelivery1|DeliveryRequirementsAttribute에 QueuedDelivery가 필요한데 지정된 계약을 가진 엔드포인트에 대한 바인딩이 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|channelDoesNotHaveADuplexSession0|현재 채널은 출력 세션 닫기를 지원하지 않습니다. 이 채널 ISessionChannel를 구현 하지 않는\<IDuplexSession >.|  
|ClientRuntimeRequiresFormatter0|SerializeRequest 및 DeserializeReply가 둘 다 false는 아니므로 지정된 ClientOperation에 포맷터가 필요합니다.|  
|CommunicationObjectAborted1|지정된 통신 개체가 중지되었기 때문에 통신에 사용할 수 없습니다.|  
|CommunicationObjectAbortedStack2|지정 된 통신 개체가 중지 되었기 때문에 통신에 사용할 수 없습니다. {1}|  
|CommunicationObjectBaseClassMethodNotCalled|지정 된 통신 개체가 가상 함수 재정의 {1} 하지만 기본 클래스에 정의 된 버전을 호출 하지는 않습니다.|  
|ContractIsNotSelfConsistentItHasOneOrMore2|지정된 계약에 하나 이상의 IsTerminating 또는 비-IsInitiating 작업이 있습니다. SessionMode 속성이 SessionMode.Required로 설정되어 있지 않습니다. IsInitiating 및 IsTerminating 특성은 세션 컨텍스트에서만 사용할 수 있습니다.|  
|CouldnTCreateChannelForChannelType2|지정된 채널 형식이 요청되었지만 지정된 바인딩에서 이를 지원하지 않거나 이를 지원하도록 제대로 구성되지 않았습니다.|  
|DispatchRuntimeRequiresFormatter0|DeserializeRequest 및 SerializeReply가 둘 다 false가 아니므로 지정된 DispatchOperation에 포맷터가 필요합니다.|  
|EndMethodsCannotBeDecoratedWithOperationContractAttribute|IAsyncResult 디자인 패턴을 사용하는 경우 End 메서드를 OperationContractAttribute와 함께 사용할 수 없습니다. 해당 Begin 메서드만 OperationContractAttribute와 함께 사용할 수 있습니다. 이 특성은 메서드의 Begin-End 쌍에 적용됩니다.|  
|EndpointListenerRequirementsCannotBeMetBy3|이러한 지정된 채널 형식 중 하나에 대한 지원이 계약에 필요하기 때문에 지정된 바인딩에 대한 IChannelListener에서 ChannelDispatcher 요구 사항을 충족할 수 없습니다. 그러나 바인딩은 이러한 지정된 채널 형식만 지원합니다.|  
|EndpointsMustHaveAValidBinding0|엔드포인트에 유효한 바인딩이 있어야 합니다.|  
|InvalidOrUnrecognizedAction|지정된 동작이 유효하지 않거나 인식되지 않기 때문에 메시지를 처리할 수 없습니다.|  
|MultipleMebesInParameters|BindingContext의 BindingParameters에 여러 MessageEncodingBindingElement가 있습니다. CustomBinding은 여러 개의 MessageEncodingBindingElements를 가질 수 없습니다. 이러한 요소 중 하나만 남기고 모두 제거합니다.|  
|MultipleStreamUpgradeProvidersInParameters|BindingContext의 BindingParameters에 여러 IStreamUpgradeProviderElement가 있습니다. CustomBinding은 여러 개의 IStreamUpgradeProviderElements를 가질 수 없습니다. 이러한 요소 중 하나만 남기고 모두 제거합니다.|  
|NoChannelBuilderAvailable|바인딩에 TransportBindingElement가 없기 때문에 바인딩을 사용하여 채널 팩터리 또는 채널 수신기를 만들 수 없습니다. 모든 바인딩에는 TransportBindingElement에서 파생되는 하나 이상의 바인딩 요소가 있어야 합니다.|  
|NotAllBindingElementsBuilt|채널 팩터리 및 채널 수신기를 작성할 때 이 바인딩의 바인딩 요소 중 일부가 사용되지 않았습니다. 바인딩 요소의 순서가 잘못되었습니다. 바인딩 요소에 대 한 권장 되는 순서는 다음과 같습니다. TransactionFlow, ReliableSession, Security, CompositeDuplex, OneWay, StreamSecurity, MessageEncoding, 전송 합니다.  TransportBindingElement가 마지막에 와야 합니다. 지정된 바인딩 요소가 빌드되지 않았습니다.|  
|RuntimeRequiresInvoker0|디스패치 작업에 호출자가 필요합니다.|  
|ServiceHasZeroAppEndpoints|지정된 서비스에 애플리케이션(비인프라) 엔드포인트가 없습니다. 애플리케이션에 대해 구성 파일이 없거나, 서비스 이름과 일치하는 서비스 요소가 구성 파일에 없거나, 아니면 서비스 요소에 엔드포인트가 정의되지 않았기 때문입니다.|  
|SFxActionMismatch|동작이 일치하지 않아서 형식화된 메시지를 만들 수 없습니다. 지정된 동작이 필요한데 다른 동작이 있습니다.|  
|SFxAnonymousTypeNotSupported|유형이 익명이므로 지정된 메시지의 지정된 파트를 RPC로 내보내거나 인코딩할 수 없습니다.|  
|SFxBadMetadataLocationNoAppropriateBaseAddress|구성 섹션의 serviceMetadata 섹션에서 ExternalMetadataLocation 속성 또는 externalMetadataLocation 특성을 통해 ServiceMetadataBehavior에 제공된 URL이 상대적 URL이며, 이 URL을 확인할 수 있는 기본 주소가 없습니다.|  
|SFxBadMetadataMustBePolicy|지정된 네임스페이스와 이름을 가진 정책 XmlElement를 제공해야 합니다. 이 XmlElement에는 지정된 네임스페이스와 이름이 있습니다.|  
|SFxBodyObjectTypeCannotBeInherited|지정된 형식은 RPC 스타일에서 본문 개체로 사용할 개체 이외의 클래스에서 상속할 수 없습니다.|  
|SFxBodyObjectTypeCannotBeInterface|지정된 형식은 지정된 인터페이스를 구현하지만 이 인터페이스는 RPC 스타일의 본문 개체에 지원되지 않습니다.|  
|SFxCallbackBehaviorAttributeOnlyOnDuplex|CallbackBehaviorAttribute는 이중 계약이 있는 엔드포인트에서 동작으로만 실행될 수 있습니다. 지정된 계약은 이중 계약이 아니고 콜백 작업을 포함하지 않습니다.|  
|SFxCallbackRequestReplyInOrder1|현재 메시지의 처리가 완료될 때까지는 이 작업으로부터 회신을 받을 수 없습니다. 순서가 맞지 않는 메시지 처리를 허용하려면 지정한 대상에서 Reentrant 또는 Multiple의 ConcurrencyMode를 지정합니다.|  
|SfxCallbackTypeCannotBeNull|DuplexChannelFactory를 통해 지정된 계약을 사용하려면 계약에서 유효한 콜백 계약을 지정해야 합니다. 계약에 콜백 계약이 있으면 DuplexChannelFactory 대신 ChannelFactory를 사용합니다.|  
|SFxCannotGetMetadataFromLocation|MetadataExchangeClient는 HTTP 및 HTTPS MetadataLocations에서만 메타데이터를 가져올 수 있습니다. 지정된 위치에서는 메타데이터를 가져올 수 없습니다.|  
|SFxCannotHttpGetMetadataFromAddress|MetadataExchangeClient는 MetadataExchangeClientMode HttpGet을 사용할 때 HTTP 또는 HTTPS 주소에서만 메타데이터를 가져올 수 있습니다. 지정된 위치에서는 메타데이터를 가져올 수 없습니다.|  
|SFxCannotImportAsParameters_Bare|지정된 작업이 RPC 또는 문서 래핑이 아니므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_DifferentWrapperName|지정된 메시지의 래퍼 이름이 기본값과 일치하지 않으므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_DifferentWrapperNs|지정된 메시지의 래퍼 네임스페이스가 기본값과 일치하지 않으므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_ElementIsNotNillable|지정된 네임스페이스의 지정된 요소 이름이 nillable로 표시되지 않았으므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_HeadersAreUnsupported|지정된 메시지에 헤더가 있으므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_Message|지정된 작업에 인수 또는 반환 형식으로 형식화되지 않은 메시지가 있으므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_MessageHasProtectionLevel|지정된 메시지를 보호해야 하므로 메시지 계약을 생성합니다.|  
|SFxCannotImportAsParameters_NamespaceMismatch|지정된 메시지 부분 네임스페이스가 기본값과 일치하지 않으므로 메시지 계약을 생성합니다.|  
|SFxCannotRequireBothSessionAndDatagram3|지정된 계약이 SessionMode.NotAllowed를 지정하고 지정된 계약이 SessionMode.Required를 지정합니다. SessionMode 값 중 하나를 변경하거나 각 엔드포인트에 대해 다른 주소 또는 ListenURI를 지정합니다.|  
|SFxCannotSetExtensionsByIndex|이 컬렉션은 인덱스를 사용한 확장명 설정을 지원하지 않습니다. InsertItem 또는 RemoveItem 메서드를 사용합니다.|  
|SFxChannelDispatcherDifferentHost0|현재 ChannelDispatcher는 제공된 ServiceHost에 연결되어 있지 않습니다.|  
|SFxChannelDispatcherMultipleHost0|ChannelDispatcher를 여러 ServiceHost에 추가할 수 없습니다.|  
|SFxChannelDispatcherNoHost0|ServiceHost에 현재 연결되어 있지 않으므로 ChannelDispatcher를 열 수 없습니다.|  
|SfxChannelFactoryDisposed|ChannelFactory가 이미 삭제되었으므로 이 ChannelFactory를 열 수 없습니다. 사용하려면 먼저 ChannelFactory를 다시 만드십시오.|  
|SFxChannelFactoryNoBinding|바인딩이 엔드포인트에 연결되어 있지 않으므로 ChannelFactory를 열 수 없습니다. 생성자 또는 엔드포인트 속성을 사용하여 바인딩을 지정합니다.|  
|SFxChannelTerminated0|IsTerminating으로 표시된 작업이 이 채널에서 이미 호출되어, 채널의 연결이 끊어졌습니다. 이 채널에서 추가로 작업을 호출할 수 없습니다. 계속 통신하려면 채널을 다시 만드십시오.|  
|SFxCloseTimedOut1|지정된 이후에 ServiceHost 닫기 작업이 중지되었습니다. 클라이언트가 필요한 시간 이내에 세션 채널을 닫지 못했기 때문일 수 있습니다. 이 작업에 할당된 시간은 더 긴 제한 시간의 일부였을 수 있습니다.|  
|SfxCloseTimedOutWaitingForDispatchToComplete|서비스 발송이 완료되기를 기다리는 동안 닫기 프로세스가 시간 초과되었습니다.|  
|SFxCodeGenIsNotAssignableFrom|지정된 항목을 할당할 수 없습니다.|  
|SFxConfigChannelConfigurationNotFound|ServiceModel 클라이언트 구성 섹션에 지정된 이름과 계약을 가진 엔드포인트 요소가 없습니다.|  
|SFxConflictingGlobalElement|지정된 네임스페이스에서 지정된 이름을 가진 최상위 Extensible Markup Language 요소가 지정된 형식을 참조할 수 없습니다. 이 요소는 이미 다른 형식을 참조하고 있습니다. 다른 작업 이름 또는 MessageBodyAttribute를 사용하여 메시지 또는 메시지 부분에 다른 이름을 지정하십시오.|  
|SFxContractHasZeroInitiatingOperations|계약에는 최소한 하나의 IsInitiating=true 작업이 있어야 합니다.|  
|SFxContractHasZeroOperations|계약에는 최소한 하나의 작업이 있어야 합니다.|  
|SFxContractInheritanceRequiresInterfaces|지정된 형식의 서비스 클래스는 ServiceContract를 정의함과 동시에 지정된 형식에서 ServiceContract를 상속합니다. 인터페이스 유형 간에만 계약 상속을 사용할 수 있습니다. ServiceContractAttribute로 표시되어 있는 클래스는 계층 구조에서 ServiceContractAttribute가 있는 유일한 형식이여야 합니다.  지정된 형식의 ServiceContractAttribute를 지정된 형식이 구현하는 별도의 인터페이스로 이동하십시오.|  
|SFxCreateDuplexChannel1|지정된 계약의 콜백 계약이 존재하지 않거나 작업을 정의하지 않습니다. 이 계약이 이중 계약이 아니면 DuplexChannelFactory 대신 ChannelFactory를 사용하십시오.|  
|SFxCreateDuplexChannelNoCallback|이 CreateChannel 오버로드는 해당 DuplexChannelFactory 인스턴스에서 호출할 수 없습니다. DuplexChannelFactory가 InstanceContext로 초기화되지 않았습니다. InstanceContext를 가져오는 CreateChannel 오버로드를 호출하십시오.|  
|SFxCreateDuplexChannelNoCallback1|이 CreateChannel 오버로드는 해당 DuplexChannelFactory 인스턴스에서 호출할 수 없습니다. DuplexChannelFactory가 Type로 초기화되고 유효한 InstanceContext가 제공되지 않았습니다. InstanceContext를 가져오는 CreateChannel 오버로드를 호출하십시오.|  
|SFxCreateDuplexChannelNoCallbackUserObject|이 CreateChannel 오버로드는 해당 DuplexChannelFactory 인스턴스에서 호출할 수 없습니다. DuplexChannelFactory에 제공된 InstanceContext에 유효한 UserObject가 없습니다.|  
|SFxCreateNonDuplexChannel1|ChannelFactory는 지정된 계약을 지원하지 않습니다. ChannelFactory는 작업이 둘 이상인 콜백 계약을 정의합니다. ChannelFactory 대신 DuplexChannelFactory를 사용하십시오.|  
|SFxCustomBindingNeedsTransport1|지정된 계약을 가진 ServiceEndpoint의 CustomBinding에 TransportBindingElement가 없습니다. 모든 바인딩에는 TransportBindingElement에서 파생되는 하나 이상의 바인딩 요소가 있어야 합니다.|  
|SFxCustomBindingWithoutTransport|TransportBindingElement가 없으므로 이 사용자 지정 바인딩에 대해 스키마를 계산할 수 없습니다. 모든 바인딩에는 TransportBindingElement에서 파생되는 하나 이상의 바인딩 요소가 있어야 합니다.|  
|SFxDataContractSerializerDoesNotSupportBareArray|DataContractSerializer는 지정된 요소에 지정된 컬렉션을 지원하지 않습니다.|  
|SFxDictionaryIsEmpty|사전이 비어 있으므로 작업을 수행할 수 없습니다.|  
|SFxDocEncodedNotSupported|지정된 항목을 반영하는 동안 오류가 발생했습니다. Document-Encoded가 지원되지 않습니다. 'Use'를 Literal로 변경하거나 'Style'을 RPC로 변경하십시오.|  
|SFxDuplicateInitiatingActionAtSameVia|이 서비스에 지정된 위치에서 수신 대기하는 여러 개의 엔드포인트가 있습니다. 엔드포인트는 지정된 동일한 초기화 동작을 공유합니다. 디스패처가 메시지 처리를 위한 올바른 엔드포인트를 확인할 수 없으므로 이 동작 메시지는 삭제됩니다.|  
|SFXEndpointBehaviorUsedOnWrongSide|지정된 IEndpointBehavior를 서버에서 사용할 수 없습니다. 이 동작은 클라이언트에만 적용됩니다.|  
|SFxEndpointNoMatchingScheme|지정된 바인딩을 가진 엔드포인트에 대해 지정된 스키마와 일치하는 기본 주소가 없습니다. 등록된 기본 주소 스키마가 지정되었습니다.|  
|SFxErrorCreatingMtomReader|메시지 전송 최적화 메커니즘 메시지에 대한 판독기를 만드는 동안 오류가 발생했습니다.|  
|SFxErrorDeserializingFault|서버에서 잘못된 단순 개체 액세스 프로토콜 오류를 반환했습니다. 자세한 내용은 InnerException을 참조하십시오.|  
|SFxErrorDeserializingHeader|지정된 메시지에서 헤더 중 하나를 deserialize하는 동안 오류가 발생했습니다. 자세한 내용은 InnerException을 참조하십시오.|  
|SFxErrorReflectingOnMethod3|지정된 메서드의 지정된 특성을 지정된 형식으로 로드하는 동안 오류가 발생했습니다.  자세한 내용은 InnerException을 참조하십시오.|  
|SFxErrorReflectingOnParameter4|지정된 메서드의 지정된 매개 변수에서 지정된 특성을 지정된 형식으로 로드하는 동안 오류가 발생했습니다. 자세한 내용은 InnerException을 참조하십시오.|  
|SFxErrorReflectingOnType2|지정된 특성을 지정된 형식으로 로드하는 동안 오류가 발생했습니다.  자세한 내용은 InnerException을 참조하십시오.|  
|SFxErrorSerializingBody|지정된 메시지의 본문을 serialize하는 동안 오류가 발생했습니다. 자세한 내용은 InnerException을 참조하십시오.|  
|SFxErrorSerializingHeader|지정된 메시지에서 헤더 중 하나를 serialize하는 동안 오류가 발생했습니다. 자세한 내용은 InnerException을 참조하십시오.|  
|SFxExpectedIMethodCallMessage|내부 오류입니다. 메시지는 올바른 IMethodCallMessage여야 합니다.|  
|SFxExportMustHaveType|유효한 CLR 형식이 없으므로 지정된 작업의 지정된 부분을 내보낼 수 없습니다.|  
|SFxHeaderNotUnderstood|메시지가 처리되지 않았습니다. 이 메시지의 수신자가 지정된 네임스페이스의 지정된 헤더를 인식하지 못했습니다. 이 오류는 일반적으로 이 메시지의 발신자가 수신자가 처리할 수 없는 통신 프로토콜을 사용했다는 것을 의미합니다. 클라이언트 바인딩 구성이 서비스 바인딩과 일치하는지 확인합니다.|  
|SFxHeadersAreNotSupportedInEncoded|지정된 메시지에 원격 프로시저 호출 인코딩 스타일에 사용할 헤더가 없어야 합니다.|  
|SFxInconsistentWsdlOperationStyleInMessageParts|지정된 작업의 모든 메시지 부분에 형식 또는 요소가 포함되어 있어야 합니다.|  
|SFxInconsistentWsdlOperationStyleInOperationMessages|지정된 작업에서 메시지로부터 유추된 지정된 스타일이 바인딩을 사용하여 지정한 예상 스타일과 일치하지 않습니다.|  
|SFxInvalidCallbackIAsyncResult|IAsyncResult가 제공되지 않거나 형식이 잘못되었습니다.|  
|SFxInvalidMessageBody|OperationFormatter에서 잘못된 메시지 본문을 발견했습니다. 지정된 이름과 네임스페이스를 가진 'Element' 노드 형식이 필요합니다. 지정된 이름과 네임스페이스를 가진 지정된 노드 형식이 있습니다.|  
|SFxInvalidMessageBodyEmptyMessage|메시지가 비어 있으므로 OperationFormatter가 메시지의 정보를 deserialize할 수 없습니다.|  
|SFxInvalidMessageBodyErrorDeserializingParameter|지정된 매개 변수를 deserialize하는 동안 오류가 발생했습니다. 자세한 내용은 InnerException을 참조하십시오.|  
|SFxInvalidMessageBodyErrorSerializingParameter|지정된 매개 변수를 serialize하는 동안 오류가 발생했습니다. InnerException 메시지가 지정되었습니다.  자세한 내용은 InnerException을 참조하십시오.|  
|SFxInvalidMessageBodyUnexpectedNode|매개 변수를 deserialize하는 동안 지정된 네임스페이스에서 지정된 예기치 않은 노드를 발견했습니다.|  
|SFxInvalidMessageContractSignature|지정된 작업에 MessageContractAttribute로 표시된 매개 변수 또는 반환 형식이 있습니다. 메시지 계약을 사용하여 요청 메시지를 나타낼 경우 작업에 MessageContractAttribute로 표시된 단일 매개 변수가 있어야 합니다. 메시지 계약을 사용하여 응답 메시지를 나타낼 경우 작업의 반환 값이 MessageContractAttribute로 표시된 형식이어야 합니다. 작업은 'out' 또는 'ref' 매개 변수를 가질 수 없습니다.|  
|SFxInvalidReplyAction|작업에 대해 나가는 회신 메시지에 지정된 Action이 있지만 해당 작업에 대한 계약에서 다른 ReplyAction을 지정합니다. 메시지에 지정된 Action이 계약의 ReplyAction과 일치하거나, 작업 계약이 ReplyAction='*'를 지정해야 합니다.|  
|SFxInvalidRequestAction|작업에 대해 나가는 요청 메시지에 지정된 Action이 있지만 해당 작업에 대한 계약에서 다른 RequestAction을 지정합니다. 메시지에 지정된 Action이 계약의 RequestAction과 일치하거나, 작업 계약이 RequestAction='*'를 지정해야 합니다.|  
|SFxInvalidStaticOverloadCalledForDuplexChannelFactory1|해당 계약이 콜백 계약을 정의하므로 지정된 계약에서 정적 CreateChannel 메서드를 사용할 수 없습니다. 정적 CreateChannel 오버 로드 중 하나를 사용 하 여\<TChannel >.|  
|SFxInvalidStreamInRequest|지정된 작업의 요청이 스트림이 되려면 형식이 Stream인 단일 매개 변수가 작업에 있어야 합니다.|  
|SFxInvalidStreamInResponse|지정된 작업의 응답이 스트림이 되려면 형식이 Stream인 반환 값이나 단일 out 매개 변수가 작업에 있어야 합니다.|  
|SFxInvalidStreamInTypedMessage|메시지 계약 프로그래밍 모델에서 스트림을 사용하려면 형식이 Stream인 단일 MessageBody 멤버가 지정된 형식에 있어야 합니다.|  
|SFxInvalidUseOfPrimitiveOperationFormatter|지원하지 않는 매개 변수 또는 반환 형식을 PrimitiveOperationFormatter에 제공했습니다.|  
|SFxMessageContractBaseTypeNotValid|지정된 형식은 MessageContract를 정의하며 MessageContract를 정의하지 않는 지정된 형식에서 파생됩니다. 지정된 상속 계층 구조에 속한 모든 개체가 MessageContract를 정의해야 합니다.|  
|SFxMethodNotSupported1|지정된 메서드가 이 개체에서 지원되지 않습니다. 메서드가 OperationContractAttribute로 표시되지 않거나 인터페이스 형식이 ServiceContractAttribute로 표시되지 않으면 이러한 현상이 발생할 수 있습니다.|  
|SFxMethodNotSupportedByType2|지정된 ServiceHost 구현 형식은 지정된 서비스 계약을 구현하지 않습니다.|  
|SFxMethodNotSupportedOnCallback1|지정된 콜백 메서드가 지원되지 않습니다. 메서드가 OperationContractAttribute로 표시되지 않거나 인터페이스 형식이 ServiceContractAttribute CallbackContract의 대상이 아닌 경우 이러한 현상이 발생할 수 있습니다.|  
|SFxMismatchedOperationParent|부모 DispatchRuntime 또는 ClientRuntime에만 DispatchOperation 또는 ClientOperation을 각각 추가할 수 있습니다.|  
|SFxNameCannotBeEmpty|Name 속성은 빈 문자열일 수 없습니다.|  
|SfxNoTypeSpecifiedForParameter|매개 변수에 대한 CLR 형식을 지정하지 않아 작업이 생성되지 않습니다.|  
|SFxOperationBehaviorAttributeOnlyOnServiceClass|OperationBehaviorAttribute는 서비스 클래스로만 이동할 수 있으며 ServiceContract 인터페이스에는 넣을 수는 없습니다. 지정된 형식의 지정된 메서드가 이 규칙을 위반합니다.|  
|SFxOperationContractOnNonServiceContract|지정된 메서드가 OperationContractAttribute로 표시되어 있지만 바깥쪽 지정된 형식이 ServiceContractAttribute로 표시되어 있지 않습니다. OperationContractAttribute는 ServiceContractAttribute 형식 또는 CallbackContract 형식의 메서드에서만 사용할 수 있습니다.|  
|SFxParameterCountMismatch|제공된 인수의 수와 필요한 인수의 수가 일치하지 않습니다. 특히 지정된 인수에는 지정된 수의 요소가 있는 반면, 필요한 인수에는 지정된 수의 요소가 있습니다.|  
|SFxPartNameMustBeUniqueInRpc|지정된 메시지 부분의 이름이 원격 프로시저 호출 메시지에서 고유하지 않습니다.|  
|SFxReplyActionMismatch3|지정된 동작의 지정된 작업에 대해 회신 메시지를 받았습니다. 그러나 클라이언트 코드에서는 지정된 동작이 필요합니다.|  
|SFxRequestReplyNone|"None" 주소를 대상으로 하는 WS-Addressing ReplyTo 또는 FaultTo 헤더가 있는 메시지를 받았습니다. 이 값은 요청-회신 작업에 유효하지 않습니다. "None"인 ReplyTo 또는 FaultTo 값을 지원하려면 단방향 작업을 사용하거나 ManualAddressing을 사용하십시오.|  
|SFxRequestTimedOut1|이 요청 작업이 지정된 구성 시간 내에 회신을 받지 못했습니다. 허용된 시간은 더 긴 제한 시간의 일부였을 수 있습니다. 서비스에서 작업을 아직 처리 중이거나 회신 메시지를 보낼 수 없기 때문일 수 있습니다.|  
|SFxRequestTimedOut2|지정된 위치로 보낸 요청 작업이 지정된 구성 시간 내에 회신을 받지 못했습니다. 허용된 시간은 더 긴 제한 시간의 일부였을 수 있습니다. 서비스에서 작업을 아직 처리 중이거나 회신 메시지를 보낼 수 없기 때문일 수 있습니다.|  
|SFxSchemaDoesNotContainType|지정된 대상 네임스페이스를 가진 스키마에 지정된 이름을 가진 형식이 없습니다.|  
|SfxServiceContractAttributeNotFound|지정된 계약 형식의 특성이 ServiceContractAttribute가 아닙니다. 유효한 계약을 정의하려면 지정한 형식의 특성이 ServiceContractAttribute여야 합니다. 형식은 계약 인터페이스 또는 서비스 클래스일 수 있습니다.|  
|SFxServiceContractGeneratorConfigRequired|GenerateServiceEndpoint 메서드를 사용하여 구성 정보를 생성하려면 유효한 구성 개체를 사용하여 ServiceContractGenerator 인스턴스를 초기화해야 합니다.|  
|SFxServiceHostBaseCannotAddEndpointAfterOpen|ServiceHost가 다음 상태 중 하나가 된 후에는 엔드포인트를 추가할 수 없습니다.<br /><br /> -열<br />오류 처리 되어<br />-종료<br />닫힘|  
|SFxServiceHostBaseCannotAddEndpointWithoutDescription|Description 속성을 초기화하기 전에는 엔드포인트를 추가할 수 없습니다.|  
|SFxServiceMetadataBehaviorNoHttpBaseAddress|ServiceMetadataBehavior의 HttpGetEnabled 속성이 true로 설정되어 있고 HttpGetUrl 속성이 상대 주소이지만 HTTP 기본 주소가 없습니다. HTTP 기본 주소를 제공하거나 HttpGetUrl을 절대 주소로 설정합니다.|  
|SFxServiceMetadataBehaviorNoHttpsBaseAddress|ServiceMetadataBehavior의 HttpsGetEnabled 속성이 true로 설정되어 있고 HttpsGetUrl 속성이 상대 주소이지만 HTTPS 기본 주소가 없습니다. HTTPS 기본 주소를 제공하거나 HttpsGetUrl을 절대 주소로 설정합니다.|  
|SFxServiceMetadataBehaviorUrlMustBeHttpOrRelative|동작 URL은 상대 URI(Uniform Resource Identifier)이거나 지정된 스키마를 가진 절대 URI(Uniform Resource Identifier)여야 합니다. 지정된 URL은 지정된 스키마를 가진 절대 URI(Uniform Resource Identifier)입니다.|  
|SFxStreamRequestMessageClosed|이 스트림을 포함하는 메시지가 닫혔습니다. 서비스 작업이 반환된 후에는 요청 스트림에 액세스할 수 없습니다.|  
|SFxStreamResponseMessageClosed|이 스트림을 포함하는 메시지가 닫혔습니다.|  
|SFxTerminateRequestProcessingException|작업 파이프라인의 확장명이 이 메시지 처리를 종료해야 합니다.|  
|SFxTerminatingOperationAlreadyCalled1|IsTerminating 작업을 호출했으므로 이 채널에서 추가 메시지를 보낼 수 없습니다.|  
|SFxThrottleLimitMustBeGreaterThanZero0|스로틀 한계는 0보다 커야 합니다. 스로틀 한계를 사용하지 않으려면 값을 Int32.MaxValue로 설정하십시오.|  
|SFxTypedOrUntypedMessageCannotBeMixedWithVoidInRpc|RPC 인코딩 스타일을 사용할 경우 작업에 매개 변수가 없거나 void 반환 값이 있으면 메시지 계약 형식 또는 System.ServiceModel.Channels.Message 형식을 사용할 수 없습니다. 빈 메시지 계약 형식을 지정된 작업에 매개 변수 또는 반환 값으로 추가하십시오.|  
|SFxUserCodeThrewException|지정된 사용자 작업이 사용자 코드에서 처리되지 않는 예외를 throw했습니다. 이 문제가 반복되면 지정된 메서드의 구현에 오류가 있다는 의미일 수 있습니다.|  
|SfxUseTypedMessageForCustomAttributes|지정된 매개 변수는 추가 특성이 필요하므로 작업 매개 변수에 매핑할 수 없습니다.|  
|SFxVersionMismatchInOperationContextAndMessage2|OperationContext.Current의 MessageVersion이 처리할 메시지의 헤더 버전과 일치하지 않으므로 메시지에 나가는 헤더를 추가할 수 없습니다.|  
|SFxWellKnownNonSingleton0|서비스 인스턴스를 사용하는 ServiceHost 생성자 중 하나를 사용하려면 서비스의 InstanceContextMode를 InstanceContextMode.Single로 설정해야 합니다. ServiceBehaviorAttribute를 통해 이렇게 구성할 수 있습니다. 아니면 Type 인수를 사용하는 ServiceHost 생성자를 사용하십시오.|  
|SFxWrapperTypeHasMultipleNamespaces|네임스페이스가 여러 개이므로 지정된 메시지에 대한 래퍼 형식을 데이터 계약 형식으로 나타낼 수 없습니다. XmlSerializer를 사용하십시오.|  
|UriMustBeAbsolute|URI는 절대 URI여야 합니다.|
