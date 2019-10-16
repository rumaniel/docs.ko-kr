---
title: IdentityModel 예외
ms.date: 03/30/2017
ms.assetid: 4ef34497-8ff5-4621-b773-7731cc721231
ms.openlocfilehash: 4b8af2620b6179ce4cff59d7f9871377f06ffe5f
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67486661"
---
# <a name="identitymodel-exceptions"></a>IdentityModel 예외
이 항목에서는 IdentityModel에 의해 생성된 모든 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|현재 문자열|  
|-------------------|--------------------|  
|ValueMustBeOf2Types|이 인수의 값은 이러한 두 가지 형식 중 하나이어야 합니다.|  
|SAMLSubjectNameIdentifierRequiresNameValue|SamlNameIdentifier에 대해 지정된 'Name'이 null이거나 길이가 0이 될 수 없습니다.|  
|TraceCodeIssuanceTokenProviderEndSecurityNegotiation|IssuanceTokenProvider가 보안 협상을 완료했습니다.|  
|TraceCodeSecurityNewServerSessionKeyIssued|서버가 새 보안 세션 키를 발급했습니다.|  
|SAMLAttributeMissingNameAttributeOnRead|읽는 중인 SamlAttribute의 'Name'이 없거나 길이가 0입니다.|  
|UnknownICryptoType|ICrypto 구현이 지원되지 않습니다.|  
|TraceCodeSecurityTokenProviderClosed|보안 토큰 공급자가 닫혔습니다.|  
|SAMLUnableToLoadAdvice|로드 하지 못했습니다는 \<saml: advice > 요소입니다.|  
|SAMLAuthenticationStatementMissingAuthenticationMethodOnRead|읽는 중인 SamlAuthenticationStatement에 대한 'AuthenticationMethod' 특성이 없거나 길이가 0입니다.|  
|UnsupportedTransformAlgorithm|지원되지 않는 변형 또는 정형화 알고리즘입니다.|  
|SAMLAudienceRestrictionShouldHaveOneAudience|SamlAudienceRestrictionCondition은 최소한 하나 이상의 Audience(URI)를 포함해야 합니다.|  
|SAMLEvidenceShouldHaveOneAssertion|SamlEvidence는 ID 또는 참조로 최소한 하나 이상의 SamlAssertion을 참조해야 합니다.|  
|SAMLAudienceRestrictionInvalidAudienceValueOnRead|읽는 중인 SamlAudienceRestrictionCondition의 'Audience' 요소에 값이 없습니다.|  
|X509ChainBuildFail|특정 X.509 인증서 체인 작성에 실패했습니다. 사용한 인증서에 확인할 수 없는 신뢰 체인이 포함되어 있습니다. 인증서를 바꾸거나 certificateValidationMode를 변경하십시오.|  
|XDCannotFindValueInDictionaryString|특정 값 ID를 사전 문자열에서 찾을 수 없습니다.|  
|TraceCodeImportSecurityChannelBindingEntry|보안 ImportChannelBinding을 시작합니다.|  
|PrivateKeyExchangeNotSupported|프라이빗 키가 교환 KeySpec을 지원하지 않습니다.|  
|TokenProviderUnableToGetToken|특정 토큰 공급자가 보안 토큰을 제공할 수 없습니다.|  
|SAMLEntityCannotBeNullOrEmpty|특정 SamlAssertion 엔터티가 null이거나 비어 있을 수 없습니다.|  
|SAMLAssertionRequireOneStatement|SamlAssertion에는 최소한 하나 이상의 문이 필요합니다. 만들려는 SamlAssertion에 최소한 하나 이상의 SamlStatement를 추가했는지 확인하십시오.|  
|AESInvalidInputBlockSize|입력 크기가 특정 바이트의 배수여야 합니다.|  
|AESCryptAcquireContextFailed|CSP 컨텍스트를 가져오지 못했습니다.|  
|SAMLAssertionRequireOneStatementOnRead|읽는 중인 SamlAssertion에 SamlStatement가 포함되어 있지 않습니다. SamlAssertion은 최소한 하나 이상의 SamlStatement를 포함해야 합니다.|  
|TraceCodeSecuritySessionClosedFaultReceived|클라이언트 보안 세션이 서버로부터 세션 닫힘 오류를 수신했습니다.|  
|TraceCodeIssuanceTokenProviderRedirectApplied|IssuanceTokenProvider가 리디렉션 헤더를 적용했습니다.|  
|TraceCodeSecuritySessionClosedFaultSendFailure|보안 세션 닫힘 오류를 클라이언트에게 보내는 동안 오류가 발생했습니다.|  
|ValueMustBeZero|이 인수의 값은 0 이어야 합니다.|  
|SAMLUnableToResolveSignatureKey|SamlAssertion 서명에서 찾은 SecurityKeyIdentifier를 확인할 수 없습니다. 특정 발급자에 대해 SamlAssertion 서명을 확인할 수 없습니다.|  
|X509IsNotInTrustedStore|특정 X.509 인증서가 신뢰된 사용자 저장소에 없습니다.|  
|SAMLElementNotRecognized|특정 요소가 지원되지 않습니다.|  
|SAMLAuthorizationDecisionStatementMissingResourceAttributeOnRead|읽는 중인 SamlAuthorizationDecisionStatement에 대한 'Resource' 특성이 없거나 길이가 0입니다.|  
|SamlTokenMissingSignature|SamlAssertion이 서명되지 않았습니다. SigningCredentials를 설정하여 SamlAssertions에 서명할 수 있습니다.|  
|ExpectedElementMissing|특정 네임스페이스를 가진 필요한 요소가 없습니다.|  
|NoKeyIdentifierClauseFound|특정 형식의 절을 SecurityKeyIdentifier에서 찾을 수 없습니다.|  
|MissingPrivateKey|프라이빗 키가 X.509 인증서에 없습니다.|  
|UnexpectedEOFFromReader|XML 판독기에서의 예기치 않은 파일의 끝입니다.|  
|UnsupportedKeyDerivationAlgorithm|특정 키 파생 알고리즘이 지원되지 않습니다.|  
|TokenDoesNotSupportKeyIdentifierClauseCreation|특정 토큰이 특정 키 식별자 절 생성을 지원하지 않습니다.|  
|LastMessageNumberExceeded|시퀀스 번호 프로토콜 위반이 감지되었습니다.|  
|SymmetricKeyLengthTooShort|지정된 대칭 키의 길이가 너무 짧습니다.|  
|SAMLAuthorityBindingMissingAuthorityKindOnRead|없거나 길이가 0인 'AuthorityKind'가 읽는 중인 SamlAuthorityBinding에 포함되어 있습니다.  이것은 허용되지 않습니다.|  
|XmlTokenBufferIsEmpty|XmlTokenBuffer가 비어 있습니다.|  
|InvalidXmlQualifiedName|정규화된 Xml 이름이 필요한데 잘못된 이름을 찾았습니다.|  
|SAMLAuthorityKindMissingName|SamlAuthorityBinding의 'AuthorityKind'를 나타내는 XmlQualifiedName은 null이거나 길이가 0일 수 없습니다.|  
|AESCryptEncryptFailed|특정 데이터를 암호화하지 못했습니다.|  
|AuthorizationContextCreated|특정 ID를 가진 권한 부여 컨텍스트가 생성됩니다.|  
|SamlSerializerUnableToReadSecurityKeyIdentifier|SecurityKeyIdentifier를 읽을 수 있는 SecurityTokenSerializer가 SamlSerializer에 없습니다. 사용자 지정 SecurityKeyIdentifier를 사용하는 경우에는 사용자 지정 SecurityTokenSerializer를 제공해야 합니다.|  
|TraceCodeIssuanceTokenProviderServiceTokenCacheFull|IssuanceTokenProvider가 서비스 토큰 캐시를 줄였습니다.|  
|TraceCodeSecurityTokenProviderOpened|보안 토큰 공급자가 열렸습니다.|  
|PublicKeyNotRSA|공개 키가 RSA 키가 아닙니다.|  
|InvalidReaderState|특정 상태가 제공된 입력 판독기에 올바르지 않습니다.|  
|UnableToResolveReferenceUriForSignature|다이제스트를 컴퓨팅하기 위해 서명의 특정 URI를 확인할 수 없습니다.|  
|EmptyBase64Attribute|필수 base64 특성 이름 및 네임스페이스에 대한 빈 값을 찾았습니다.|  
|SAMLSubjectRequiresConfirmationMethodWhenConfirmationDataOrKeyInfoIsSpecified|확인 데이터 또는 KeyInfo를 지정할 경우 SAML SubjectConfirmation에 Confirmation 메서드가 필요합니다.|  
|SAMLAudienceRestrictionShouldHaveOneAudienceOnRead|읽는 중인 SamlAudienceRestrictionCondition은 최소한 하나 이상의 'Audience' 값을 포함해야 하지만 이 값을 찾을 수 없습니다.|  
|TokenProviderUnableToRenewToken|특정 토큰 공급자가 보안 토큰을 갱신할 수 없습니다.|  
|AESIVLengthNotSupported|특정 비트 IV가 지원되지 않습니다. 128비트 IV만 지원됩니다.|  
|SAMLAuthorityBindingMissingAuthorityKind|SamlAuthorityBinding은 null이 아닌 'AuthorityKind'를 포함해야 합니다.|  
|TraceCodeSecuritySessionDemuxFailure|들어오는 메시지가 기존 보안 세션의 일부가 아닙니다.|  
|TokenRenewalNotSupported|특정 토큰 공급자가 토큰 갱신을 지원하지 않습니다.|  
|AtLeastOneReferenceRequired|최소한 하나 이상의 참조가 서명에 필요합니다.|  
|SAMLSignatureAlreadyRead|서명을 이미 SAML 어설션에서 읽었습니다.|  
|AlgorithmAndPrivateKeyMisMatch|지정된 알고리즘과 프라이빗 키가 일치하지 않습니다.|  
|EmptyTransformChainNotSupported|비어 있는 변형 체인이 지원되지 않습니다.|  
|SspiWrapperEncryptDecryptAssert1|SSPIWrapper::EncryptDecryptHelper&#124;'offset' 범위를 벗어났습니다.|  
|SspiWrapperEncryptDecryptAssert2|SSPIWrapper::EncryptDecryptHelper&#124;'크기'가 범위를 벗어났습니다. SecurityTokenManagerCannotCreateAuthenticatorForRequirement=보안 토큰 관리자가 특정 요구 사항에 대한 토큰 인증자를 만들 수 없습니다.|  
|UnableToCreateKeyedHashAlgorithm|특정 서명 알고리즘에 대한 특정 값에서 KeyedHashAlgorithm을 만들 수 없습니다.|  
|SAMLUnableToLoadAssertion|\<saml: assertion > 요소를 로드 하지 못했습니다.|  
|X509FindValueMismatchMulti|특정 X509FindType에서는 인수 findValue의 형식이 두 가지 값 중 하나이어야 합니다. 인수 findValue는 다른 형식입니다.|  
|TraceCodeSecurityIdentityDeterminationSuccess|EndpointAddress에 대해 ID를 확인했습니다.|  
|UndefinedUseOfPrefixAtElement|요소에서 사용되는 특정 접두사에 네임스페이스가 정의되지 않았습니다.|  
|TraceCodeSecuritySessionResponderOperationFailure|보안 세션 작업을 서버에서 실행하지 못했습니다.|  
|CannotFindCert|특정 검색 조건을 사용 하 여 X.509 인증서를 찾을 수 없습니다. StoreName , StoreLocation, FindType, FindValue.|  
|X509InvalidUsageTime|특정 X.509 인증서 사용 시간이 잘못되었습니다. 사용 시간이 필요한 NotBefore 시간 및 NotAfter 시간 사이에 속하지 않습니다.|  
|TraceCodeSecurityIdentityDeterminationFailure|EndpointAddress에 대해 ID를 확인할 수 없습니다.|  
|AsyncObjectAlreadyEnded|End 메서드가 이 비동기 결과 개체에서 이미 호출되었습니다.|  
|ExternalDictionaryDoesNotContainAllRequiredStrings|외부 사전에 모든 필수 문자열에 대한 정의가 없습니다. 특정 문자열을 원격 사전에서 사용할 수 없습니다.|  
|TraceCodeSecuritySessionKeyRenewalFaultReceived|클라이언트 보안 세션이 서버로부터 키 갱신 오류를 받았습니다.|  
|SAMLActionNameRequired|SamlAction을 나타내는 문자열은 null이거나 길이가 0일 수 없습니다.|  
|SignatureVerificationFailed|서명을 확인하지 못했습니다.|  
|TraceCodeSecurityContextTokenCacheFull|SecurityContextSecurityToken 캐시가 꽉 찼습니다.|  
|SAMLAssertionMissingMajorVersionAttributeOnRead|읽는 중인 SamlAssertion의 MajorVersion이 없거나 길이가 0입니다.|  
|SamlAttributeClaimRightShouldBePossessProperty|이 SamlAttribute 생성자에서는 클레임 권한이 System.IdentityModel.Claims.Rights.PossessProperty 값을 가질 것을 요구합니다.|  
|AuthorizationPolicyEvaluated|특정 ID가 있는 정책을 확인합니다.|  
|SAMLUnableToLoadCondtions<!-- the misspelling here is deliberate. -->|\<saml: conditions > 요소를 로드 하지 못했습니다.|  
|AESKeyLengthNotSupported|특정 비트 키가 지원되지 않습니다. 128, 192 및 256 비트 키만 지원됩니다.|  
|UserNameCannotBeEmpty|사용자 이름은 비어 있을 수 없습니다.|  
|AlgorithmAndPublicKeyMisMatch|지정된 알고리즘과 공개 키가 일치하지 않습니다.|  
|SAMLUnableToLoadCondtion<!-- the misspelling here is deliberate. -->|\<saml: conditions > 요소를 로드 하지 못했습니다.|  
|SamlAssertionMissingSigningCredentials|SigningCredentials가 SamlAssertion에서 설정되지 않았습니다. SamlAssertions는 서명되어야 합니다. 계속하려면 SamlAssertion에서 올바른 SigningCredentials를 설정하십시오.|  
|SspiPayloadNotEncrypted|이진 데이터가 SSPI 보안 컨텍스트로 암호화되지 않았습니다.|  
|SAMLAuthorizationDecisionShouldHaveOneActionOnRead|읽는 중인 SamlAuthorizationDecisionStatement에 SamlAction이 없습니다.|  
|TraceCodeSecurityBindingSecureOutgoingMessageFailure|보안 프로토콜에서 보내는 메시지를 보안 처리할 수 없습니다.|  
|UndefinedUseOfPrefixAtAttribute|특정 특성에서 사용되는 특정 접두사에 네임스페이스가 정의되지 않았습니다.|  
|NoInputIsSetForCanonicalization|정형화된 출력을 쓰기 위한 입력이 설정되지 않았습니다.|  
|TraceCodeSecurityPendingServerSessionAdded|보류 중인 보안 세션을 서버에 추가합니다.|  
|AsyncCallbackException|AsyncCallback에 예외가 발생했습니다.|  
|PrivateKeyNotRSA|프라이빗 키가 RSA 키가 아닙니다.|  
|TraceCodeSecurityClientSessionKeyRenewed|클라이언트 보안 세션에서 세션 키를 갱신했습니다.|  
|SAMLAuthorizationDecisionStatementMissingDecisionAttributeOnRead|읽는 중인 SamlAuthorizationDecisionStatement에 대한 'Decision'이 없거나 길이가 0입니다.|  
|SAMLAttributeNameAttributeRequired|SamlAttribute에 지정된 'Name'은 null이거나 길이가 0일 수 없습니다.|  
|SamlSerializerRequiresExternalSerializers|SamlSerializer는 토큰에 있는 SecurityKeyIdentifier를 serialize하는 데 SecurityTokenSerializer를 필요로 합니다.|  
|UnableToResolveKeyReference|토큰 확인자가 특정 보안 키 참조를 확인할 수 없습니다.|  
|UnsupportedKeyWrapAlgorithm|특정 키 래핑 알고리즘이 지원되지 않습니다.|  
|SAMLAssertionMissingIssuerAttributeOnRead|읽는 중인 SamlAssertion의 'Issuer'가 없거나 길이가 0입니다.|  
|TraceCodeIssuanceTokenProviderUsingCachedToken|IssuanceTokenProvider가 캐시된 서비스 토큰을 사용했습니다.|  
|AESCryptGetKeyParamFailed|특정 키 매개 변수를 가져오지 못했습니다.|  
|InvalidNamespaceForEmptyPrefix|네임스페이스가 빈 접두사에 대해 올바르지 않습니다.|  
|AESCipherModeNotSupported|특정 암호화 모드가 지원되지 않습니다. CBC만 지원됩니다.|  
|ArgumentCannotBeEmptyString|인수는 비어 있지 않은 문자열이어야 합니다.|  
|SAMLAssertionMissingMinorVersionAttributeOnRead|읽는 중인 SamlAssertion의 MinorVersion이 없거나 길이가 0입니다.|  
|SpecifiedStringNotAvailableInDictionary|지정된 문자열이 현재 사전의 항목이 아닙니다.|  
|KerberosApReqInvalidOrOutOfMemory|AP-REQ가 잘못되었거나 시스템에 충분한 메모리가 없습니다.|  
|FailLogonUser|지정된 사용자에 대한 LogonUser가 실패했습니다. 사용자에게 올바른 Windows 계정이 있는지 확인하십시오.|  
|ValueMustBeNonNegative|이 인수의 값은 음수가 아니어야 합니다.|  
|X509ValidationFail|지정된 X.509 인증서를 확인하지 못했습니다.|  
|TraceCodeSecuritySessionRequestorOperationSuccess|보안 세션 작업이 클라이언트에서 완료되었습니다.|  
|SAMLActionNameRequiredOnRead|읽는 중인 SamlAction에 대한 문자열이 없거나 길이가 0입니다.|  
|KerberosMultilegsNotSupported|ID가 UPN으로 지정되었습니다. Kerberos 다중 레그가 필요한 사용자 계정으로 실행되는 서비스를 인증하는 것은 지원되지 않습니다.|  
|SAMLAssertionIdRequired|SamlAssertion에 대한 'assertionId'가 null이거나 비어 있을 수 없습니다.|  
|InvalidOperationForWriterState|지정된 작업이 지정된 XmlWriter 상태에서 올바르지 않습니다.|  
|CannotValidateSecurityTokenType|지정된 보안 토큰 인증자가 지정된 형식의 토큰을 확인할 수 없습니다.|  
|X509FindValueMismatch|지정된 X509FindType에서는 인수 findValue의 형식이 지정된 값이어야 합니다. 인수 findValue는 다른 형식입니다.|  
|TraceCodeSecurityClientSessionCloseSent|클라이언트 보안 세션에서 Close 메시지를 보냈습니다.|  
|SuiteDoesNotAcceptAlgorithm|지정된 알고리즘이 지정된 알고리즘 모음의 지정된 작업에 허용되지 않습니다.|  
|TraceCodeSecuritySessionRequestorOperationFailure|클라이언트 보안 세션 작업을 실행하지 못했습니다.|  
|SAMLUnableToLoadStatement|SamlStatement를 로드하지 못했습니다.|  
|InnerReaderMustBeAtElement|내부 판독기가 요소에 있어야 합니다.|  
|UnableToCreateTokenReference|보안 토큰 참조를 만들 수 없습니다.|  
|TraceCodeSecurityBindingIncomingMessageVerified|보안 프로토콜에서 들어오는 메시지를 확인했습니다.|  
|ObjectIsReadOnly|개체가 읽기 전용입니다.|  
|TraceCodeSecurityClientSessionPreviousKeyDiscarded|클라이언트 보안 세션에서 이전 세션 키를 삭제했습니다.|  
|SAMLTokenTimeInvalid|SamlToken의 시간이 잘못되었습니다. 현재 시간이 토큰의 유효 기간 및 만료 시간을 벗어났습니다.|  
|TraceCodeSecurityIdentityVerificationSuccess|ID를 확인했습니다.|  
|SigningTokenHasNoKeys|지정된 서명 토큰에 키가 없습니다.|  
|TraceCodeSecurityIdentityVerificationFailure|ID를 확인하지 못했습니다.|  
|AESCryptImportKeyFailed|키 자료를 가져오지 못했습니다.|  
|FailInitializeSecurityContext|InitializeSecurityContent가 실패했습니다. 서비스 사용자 이름이 올바른지 확인하십시오.|  
|TraceCodeStreamSecurityUpgradeAccepted|스트림 보안 업그레이드가 수락되었습니다.|  
|SAMLAuthorityBindingRequiresLocation|SamlAuthorityBinding에 지정된 'Location' 특성은 null이거나 길이가 0일 수 없습니다.|  
|PublicKeyNotDSA|공개 키가 DSA 키가 아닙니다.|  
|ImpersonationLevelNotSupported|Kerberos를 사용하는 인증 모드가 지정된 가장 수준을 지원하지 않습니다. 올바른 ID 또는 가장 수준을 지정하십시오.|  
|RequiredTargetNotSigned|지정된 ID를 가진 요소에 서명해야 하지만 하지 않았습니다.|  
|SAMLAuthenticationStatementMissingAuthenticationInstanceOnRead|읽는 중인 SamlAuthenticationStatement에 대한 'AuthenticationInstant' 특성이 없거나 길이가 0입니다.|  
|SAMLEvidenceShouldHaveOneAssertionOnRead|포함된 SamlAssertion이나 이에 대한 참조가 읽는 중인 SamlEvidence에 없습니다.|  
|LengthOfArrayToConvertMustGreaterThanZero|정수로 변환할 배열의 길이는 0보다 커야 합니다.|  
|InvalidAsyncResult|잘못된 AsyncResult입니다.|  
|TraceCodeIssuanceTokenProviderRemovedCachedToken|IssuanceTokenProvider에서 만료된 서비스 토큰을 제거했습니다.|  
|IncorrectUserNameFormat|사용자 이름의 형식이 잘못되었습니다. 형식의 사용자 이름 형식 이어야 합니다 "username' 또는 ' 도메인\\\username'.|  
|TraceCodeExportSecurityChannelBindingEntry|보안 ExportChannelBinding을 시작하는 중입니다.|  
|UnsupportedInputTypeForTransform|지정된 입력 형식이 변형에 지원되지 않습니다.|  
|CannotFindDocumentRoot|문서의 루트를 찾을 수 없습니다.|  
|XmlBufferQuotaExceeded|XML 콘텐츠를 버퍼링하는 데 필요한 크기가 버퍼 할당량을 초과했습니다.|  
|TraceCodeSecuritySessionClosedResponseSendFailure|보안 세션 Close 응답을 클라이언트에게 보내는 동안 오류가 발생했습니다.|  
|UnableToResolveReferenceInSamlSignature|AssertionID를 가진 SAML 서명에서 지정된 참조를 확인할 수 없습니다.|  
|SAMLSubjectRequiresNameIdentifierOrConfirmationMethod|SamlSubject에서는 'NameIdentifier' 또는 'ConfirmationMethod'를 지정해야 하는데, 두 개 모두 없습니다.|  
|SAMLAttributeMissingNamespaceAttributeOnRead|읽는 중인 SamlAttribute의 'Namespace'가 없거나 길이가 0입니다.|  
|SAMLSubjectConfirmationClauseMissingConfirmationMethodOnRead|읽는 중인 SamlSubjectConfirmation에서 'ConfirmationMethod'를 찾을 수 없습니다.|  
|SecurityTokenRequirementHasInvalidTypeForProperty|토큰 요구 사항에 지정된 속성에 대한 예기치 않은 형식이 있습니다. 필요한 속성 형식은 다른 값입니다.|  
|TraceCodeNegotiationTokenProviderAttached|NegotiationTokenProvider가 연결되었습니다.|  
|TraceCodeSpnegoClientNegotiationCompleted|SpnegoTokenProvider가 SSPI 협상을 완료했습니다.|  
|SAMLUnableToLoadUnknownElement|선택한 SamlSerializer가 이 요소를 deserialize할 수 없습니다. 사용자 지정 요소를 deserialize하려면 사용자 지정 SamlSerializer를 등록하십시오.|  
|CreateSequenceRefused|시퀀스 만들기 요청이 RM 대상에 의해 거부되었습니다.|  
|TraceCodeSecuritySessionRedirectApplied|클라이언트 보안 세션이 리디렉션되었습니다.|  
|SecurityTokenRequirementDoesNotContainProperty|토큰 요구 사항에 지정된 속성이 포함되어 있지 않습니다.|  
|SAMLAttributeValueCannotBeNull|SamlAttribute에서 발견된 attributeValues 중 하나가 null 값입니다. SamlAttribute를 만들 때 목록이 null이 아닌지 확인하십시오.|  
|ValueMustBeGreaterThanZero|이 인수의 값은 0보다 커야 합니다.|  
|TraceCodeNegotiationAuthenticatorAttached|NegotiationTokenAuthenticator가 연결되었습니다.|  
|ValueMustBePositive||  
|SAMLAuthorizationDecisionShouldHaveOneAction|SamlAuthorizationDecisionStatement에 최소한 하나 이상의 SamlAction이 있어야 합니다.|  
|TraceCodeSecurityTokenAuthenticatorClosed|보안 토큰 인증자가 닫혔습니다.|  
|TraceCodeSecurityAuditWrittenSuccess|보안 감사 로그가 기록되었습니다.|  
|PrivateKeyNotDSA|프라이빗 키가 DSA 키가 아닙니다.|  
|MessageNumberRollover|이 시퀀스에 대한 최대 시퀀스 번호를 초과했습니다.|  
|AESPaddingModeNotSupported|지정된 패딩 모드가 지원되지 않습니다. PKCS7 및 ISO10126만 지원됩니다.|  
|SAMLSubjectRequiresNameIdentifierOrConfirmationMethodOnRead|읽는 중인 SamlSubject에 대한 필수 'NameIdentifier' 및 'ConfrimationMethod' 요소를 찾을 수 없습니다.|  
|TraceCodeSecurityAuditWrittenFailure|보안 감사 로그에 기록하는 동안 오류가 발생했습니다.|  
|UnsupportedCryptoAlgorithm|이 컨텍스트에서 지정된 암호화 알고리즘을 지원되지 않습니다.|  
|SigningTokenHasNoKeysSupportingTheAlgorithmSuite|서명 토큰에 지정된 알고리즘 모음을 지원하는 키가 없습니다.|  
|SAMLNameIdentifierMissingIdentifierValueOnRead|읽는 중인 SamlNameIdentifier에 대한 'Identifier' 문자열이 없습니다.|  
|SAMLSubjectStatementRequiresSubject|SAML Subject Statement에서는 SAML 주체를 지정해야 합니다.|  
|TraceCodeSslClientCertMissing|원격 SSL 클라이언트가 필수 인증서를 제공하지 못했습니다.|  
|SAMLTokenVersionNotSupported|지정된 주 버전 및 부 버전이 지원되지 않습니다.|  
|TraceCodeConfigurationIsReadOnly|구성이 읽기 전용인 경우|  
|TraceCodeSecuritySessionRenewFaultSendFailure|보안 세션 키의 갱신 오류를 클라이언트에게 보내는 동안 오류가 발생했습니다.|  
|TraceCodeSecurityInactiveSessionFaulted|서버에서 비활성 보안 세션에 대한 오류가 발생했습니다.|  
|SAMLUnableToLoadAttribute|SamlAttribute를 로드하지 못했습니다.|  
|Psha1KeyLengthInvalid|지정된 PSHA1 키 길이가 잘못되었습니다.|  
|KeyIdentifierCannotCreateKey|이 SecurityKeyIdentifier에는 키를 만들 수 있는 절이 없습니다.|  
|X509IsInUntrustedStore|지정된 X.509 인증서가 신뢰할 수 없는 인증서 저장소에 있습니다.|  
|UnexpectedXmlChildNode|지정된 형식의 지정된 XML 자식 노드가 지정된 요소에 필요한 자식 노드가 아닙니다.|  
|TokenDoesNotMeetKeySizeRequirements|지정된 토큰이 지정된 알고리즘 모음에 대한 키 크기 요구 사항을 충족하지 않습니다.|  
|TraceCodeSecuritySessionRequestorStartOperation|보안 세션 작업이 클라이언트에서 시작되었습니다.|  
|InvalidHexString|16진수 문자열 형식이 잘못되었습니다.|  
|SamlAttributeClaimResourceShouldBeAString|이 SamlAttribute 생성자에서는 클레임의 리소스가 'string' 형식이어야 합니다.|  
|SamlSigningTokenNotFound|SamlAssertion이 서명되었지만 SamlAssertion에 서명한 토큰을 찾을 수 없습니다. SamlAssertion에 서명한 토큰이 SecurityTokenResolver에 포함되어 있는지 확인하십시오.|  
|TraceCodeSecuritySpnToSidMappingFailure|ServicePrincipalName을 SecurityIdentifier로 매핑할 수 없습니다.|  
|UnableToCreateSignatureFormatterFromAsymmetricCrypto|지정된 비대칭 암호화에서 지정된 알고리즘에 대한 서명 포맷터를 만들 수 없습니다.|  
|TraceCodeSecurityServerSessionClosedFaultSent|서버 보안 세션이 세션 닫힘 오류를 클라이언트에게 보냈습니다.|  
|UnableToFindPrefix|지정된 요소에서 시각적으로 사용되는 지정된 접두사에 대한 접두사를 찾을 수 없습니다.|  
|TraceCodeSecurityTokenAuthenticatorOpened|보안 토큰 인증자가 열렸습니다.|  
|RequiredAttributeMissing|지정된 요소에 지정된 특성이 필요합니다.|  
|LocalIdCannotBeEmpty|localId는 비어 있을 수 없습니다. 올바른 'localId'를 지정하십시오.|  
|ValueMustBeInRange|이 인수의 값은 지정된 범위 내에 속해야 합니다.|  
|TraceCodeIssuanceTokenProviderBeginSecurityNegotiation|IssuanceTokenProvider가 새 보안 협상을 시작했습니다.|  
|InvalidNtMapping|지정된 X.509 인증서를 Windows 계정에 매핑할 수 없습니다. UPN 주체의 대체 이름이 필요합니다.|  
|AESCryptSetKeyParamFailed|지정된 키 매개 변수를 설정하지 못했습니다.|  
|TraceCodeSecuritySessionClosedResponseReceived|클라이언트 보안 세션에서 서버로부터 닫힘 응답을 받았습니다.|  
|UnableToCreateSignatureDeformatterFromAsymmetricCrypto|지정된 비대칭 암호화에서 지정된 알고리즘에 대한 서명 디포맷터를 만들 수 없습니다.|  
|TraceCodeIdentityModelAsyncCallbackThrewException|비동기 콜백에 예외가 발생했습니다.|  
|LengthMustBeGreaterThanZero|이 인수의 길이는 0보다 커야 합니다.|  
|FoundMultipleCerts|지정 된 검색 조건을 사용 하 여 여러 X.509 인증서를 찾았습니다. StoreName, StoreLocation, FindType, FindValue. 더 구체적인 찾기 값을 제공하십시오.|  
|AtLeastOneTransformRequired|변형 요소는 최소한 하나 이상의 변형을 포함해야 합니다.|  
|SAMLTokenNotSerialized|SamlAssertion을 XML로 serialize할 수 없습니다. 자세한 내용은 내부 예외를 참조하십시오.|  
|TraceCodeSecurityBindingOutgoingMessageSecured|보안 프로토콜에서 보내는 메시지를 보안 처리했습니다.|  
|KeyIdentifierClauseDoesNotSupportKeyCreation|이 SecurityKeyIdentifierClause는 키 작성을 지원하지 않습니다.|  
|UnableToResolveTokenReference|토큰 확인자가 지정된 토큰 참조를 확인할 수 없습니다.|  
|UnsupportedEncryptionAlgorithm|지정된 암호화 알고리즘이 지원되지 않습니다.|  
|SamlSerializerUnableToWriteSecurityKeyIdentifier|지정한 SecurityKeyIdentifier를 serialize할 수 있는 SecurityTokenSerializer가 SamlSerializer에 없습니다. 사용자 지정 SecurityKeyIdentifier를 사용하는 경우에는 사용자 지정 SecurityTokenSerializer를 제공해야 합니다.|  
|SAMLAttributeShouldHaveOneValue|특성 값을 찾을 수 없습니다. SamlAttribute 특성에는 최소한 하나 이상의 특성 값이 있어야 합니다.|  
|TraceCodeSecurityBindingVerifyIncomingMessageFailure|보안 프로토콜에서 들어오는 메시지를 확인할 수 없습니다.|  
|SamlSigningTokenMissing|SamlSecurityTokenAuthenticator에 전달된 SamlAssertion에 서명 토큰이 없습니다.|  
|NoPrivateKeyAvailable|프라이빗 키를 사용할 수 없습니다.|  
|ValueMustBeOne|이 인수의 값은 1이어야 합니다.|  
|TraceCodeSecurityPendingServerSessionRemoved|서버가 보류 중인 보안 세션을 활성화했습니다.|  
|TraceCodeImportSecurityChannelBindingExit|보안 ImportChannelBinding을 완료했습니다.|  
|X509CertStoreLocationNotValid|StoreLocation은 LocalMachine 또는 CurrentUser여야 합니다.|  
|SettingdMayBeModifiedOnlyWhenTheWriterIsInStartState|작성기가 Start 상태인 경우에만 작성기 설정을 수정할 수 있습니다.|  
|ArgumentInvalidCertificate|인증서가 잘못되었습니다.|  
|DigestVerificationFailedForReference|지정된 참조에 대한 다이제스트 확인에 실패했습니다.|  
|SAMLAuthorityBindingRequiresBinding|SamlAuthorityBinding에 지정된 'Binding' 특성은 null이거나 길이가 0일 수 없습니다.|  
|AESInsufficientOutputBuffer|출력 버퍼가 지정된 바이트보다 커야 합니다.|  
|SAMLAuthorityBindingMissingBindingOnRead|읽는 중인 SamlAuthorityBinding에 대한 'Binding' 특성이 없거나 길이가 0입니다.|  
|SAMLAuthorityBindingInvalidAuthorityKind|읽는 중인 SamlAuthorityBinding에 잘못된 AuthorityKind가 있습니다. AuthorityKind의 형식은 QName이어야 합니다.|  
|ProvidedNetworkCredentialsForKerberosHasInvalidUserName|Kerberos 토큰에 제공된 NetworkCredentials에 올바른 UserName이 없습니다.|  
|SSPIPackageNotSupported|지정된 SSPI 패키지가 지원되지 않습니다.|  
|TokenCancellationNotSupported|지정된 토큰 공급자가 토큰 취소를 지원하지 않습니다.|  
|UnboundPrefixInQName|바인딩되지 않은 접두사가 지정된 정규화된 이름에서 사용됩니다.|  
|SAMLAuthorizationDecisionResourceRequired|SamlAuthorizationDecisionStatement에 지정된 'resource'는 null이거나 길이가 0일 수 없습니다.|  
|TraceCodeSecurityNegotiationProcessingFailure|서비스 보안 협상을 처리하지 못했습니다.|  
|SAMLAssertionIssuerRequired|SamlAssertion에 대해 지정된 'Issuer'가 null이거나 비어 있을 수 없습니다.|  
|UnableToCreateHashAlgorithmFromAsymmetricCrypto|지정된 비대칭 암호화에서 지정된 알고리즘에 대한 HashAlgorithm을 만들 수 없습니다.|  
|SamlUnableToExtractSubjectKey|SamlSubject에서 찾은 SecurityKeyIdentifier를 SecurityToken으로 확인할 수 없습니다. SecurityTokenResolver는 SecurityKeyIdentifier가 확인되는 SecurityToken을 포함해야 합니다.|  
|ChildNodeTypeMissing|지정된 XML 요소에 지정된 형식의 자식 항목이 없습니다.|  
|TraceCodeSecurityPendingServerSessionClosed|서버가 보류 중인 보안 세션을 닫았습니다.|  
|TraceCodeSecuritySessionCloseResponseSent|서버 보안 세션이 Close 응답을 클라이언트에게 보냈습니다.|  
|TraceCodeSecurityIdentityHostNameNormalizationFailure|엔드포인트 주소의 HostName 부분을 정규화할 수 없습니다.|  
|FailAcceptSecurityContext|AcceptSecurityContext가 실패했습니다.|  
|EmptyXmlElementError|지정된 요소가 비어 있을 수 없습니다.|  
|PrefixNotDefinedForNamespace|지정된 네임스페이스에 대한 접두사가 이 컨텍스트에 정의되지 않았으므로 선언할 수 없습니다.|  
|SAMLAuthorizationDecisionHasMoreThanOneEvidence|읽는 중인 SamlAuthorizationDecisionStatement에 둘 이상의 증거가 포함되어 있습니다. 이것은 허용되지 않습니다.|  
|SamlTokenAuthenticatorCanOnlyProcessSamlTokens|SamlSecurityTokenAuthenticator는 SamlSecurityTokens만 처리할 수 있습니다. 지정된 SecurityTokenType이 수신되었습니다.|  
|SAMLAttributeStatementMissingAttributeOnRead|읽는 중인 SamlAttributeStatement에 'SamlAttribute' 요소가 없습니다. 이것은 허용되지 않습니다.|  
|CouldNotFindNamespaceForPrefix|지정된 접두사에 대한 네임스페이스를 찾을 수 없습니다.|  
|TraceCodeExportSecurityChannelBindingExit|보안 ExportChannelBinding을 완료했습니다.|  
|AESCryptDecryptFailed|지정된 데이터를 해독하지 못했습니다.|  
|SAMLAttributeNamespaceAttributeRequired|SamlAttribute에 지정된 'Namespace'는 null이거나 길이가 0일 수 없습니다.|  
|TraceCodeSpnegoServiceNegotiationCompleted|SpnegoTokenAuthenticator가 SSPI 협상을 완료했습니다.|  
|TraceCodeSecurityServerSessionRenewalFaultSent|서버 보안 세션에서 클라이언트로 키 갱신 오류를 보냈습니다.|  
|AlgorithmMismatchForTransform|변형을 위한 알고리즘에서 불일치가 발생했습니다.|  
|UserNameAuthenticationFailed|지정된 메커니즘을 사용하여 사용자 이름/암호를 인증하지 못했습니다. 사용자가 인증되지 않습니다.|  
|SamlInvalidSigningToken|SamlAssertion이 프로토콜에 따라 확인되지 않은 토큰으로 서명되었습니다. X.509 인증서를 사용하는 경우에는 유효성 검사 기능을 검토하십시오.|  
|TraceCodeSecurityServerSessionKeyUpdated|서버에서 보안 세션 키를 업데이트했습니다.|  
|TraceCodeSecurityServerSessionCloseReceived|서버 보안 세션이 클라이언트로부터 Close 메시지를 수신했습니다.|  
|SAMLAuthenticationStatementMissingSubject|SamlAuthenticationStatement에 필수 SamlSubjectStatement가 없습니다.|  
|UnexpectedEndOfFile|예기치 않은 파일의 끝입니다.|  
|UnsupportedAlgorithmForCryptoOperation|지정된 알고리즘이 지정된 작업에 대해 지원되지 않습니다.|  
|XmlLangAttributeMissing|필수 xml:lang 특성이 없습니다.|  
|TraceCodeSecurityImpersonationSuccess|서버에서 보안 가장을 실행했습니다.|  
|SAMLAuthorityBindingMissingLocationOnRead|읽는 중인 SamlAuthorityBinding에 대한 'Location' 특성이 없거나 길이가 0입니다.|  
|SAMLAttributeStatementMissingSubjectOnRead|SamlAttributeStatement에 대한 'SamlSubject' 요소가 없습니다.|  
|SAMLAuthorizationDecisionStatementMissingSubjectOnRead|읽는 중인 SamlAuthorizationDecisionStatement에 대한 'SamlSubject' 요소가 없습니다.|  
|SAMLBadSchema|SamlAssertion을 읽는 동안 이 지정된 요소가 스키마를 따르지 않는 것으로 확인되었습니다.|  
|SAMLAssertionIDIsInvalid|SamlAssertion에 대한 'assertionId'는 문자나 '_'으로 시작해야 합니다.|  
|TraceCodeSecurityActiveServerSessionRemoved|활성 보안 세션이 서버에 의해 제거되었습니다.|  
|UnableToCreateKeyedHashAlgorithmFromSymmetricCrypto|지정된 대칭 암호화에서 지정된 알고리즘에 대한 keyedHashAlgorithm을 만들 수 없습니다.|  
|SAMLAuthenticationStatementMissingAuthenticationMethod|SamlAuthenticationStatement에 대해 지정된 'AuthenticationMethod'는 null이거나 길이가 0일 수 없습니다.|  
|TraceCodeSecurityImpersonationFailure|서버에서 보안 가장을 실행하지 못했습니다.|  
|기본|(기본값)|  
|UnsupportedNodeTypeInReader|지정된 이름을 가진 지정된 노드 형식이 지원되지 않습니다.|
