---
title: FindPrivateKey 샘플-WCF
ms.date: 12/04/2017
helpviewer_keywords:
- FindPrivateKey
ms.assetid: 16b54116-0ceb-4413-af0c-753bb2a785a6
ms.openlocfilehash: 4ba4316489c1494da9421bea5c513e44c6eb50a7
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989879"
---
# <a name="findprivatekey-sample"></a>FindPrivateKey 샘플

인증서 저장소에서 특정 X.509 인증서와 연결된 프라이빗 키 파일의 위치 및 이름을 찾기가 어려울 수 있습니다. FindPrivateKey.exe 도구는 이 과정에 도움이 됩니다.

> [!IMPORTANT]
> FindPrivateKey는 사용하기 전에 컴파일되어야 하는 샘플입니다. FindPrivateKey 도구를 빌드하는 방법에 대 한 지침은 [FindPrivateKey 프로젝트를 빌드하](#to-build-the-findprivatekey-project) 는 방법 섹션을 참조 하세요.

X.509 인증서는 관리자 또는 시스템에 있는 모든 사용자가 설치합니다. 그러나 다른 계정으로 실행 되는 서비스에서 인증서에 액세스할 수 있습니다. 예를 들어 네트워크 서비스 계정이 있습니다.

처음에 인증서를 이 계정으로 설치하지 않았기 때문에 이 계정에 프라이빗 키 파일에 대한 액세스 권한이 없을 수도 있습니다. FindPrivateKey 도구는 지정된 X.509 인증서의 개인 키 파일 위치를 알려줍니다. 특정 X.509 인증서의 프라이빗 키 파일 위치를 알고 나면 이 파일의 사용 권한을 추가하거나 제거할 수 있습니다.

보안을 위해 인증서를 사용 하는 샘플은 *설치 .bat* 파일의 FindPrivateKey 도구를 사용 합니다. 개인 키 파일이 발견 되 면 *cacls.exe* 와 같은 다른 도구를 사용 하 여 파일에 대 한 적절 한 액세스 권한을 설정할 수 있습니다.

사용자 계정 (예: 자체 호스팅 실행 파일)에서 WCF (Windows Communication Foundation) 서비스를 실행 하는 경우 사용자 계정에 파일에 대 한 읽기 전용 액세스 권한이 있는지 확인 합니다. 인터넷 정보 서비스 (IIS)에서 WCF 서비스를 실행 하는 경우 서비스를 실행 하는 기본 계정은 IIS 7 및 이전 버전의 네트워크 서비스 이거나 IIS 7.5 이상 버전의 응용 프로그램 풀 Id입니다. 자세한 내용은 [응용 프로그램 풀 id](/iis/manage/configuring-security/application-pool-identities)를 참조 하세요.

## <a name="examples"></a>예

프로세스에 읽기 권한이 없는 인증서에 액세스 하는 경우 다음 예제와 비슷한 예외 메시지가 표시 됩니다.

```output
System.ArgumentException was unhandled
Message="The certificate 'CN=localhost' must have a private key that is capable of key exchange.  The process must have access rights for the private key."
Source="System.ServiceModel"
```

이 문제가 발생 하는 경우 FindPrivateKey 도구를 사용 하 여 개인 키 파일을 찾은 다음 서비스가 실행 되 고 있는 프로세스에 대 한 액세스 권한을 설정 합니다. 예를 들어 다음 예제와 같이 Cacls.exe 도구를 사용 하 여이 작업을 수행할 수 있습니다.

```console
cacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /E /G "NETWORK SERVICE":R
```

#### <a name="to-build-the-findprivatekey-project"></a>FindPrivateKey 프로젝트를 빌드하려면

프로젝트를 다운로드 하려면 [.NET Framework 4에 대 한 Windows Communication Foundation (WCF) 및 Windows Workflow Foundation (WF) 샘플](https://www.microsoft.com/download/details.aspx?id=21459)을 참조 하세요.

1. 파일 탐색기를 열고 샘플을 설치한 디렉터리 위치 아래의 *WF_WCF_Samples\WCF\Setup\FindPrivateKey\CS* 폴더로 이동 합니다.

2. .sln 파일 아이콘을 두 번 클릭하여 Visual Studio에서 파일을 엽니다.

3. **빌드** 메뉴에서 **솔루션 다시 빌드**를 선택 합니다.

4. 솔루션을 빌드하면 파일이 생성 됩니다. FindPrivateKey.exe.

## <a name="conventionscommand-line-entries"></a>규칙-명령줄 항목

 "[*option*]"은 선택적 매개 변수 집합을 나타냅니다.

 "{*option*}"은 (는) 필수 매개 변수 집합을 나타냅니다.

 "*옵션 1 마이그레이션* &#124; *옵션 2 마이그레이션*"는 옵션 집합 사이의 선택을 나타냅니다.

 "\<*value*>"는 입력할 매개 변수 값을 나타냅니다.

## <a name="usage"></a>사용

```console
FindPrivateKey <storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]
```

각 항목이 나타내는 의미는 다음과 같습니다.

| 매개 변수         | 설명                                                                       |
|-----------------|-----------------------------------------------------------------------------------|
| `<subjectName>` | 인증서의 주체 이름입니다.                                               |
| `<thumbprint>`  | 인증서의 손 도장 (Certmgr.exe 도구를 사용 하 여 찾을 수 있음) |
| `-f`            | 출력 파일 이름만                                                             |
| `-d`            | 출력 디렉터리만                                                             |
| `-a`            | 출력 절대 파일 이름                                                         |

명령 프롬프트에서 매개 변수를 지정 하지 않으면이 정보를 포함 하는 도움말 텍스트가 표시 됩니다.

## <a name="examples"></a>예

이 예에서는 현재 사용자의 개인 저장소에서 주체 이름이 "CN = localhost" 인 인증서의 파일 이름을 찾습니다.

```console
FindPrivateKey My CurrentUser -n "CN=localhost"
```

이 예제에서는 현재 사용자의 개인 저장소에서 주체 이름이 "CN = localhost" 인 인증서의 파일 이름을 찾고 전체 디렉터리 경로를 출력 합니다.

```console
FindPrivateKey My CurrentUser -n "CN=localhost" -a
```

이 예제에서는 로컬 컴퓨터의 개인 저장소에서 지문이 "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52"인 인증서의 파일 이름을 찾습니다.

```console
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52"
```
