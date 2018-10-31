---
title: 보안 예외
ms.date: 03/30/2017
ms.assetid: 76d5e5cd-e4f4-404f-9a5a-ec3522494ad8
ms.openlocfilehash: c1eeca9111837b9833de54ecafbc981d1c2b6343
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201376"
---
# <a name="security-exceptions"></a>보안 예외
이 항목에서는 모든 보안 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|AnonymousLogonsAreNotAllowed|서비스에서 익명 로그온을 허용하지 않습니다.|  
|AtLeastOneContractOperationRequestRequiresProtectionLevelNotSupportedByBinding|요청 메시지를 보호해야 합니다. 지정된 계약의 작업에 이 보호가 필요합니다. 보호는 지정된 바인딩에 의해 제공되어야 합니다.|  
|AtLeastOneContractOperationResponseRequiresProtectionLevelNotSupportedByBinding|응답 메시지를 보호해야 합니다. 지정된 계약의 작업에 이 보호가 필요합니다. 보호는 지정된 바인딩에 의해 제공되어야 합니다.|  
|AtMostOnePrimarySignatureInReceiveSecurityHeader|하나의 주 서명만 보안 헤더에서 허용됩니다.|  
|BadContextTokenFaultReason|보안 컨텍스트 토큰이 만료되었거나 잘못되었습니다. 메시지가 처리되지 않았습니다.|  
|BadEncryptionState|EncryptedData 또는 EncryptedKey가 이 작업에 사용할 수 없는 상태입니다.|  
|BasicHttpMessageSecurityRequiresCertificate|BasicHttp 바인딩에서는 BasicHttpBinding.Security.Message.ClientCredentialType이 보안 메시지에 대한 BasicHttpMessageCredentialType.Certificate 자격 증명 형식과 동일해야 합니다. UserName 자격 증명에 대해 Transport 또는 TransportWithMessageCredential 보안을 선택하십시오.|  
|BasicTokenCannotBeWrittenWithoutEncryption|기본 토큰은 암호화 없이 쓸 수 없습니다.|  
|BindingDoesNotSupportProtectionForRst|지정된 계약에 대해 지정된 바인딩이 SecureConversation으로 구성되었지만 인증 모드가 협상에 필요한 요청/회신 기반 무결성 및 기밀성을 제공할 수 없습니다.|  
|BindingDoesNotSupportWindowsIdenityForImpersonation|지정된 계약 작업에는 자동 가장을 위한 Windows ID가 필요합니다. 호출자를 나타내는 Windows ID는 지정된 계약에 대해 지정된 바인딩에 의해 제공되지 않습니다.|  
|CachedNegotiationStateQuotaReached|지정된 용량에 도달했기 때문에 서비스가 협상 상태를 캐시할 수 없습니다. 요청을 다시 시도하십시오.|  
|CacheQuotaReached|항목을 추가할 수 없습니다. 최대 캐시 크기가 지정되었습니다.|  
|CannotDetermineSPNBasedOnAddress|클라이언트가 SspiNegotiation/Kerberos 용도로 지정된 대상 주소의 ID에 기초하여 서비스 사용자 이름을 확인할 수 없습니다. 대상 주소 id는 UPN id 여야 합니다 (예: acmedomain\\\alice) 또는 SPN id (예 호스트/bobs-machine).|  
|CannotFindCert|지정된 검색 조건인 StoreName, StoreLocation, FindType, FindValue를 사용하여 X.509 인증서를 찾을 수 없습니다.|  
|CannotFindCertForTarget|지정된 대상에 대해 지정된 검색 조건인 StoreName, StoreLocation, FindType, FindValue를 사용하여 X.509 인증서를 찾을 수 없습니다.|  
|CannotFindCorrelationStateForApplyingSecurity|응답자에서의 회신에 보안을 적용하기 위한 상관 관계 상태를 찾을 수 없습니다.|  
|CannotFindNegotiationState|지정된 컨텍스트에 대한 협상 상태를 찾을 수 없습니다.|  
|CannotFindSecuritySession|지정된 ID가 있는 보안 세션을 찾을 수 없습니다.|  
|CannotImportProtectionLevelForContract|프로세스를 가져오기 위한 정책이 지정된 계약에 대한 바인딩을 가져올 수 없습니다. 바인딩에 대한 보호 요구 사항이 계약에 대해 이미 가져온 바인딩과 호환되지 않습니다. 바인딩을 다시 구성해야 합니다.|  
|CannotImportSupportingTokensForOperationWithoutRequestAction|보안 정책을 가져오지 못했습니다. 보안 정책이 작업 범위에서 지원 토큰 요구 사항을 포함하고 있습니다. 계약 설명이 이 작업과 연결된 요청 메시지에 대한 동작을 지정하지 않습니다.|  
|CannotIssueRstTokenType|토큰 또는 지정된 형식을 발급할 수 없습니다.|  
|CannotObtainIssuedTokenKeySize|발급된 토큰의 키 크기를 확인할 수 없습니다.|  
|CannotPerformImpersonationOnUsernameToken|클라이언트 토큰을 사용하는 가장은 불가능합니다. 지정된 계약에 대해 지정된 바인딩이 멤버 자격 공급자가 등록된 클라이언트 인증을 위해 사용자 이름 보안 토큰을 사용합니다. 클라이언트에 대한 다른 형식의 보안 토큰을 사용하십시오.|  
|CannotPerformS4UImpersonationOnPlatform|지정된 계약에 대해 지정된 바인딩이 [!INCLUDE[ws2003](../../../../../includes/ws2003-md.md)] 및 최신 버전의 Windows에서만 가장을 지원합니다. 취소를 사용하도록 설정된 보안 대화와 함께 SspiNegotiated 인증 및 바인딩을 사용하십시오.|  
|CannotReadKeyIdentifier|지정된 네임스페이스를 가진 지정된 요소에서 KeyIdentifier를 읽을 수 없습니다.|  
|CannotReadToken|BinarySecretSecurityToken에 대해 지정된 네임스페이스를 가진 지정된 요소에서 지정된 ValueType의 토큰을 읽을 수 없습니다. 이 요소가 올바른지 보려면 보안이 해당 이름, 네임스페이스 및 값 형식이 지정된 토큰을 사용하도록 구성되었는지 확인하십시오.|  
|CertificateUnsupportedForHttpTransportCredentialOnly|인증서 기반 클라이언트 인증이 TransportCredentialOnly 보안 모드에서 지원되지 않습니다. Transport 보안 모드를 선택하십시오.|  
|ClaimTypeCannotBeEmpty|claimType은 빈 문자열일 수 없습니다.|  
|ClientCertificateNotProvided|클라이언트에 대한 인증서가 제공되지 않았습니다. ClientCredentials 또는 ServiceCredentials에서 인증서를 설정할 수 있습니다.|  
|ClientCredentialTypeMustBeSpecifiedForMixedMode|ClientCredentialType.None은 TransportWithMessageCredential 보안 모드에 사용할 수 없습니다. 자격 증명 형식을 지정하거나 다른 보안 모드를 사용하십시오.|  
|ConfigurationSchemaInsuffientForSecurityBindingElementInstance|구성 스키마가 다음 보안 바인딩 요소의 비표준 구성을 설명하는 데 충분하지 않습니다.|  
|DerivedKeyTokenGenerationAndLengthTooHigh|파생 키의 지정된 생성 및 길이로 인해 허용되는 최대 오프셋보다 큰 키 파생 오프셋이 발생합니다.|  
|DnsIdentityCheckFailedForIncomingMessage|들어오는 메시지의 ID를 검사하지 못했습니다. 원격 엔드포인트의 필요한 DNS(Domain Name System) ID가 지정되었습니다. 원격 엔드포인트가 지정된 DNS(Domain Name System) 클레임을 제공했습니다. 이 엔드포인트가 올바른 원격 엔드포인트인 경우 채널 프록시를 만들 때 Domain Name System ID를 EndpointAddress의 Identity 속성으로 지정하여 이 문제를 해결할 수 있습니다.|  
|DnsIdentityCheckFailedForOutgoingMessage|보내는 메시지의 ID를 검사하지 못했습니다. 원격 엔드포인트에 지정된 Domain Name System ID가 있어야 합니다. 원격 엔드포인트가 DNS(Domain Name System) 클레임을 제공했습니다. 이 엔드포인트가 올바른 원격 엔드포인트인 경우 채널 프록시를 만들 때 DNS ID를 EndpointAddress의 Identity 속성으로 명시적으로 지정하여 이 문제를 해결할 수 있습니다.|  
|DuplicateIdInMessageToBeVerified|확인을 위해 제공된 메시지에서 지정된 ID가 두 번 발견되었습니다.|  
|EmptyBase64Attribute|필수 base-64 특성 이름 및 네임스페이스에 대한 빈 값을 찾았습니다.|  
|ExportOfBindingWithAsymmetricAndTransportSecurityNotSupported|보안 정책을 내보내지 못했습니다. 바인딩에 AsymmetricSecurityBindingElement 및 보안 전송 바인딩 요소가 모두 포함되어 있습니다. 이러한 바인딩에 대한 정책 내보내기가 지원되지 않습니다.|  
|ExportOfBindingWithSymmetricAndTransportSecurityNotSupported|보안 정책을 내보내지 못했습니다. 바인딩에 SymmetricSecurityBindingElement 및 보안 전송 바인딩 요소가 모두 포함되어 있습니다. 이러한 바인딩에 대한 정책 내보내기가 지원되지 않습니다.|  
|ExportOfBindingWithTransportSecurityBindingElementAndNoTransportSecurityNotSupported|보안 정책을 내보내지 못했습니다. 바인딩에 TransportSecurityBindingElement가 포함되어 있지만 ITransportTokenAssertionProvider를 구현하는 전송 바인딩 요소가 없습니다. 이러한 바인딩에 대한 정책 내보내기가 지원되지 않습니다. 바인딩의 전송 바인딩 요소가 ITransportTokenAssertionProvider 인터페이스를 구현하는지 확인하십시오.|  
|FoundMultipleCerts|지정된 검색 조건을 사용하여 여러 X.509 인증서를 찾았습니다. StoreName, StoreLocation, FindType, FindValue. 더 구체적인 찾기 값을 제공하십시오.|  
|FoundMultipleCertsForTarget|지정된 검색 조건을 사용하여 여러 X.509 인증서를 찾았습니다. StoreName, StoreLocation, FindType, FindValue(지정된 대상에 대한). 더 구체적인 찾기 값을 제공하십시오.|  
|HeaderDecryptionNotSupportedInWsSecurityJan2004|SecurityVersion.WSSecurityJan2004가 헤더 암호 해독을 지원하지 않습니다. SecurityVersion.WsSecurityXXX2005 이상을 사용하거나 전송 보안을 사용하여 전체 메시지를 암호화하십시오.|  
|IdentityCheckFailedForIncomingMessage|들어오는 메시지의 ID를 검사하지 못했습니다. 대상 엔드포인트에 대해 필요한 ID가 지정되었습니다.|  
|IdentityCheckFailedForOutgoingMessage|보내는 메시지의 ID를 검사하지 못했습니다. 대상 엔드포인트에 대해 필요한 ID가 지정되었습니다.|  
|IncorrectSpnOrUpnSpecified|SSPI(보안 지원 공급자 인터페이스) 인증에 실패했습니다. 서버가 지정된 ID를 가진 계정에서 실행 중이 아닐 수 있습니다. 서버가 서비스 계정(예: 네트워크 서비스)에서 실행 중인 경우 계정의 ServicePrincipalName을 서버의 EndpointAddress에서 ID로 지정하세요. 서버가 사용자 계정에서 실행 중인 경우 계정의 UserPrincipalName을 서버의 EndpointAddress에서 ID로 지정하세요.|  
|InvalidAttributeInSignedHeader|지정한 서명된 헤더에 지정된 특성이 있습니다. 필요한 특성이 지정되었습니다.|  
|InvalidCloseResponseAction|보안 세션 닫기 응답이 지정된 잘못된 동작과 함께 수신되었습니다.|  
|InvalidQName|QName이 잘못되었습니다.|  
|InvalidRenewResponseAction|보안 세션 갱신 응답이 지정된 잘못된 동작과 함께 수신되었습니다.|  
|InvalidSspiNegotiation|보안 지원 공급자 인터페이스 협상에 실패했습니다.|  
|IssuerBindingNotPresentInTokenRequirement|보안 토큰 관리자에서는 보안 대화를 설명하는 토큰 요구 사항에 부트스트랩 보안 바인딩 요소를 지정해야 합니다. 지정된 토큰 요구 사항은 다음과 같습니다.|  
|KeyLengthMustBeMultipleOfEight|지정된 키 길이가 대칭 키에 대하여 8의 배수가 아닙니다.|  
|LsaAuthorityNotContacted|내부 SSL 오류입니다(자세한 내용은 Win32 상태 코드 참조). 서버 인증서를 검사하여 키 교환을 수행할 수 있는지 확인하십시오.|  
|MaximumPolicyRedirectionsExceeded|재귀 정책 반입 한도에 도달했습니다. 페더레이션 서비스 체인에 루프가 있는지 확인하십시오.|  
|MessagePartSpecificationMustBeImmutable|메시지 부분 지정을 설정하기 전에 상수로 만들어야 합니다.|  
|MissingCustomCertificateValidator|X509CertificateValidationMode.Custom에는 CustomCertificateValidator가 필요합니다. CustomCertificateValidator 속성을 지정하십시오.|  
|MissingCustomUserNamePasswordValidator|UserNamePasswordValidationMode.Custom에는 CustomUserNamePasswordValidator가 필요합니다. CustomUserNamePasswordValidator 속성을 지정하십시오.|  
|MissingMembershipProvider|UserNamePasswordValidationMode.MembershipProvider에는 MembershipProvider가 필요합니다. MembershipProvider 속성을 지정하십시오.|  
|NoBinaryNegoToSend|상대방에게 이진 협상이 보내지지 않았습니다.|  
|NoEncryptionPartsSpecified|지정된 동작을 가진 메시지에 대해 암호화 메시지 부분이 지정되지 않았습니다.|  
|NoKeyInfoInEncryptedItemToFindDecryptingToken|암호 해독 토큰을 찾기 위한 KeyInfo 값을 암호화된 항목에서 찾을 수 없습니다.|  
|NonceLengthTooShort|지정된 nonce가 너무 짧습니다. 필요한 최소 nonce 길이는 4바이트입니다.|  
|NoOutgoingEndpointAddressAvailableForDoingIdentityCheck|보낼 메시지의 ID를 검사하는 데 사용할 수 있는 보내는 EndpointAddress가 없습니다.|  
|NoOutgoingEndpointAddressAvailableForDoingIdentityCheckOnReply|수신한 회신의 ID를 검사하는 데 사용할 수 있는 보내는 EndpointAddress가 없습니다.|  
|NoPartsOfMessageMatchedPartsToSign|제공된 메시지 부분 지정과 일치하는 메시지 부분이 없기 때문에 서명이 만들어지지 않았습니다.|  
|NoPrincipalSpecifiedInAuthorizationContext|사용자 지정 사용자가 권한 부여 컨텍스트에 지정되지 않았습니다.|  
|NoSignatureAvailableInSecurityHeaderToDoReplayDetection|재생 검색에 대한 nonce를 제공하는 데 사용할 수 있는 서명이 보안 헤더에 없습니다.|  
|NoSignaturePartsSpecified|지정된 동작을 가진 메시지에 대해 서명 메시지 부분이 지정되지 않았습니다.|  
|NoSigningTokenAvailableToDoIncomingIdentityCheck|들어오는 ID 검사를 수행하는 데 사용할 수 있는 서명 토큰이 없습니다.|  
|NoTimestampAvailableInSecurityHeaderToDoReplayDetection|재생 검색을 수행하는 데 사용할 수 있는 타임스탬프가 보안 헤더에 없습니다.|  
|NoTransportTokenAssertionProvided|보안 정책을 내보내지 못했습니다. 지정된 형식의 제공된 전송 토큰 어설션이 sp:TransportBinding 보안 정책 어설션을 포함하기 위한 전송 토큰 어설션을 만들지 않았습니다.|  
|OnlyOneOfEncryptedKeyOrSymmetricBindingCanBeSelected|대칭 보안 프로토콜을 대칭 토큰 공급자 및 대칭 토큰 인증자로 구성하거나 비대칭 토큰 공급자로 구성할 수 있습니다. 둘 모두로 구성할 수는 없습니다.|  
|OperationCannotBeDoneOnReceiverSideSecurityHeaders|수신자 보안 헤더에서 이 작업을 수행할 수 없습니다.|  
|OperationDoesNotAllowImpersonation|지정된 이름 및 네임스페이스를 가진 계약에 속한 지정된 서비스 작업에서 가장이 허용되지 않습니다.|  
|PolicyRequiresConfidentialityWithoutIntegrity|지정된 동작에 대한 메시지 보안 정책에는 무결성 없는 기밀성이 필요합니다. 무결성 없는 기밀성은 지원되지 않습니다.|  
|PrimarySignatureIsRequiredToBeEncrypted|주 서명은 암호화되어야 합니다.|  
|PropertySettingErrorOnProtocolFactory|지정된 보안 프로토콜 팩터리의 필수 속성이 설정되지 않았거나 그 값이 잘못되었습니다.|  
|ProtocolFactoryCouldNotCreateProtocol|프로토콜 팩터리가 프로토콜을 만들 수 없습니다.|  
|PublicKeyNotRSA|공개 키가 RSA 키가 아닙니다.|  
|RequiredMessagePartNotEncrypted|지정된 필수 메시지 부분이 암호화되지 않았습니다.|  
|RequiredMessagePartNotEncryptedNs|지정된 필수 메시지 부분이 암호화되지 않았습니다.|  
|RequiredMessagePartNotSigned|지정된 필수 메시지 부분이 서명되지 않았습니다.|  
|RequiredMessagePartNotSignedNs|지정된 필수 메시지 부분이 서명되지 않았습니다.|  
|RequiredSecurityHeaderElementNotSigned|지정된 ID가 있는 지정된 보안 헤더 요소에 서명해야 합니다.|  
|RequiredSecurityTokenNotEncrypted|지정된 첨부 모드를 가진 지정된 보안 토큰을 암호화해야 합니다.|  
|RequiredSecurityTokenNotSigned|지정된 첨부 모드를 가진 지정된 보안 토큰에 서명해야 합니다.|  
|RequiredSignatureMissing|서명이 보안 헤더에 있어야 합니다.|  
|RequireNonCookieMode|지정된 네임스페이스를 가진 지정된 바인딩이 쿠키 보안 컨텍스트 토큰을 발급하도록 구성되었습니다. COM+ 통합 서비스가 쿠키 보안 컨텍스트 토큰을 지원하지 않습니다.|  
|RevertingPrivilegeFailed|지정된 예외로 인해 되돌리기 작업에 실패했습니다.|  
|RSTRAuthenticatorIncorrect|RequestSecurityTokenResponse CombinedHash가 잘못되었습니다.|  
|SecureConversationCancelNotAllowedFaultReason|보안 대화 취소가 바인딩에서 허용되지 않습니다.|  
|SecureConversationDriverVersionDoesNotSupportSession|구성된 SecureConversation 버전이 세션을 지원하지 않습니다. WSSecureConversationFeb2005 이상을 사용하십시오.|  
|SecureConversationRequiredByReliableSession|보안 대화 없이 신뢰할 수 있는 세션을 설정할 수 없습니다. 보안 대화를 사용하도록 설정하십시오.|  
|SecurityAuditFailToLoadDll|지정된 동적 연결 라이브러리(dll)를 로드할 수 없습니다.|  
|SecurityAuditNotSupportedOnChannelFactory|SecurityAuditBehavior가 채널 팩터리에서 지원되지 않습니다.|  
|SecurityAuditPlatformNotSupported|감사 메시지를 보안 로그에 쓰는 것이 현재 플랫폼에서 지원되지 않습니다. 감사 메시지는 응용 프로그램 로그에 써야 합니다.|  
|SecurityBindingElementCannotBeExpressedInConfig|엔드포인트에 대한 보안 정책을 가져왔습니다. Windows Communication Foundation 구성에서 나타낼 수 없는 요구 사항이 보안 정책에 포함되어 있습니다. 생성된 구성 파일에서 필요한 SecurityBindingElement 매개 변수에 대한 설명을 확인하십시오. 코드를 사용하여 올바른 바인딩 요소를 만드십시오. 구성 파일에 있는 바인딩 구성은 보안되지 않습니다.|  
|SecurityBindingSupportsOneWayOnly|지정된 계약의 지정된 바인딩에 대한 SecurityBinding은 OneWay 작업만 지원합니다.|  
|SecurityContextDoesNotAllowImpersonation|지정된 동작을 가진 요청 메시지의 UltimateReceiver 역할에 대한 SecurityContext가 Windows ID에 매핑되지 않기 때문에 가장을 시작할 수 없습니다.|  
|SecurityListenerClosing|수신기를 닫는 중이기 때문에 새 보안 대화를 수신기에서 수락하지 않습니다.|  
|SecurityListenerClosingFaultReason|서버를 닫는 중이기 때문에 새 보안 대화를 서버에서 수락하지 않습니다. 나중에 다시 시도하십시오.|  
|SecurityProtocolFactoryShouldBeSetBeforeThisOperation|이 작업을 수행하기 전에 보안 프로토콜 팩터리를 설정해야 합니다.|  
|SecuritySessionAbortedFaultReason|보안 세션이 종료되었습니다. 이것은 세션에서 메시지가 너무 오래 수신되지 않았기 때문일 수 있습니다|  
|SecuritySessionKeyIsStale|세션 키가 응용 프로그램 메시지를 보안할 수 있으려면 먼저 세션 키를 갱신해야 합니다.|  
|SecuritySessionLimitReached|보안 세션을 만들 수 없습니다 나중에 다시 시도하십시오.|  
|SecuritySessionNotPending|지정된 ID가 있는 보안 세션 중 보류 중인 세션이 없습니다.|  
|SecurityTokenParametersHasIncompatibleInclusionMode|지정된 바인딩이 호환되지 않는 지정된 보안 토큰 포함 모드를 가지는 보안 토큰 매개 변수로 구성되었습니다. 대체 보안 토큰 포함 모드를 지정하십시오.|  
|SecurityVersionDoesNotSupportEncryptedKeyBinding|지정된 계약에 대해 지정된 바인딩이 EncryptedKeys에 대한 연결되지 않은 참조를 지원하지 않는 호환되지 않는 보안 버전으로 구성되었습니다. 지정된 값 이상을 바인딩에 대한 보안 버전으로 사용하십시오.|  
|SecurityVersionDoesNotSupportSignatureConfirmation|지정된 SecurityVersion이 서명 확인을 지원하지 않습니다. 이후의 SecurityVersion을 사용하십시오.|  
|SecurityVersionDoesNotSupportThumbprintX509KeyIdentifierClause|지정된 계약에 대해 지정된 바인딩이 인증서의 지문 값을 사용하는 X.509 토큰에 대한 외부 참조를 지원하지 않는 보안 버전으로 구성되었습니다. 지정된 값 이상을 바인딩에 대한 보안 버전으로 사용하십시오.|  
|SenderSideSupportingTokensMustSpecifySecurityTokenParameters|각 메시지에 대해 지원 토큰을 사용하여 보안 토큰 매개 변수를 지정해야 합니다.|  
|ServerCertificateNotProvided|수신자가 자체 인증서를 제공하지 않습니다. TLS 프로토콜에서는 이 인증서가 필요합니다. 양 당사자는 자체 인증서에 액세스해야 합니다.|  
|SignatureConfirmationNotSupported|구성된 SecurityVersion이 서명 확인을 지원하지 않습니다. WSSecurityXXX2005 이상을 사용하십시오.|  
|SignatureConfirmationRequiresRequestReply|서명 확인을 제공하려면 프로토콜 팩터리가 요청/회신 보안을 지원해야 합니다.|  
|SignatureNotExpected|이 메시지에 서명이 필요하지 않습니다.|  
|SigningTokenHasNoKeys|지정된 서명 토큰에 키가 없습니다. 보안 토큰이 암호화 작업을 수행하기 위해 이 토큰을 필요로 하는 컨텍스트에서 사용되지만, 토큰에 암호화 키가 없습니다. 토큰 유형이 암호화 작업을 지원하지 않거나, 특정 토큰 인스턴스에 암호화 키가 없습니다. 구성을 점검하여 암호화 사용이 불가능한 토큰 유형(예: UserNameSecurityToken)이 암호화 작업(예: 지원 토큰 확인)이 필요한 컨텍스트에 지정되어 있지 않은지 확인하십시오.|  
|SpnegoImpersonationLevelCannotBeSetToNone|보안 지원 공급자 인터페이스가 가장 수준 '없음'을 지원하지 않습니다. 확인, 가장 또는 위임 수준을 지정하십시오.|  
|SslClientCertMustHavePrivateKey|지정된 인증서에는 개인 키가 있어야 합니다. 프로세스에는 개인 키에 대한 액세스 권한이 있어야 합니다.|  
|SslServerCertMustDoKeyExchange|지정된 인증서에는 키 교환이 가능한 개인 키가 있어야 합니다. 프로세스에는 개인 키에 대한 액세스 권한이 있어야 합니다.|  
|StandardsManagerCannotWriteObject|토큰 Serializer가 지정된 개체를 serialize할 수 없습니다.  사용자 지정 유형인 경우에는 사용자 지정 serializer를 제공해야 합니다.|  
|TimeStampHasCreationAheadOfExpiry|만든 시간이 만료 시간보다 크거나 같으므로 보안 타임스탬프가 잘못되었습니다.|  
|TimeStampHasCreationTimeInFuture|만든 시간이 미래의 시간이므로 보안 타임스탬프가 잘못되었습니다. 현재 시간과 허용된 클럭 오차가 지정되었습니다.|  
|TimeStampHasExpiryTimeInPast|만료 시간이 과거의 시간이므로 보안 타임스탬프가 잘못되었습니다. 현재 시간과 허용된 클럭 오차가 지정되었습니다.|  
|TimeStampWasCreatedTooLongAgo|만든 시간이 너무 오래 전이므로 보안 타임스탬프가 잘못되었습니다. 현재 시간, 최대 타임스탬프 수명 및 허용된 클럭 오차가 지정되었습니다.|  
|TokenProviderCannotGetTokensForTarget|토큰 공급자가 지정된 대상에 대한 토큰을 가져올 수 없습니다.|  
|TooManyIssuedSecurityTokenParameters|페더레이션 보안 체인의 레그에 IssuedSecurityTokenParameters가 여러 개 있습니다. InfoCard 시스템은 각 레그에 대해 하나의 IssuedSecurityTokenParameters만 지원합니다.|  
|TransportDoesNotProtectMessage|전송 수준 무결성 및 기밀성이 필요한 인증 모드로 지정된 계약에 대해 지정된 바인딩이 구성되어 있습니다. 그러나 전송 시 무결성 및 기밀성을 제공할 수 없습니다.|  
|TrustApr2004DoesNotSupportCertainIssuedTokens|WSTrustApr2004에서는 X.509 인증서 또는 EncryptedKeys의 발급을 지원하지 않습니다. WsTrustFeb2005 이상을 사용하십시오.|  
|TrustDriverVersionDoesNotSupportSession|구성된 트러스트 버전이 세션을 지원하지 않습니다. WSTrustFeb2005 이상을 사용하십시오.|  
|UnableToCreateICryptoFromTokenForSignatureVerification|서명 확인을 위한 지정된 토큰에서 ICrypto 인터페이스를 만들 수 없습니다.|  
|UnableToCreateSymmetricAlgorithmFromToken|토큰에서 지정된 대칭 알고리즘을 만들 수 없습니다.|  
|UnableToDeriveKeyFromKeyInfoClause|지정된 KeyInfo 절이 파생에 사용할 수 있는 대칭 키를 포함하지 않는 지정된 토큰으로 확인되었습니다.|  
|UnableToFindTokenAuthenticator|지정된 토큰 유형에 대한 토큰 인증자를 찾을 수 없습니다. 현재 보안 설정에 따라 해당 유형의 토큰을 수락할 수 없습니다.|  
|UnableToLoadCertificateIdentity|구성에 지정된 X.509 인증서 ID를 로드할 수 없습니다.|  
|UnexpectedEmptyElementExpectingClaim|지정된 네임스페이스에서의 지정된 요소가 비어 있으며 올바른 ID 클레임을 지정하지 않습니다.|  
|UnknownEncodingInBinarySecurityToken|이진 보안 토큰을 읽는 동안 인식할 수 없는 인코딩이 발생했습니다.|  
|UnsecuredMessageFaultReceived|상대방으로부터 보호되지 않거나 잘못 보호된 오류를 받았습니다. 오류 코드 및 세부 정보는 내부 FaultException을 참조하십시오.|  
|UnsupportedPasswordType|지정된 사용자 이름 토큰에 지원되지 않는 암호 유형이 있습니다.|  
|UnsupportedSecureConversationBootstrapProtectionRequirements|보안 정책을 가져올 수 없습니다. 보안 대화 부트스트랩 바인딩에 대한 보호 요구 사항이 지원되지 않습니다. 보안 대화 부트스트랩에 대한 보호 요구 사항은 요청 및 응답의 서명 및 암호화를 모두 요구해야 합니다.|  
|UnsupportedSecurityPolicyAssertion|지정된 보안 정책 가져오기 중에 지원되지 않는 보안 정책 어설션이 검색되었습니다.|
