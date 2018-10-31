---
title: Certmgr.exe(인증서 관리자 도구)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- certificates, managing
- CRLs
- certificate trust lists
- Certmgr.exe
- Certificate Manager tool
- CTLs
- certificate revocation lists
ms.assetid: 7e953b43-1374-4bbc-814f-53ca1b6b52bb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9ad1cbd9da3a6b55dbb23eaf97c10e6090077fd8
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198486"
---
# <a name="certmgrexe-certificate-manager-tool"></a>Certmgr.exe(인증서 관리자 도구)
인증서 관리자 도구(Certmgr.exe)를 사용하면 인증서, CTL(인증서 신뢰 목록) 및 CRL(인증서 해지 목록)을 관리할 수 있습니다.  
  
 인증서 관리자는 Visual Studio와 함께 자동으로 설치됩니다. 도구를 시작하려면 [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)를 사용합니다.  
  
> [!NOTE]
>  인증서 관리자 도구(Certmgr.exe)는 명령줄 유틸리티인 반면, 인증서(Certmgr.msc)는 MMC(Microsoft Management Console) 스냅인입니다. Certmgr.msc는 대개 Windows 시스템 디렉터리에서 발견되기 때문에 명령줄에 `certmgr`을 입력하면 Visual Studio 명령 프롬프트를 연 경우에도 인증서 MMC 스냅인을 로드할 수 있습니다. 이는 PATH 환경 변수에서 스냅인 경로가 인증서 관리자 도구로의 경로 앞에 오기 때문에 발생합니다. 이 문제가 발생하는 경우 실행 파일에 대한 경로를 지정하여 Certmgr.exe 명령을 실행할 수 있습니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)를 참조하세요.  
  
 X.509 인증서에 대한 개요는 [인증서 작업](../../../docs/framework/wcf/feature-details/working-with-certificates.md)을 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```  
      certmgr [/add | /del | /put] [options]  
[/s[/r registryLocation]] [sourceStorename]  
[/s[/r registryLocation]] [destinationStorename]  
```  
  
#### <a name="parameters"></a>매개 변수  
  
|인수|설명|  
|--------------|-----------------|  
|*sourceStorename*|추가, 삭제, 저장 또는 표시할 CRL 또는 CTL, 기존 인증서를 포함하는 인증서 저장소입니다. 이는 저장소 파일 또는 시스템 저장소가 될 수 있습니다.|  
|*destinationStorename*|출력 인증서 저장소 또는 파일을 나타냅니다.|  
  
|옵션|설명|  
|------------|-----------------|  
|**/add**|인증서, CTL 및 CRL을 인증서 저장소에 추가합니다.|  
|**/all**|**/add** 옵션과 함께 사용하면 모든 항목을 추가합니다. **/del** 옵션과 함께 사용하면 모든 항목을 삭제합니다. /add 또는 **/del** 옵션 없이 사용하면 모든 항목을 표시합니다. **/all** 옵션은 **/put**과 함께 사용할 수 없습니다.|  
|**/c**|**/add** 옵션과 함께 사용하면 인증서를 추가합니다. **/del** 옵션과 함께 사용하면 인증서를 삭제합니다. **/put** 옵션과 함께 사용하면 인증서를 저장합니다. **/add**, **/del** 또는 **/put** 옵션 없이 사용하면 인증서를 표시합니다.|  
|**/CRL**|**/add**와 함께 사용하면 CRL을 추가합니다. **/del**과 함께 사용하면 CRL을 삭제합니다. **/put**과 함께 사용하면 CRL을 저장합니다. **/add**, **/del** 또는 **/put** 옵션 없이 사용하면 CRL을 표시합니다.|  
|**/CTL**|**/add**와 함께 사용하면 CTL을 추가합니다. **/del**과 함께 사용하면 CTL을 삭제합니다. **/put**과 함께 사용하면 CTL을 저장합니다. **/add**, **/del** 또는 **/put** 옵션 없이 사용하면 CTL을 표시합니다.|  
|**/del**|인증서, CTL 및 CRL을 인증서 저장소에서 삭제합니다.|  
|**/e** *encodingType*|인증서 인코딩 형식을 지정합니다. 기본값은 `X509_ASN_ENCODING`입니다.|  
|**/f** *dwFlags*|저장소 열기 플래그를 지정합니다. 저장소 열기 플래그는 **CertOpenStore**에 전달되는 *dwFlags* 매개 변수입니다. 기본값은 CERT_SYSTEM_STORE_CURRENT_USER이고, 이 옵션은 **/y** 옵션이 사용된 경우에만 고려됩니다.|  
|**/h**[**elp**]|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|**/n** *nam*|추가, 삭제 또는 저장할 인증서의 일반 이름을 지정합니다. 이 옵션은 인증서에 대해서만 사용할 수 있으며, CTL 또는 CRL에 대해서는 사용할 수 없습니다.|  
|**/put**|인증서 저장소의 X.509 인증서, CTL 또는 CRL을 파일에 저장합니다. 이 파일은 X.509 형식으로 저장됩니다. **/7** 옵션을 **/put** 옵션과 함께 사용하여 파일을 PKCS #7 형식으로 저장할 수 있습니다. **/put** 옵션 다음에는 **/c**, **/CTL** 또는 **/CRL** 중 하나를 사용해야 하며, **/all** 옵션은 **/put**과 함께 사용할 수 없습니다.|  
|**/r** *위치*|시스템 저장소의 레지스트리 위치를 식별합니다. 이 옵션은 **/s** 옵션을 지정하는 경우에만 고려됩니다. *위치*는 다음 중 하나여야 합니다.<br /><br /> -   `currentUser`는 인증서 저장소가 HKEY_CURRENT_USER 키 아래에 있음을 나타냅니다. 이 값이 기본값입니다.<br />-   `localMachine`은 인증서 저장소가 HKEY_LOCAL_MACHINE 키 아래에 있음을 나타냅니다.|  
|**/s**|인증서 저장소가 시스템 저장소임을 나타냅니다. 이 옵션을 지정하지 않으면 저장소가 **StoreFile**로 간주됩니다.|  
|**/sha1** *sha1Hash*|추가, 삭제 또는 저장할 인증서, CTL 또는 CRL의 SHA1 해시를 지정합니다.|  
|**/v**|세부 정보 표시 모드를 지정합니다. 즉, 인증서, CTL 및 CRL에 대한 자세한 정보를 표시합니다. 이 옵션은 **/add**, **/del** 또는 **/put** 옵션과 함께 사용할 수 없습니다.|  
|**/y** *공급자*|저장소 공급자의 이름을 지정합니다.|  
|**/7**|대상 저장소를 PKCS #7 개체로 저장합니다.|  
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
## <a name="remarks"></a>설명  
 Certmgr.exe를 사용하여 다음과 같은 기본 기능을 수행할 수 있습니다.  
  
-   인증서, CTL 및 CRL을 콘솔에 표시합니다.  
  
-   인증서, CTL 및 CRL을 인증서 저장소에 추가합니다.  
  
-   인증서, CTL 및 CRL을 인증서 저장소에서 삭제합니다.  
  
-   인증서 저장소의 X.509 인증서, CTL 또는 CRL을 파일에 저장합니다.  
  
 Certmgr.exe를 사용하면 두 가지 형식의 인증서 저장소(**StoreFile** 및 시스템 저장소)를 사용하여 작업할 수 있습니다. 그러나 Certmgr.exe로 저장소 형식을 식별한 다음 적합한 작업을 수행할 수 있으므로 인증서 저장소 형식을 지정할 필요는 없습니다.  
  
 옵션을 지정하지 않고 Certmgr.exe를 실행하면 명령줄에서도 사용할 수 있는 인증서 관리 작업을 돕는 GUI인 certmgr.msc snap-in이 실행됩니다. 이 GUI를 통해 디스크의 인증서, CTL 및 CRL을 인증서 저장소에 복사하는 가져오기 마법사를 사용할 수 있습니다.  
  
 `sourceStorename` 및 `destinationStorename` 매개 변수에 대한 X509Certificate 저장소의 이름을 다음 코드를 컴파일 및 실행하여 찾을 수 있습니다.  
  
 [!code-csharp[Tools.CertMgr#1](../../../samples/snippets/csharp/VS_Snippets_CLR/tools.certmgr/cs/storenames1.cs#1)]
 [!code-vb[Tools.CertMgr#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/tools.certmgr/vb/storenames1.vb#1)]  
  
 자세한 내용은 [인증서 작업](../../../docs/framework/wcf/feature-details/working-with-certificates.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 명령을 사용하여 `my`라는 기본 시스템 저장소를 자세한 정보와 함께 표시합니다.  
  
```  
certmgr /v /s my  
```  
  
 다음 명령을 사용하여 `myFile.ext`라는 파일에 있는 모든 인증서를 `newFile.ext`라는 새 파일에 추가합니다.  
  
```  
certmgr /add /all /c myFile.ext newFile.ext  
```  
  
 다음 명령은 `testcert.cer`이라는 파일의 인증서를 `my` 시스템 저장소에 추가합니다.  
  
```  
certmgr /add /c testcert.cer /s my  
```  
  
 다음 명령은 `TrustedCert.cer`이라는 파일의 인증서를 루트 인증서 저장소에 추가합니다.  
  
```  
certmgr /c /add TrustedCert.cer /s root  
```  
  
 다음 명령을 사용하여 `myCert`시스템 저장소에 있는 `my`라는 일반 이름의 인증서를 `newCert.cer`이라는 파일에 저장합니다.  
  
```  
certmgr /add /c /n myCert /s my newCert.cer  
```  
  
 다음 명령을 사용하여 `my` 시스템 저장소에 있는 모든 CTL을 삭제하고 그 결과로 만들어지는 저장소를 `newStore.str`이라는 파일에 저장합니다.  
  
```  
certmgr /del /all /ctl /s my newStore.str  
```  
  
 다음 명령을 사용하여 `my`시스템 저장소의 인증서를 `newFile` 파일에 저장합니다. 그러면 `my`에 넣을 `newFile`의 인증서 번호를 입력하라는 메시지가 표시됩니다.  
  
```  
certmgr /put /c /s my newFile  
```  
  
## <a name="see-also"></a>참고 항목  
 [도구](../../../docs/framework/tools/index.md)  
 [Makecert.exe(인증서 작성 도구)](/windows/desktop/SecCrypto/makecert)  
 [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
