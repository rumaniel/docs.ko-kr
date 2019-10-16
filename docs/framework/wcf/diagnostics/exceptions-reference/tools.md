---
title: 도구
ms.date: 03/30/2017
ms.assetid: 89c907f9-313f-408c-992a-631f1eadf1da
ms.openlocfilehash: 6c4ada74c2fc6aba84eb1fe46f4d7cdee9978d13
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61780746"
---
# <a name="tools"></a>도구
이 항목에서는 Windows Communication Foundation (WCF) 도구에서 생성 된 모든 예외를 나열 합니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|ParametersTarget|\<enum>|  
|ParametersToolConfig|\<configFile>|  
|ErrInvalidPath|지정한 경로는 잘못된 경로입니다. 지정된 인수를 확인합니다.|  
|ParametersReference|\<파일 경로 >|  
|WrnCannotLoadConfigFileForValidation|지정된 위치에서 로드된 구성 파일을 처리하는 동안 오류가 발생했습니다. 이 구성 파일에 정의되어 있는 서비스의 유효성을 검사할 수 없습니다.|  
|MoreHelp|자세한 내용을 보려면 지정된 인수를 포함하여 "svcutil"을 입력하십시오.|  
|HelpMergeConfig|생성된 구성이 기존 파일을 덮어쓰지 않고 기존 파일에 병합됩니다.|  
|ErrCannotWriteFile|출력 파일에 쓸 수 없습니다.|  
|ErrInvalidNamespaceArgument|지정된 잘못된 값이 지정된 옵션에 전달되었습니다. 쉼표로 구분된 대상 네임스페이스 및 CLR 네임스페이스 쌍을 지정하십시오.|  
|HelpImportXmlType|비데이터 계약 형식을 IXmlSerializable 형식으로 가져오도록 데이터 계약 serializer를 구성합니다.|  
|ErrExclusiveOptionsSpecified|지정된 다른 옵션을 지정한 경우 지정된 옵션을 사용할 수 없습니다.|  
|WrnHttpGetFailed|지정된 URI에 HTTP GET 오류가 발생했습니다.|  
|ErrInputFileNotAssemblyOrMetadata|지정된 입력 인수를 통해 읽은 지정된 위치의 파일이 XML 메타데이터 파일 또는 올바른 어셈블리가 아닙니다.|  
|WrnUnknownMetadataFound|인식할 수 없는 지정된 형식의 메타데이터 문서를 저장할 수 없습니다.|  
|ErrDirectoryContainsInvalidCharacters|지정된 잘못된 값이 지정된 옵션에 전달되었습니다. 경로에서 지정된 문자를 사용할 수 없습니다.|  
|WrnCannotResolveServiceForValidation|지정된 configName의 서비스를 로드할 수 없습니다. 서비스의 유효성을 검사하려면 서비스 유형이 포함된 어셈블리와 이 서비스에 대한 구성이 포함된 실행 파일을 모두 제공하십시오.|  
|ErrUnexpectedValue|지정된 옵션은 값을 지원하지 않습니다.|  
|#InvalidArg|잘못된 인수가 있습니다.|  
|ParametersExcludeType|\<type>|  
|HelpXmlSerializer|serialization 및 deserialization을 위해 XmlSerializer를 사용하는 데이터 형식을 생성합니다.|  
|#|---------------------------------------------------------------------------------------------------------------------=|  
|ErrUnexpectedError|도구에서 오류가 발생했습니다.|  
|HelpNologo|저작권 및 배너 메시지가 표시되지 않습니다|  
|ErrInputConflictsWithTarget|지정된 옵션을 지정된 값으로 설정하면 지정된 값에서 읽은 입력 형식을 사용할 수 없습니다.|  
|WrnCannotLoadServiceForExport|내보낼 서비스 유형을 로드하는 동안 오류가 발생했습니다.|  
|HelpMetadataDownloadCategory|-= 메타데이터 다운로드 =-|  
|WrnNoServiceContractTypes|지정된 어셈블리에 대한 XmlSerializer 형식을 생성할 수 없습니다. 서비스 계약 형식을 찾을 수 없습니다.|  
|WrnCouldNotLoadTypesFromReferenceAssemblyAt|지정된 위치에서 로드된 어셈블리의 형식을 로드하는 동안 오류가 발생했습니다. 어셈블리의 일부 형식은 로드할 수 없고 도구에 사용할 수 없습니다.|  
|ErrDirectoryPointsToAFile|지정된 잘못된 값이 지정된 옵션에 전달되었습니다. 지정된 값은 파일 경로입니다.|  
|Error|오류:|  
|ErrDuplicateReferenceValues|지정된 어셈블리가 지정된 옵션을 사용하여 두 번 로드되었습니다. 어셈블리는 한 번만 참조할 수 있습니다.|  
|WrnNoXmlSerializerOperationBehavior|지정된 어셈블리에 대한 XmlSerializer를 생성할 수 없습니다. 해당 어셈블리의 서비스 계약에 XmlSerializerOperationBehavior가 포함된 작업이 없습니다.|  
|ErrCannotCreateDirectory|지정된 디렉터리를 만들 수 없습니다.|  
|ErrCouldNotLoadTypesFromAssemblyAt|지정된 어셈블리에 있는 형식을 로드할 수 없습니다.|  
|ErrUnknownSwitch|지정된 스위치는 인식되지 않는 옵션입니다.|  
|Logo|도구의 로고는 "Microsoft ® Service Model Metadata Tool" 버전입니다.|  
|NoCodeWasGenerated|코드가 생성되지 않았습니다.<br /><br /> 클라이언트를 생성하려고 하는 경우 메타데이터 문서에 올바른 계약 또는 서비스가 포함되지 않았거나<br /><br /> 모든 계약/서비스가 참조 어셈블리에 있기 때문일 수 있습니다. 모든 메타데이터 문서를 도구에 전달했는지 확인하십시오.|  
|WrnUnableToLoadContractForSGen|계약 형식을 로드하는 동안 오류가 발생했습니다. 이 계약에 대한 XmlSerializer 형식을 생성할 수 없습니다. 형식 및 세부 사항이 지정되었습니다.|  
|WrnOptionConflictsWithInput|여러 입력 어셈블리에 지정된 옵션을 사용할 수 없습니다. 지정된 옵션이 무시됩니다.|  
|ErrUnableToImportMetadata|메타데이터를 가져오는 동안 오류가 발생했습니다.|  
|ErrInvalidSerializer|잘못된 serializer 값이 지정된 옵션에 전달되었습니다. 지원되는 serializer가 지정되었습니다.|  
|SavingDownloadedMetadata|다운로드한 메타데이터 파일 저장 중...|  
|WrnNoConfigForServices|전달된 어셈블리가 구성 파일로 실행할 수 없거나 구성 파일에 지정된 구성 이름을 가진 서비스가 포함되어 있지 않습니다.|  
|ErrInputConflictsWithOption|지정된 옵션에서 읽은 입력과 지정된 옵션은 서로 다른 도구 작업 모드를 나타내므로 함께 사용할 수 없습니다|  
|ErrUnableToExportEndpoints|지정된 서비스 유형을 내보내는 동안 오류가 발생했습니다.|  
|ErrInputSchemaParseError|지정된 XML을 읽는 동안 XML 스키마 구문 분석 오류가 발생했습니다. XML이 유효하고 형식이 올바른지 확인하십시오.|  
|ErrInputPolicyParseError|지정된 XML을 읽는 동안 WS-Policy 구문 분석 오류가 발생했습니다. XML이 유효하고 형식이 올바른지 확인하십시오.|  
|ErrUnableToLoadReferenceType|참조된 계약 형식을 로드하는 동안 오류가 발생했습니다. 지정된 이 형식이 무시됩니다.|  
|WrnCannotLoadServiceForValidation|유효성을 검사할 서비스를 로드하는 동안 오류가 발생했습니다. 형식 및 세부 사항이 지정되었습니다.|  
|HelpCodeGenerationCategory|-= 코드 생성 =-|  
|RetreivingMetadataWithMexAndDisco|WS-Metadata Exchange 또는 DISCO를 사용하여 지정된 위치에서 메타데이터를 다운로드하고 있습니다.|  
|ErrGeneralSchemaValidation|내보내기 도중에 생성된 XML 스키마를 확인하는 동안 오류가 발생했습니다.|  
|ParametersDirectory|\<directory>|  
|ErrCannotLoadSpecifiedType|지정된 옵션에 전달된 지정된 값에 대한 형식을 로드할 수 없습니다. 이 형식이 속해 있는 어셈블리가 지정된 옵션을 통해 지정되어 있는지 확인하십시오.|  
|ErrOptionModeConflict|지정된 옵션과 지정된 또 다른 옵션은 서로 다른 출력 형식을 나타내므로 함께 사용할 수 없습니다.|  
|ErrIsNotAnAssembly|지정된 파일을 어셈블리로 로드할 수 없습니다. 이 파일이 .NET 어셈블리인지 확인하십시오.|  
|ErrInputConflictsWithMode|지정된 옵션에서 읽은 입력이 다른 옵션과 일관되지 않습니다.|  
|ErrDuplicateValuePassedToTypeArg|지정된 값이 지정된 옵션에 여러 번 전달되었습니다. 각 형식은 한 번만 지정할 수 있습니다.|  
|ErrInputEPRFileParseError|지정된 XML에서 엔드포인트 참조를 읽을 수 없습니다. XML이 유효하고 형식이 올바른지 확인하십시오.|  
|ErrCouldNotCreateCodeProvider|에 전달 된 지정된 된 값에 대 한 코드 공급자를 만들 수 없습니다는 /{1} 인수입니다. 코드 공급자를 올바르게 설치하고 구성했는지 확인하십시오.|  
|ErrPathTooLongDirOnly|지정된 결과 경로가 너무 깁니다. 지정된 인수를 검토합니다.|  
|HelpDataContractSerializer|serialization 및 deserialization을 위해 DataContract Serializer를 사용하는 데이터 형식을 생성합니다.|  
|ErrUnableToExportEndpoint|어셈블리에 대해 로드된 구성 파일에 있는 지정된 서비스 유형에서 지정된 네임스페이스의 지정된 엔드포인트 이름을 내보내는 동안 오류가 발생했습니다.|  
|HelpUsage1|도움말 사용법을 표시합니다.|  
|HelpUsage2|도움말 사용법을 표시합니다.|  
|HelpUsage3|도움말 사용법을 표시합니다.|  
|HelpUsage4|도움말 사용법을 표시합니다.|  
|HelpUsage5|도움말 사용법을 표시합니다.|  
|ErrDirectoryNotFound|지정된 디렉터리를 찾을 수 없습니다. 디렉터리가 있는지 확인하고 해당 디렉터리를 읽을 수 있는 권한이 있는지 확인하십시오.|  
|ErrUnableToLoadFile|지정된 파일을 읽을 수 없습니다.|  
|ErrNoFilesFound|지정된 입력 경로가 기존 파일을 참조하지 않습니다.|  
|ParametersConfig|\<configFile>|  
|ErrDirectoryInsteadOfFile|지정된 입력 경로가 디렉터리입니다. 입력은 URL 또는 파일 경로여야 합니다.|  
|HelpConfig|제공된 이름의 구성 파일을 생성하도록 도구에 지시합니다. 기본값: output.config.|  
|ErrSingleUseSwitch|지정된 옵션은 여러 번 지정할 수 없습니다.|  
|경고|경고:|  
|WrnAmbiguousServiceConfig|지정된 구성 이름을 가진 여러 서비스 구성을 찾았습니다. 다음 어셈블리가 지정되었습니다.|  
|ErrInvalidInputPath|지정된 입력 경로가 기존 파일을 참조하지 않으며 유효한 URI가 아닙니다.|  
|ErrUnableToLoadInputs|로드된 메타데이터를 읽는 동안 오류가 발생했습니다.|  
|GeneratingSerializer|XML serializer 생성 중...|  
|HelpToolConfig|애플리케이션 구성 파일 대신에 사용할 사용자 지정 구성 파일입니다. 이 파일을 사용하면 도구의 구성 파일을 바꾸지 않고 구성 확장을 등록하거나 메타데이터 구성을 변경할 수 있습니다.|  
|ErrValidateInvalidUse|지정된 옵션과 지정된 또 다른 옵션은 함께 사용할 수 없습니다.|  
|WrnWSMExFailed|지정된 URI에 WS-Metadata Exchange 오류가 발생했습니다.|  
|HelpNoconfig|구성을 생성하지 않습니다.|  
|HelpCodeGenerationDescription|메타데이터 문서를 사용하여 서비스 계약, 클라이언트 및 데이터 형식을 생성할 수 있습니다.|  
|HelpTargetMetadata|메타데이터를 출력합니다. 입력이 URL이면 Svcutil.exe는 디스크에 메타데이터를 저장하고 코드를 생성하지 않습니다. 입력이 하나 이상의 어셈블리이면 Svcutil.exe는 어셈블리의 형식에서 메타데이터를 생성합니다.|  
|ErrAmbiguousOptionModeConflict|지정된 옵션이 다른 옵션과 충돌합니다. 도구 사용을 검토하십시오.|  
|ErrNotLanguageOrCodeDomType|지정된 인수에 전달된 지정된 값이 정의된 언어를 나타내지 않으므로 정규화된 CLR 형식으로 로드할 수 없습니다.|  
|ErrUnableToUniquifyFilename|출력 파일 이름을 만들 수 없습니다. 지정된 접두사를 사용하여 너무 많은 파일을 만들고 있습니다.|  
|ErrCannotCreateFile|지정된 출력 파일을 만들 수 없습니다.|  
|ErrExpectedValue|지정된 옵션에서는 값을 지정해야 합니다.|  
|ErrCannotDisambiguateSpecifiedTypes|참조된 어셈블리 집합에 동일한 이름을 가진 둘 이상의 형식이 있습니다. 정규화된 어셈블리 이름을 사용하여 지정된 옵션에 대한 지정된 형식을 구분하십시오.|  
|RetreivingMetadataWithMexOnly|WS-Metadata Exchange를 사용하여 지정된 위치에서 메타데이터를 다운로드하고 있습니다. 이 URL은 DISCO를 지원하지 않습니다.|  
|ErrInvalidTarget|지정된 옵션을 사용하여 지정된 경우 지정된 대상이 잘못되었습니다. 지원되는 대상이 지정되었습니다.|  
|ErrPathTooLong|결과 경로가 너무 깁니다. 지정된 인수를 검토합니다.|  
|HelpCommonOptionsCategory|-= 일반 옵션 =-|  
|ParametersServiceName|\<serviceConfigName>|  
|ErrNoValidInputFilesSpecified|올바른 입력 파일이 지정되지 않았습니다. 메타데이터 문서 또는 어셈블리 파일을 지정하십시오.|  
|ParametersLanguage|\<language>|  
|ErrUnableToLoadMetadataDocument|로드된 문서 중 하나에서 메타데이터를 읽은 동안 오류가 발생했습니다. 문서 식별자가 지정되었습니다.|  
|ErrConflictingInputs|지정된 입력 인수와 지정된 인수가 서로 다른 도구 작업 모드를 나타내므로 충돌합니다.|  
|WrnUnableToLoadContractForValidation|계약 형식을 로드하는 동안 오류가 발생했습니다. 형식 및 세부 사항이 지정되었습니다.|  
|WrnAttributeReflectionErrors|지정된 위치에서 로드된 어셈블리의 일부 형식에 대해 특성을 반영하지 못했습니다. 적합한 보안 권한으로 이 어셈블리를 이 위치에서 로드할 수 있는지 확인하십시오.|  
|HelpMetadataExportCategory|-= 메타데이터 내보내기 =-|  
|HelpValidationCategory|-= 서비스 유효성 검사 =-|  
|ValidationError|유효성 검사 오류:|  
|GeneratingFiles|파일 생성 중...|  
|ErrCannotSpecifyMultipleMappingsForNamespace|잘못된 값이 지정된 옵션에 전달되었습니다. 지정된 대상 네임스페이스가 지정된 대로 여러 CLR 네임스페이스에 매핑될 수 없습니다.|  
|ErrCouldNotLoadReferenceAssemblyAt|지정된 참조 어셈블리를 로드할 수 없습니다.|  
|ParametersOut|\<file>|  
|NoCodeWasGeneratedSuggestDCOnly|스키마에서 계약을 생성하려면 지정된 옵션을 사용합니다.|  
|ErrUnableToLoadInputConfig|지정된 구성 파일을 로드할 수 없습니다.|  
|ErrUnexpectedDelimiter|잘못된 인수 구분 기호(':' 또는 '=')로 옵션을 시작할 수 없습니다.|  
|ErrMergeConfigUsedWithoutConfig|지정된 다른 옵션을 지정하지 않고 지정된 옵션을 사용할 수 없습니다.|  
|ErrUnableToExportContract|지정된 형식에서 로드된 계약을 내보내는 동안 오류가 발생했습니다.|  
|GeneratingMetadata|메타데이터 파일 생성 중...|  
|ErrNotCodeDomType|지정된 인수에 전달된 지정된 형식이 지정된 파생 클래스가 아닙니다.|  
|WrnNoTypeForServices|전달된 어셈블리에 지정된 구성 이름을 가진 서비스 유형이 포함되어 있지 않습니다.|  
|ErrAssemblyLoadFailed|지정된 파일을 어셈블리로 로드할 수 없습니다. 자세한 내용은 FusionLogs를 확인하십시오.|  
|NoMetadataWasGenerated|메타데이터 파일이 생성되지 않았습니다. 서비스 계약이 내보내지지 않았습니다.<br /><br /> 서비스를 내보내려면 지정된 옵션을 사용하십시오. 데이터 계약을 내보내려면 옵션을 지정하십시오.|  
|WrnCannotResolveServiceForExport|지정된 configName의 서비스를 로드할 수 없습니다. 서비스를 내보내려면 서비스 유형이 포함된 어셈블리와 이 서비스에 대한 구성이 포함된 실행 파일을 모두 제공하십시오.|  
|ParametersCollectionType|\<type>|  
|ErrOptionConflictsWithTarget|지정된 옵션을 지정된 값으로 설정하면 지정된 옵션을 사용할 수 없습니다.|  
|ErrCodegenError|지정한 언어로 코드를 생성하는 동안 오류가 발생했습니다.<br /><br /> 이 언어에서 생성 중인 코드 요소 중 일부만 지원합니다. 다른 언어를 사용해야 합니다.|  
|ErrInputWsdlParseError|지정된 XML을 읽는 동안 WSDL 구문 분석 오류가 발생했습니다. XML이 유효하고 형식이 올바른지 확인하십시오.|  
|ErrCouldNotCreateInstance|지정된 인수에 전달된 지정된 형식의 인스턴스를 만들 수 없습니다.|  
|ParametersNamespace|\<string,string>|  
|HelpNostdlib|표준 라이브러리(기본적으로 mscorlib.dll 및 system.servicemodel.dll 참조)를 참조하지 않습니다.|  
|WrnCannotLoadConfigFileForExport|지정된 위치에서 로드된 구성 파일을 처리하는 동안 오류가 발생했습니다. 이 구성 파일에 정의되어 있는 서비스를 로드할 수 없습니다.|  
|WrnUnableToLoadContractForExport|계약 형식을 로드하는 동안 오류가 발생했습니다. 지정된 이 형식을 내보낼 수 없습니다.|
