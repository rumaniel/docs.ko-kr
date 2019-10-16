---
title: SignTool.exe(서명 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- Sign tool
- SignTool.exe
ms.assetid: 0c25ff6c-bff3-422e-b017-146a3ee86cb9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f99b2fd4716b069d4ec7a21e369c5178990ce16d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044202"
---
# <a name="signtoolexe-sign-tool"></a>SignTool.exe(서명 도구)
서명 도구는 파일에 디지털 서명을 하고, 파일의 서명을 확인하고, 파일에 타임스탬프를 기록하는 명령줄 도구입니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
signtool [command] [options] [file_name | ...]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|인수|설명|  
|--------------|-----------------|  
|`command`|파일에서 수행할 연산을 지정하는 명령 4개(`catdb`, `sign`, `Timestamp` 또는 `Verify`) 중 하나입니다. 각 명령의 설명에 대해서는 다음 표를 참조하세요.|  
|`options`|명령을 수정하는 옵션입니다. 전역 `/q` 및 `/v` 옵션 이외에도 각 명령은 고유한 옵션 집합을 지원합니다.|  
|`file_name`|서명할 파일 경로입니다.|  
  
 다음은 서명 도구에서 지원되는 명령입니다. 각 명령은 각 섹션에 나열된 옵션의 고유 집합과 함께 사용됩니다.  
  
|명령|설명|  
|-------------|-----------------|  
|`catdb`|카탈로그 데이터베이스에서 카탈로그 파일을 추가하거나 제거합니다. 카탈로그 데이터베이스는 카탈로그 파일의 자동 조회에 사용되며 GUID를 통해 식별됩니다. `catdb` 명령에서 지원하는 옵션 목록은 [catdb 명령 옵션](signtool-exe.md#catdb)을 참조하세요.|  
|`sign`|파일에 디지털 서명을 수행합니다. 디지털 서명은 파일 조작으로부터 보호하고 사용자가 서명 인증서를 기반으로 서명자를 확인할 수 있습니다. `sign` 명령에서 지원하는 옵션 목록은 [sign 명령 옵션](signtool-exe.md#sign)을 참조하세요.|  
|`Timestamp`|파일에 타임스탬프를 기록합니다. `TimeStamp` 명령에서 지원하는 옵션 목록은 [TimeStamp 명령 옵션](signtool-exe.md#TimeStamp)을 참조하세요.|  
|`Verify`|파일의 디지털 서명을 검사하여 신뢰할 수 있는 기관에서 발행한 서명 인증서인지, 해당 서명 인증서가 취소되었는지, 아니면 서명 인증서가 특정 정책에 대해 유효한지를 선택적으로 확인합니다. `Verify` 명령에서 지원하는 옵션 목록은 [Verify 명령 옵션](signtool-exe.md#Verify)을 참조하세요.|  
  
 다음 옵션은 모든 서명 도구 명령에 적용됩니다.  
  
|전역 옵션|설명|  
|-------------------|-----------------|  
|**/q**|명령이 성공적으로 실행되는 경우 출력을 표시하지 않고, 명령이 실패하는 경우 최소 출력을 표시합니다.|  
|**/v**|명령이 성공적으로 실행되는지 또는 실패하는지 여부와 상관없이 자세한 정보 출력을 표시하고 경고 메시지를 표시합니다.|  
|**/debug**|디버깅 정보를 표시합니다.|  
  
<a name="catdb"></a>   
## <a name="catdb-command-options"></a>catdb 명령 옵션  
 다음 표에는 `catdb` 명령에 사용할 수 있는 옵션이 나열되어 있습니다.  
  
|Catdb 옵션|설명|  
|------------------|-----------------|  
|`/d`|기본 카탈로그 데이터베이스가 업데이트되도록 지정합니다. `/d`와 `/g` 옵션을 모두 사용하지 않을 경우 서명 도구에서 시스템 구성 요소와 드라이버 데이터베이스를 업데이트합니다.|  
|`/g` *GUID*|*GUID*(Globally Unique Identifier)로 식별된 카탈로그 데이터베이스가 업데이트되도록 지정합니다.|  
|`/r`|지정된 카탈로그를 카탈로그 데이터베이스에서 제거합니다. 이 옵션을 지정하지 않으면 서명 도구는 지정된 카탈로그를 카탈로그 데이터베이스에 추가합니다.|  
|`/u`|추가된 카탈로그 파일에 대해 고유한 이름이 자동으로 생성되도록 지정합니다. 필요한 경우 기존 카탈로그 파일과의 이름 충돌을 방지하기 위해 카탈로그 파일의 이름을 바꿉니다. 이 옵션을 지정하지 않으면 서명 도구는 추가하려는 카탈로그와 같은 이름의 기존 카탈로그를 덮어씁니다.|  
  
<a name="sign"></a>   
## <a name="sign-command-options"></a>sign 명령 옵션  
 다음 표에는 `sign` 명령에 사용할 수 있는 옵션이 나열되어 있습니다.  
  
|Sign 명령 옵션|설명|  
|-------------------------|-----------------|  
|`/a`|가장 적합한 서명 인증서를 자동으로 선택합니다. 서명 도구는 지정한 모든 조건을 만족하는 유효한 모든 인증서를 찾아서 최대 시간 동안 유효한 인증서를 선택합니다. 이 옵션이 없으면 서명 도구는 유효한 서명 인증서를 하나만 찾게 됩니다.|  
|`/ac`  *file*|*file*의 추가 인증서를 시그니처 블록에 추가합니다.|  
|`/as`|이 서명을 추가합니다. 주 서명이 없으면, 이 서명이 기본 서명을 대체합니다.|  
|`/c`  *CertTemplateName*|서명 인증서의 인증서 템플릿 이름(Microsoft 확장명)을 지정합니다.|  
|`/csp`  *CSPName*|프라이빗 키 컨테이너를 포함하는 CSP(암호화 서비스 공급자)를 지정합니다.|  
|`/d`  *Desc*|서명된 콘텐츠에 대한 설명을 지정합니다.|  
|`/du`  *URL*|서명한 콘텐츠의 부연 설명에 대한 URL(Uniform Resource Locator)을 지정합니다.|  
|`/f`  *SignCertFile*|파일에 있는 서명 인증서를 지정합니다. 파일이 PFX(개인 정보 교환) 형식이면서 암호로 보호되는 경우, `/p` 옵션을 사용하여 암호를 지정합니다. 파일에 프라이빗 키가 없으면 `/csp` 및 `/kc` 옵션을 사용하여 CSP 및 프라이빗 키 컨테이너 이름을 지정합니다.|  
|`/fd`|파일 서명을 만드는 데 사용할 파일 다이제스트 알고리즘을 지정합니다. 기본값은 SHA1입니다.|  
|`/i`  *IssuerName*|서명 인증서의 발급자 이름을 지정합니다. 이 값은 발급자의 전체 이름에서 부분 문자열이 될 수 있습니다.|  
|`/kc`  *PrivKeyContainerName*|프라이빗 키 컨테이너 이름을 지정합니다.|  
|`/n`  *SubjectName*|서명 인증서의 주체 이름을 지정합니다. 이 값은 주체의 전체 이름에서 부분 문자열이 될 수 있습니다.|  
|`/nph`|지원되는 경우 실행 파일에 대한 페이지 해시를 억제합니다. 기본값은 SIGNTOOL_PAGE_HASHES 환경 변수 및 wintrust.dll 버전에 의해 결정됩니다. PE 파일이 아닌 경우 이 옵션이 무시됩니다.|  
|`/p`  *Password*|PFX 파일을 열 때 사용할 암호를 지정합니다. (`/f` 옵션을 사용하여 PFX 파일을 지정합니다.)|  
|`/p7` *Path*|지정된 각 콘텐츠 파일에 대한 PKCS(공개 키 암호화 표준) #7 파일이 생성되도록 지정합니다. PKCS #7 파일의 이름은 *path*\\*filename*.p7입니다.|  
|`/p7ce` *Value*|서명된 PKCS #7 콘텐츠에 대한 옵션을 지정합니다. 서명된 콘텐츠를 PKCS #7 파일에 포함하려면 *Value*를 "Embedded"로 설정하고, 분리된 PKCS #7 파일의 서명된 데이터 부분을 생성하려면 "DetachedSignedData"로 설정합니다. `/p7ce` 옵션을 사용하지 않을 경우 서명된 내용이 기본으로 포함됩니다.|  
|`/p7co` *\<OID>*|서명된 PKCS #7 콘텐츠를 식별하는 OID(개체 식별자)를 지정합니다.|  
|`/ph`|지원되지 않는 경우 실행 파일에 대한 페이지 해시를 생성합니다.|  
|`/r`  *RootSubjectName*|서명 인증서와 연결해야 하는 루트 인증서의 주체 이름을 지정합니다. 이 값은 루트 인증서 주체의 전체 이름에서 부분 문자열이 될 수 있습니다.|  
|`/s`  *StoreName*|인증서를 검색할 때 열 저장소를 지정합니다. 이 옵션을 지정하지 않으면 `My` 저장소가 열립니다.|  
|`/sha1`  *Hash*|서명 인증서의 SHA1 해시를 지정합니다. 남은 스위치가 지정한 기준을 여러 인증서가 충족시키는 경우 SHA1 해시는 일반적으로 지정됩니다.|  
|`/sm`|사용자 저장소 대신 컴퓨터 저장소가 사용되도록 지정합니다.|  
|`/t`  *URL*|타임스탬프 서버의 URL을 지정합니다. 이 옵션(또는 `/tr`)이 없으면 서명 파일에 타임스탬프가 기록되지 않습니다. 타임스탬프 기록에 실패하면 경고가 생성됩니다. 이 옵션은 `/tr` 옵션과 함께 사용할 수 없습니다.|  
|`/td`  *alg*|`/tr` 옵션을 사용하여 RFC 3161 타임스탬프 서버에서 사용하는 다이제스트 알고리즘을 요청합니다.|  
|`/tr`  *URL*|RFC 3161 타임스탬프 서버의 URL을 지정합니다. 이 옵션(또는 `/t`)이 없으면 서명 파일에 타임스탬프가 기록되지 않습니다. 타임스탬프 기록에 실패하면 경고가 생성됩니다. 이 옵션은 `/t` 옵션과 함께 사용할 수 없습니다.|  
|`/u`  *Usage*|EKU(확장된 키 사용)가 서명 인증서에 있도록 지정합니다. 용도 값은 OID 또는 문자열로 지정될 수 있습니다. 기본 용도는 "코드 서명"(1.3.6.1.5.5.7.3.3)입니다.|  
|`/uw`|"Windows 시스템 구성 요소 확인"의 사용을 지정합니다(1.3.6.1.4.1.311.10.3.6).|  
  
 사용 예제는 [SignTool을 사용하여 파일에 서명](/windows/desktop/SecCrypto/using-signtool-to-sign-a-file)을 참조하세요.  
  
<a name="TimeStamp"></a>   
## <a name="timestamp-command-options"></a>TimeStamp 명령줄 옵션  
 다음 표에는 `TimeStamp` 명령에 사용할 수 있는 옵션이 나열되어 있습니다.  
  
|TimeStamp 옵션|설명|  
|----------------------|-----------------|  
|`/p7`|파일에 PKCS #7 타임스탬프를 기록합니다.|  
|`/t`  *URL*|타임스탬프 서버의 URL을 지정합니다. 타임스탬프가 기록되는 파일은 이전에 서명되었어야 합니다. `/t` 또는 `/tr` 옵션이 필요합니다.|  
|`/td`  *alg*|RFC 3161 타임 스탬프 서버에서 사용하는 다이제스트 알고리즘을 요청합니다. `/td`는 `/tr` 옵션과 함께 사용됩니다.|  
|`/tp` *index*|*index*에서 시그니처에 타임스탬프를 지정합니다.|  
|`/tr`  *URL*|RFC 3161 타임스탬프 서버의 URL을 지정합니다. 타임스탬프가 기록되는 파일은 이전에 서명되었어야 합니다. `/tr` 또는 `/t` 옵션이 필요합니다.|  
  
 사용 예제는 [이전에 서명한 파일에 타임스탬프 추가](/windows/desktop/SecCrypto/adding-time-stamps-to-previously-signed-files)를 참조하세요.  
  
<a name="Verify"></a>   
## <a name="verify-command-options"></a>명령 옵션 확인  
  
|옵션 확인|설명|  
|-------------------|-----------------|  
|`/a`|모든 메서드를 사용하여 파일을 확인할 수 있도록 지정합니다. 먼저 카탈로그 데이터베이스를 검색하여 카탈로그에서 파일이 서명되었는지 여부를 확인합니다. 어떤 카탈로그에서도 파일이 서명되지 않은 경우에는 서명 도구에서 파일에 포함된 서명을 확인하려고 합니다. 이 옵션은 카탈로그에서 서명되거나 서명되지 않은 파일을 확인할 때 권장됩니다. 이러한 파일의 예로는 Windows 파일 또는 드라이버가 있습니다.|  
|`/ad`|기본 카탈로그 데이터베이스를 사용하여 카탈로그를 찾습니다.|  
|`/ag` *CatDBGUID*|카탈로그 데이터베이스에서 *CatDBGUID*로 식별된 카탈로그를 찾습니다.|  
|`/all`|여러 개의 시그니처를 포함하는 파일의 모든 시그니처를 확인합니다.|  
|`/as`|시스템 구성 요소(드라이버) 카탈로그 데이터베이스를 사용하여 해당 카탈로그를 찾습니다.|  
|`/c` *CatFile*|이름별로 카탈로그 파일을 지정합니다.|  
|`/d`|서명 도구가 설명과 설명 URL을 인쇄하도록 지정합니다.|  
|`/ds`  *Index*|지정된 위치에서 시그니처를 확인합니다.|  
|`/hash` (`SHA1`&#124;`SHA256`)|카탈로그에서 파일을 검색할 때 사용할 선택적 해시 알고리즘을 지정합니다.|  
|`/kp`|커널 모드 드라이버 서명 정책을 이용하여 검증을 수행하도록 지정합니다.|  
|`/ms`|여러 확인 의미 체계를 사용합니다. 이는 [!INCLUDE[win8](../../../includes/win8-md.md)] 이상에 대한 [WinVerifyTrust](/windows/desktop/api/wintrust/nf-wintrust-winverifytrust) 호출의 기본 동작입니다.|  
|`/o` *Version*|운영 체제 버전별로 파일을 확인합니다. *Version*의 형식은 다음과 같습니다. *PlatformID*:*VerMajor*.*VerMinor*.*BuildNumber*. *PlatformID*는 <xref:System.PlatformID> 열거형 멤버의 내부 값을 나타냅니다. **중요:**  `/o` 스위치를 사용하는 것이 좋습니다. `/o`가 지정되지 않으면 SignTool.exe가 예기치 않은 결과를 반환할 수 있습니다. 예를 들어 `/o` 스위치가 포함되지 않는 경우 이전 운영 체계에서 유효성이 제대로 입증된 시스템 카탈로그가 새로운 운영 체계에서는 유효성이 제대로 입증되지 않을지 모릅니다.|  
|`/p7`|PKCS #7 파일을 확인합니다. PKCS #7 유효성 검사에 기존 정책이 사용되지 않습니다. 서명이 확인되고 서명 인증서에 대한 체인이 빌드됩니다.|  
|`/pa`|기본 Authenticode 확인 정책이 사용되도록 지정합니다. `/pa` 옵션을 지정하지 않으면 서명 도구는 Windows 드라이버 확인 정책을 사용합니다. 이 옵션은 `catdb` 옵션과 함께 사용할 수 없습니다.|  
|`/pg` *PolicyGUID*|GUID를 기준으로 확인 정책을 지정합니다. *PolicyGUID*는 확인 정책의 ActionID에 해당합니다. 이 옵션은 `catdb` 옵션과 함께 사용할 수 없습니다.|  
|`/ph`|서명 도구가 페이지 해시 값을 인쇄 및 확인하도록 지정합니다.|  
|`/r` *RootSubjectName*|서명 인증서와 연결해야 하는 루트 인증서의 주체 이름을 지정합니다. 이 값은 루트 인증서 주체의 전체 이름에서 부분 문자열이 될 수 있습니다.|  
|`/tw`|서명에 타임스탬프가 기록되지 않으면 경고가 생성되도록 지정합니다.|  
  
 사용 예제는 [SignTool을 사용하여 파일 시그니처 확인](/windows/desktop/SecCrypto/using-signtool-to-verify-a-file-signature)을 참조하세요.  
  
## <a name="return-value"></a>Return Value  
 서명 도구는 종료할 때 다음 종료 코드 중 하나를 반환합니다.  
  
|종료 코드|설명|  
|---------------|-----------------|  
|0|실행이 완료되었습니다.|  
|1|실행하지 못했습니다.|  
|2|실행이 경고와 함께 완료되었습니다.|  
  
## <a name="examples"></a>예  
 다음 명령은 카탈로그 파일 MyCatalogFileName.cat를 시스템 구성 요소와 드라이버 데이터베이스에 추가합니다. `/u` 옵션은 `MyCatalogFileName.cat`라는 기존 카탈로그 파일이 바뀌지 않도록 해야 하는 경우 고유 이름을 생성합니다.  
  
```console  
signtool catdb /v /u MyCatalogFileName.cat  
```  
  
 다음 명령은 가장 적합한 인증서를 사용하여 파일에 자동으로 서명합니다.  
  
```console  
signtool sign /a MyFile.exe  
```  
  
 다음 명령은 암호로 보호된 PFX 파일에 저장된 인증서를 사용하여 파일에 디지털 서명을 합니다.  
  
```console  
signtool sign /f MyCert.pfx /p MyPassword MyFile.exe  
```  
  
 다음 명령은 파일에 디지털 서명을 하고 타임스탬프를 기록합니다. 파일에 서명하는 데 사용할 인증서는 PFX 파일로 저장됩니다.  
  
```console  
signtool sign /f MyCert.pfx /t http://timestamp.digicert.com MyFile.exe  
```  
  
 다음 명령은 `My`의 주체 이름이 있는 `My Company Certificate` 저장소에 위치한 인증서를 사용하여 파일에 서명합니다.  
  
```console  
signtool sign /n "My Company Certificate" MyFile.exe  
```  
  
 다음 명령은 ActiveX 컨트롤에 서명하고 컨트롤을 설치하도록 사용자에게 메시지가 표시될 때 Internet Explorer에 표시되는 정보를 제공합니다.  
  
```console  
Signtool sign /f MyCert.pfx /d: "MyControl" /du http://www.example.com/MyControl/info.html MyControl.exe  
```  
  
 다음 명령은 이미 디지털 서명된 파일에 타임스탬프를 기록합니다.  
  
```console  
signtool timestamp /t http://timestamp.digicert.com MyFile.exe  
```  
  
 다음 명령은 파일이 서명되었는지를 확인합니다.  
  
```console  
signtool verify MyFile.exe  
```  
  
 다음 명령은 카탈로그에서 서명될 수 있는 시스템 파일을 확인합니다.  
  
```console  
signtool verify /a SystemFile.dll  
```  
  
 다음 명령은 `MyCatalog.cat`라는 카탈로그에서 서명된 시스템 파일을 확인합니다.  
  
```console  
signtool verify /c MyCatalog.cat SystemFile.dll  
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
