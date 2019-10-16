---
title: 패딩을 사용하는 CBC 모드 대칭 암호 해독의 타이밍 취약성
description: 검색 및 패딩을 사용 하 여 Cipher Block Chaining CBC () 모드 대칭 해독을 사용 하 여 타이밍 취약성을 완화 하는 방법에 알아봅니다.
ms.date: 06/12/2018
author: blowdart
ms.author: mairaw
ms.openlocfilehash: 6d8c2593cdbc4bbff2b1507196989282b16aa9a8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61933902"
---
# <a name="timing-vulnerabilities-with-cbc-mode-symmetric-decryption-using-padding"></a>패딩을 사용하는 CBC 모드 대칭 암호 해독의 타이밍 취약성

Microsoft가는 것이 더 이상 안전 안정형 안쪽 여백을 제외 하 고 암호화 텍스트의 무결성을 확인 하지 않고 적용 된 경우 대칭 암호화의 Cipher Block Chaining (CBC) 모드를 사용 하 여 암호화 된 데이터를 암호 해독에 매우 구체적인 상황입니다. 이 결정을이 내리도록 현재 알려진된 암호화 연구를 기반으로 합니다. 

## <a name="introduction"></a>소개

안쪽 여백 oracle 공격에는 공격 공격자는 키를 알 필요 없이 데이터의 내용을 해독 하는 암호화 된 데이터의 형식입니다.

Oracle을 "알릴" 실행 하는 작업을 올바른 인지 여부에 대 한 공격자가 정보를 제공 하는 참조 합니다. 보드 재생 가정해 보겠습니다. 또는 자식이 있는 게임 카드. 경우 자신의 얼굴 단계인 큰 웃는 얼굴을 사용 하 여 그녀는 그녀가 생각 하기 때문에 oracle는는 적절 한 전환 하려고 합니다. 를 상대,으로 사용할 수 있습니다이 oracle 다음으로 이사를 적절 하 게 계획.

안쪽 여백은 특정 암호화 용어입니다. 일부 암호화 알고리즘에 데이터를 암호화 하는 데 사용 되는 각 블록의 크기가 고정된 되어 있는 데이터 블록에서 작동 합니다. 암호화할 데이터 블록에 맞게 적절 한 크기를 없는 경우 완료 될 때까지 데이터가 채워집니다. 다양 한 형태의 안쪽 여백에는 항상 있어야, 적절 한 크기의 원래 입력 된 경우에 해당 패딩이 필요 합니다. 따라서 제거할 항상 안전 하 게 암호 해독 시 패딩 합니다.

두 가지를 결합, 안쪽 여백 oracle 사용 하는 소프트웨어 구현 해독 된 데이터에 올바른 안쪽 여백에 있는지 여부를 알 수 있습니다. Oracle에는 "잘못 된 패딩이" 라는 값을 반환할 때 간단한 또는 눈에 띄게 다른 시간 잘못 된 블록이 아니라 유효한 블록을 처리 하는 것과 같은 보다 복잡 한 수 있습니다.

블록 기반 암호화 모드를 두 번째 블록의 데이터를 첫 번째 블록에는 데이터의 관계를 결정 하는 호출 이라는 다른 속성이 등에입니다. 가장 자주 사용 되는 모드 중 하나는 CBC입니다. CBC로는 IV (Initialization Vector), 알려진 초기 임의 블록을 정의 하 고 동일한 키를 사용 하 여 동일한 메시지를 암호화 하지 항상 생성 되는 동일한 암호화 된 출력을 확인 하기 위해 정적 암호화의 결과 사용 하 여 이전 블록을 결합 합니다.

공격자는 안쪽 여백 oracle CBC 데이터를 구조화 하는 방법을 함께에서 사용할 수 있습니다, 그리고 oracle를 노출 하는 코드를 약간 변경 된 메시지를 보내고 oracle 알려 될 때까지 데이터를 전송할 데이터가 올바른 합니다. 이 응답에서 공격자는 바이트 단위로 메시지를 해독할 수 있습니다.

최신 컴퓨터 네트워크는 이러한 높은 품질 공격자를 매우 작은 (0.1 밀리초 미만) 원격 시스템에서 실행의 차이점 시간을 검색할 수 있습니다. 데이터 변조 되지 않은 경우 성공적으로 해독만 발생할 수 있음을 가정 하는 응용 프로그램 성공 및 실패 한 암호 해독의 차이 관찰 하도록 설계 된 도구에서 공격에 취약할 수 있습니다. 이 시간 차이 다른 항목 보다 일부 언어 또는 라이브러리에서 더 중요 수 있지만, 이제 믿고이 모든 언어 및 라이브러리에 대 한 실용적인 위협 실패에 대 한 응용 프로그램의 응답은 고려 하는 경우.

이 공격은 암호화 된 데이터를 변경 하 고 oracle 사용 하 여 결과 테스트 하는 기능에 의존 합니다. 완벽 하 게 공격을 완화 하는 유일한 방법은 암호화 된 데이터의 변경 내용을 감지 하 여 모든 작업을 수행할 거부 됩니다. 이 작업을 수행 하는 표준 방법은 데이터에 대 한 서명을 만들고 모든 작업을 수행 하기 전에 해당 서명 유효성을 검사 하는 경우 서명을 확인할 수 있어야 합니다. 공격자가 만들 수 없으므로, 그렇지 않으면 암호화 된 데이터를 변경는 다음 서명을 계산 하는 새 변경된 데이터를 기반으로 합니다. 한 가지 일반적인 유형의 적절 한 시그니처가 키 해시 메시지 인증 코드 (HMAC) 라고 합니다. HMAC 걸리는 비밀 키, 사용자 유효성을 검사 하는 HMAC를 생성 하는 사용자 에게만 알려진 점에서 체크섬과 다릅니다. 키를 소유 하지 않고 올바른 HMAC를 생성할 수 없습니다. 데이터를 받으면 암호화 된 데이터를 독립적으로 계산 HMAC 비밀 키를 사용 하는 보낸 사람에 게 공유 하 고 해당 보낸 것에 대해 HMAC를 계산 하는 비교 하 합니다. 이 비교 상수 시간 이어야 합니다. 그렇지 않으면 추가한 다음 또 다른 검색 가능한 oracle, 다른 유형의 공격을 허용 합니다.

요약 하자면, 사용할 블록 암호화 CBC을 안전 하 게 채워진, HMAC (또는 다른 데이터 무결성 검사) 시도 하기 전에 일정 시간 비교를 사용 하 여 데이터를 해독 하려면 유효성 검사를 사용 하 여 결합 해야 합니다. 모든 변경된 메시지 응답을 생성 하기 위해 동일한 시간을 걸릴, 있으므로 공격 방지 됩니다.

## <a name="who-is-vulnerable"></a>취약 한 사람은 누구 인가요

이 취약점으로 인이 한 고유한 암호화 및 암호 해독을 수행 하는 관리 및 네이티브 응용 프로그램에 적용 됩니다. 이 예를 들어:

- 서버에서 이상 암호 해독에 대 한 쿠키를 암호화 하는 응용 프로그램입니다.
- 열이 있는 테이블에 데이터를 삽입 하는 사용자에 대 한 기능을 제공 하는 데이터베이스 응용 프로그램을 나중에 암호 해독 됩니다.
- 공유 키를 사용 하 여 전송 중인 데이터를 보호 하기 위해 암호화를 사용 하는 데이터 전송 응용 프로그램입니다.
- 암호화 하 고 "내부" TLS 터널 메시지를 해독 하는 응용 프로그램입니다.

단독으로 TLS를 사용 하 여 수 보호 하지 이러한 시나리오에서 참고 합니다.

취약 한 응용 프로그램:

- CBC 암호화 모드를 사용 하 여 PKCS #7 ANSI X.923 등을 확인할 수 있는 패딩 모드를 사용 하 여 데이터를 해독 합니다.
- (MAC 또는 비대칭는 디지털 서명)를 통해 데이터 무결성 검사를 수행 하지 않고 암호 해독을 수행 합니다.

암호화 메시지 구문 (PKCS #7/CMS) EnvelopedData 구조와 같이 이러한 기본형 맨 위에 추상화를 기반으로 빌드된 응용 프로그램에도 적용 됩니다.

## <a name="related-areas-of-concern"></a>관련 된 영역의 문제

연구에 채워집니다. ISO 10126에 해당 하는 메시지에는 잘 알려진 또는 예측 가능한 바닥글 구조를 패딩 하는 CBC 메시지에 대 한 추가 문제는 그리 Microsoft 되었습니다. W3C XML 암호화 구문 및 처리 권장 사항 (xmlenc EncryptedXml)의 규칙에 따라 준비 된 콘텐츠 예입니다. 메시지에 서명 하 고 암호화 W3C 지침 것으로 간주 되 적절 한 시점에, 하는 동안 이제 권장 항상 다음 암호화-로그인을 수행 합니다.

비대칭 키와는 임의의 메시지 간에 내재 된 트러스트 관계가 없는 그대로 항상 응용 프로그램 개발자는 비대칭 서명 키를 적용할 수 있는지를 확인 하는 유의 해야 해야 합니다.

## <a name="details"></a>설명

지금까지 암호화 및 HMAC 또는 RSA 서명 같은 의미를 사용 하 여 중요 한 데이터를 인증 해야 하는 합의 되었습니다. 그러나 암호화 및 인증 작업을 시퀀싱 하는 방법에 대 한 명확한 지침 적은 되었습니다. 이 문서에 자세히 설명 된 취약점으로 인해 Microsoft의 지침이 되었습니다 항상 "암호화 후 서명할" 패러다임을 사용 합니다. 즉, 먼저 대칭 키를 사용 하 여 데이터를 암호화 한 다음 암호 텍스트 (암호화 된 데이터)를 통해 MAC 또는 비대칭 서명 계산 합니다. 데이터의 암호를 해독 하는 경우 반대를 수행 합니다. 먼저, MAC 또는 암호화 텍스트의 서명을 확인 다음 암호를 해독 합니다.

"Oracle 공격 패딩" 것으로 알려져 10 년에 대 한 알려진 취약점의 클래스입니다. 이 취약점 데이터 블록 마다 4096 개 이하로 시도 사용 하 여 AES 및 3DES와 같은 대칭 블록 알고리즘으로 암호화 된 데이터의 암호를 해독 하는 공격자가 있습니다. 이러한 취약성 확인 사용 하 여 암호화를 차단 하는 팩트의 끝에 패딩 검증할 수 있는 데이터를 사용 하 여 가장 자주 사용 됩니다. 공격자가 ciphertext를 사용 하 여 변조 여부 끝에 패딩 형식의 오류를 일으킨 변조 확인 수를 공격자가 데이터를 해독할 수 찾을 수 있습니다.

처음에 실제 공격 기반 서비스에서 반환 되는 패딩 ASP.NET 취약점으로 인 한 같은 유효한 했는지 여부에 따라 다른 오류 코드 [m s 10 070](/security-updates/SecurityBulletins/2010/ms10-070)합니다. 그러나 Microsoft만 유효 하 고 잘못 된 안쪽 여백 처리 타이밍의 차이 사용 하 여 비슷한 공격을 수행할 수는 이제 생각 합니다.

모든 정보를 내보내지 않고 데이터 무결성을 확인할 수는 암호화 체계를 사용 하 여 서명 및 서명 확인 (내용)와 관계 없이 데이터의 지정 된 길이 대 한 고정 런타임에 수행 되는 통해 공격자는 [쪽 채널](https://en.wikipedia.org/wiki/Side-channel_attack)합니다. 변조 된 모든 메시지를 거부 하는 무결성 검사, 이후 패딩 oracle 위협 완화 됩니다.

## <a name="guidance"></a>지침

무엇 보다도, 기밀성에 있는 모든 데이터 필요를 통해 보안 TLS (전송 계층), 보안 소켓 레이어 (SSL)를 후속 전송 될 것이 좋습니다.

다음으로, 응용 프로그램 분석:

- 수행 하는 어떤 암호화 정확 하 게 이해 하 고 플랫폼 및 Api를 사용 하는 제공 되는 암호화 키를 누릅니다.
- 대칭의 각 계층에서 각 사용 하는 특정 수 [블록 암호화 알고리즘](https://en.wikipedia.org/wiki/Block_cipher#Notable_block_ciphers)등 AES 및 3DES CBC 모드에서 비밀 키가 지정 된 데이터 무결성 검사를 사용 하 여 통합 (HMAC에는 비대칭 서명 또는 암호화 모드를 변경 하려면 [암호화 인증](https://en.wikipedia.org/wiki/Authenticated_encryption) GCM 등 CCM (AE) 모드).

현재 연구 결과 따라 일반적으로 믿고 AE 아닌 모드 암호화에 대 한 인증 및 암호화 단계를 독립적으로 수행 됩니다, 경우 인증 암호 텍스트 (암호화 후 서명할)는 가장 일반적인 옵션입니다. 그러나 암호화에는 없는 모든 상황에 맞는 올바른 답 하는이 일반화 전문 암호 조언 방향이 지정 된 것입니다.

완화와 같은 통합 하려고 메시징 형식으로 변경 하지만 인증 되지 않은 CBC 암호 해독을 수행 하는 일을 할 수 없는 응용 프로그램을 사용 하는 것이 좋습니다.

- 확인 하거나 패딩 제거 하려면 암호 해독기를 허용 하지 않고 암호 해독:
  - 적용 된 모든 패딩 제거 하거나 무시 해야, 응용 프로그램에 부담을 이동 하는 합니다.
  - 장점은 다른 응용 프로그램 데이터 확인 논리에 안쪽 여백 확인 및 제거를 통합할 수 있습니다. 일정 한 시간에 안쪽 여백 확인 및 데이터 확인을 수행할 수 있습니다, 위협이 줄어듭니다.
  - 안쪽 여백의 해석은 인식된 메시지 길이 변경 하므로이 접근 방식에서 발생 하는 타이밍 정보 수 여전히 있습니다.
- ISO10126를 암호 해독 된 패딩 모드를 변경 합니다.
  - ISO10126 암호 해독 안쪽 여백은 PKCS7 암호화 패딩입니다와 ANSIX923 암호화 패딩입니다 호환입니다.
  - 모드를 변경 하면이 패딩 oracle 기술을 전체 블록 대신 1 바이트를 줄입니다. 그러나 콘텐츠는 닫기 XML 요소와 같은 잘 알려진 바닥글에 관련된 공격 계속 메시지의 나머지 부분을 공격할 수 있습니다.
  - 또한이 공격자가 다양 한 메시지 오프셋을 사용 하 여 여러 번 암호화 같은 일반 텍스트 강제 변환할 수 있는 상황에서 일반 텍스트 복구를 방지 하지 않습니다.
- 게이트 평가에 대 한 암호 해독 호출 타이밍 신호를 완화 합니다.
  - 보류 시간 계산에 안쪽 여백을 포함 하는 모든 데이터 세그먼트에 대 한 암호 해독 작업 걸리는 시간의 최대 크기를 초과 하는 최소가 있어야 합니다.
  - 지침에 따라 시간 계산을 수행 해야 [고해상도 타임 스탬프를 획득](/windows/desktop/sysinfo/acquiring-high-resolution-time-stamps)를 사용 하 여 <xref:System.Environment.TickCount?displayProperty=nameWithType> (오버플로) 롤포워드-조치 될 수 있습니다 (NTP 조정에 따라 두 가지 시스템 타임 스탬프를 뺀 또는 오류)입니다.
  - 시간 계산의 모든 잠재적 예외를 포함 하 여 암호 해독 작업을 포함 하 여 관리 해야 하거나 C++ 응용 프로그램 뿐 아니라 끝에 패딩 합니다.
  - 성공 또는 실패 확인 된 경우에 아직, 타이밍 성문 만료 되 면 오류를 반환 해야 합니다.
- 인증 되지 않은 암호 해독을 수행 하는 서비스에에서 모니터링을 통해 대량의 "잘못 된" 메시지에 올라오는 검색할 설정 해야 합니다.
  - 이 신호는 거짓 긍정 (합법적인 방식으로 손상 된 데이터) 및 거짓 부정 (검색을 피할 충분히 긴 시간이 지남에 따라 공격 확산)는 것을 염두에 두십시오.

## <a name="finding-vulnerable-code---native-applications"></a>취약 한 코드-네이티브 응용 프로그램 찾기

Windows 암호화에 대해 빌드된 프로그램: 다음 세대 (CNG) 라이브러리:

- 암호 해독 호출 하는 것 [BCryptDecrypt](/windows/desktop/api/bcrypt/nf-bcrypt-bcryptdecrypt)을 지정 하 고는 `BCRYPT_BLOCK_PADDING` 플래그입니다.
- 키 핸들을 호출 하 여 활성화 되었습니다 [BCryptSetProperty](/windows/desktop/api/bcrypt/nf-bcrypt-bcryptsetproperty) 사용 하 여 [BCRYPT_CHAINING_MODE](/windows/desktop/SecCNG/cng-property-identifiers#BCRYPT_CHAINING_MODE) 로 `BCRYPT_CHAIN_MODE_CBC`합니다.
  - 이후 `BCRYPT_CHAIN_MODE_CBC` 기본값인 영향을 받는 코드에 대 한 값 할당 하지 `BCRYPT_CHAINING_MODE`합니다.

이전 Windows 암호화 API에 대해 빌드된 프로그램:

- 암호 해독 호출 하는 것 [CryptDecrypt](/windows/desktop/api/wincrypt/nf-wincrypt-cryptdecrypt) 사용 하 여 `Final=TRUE`입니다.
- 키 핸들을 호출 하 여 활성화 되었습니다 [CryptSetKeyParam](/windows/desktop/api/wincrypt/nf-wincrypt-cryptsetkeyparam) 사용 하 여 [KP_MODE](/windows/desktop/api/wincrypt/nf-wincrypt-cryptgetkeyparam) 로 `CRYPT_MODE_CBC`합니다.
  - 이후 `CRYPT_MODE_CBC` 기본값인 영향을 받는 코드에 대 한 값 할당 하지 `KP_MODE`합니다.

## <a name="finding-vulnerable-code---managed-applications"></a>취약 한 코드 찾기-관리 되는 응용 프로그램

- 암호 해독 호출 하는 것은 <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor> 또는 <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor(System.Byte[],System.Byte[])> 메서드를 <xref:System.Security.Cryptography.SymmetricAlgorithm?displayProperty=nameWithType>입니다.
  - 이.NET 내의 다음 파생된 형식을 포함 하지만 타사 형식을 포함할 수도 있습니다.
    - <xref:System.Security.Cryptography.Aes>
    - <xref:System.Security.Cryptography.AesCng>
    - <xref:System.Security.Cryptography.AesCryptoServiceProvider>
    - <xref:System.Security.Cryptography.AesManaged>
    - <xref:System.Security.Cryptography.DES>
    - <xref:System.Security.Cryptography.DESCryptoServiceProvider>
    - <xref:System.Security.Cryptography.RC2>
    - <xref:System.Security.Cryptography.RC2CryptoServiceProvider>
    - <xref:System.Security.Cryptography.Rijndael>
    - <xref:System.Security.Cryptography.RijndaelManaged>
    - <xref:System.Security.Cryptography.TripleDES>
    - <xref:System.Security.Cryptography.TripleDESCng>
    - <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Padding?displayProperty=nameWithType> 속성 설정한 <xref:System.Security.Cryptography.PaddingMode.PKCS7?displayProperty=nameWithType>, <xref:System.Security.Cryptography.PaddingMode.ANSIX923?displayProperty=nameWithType>, 또는 <xref:System.Security.Cryptography.PaddingMode.ISO10126?displayProperty=nameWithType>합니다.
  - 이후 <xref:System.Security.Cryptography.PaddingMode.PKCS7?displayProperty=nameWithType> 기본값인 영향을 받는 코드 할당 되지 않을 수 있습니다는 <xref:System.Security.Cryptography.SymmetricAlgorithm.Padding?displayProperty=nameWithType> 속성입니다.
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Mode?displayProperty=nameWithType> 속성이로 설정 된 <xref:System.Security.Cryptography.CipherMode.CBC?displayProperty=nameWithType>
  - 이후 <xref:System.Security.Cryptography.CipherMode.CBC?displayProperty=nameWithType> 기본값인 영향을 받는 코드 할당 되지 않을 수 있습니다는 <xref:System.Security.Cryptography.SymmetricAlgorithm.Mode?displayProperty=nameWithType> 속성입니다.

## <a name="finding-vulnerable-code---cryptographic-message-syntax"></a>암호화 메시지 구문 취약 한 코드 찾기

암호화 된 내용이 AES (2.16.840.1.101.3.4.1.2, 2.16.840.1.101.3.4.1.22 2.16.840.1.101.3.4.1.42), DES (1.3.14.3.2.7), 3DES CBC 모드를 사용 하는 인증 되지 않은 CMS EnvelopedData 메시지 (1.2.840.113549.3.7) 또는 RC2 (1.2.840.113549.3.2)은 취약 한도 메시지를 다른 블록 암호화 알고리즘을 사용 하 여 CBC 모드에서 합니다.

이 문제에 취약 스트림 암호화 하지 않음, 하는 동안 항상 ContentEncryptionAlgorithm 값 검사를 통해 데이터를 인증 하는 것이 좋습니다.

Blob 수를 CMS EnvelopedData 관리 되는 응용 프로그램에 전달 되는 모든 값을 검색 <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.Decode(System.Byte[])?displayProperty=fullName>합니다.

네이티브 응용 프로그램에 대 한 CMS EnvelopedData blob을 통해 CMS 핸들에 지정 된 값으로 검색 수 [CryptMsgUpdate](/windows/desktop/api/wincrypt/nf-wincrypt-cryptmsgupdate) 인 결과 [CMSG_TYPE_PARAM](/windows/desktop/api/wincrypt/nf-wincrypt-cryptmsggetparam) 는 `CMSG_ENVELOPED` CMS 핸들이 및/또는 나중에 전송 되는 `CMSG_CTRL_DECRYPT` 명령을 통해 [CryptMsgControl](/windows/desktop/api/wincrypt/nf-wincrypt-cryptmsgcontrol)합니다.

## <a name="vulnerable-code-example---managed"></a>취약 한 코드 예제에서는-관리

이 메서드는 쿠키를 읽고 해독 하 고 데이터 무결성 검사 안 함이 표시 됩니다. 따라서이 방법으로 읽을 수 있는 쿠키의 내용이 받은 사용자가 또는 모든 공격자가 암호화 된 쿠키 값을 획득 하는 공격 받을 수입니다.

```csharp
private byte[] DecryptCookie(string cookieName)
{
    HttpCookie cookie = Request.Cookies[cookieName];

    if (cookie == null)
    {
        return null;
    }

    using (ICryptoTransform decryptor = _aes.CreateDecryptor())
    using (MemoryStream memoryStream = new MemoryStream())
    using (CryptoStream cryptoStream =
        new CryptoStream(memoryStream, decryptor, CryptoStreamMode.Write))
    {
        byte[] readCookie = Convert.FromBase64String(cookie.Value);
        cryptoStream.Write(readCookie, 0, readCookie.Length);
        cryptoStream.FlushFinalBlock();
        return memoryStream.ToArray();
    }
}
```

## <a name="example-code-following-recommended-practices---managed"></a>다음 코드 예에서는 권장 되는 정보-관리

다음 샘플 코드의 비표준 메시지 형식을 사용합니다

`cipher_algorithm_id || hmac_algorithm_id || hmac_tag || iv || ciphertext`

여기서는 `cipher_algorithm_id` 및 `hmac_algorithm_id` 알고리즘 식별자는 해당 알고리즘의 응용 프로그램 지역 (비표준) 표현입니다. 이러한 식별자는 완전 연결된 bytestream으로 대신 기존 메시징 프로토콜의 다른 부분에서 의미를 만들 수 있습니다.

또한이 예제에서는 HMAC 키와 암호화 키를 파생 시키는 단일 마스터 키를 사용 합니다. 두 키와 다른 값을 유지 하는 것이 좋습니다에 이중 키가 지정 된 응용 프로그램에 단일 키가 지정 된 응용 프로그램 설정에 대 한 편의 기능으로 제공 됩니다. 추가 동기화 HMAC 키 및 암호화 키를 가져올 수 없습니다 보장 합니다.

이 샘플에 맞지는 <xref:System.IO.Stream> 암호화 또는 암호 해독 합니다. 현재 데이터 형식을 사용 하면 단일 패스 어려운 암호화 때문에 `hmac_tag` 값 텍스트 앞에 옵니다. 그러나이 형식은 파서가 보다 간단 하 게 시작할 모든 고정 크기 요소를 유지 하기 때문에 선택 되었습니다. 이 데이터 형식을 사용 하 여 GetHashAndReset 호출 TransformFinalBlock를 호출 하기 전에 결과 확인 하는 구현자는 주의가 요구 하지만 단일 패스 해독이 가능 합니다. 스트리밍 암호화 중요 한 경우 다른 AE 모드로 필요할 수 있습니다.

```csharp
// ==++==
//
//   Copyright (c) Microsoft Corporation.  All rights reserved.
//
//   Shared under the terms of the Microsoft Public License,
//   https://opensource.org/licenses/MS-PL
//
// ==--==

using System;
using System.Diagnostics;
using System.IO;
using System.Runtime.CompilerServices;
using System.Security.Cryptography;

namespace Microsoft.Examples.Cryptography
{
    public enum AeCipher : byte
    {
        Unknown,
        Aes256CbcPkcs7,
    }

    public enum AeMac : byte
    {
        Unknown,
        HMACSHA256,
        HMACSHA384,
    }

    /// <summary>
    /// Provides extension methods to make HashAlgorithm look like .NET Core's
    /// IncrementalHash
    /// </summary>
    internal static class IncrementalHashExtensions
    {
        public static void AppendData(this HashAlgorithm hash, byte[] data)
        {
            hash.TransformBlock(data, 0, data.Length, null, 0);
        }

        public static void AppendData(
            this HashAlgorithm hash,
            byte[] data,
            int offset,
            int length)
        {
            hash.TransformBlock(data, offset, length, null, 0);
        }

        public static byte[] GetHashAndReset(this HashAlgorithm hash)
        {
            hash.TransformFinalBlock(Array.Empty<byte>(), 0, 0);
            return hash.Hash;
        }
    }

    public static partial class AuthenticatedEncryption
    {
        /// <summary>
        /// Use <paramref name="masterKey"/> to derive two keys (one cipher, one HMAC)
        /// to provide authenticated encryption for <paramref name="message"/>.
        /// </summary>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <param name="message">The message to encrypt</param>
        /// <returns>
        /// A concatenation of
        /// [cipher algorithm+chainmode+padding][mac algorithm][authtag][IV][ciphertext],
        /// suitable to be passed to <see cref="Decrypt"/>.
        /// </returns>
        /// <remarks>
        /// <paramref name="masterKey"/> should be a 128-bit (or bigger) value generated
        /// by a secure random number generator, such as the one returned from
        /// <see cref="RandomNumberGenerator.Create()"/>.
        /// This implementation chooses to block deficient inputs by length, but does not
        /// make any attempt at discerning the randomness of the key.
        ///
        /// If the master key is being input by a prompt (like a password/passphrase)
        /// then it should be properly turned into keying material via a Key Derivation
        /// Function like PBKDF2, represented by Rfc2898DeriveBytes. A 'password' should
        /// never be simply turned to bytes via an Encoding class and used as a key.
        /// </remarks>
        public static byte[] Encrypt(byte[] masterKey, byte[] message)
        {
            if (masterKey == null)
                throw new ArgumentNullException(nameof(masterKey));
            if (masterKey.Length < 16)
                throw new ArgumentOutOfRangeException(
                    nameof(masterKey),
                    "Master Key must be at least 128 bits (16 bytes)");
            if (message == null)
                throw new ArgumentNullException(nameof(message));

            // First, choose an encryption scheme.
            AeCipher aeCipher = AeCipher.Aes256CbcPkcs7;

            // Second, choose an authentication (message integrity) scheme.
            //
            // In this example we use the master key length to change from HMACSHA256 to
            // HMACSHA384, but that is completely arbitrary. This mostly represents a
            // "cryptographic needs change over time" scenario.
            AeMac aeMac = masterKey.Length < 48 ? AeMac.HMACSHA256 : AeMac.HMACSHA384;

            // It's good to be able to identify what choices were made when a message was
            // encrypted, so that the message can later be decrypted. This allows for
            // future versions to add support for new encryption schemes, but still be
            // able to read old data. A practice known as "cryptographic agility".
            //
            // This is similar in practice to PKCS#7 messaging, but this uses a
            // private-scoped byte rather than a public-scoped Object IDentifier (OID).
            // Please note that the scheme in this example adheres to no particular
            // standard, and is unlikely to survive to a more complete implementation in
            // the .NET Framework.
            //
            // You may be well-served by prepending a version number byte to this
            // message, but may want to avoid the value 0x30 (the leading byte value for
            // DER-encoded structures such as X.509 certificates and PKCS#7 messages).
            byte[] algorithmChoices = { (byte)aeCipher, (byte)aeMac };
            byte[] iv;
            byte[] cipherText;
            byte[] tag;

            // Using our algorithm choices, open an HMAC (as an authentication tag
            // generator) and a SymmetricAlgorithm which use different keys each derived
            // from the same master key.
            //
            // A custom implementation may very well have distinctly managed secret keys
            // for the MAC and cipher, this example merely demonstrates the master to
            // derived key methodology to encourage key separation from the MAC and
            // cipher keys.
            using (HMAC tagGenerator = GetMac(aeMac, masterKey))
            {
                using (SymmetricAlgorithm cipher = GetCipher(aeCipher, masterKey))
                using (ICryptoTransform encryptor = cipher.CreateEncryptor())
                {
                    // Since no IV was provided, a random one has been generated
                    // during the call to CreateEncryptor.
                    //
                    // But note that it only does the auto-generation once. If the cipher
                    // object were used again, a call to GenerateIV would have been
                    // required.
                    iv = cipher.IV;

                    cipherText = Transform(encryptor, message, 0, message.Length);
                }

                // The IV and ciphertest both need to be included in the MAC to prevent
                // tampering.
                //
                // By including the algorithm identifiers, we have technically moved from
                // simple Authenticated Encryption (AE) to Authenticated Encryption with
                // Additional Data (AEAD). By including the algorithm identifiers in the
                // MAC, it becomes harder for an attacker to change them as an attempt to
                // perform a downgrade attack.
                //
                // If you've added a data format version field, it can also be included
                // in the MAC to further inhibit an attacker's options for confusing the
                // data processor into believing the tampered message is valid.
                tagGenerator.AppendData(algorithmChoices);
                tagGenerator.AppendData(iv);
                tagGenerator.AppendData(cipherText);
                tag = tagGenerator.GetHashAndReset();
            }

            // Build the final result as the concatenation of everything except the keys.
            int totalLength =
                algorithmChoices.Length +
                tag.Length +
                iv.Length +
                cipherText.Length;

            byte[] output = new byte[totalLength];
            int outputOffset = 0;

            Append(algorithmChoices, output, ref outputOffset);
            Append(tag, output, ref outputOffset);
            Append(iv, output, ref outputOffset);
            Append(cipherText, output, ref outputOffset);

            Debug.Assert(outputOffset == output.Length);
            return output;
        }

        /// <summary>
        /// Reads a message produced by <see cref="Encrypt"/> after verifying it hasn't
        /// been tampered with.
        /// </summary>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <param name="cipherText">
        /// The output of <see cref="Encrypt"/>: a concatenation of a cipher ID, mac ID,
        /// authTag, IV, and cipherText.
        /// </param>
        /// <returns>The decrypted content.</returns>
        /// <exception cref="ArgumentNullException">
        /// <paramref name="masterKey"/> is <c>null</c>.
        /// </exception>
        /// <exception cref="ArgumentNullException">
        /// <paramref name="cipherText"/> is <c>null</c>.
        /// </exception>
        /// <exception cref="CryptographicException">
        /// <paramref name="cipherText"/> identifies unknown algorithms, is not long
        /// enough, fails a data integrity check, or fails to decrypt.
        /// </exception>
        /// <remarks>
        /// <paramref name="masterKey"/> should be a 128-bit (or larger) value
        /// generated by a secure random number generator, such as the one returned from
        /// <see cref="RandomNumberGenerator.Create()"/>. This implementation chooses to
        /// block deficient inputs by length, but doesn't make any attempt at
        /// discerning the randomness of the key.
        ///
        /// If the master key is being input by a prompt (like a password/passphrase),
        /// then it should be properly turned into keying material via a Key Derivation
        /// Function like PBKDF2, represented by Rfc2898DeriveBytes. A 'password' should
        /// never be simply turned to bytes via an Encoding class and used as a key.
        /// </remarks>
        public static byte[] Decrypt(byte[] masterKey, byte[] cipherText)
        {
            // This example continues the .NET practice of throwing exceptions for
            // failures. If you consider message tampering to be normal (and thus
            // "not exceptional") behavior, you may like the signature
            // bool Decrypt(byte[] messageKey, byte[] cipherText, out byte[] message)
            // better.
            if (masterKey == null)
                throw new ArgumentNullException(nameof(masterKey));
            if (masterKey.Length < 16)
                throw new ArgumentOutOfRangeException(
                    nameof(masterKey),
                    "Master Key must be at least 128 bits (16 bytes)");
            if (cipherText == null)
                throw new ArgumentNullException(nameof(cipherText));

            // The format of this message is assumed to be public, so there's no harm in
            // saying ahead of time that the message makes no sense.
            if (cipherText.Length < 2)
            {
                throw new CryptographicException();
            }

            // Use the message algorithm headers to determine what cipher algorithm and
            // MAC algorithm are going to be used. Since the same Key Derivation
            // Functions (KDFs) are being used in Decrypt as Encrypt, the keys are also
            // the same.
            AeCipher aeCipher = (AeCipher)cipherText[0];
            AeMac aeMac = (AeMac)cipherText[1];

            using (SymmetricAlgorithm cipher = GetCipher(aeCipher, masterKey))
            using (HMAC tagGenerator = GetMac(aeMac, masterKey))
            {
                int blockSizeInBytes = cipher.BlockSize / 8;
                int tagSizeInBytes = tagGenerator.HashSize / 8;
                int headerSizeInBytes = 2;
                int tagOffset = headerSizeInBytes;
                int ivOffset = tagOffset + tagSizeInBytes;
                int cipherTextOffset = ivOffset + blockSizeInBytes;
                int cipherTextLength = cipherText.Length - cipherTextOffset;
                int minLen = cipherTextOffset + blockSizeInBytes;

                // Again, the minimum length is still assumed to be public knowledge,
                // nothing has leaked out yet. The minimum length couldn't just be calculated
                // without reading the header.
                if (cipherText.Length < minLen)
                {
                    throw new CryptographicException();
                }

                // It's very important that the MAC be calculated and verified before
                // proceeding to decrypt the ciphertext, as this prevents any sort of
                // information leaking out to an attacker.
                //
                // Don't include the tag in the calculation, though.

                // First, everything before the tag (the cipher and MAC algorithm ids)
                tagGenerator.AppendData(cipherText, 0, tagOffset);

                // Skip the data before the tag and the tag, then read everything that
                // remains.
                tagGenerator.AppendData(
                    cipherText,
                    tagOffset + tagSizeInBytes,
                    cipherText.Length - tagSizeInBytes - tagOffset);

                byte[] generatedTag = tagGenerator.GetHashAndReset();

                // The time it took to get to this point has so far been a function only
                // of the length of the data, or of non-encrypted values (e.g. it could
                // take longer to prepare the *key* for the HMACSHA384 MAC than the
                // HMACSHA256 MAC, but the algorithm choice wasn't a secret).
                //
                // If the verification of the authentication tag aborts as soon as a
                // difference is found in the byte arrays then your program may be
                // acting as a timing oracle which helps an attacker to brute-force the
                // right answer for the MAC. So, it's very important that every possible
                // "no" (2^256-1 of them for HMACSHA256) be evaluated in as close to the
                // same amount of time as possible. For this, we call CryptographicEquals
                if (!CryptographicEquals(
                    generatedTag,
                    0,
                    cipherText,
                    tagOffset,
                    tagSizeInBytes))
                {
                    // Assuming every tampered message (of the same length) took the same
                    // amount of time to process, we can now safely say
                    // "this data makes no sense" without giving anything away.
                    throw new CryptographicException();
                }

                // Restore the IV into the symmetricAlgorithm instance.
                byte[] iv = new byte[blockSizeInBytes];
                Buffer.BlockCopy(cipherText, ivOffset, iv, 0, iv.Length);
                cipher.IV = iv;

                using (ICryptoTransform decryptor = cipher.CreateDecryptor())
                {
                    return Transform(
                        decryptor,
                        cipherText,
                        cipherTextOffset,
                        cipherTextLength);
                }
            }
        }

        private static byte[] Transform(
            ICryptoTransform transform,
            byte[] input,
            int inputOffset,
            int inputLength)
        {
            // Many of the implementations of ICryptoTransform report true for
            // CanTransformMultipleBlocks, and when the entire message is available in
            // one shot this saves on the allocation of the CryptoStream and the
            // intermediate structures it needs to properly chunk the message into blocks
            // (since the underlying stream won't always return the number of bytes
            // needed).
            if (transform.CanTransformMultipleBlocks)
            {
                return transform.TransformFinalBlock(input, inputOffset, inputLength);
            }

            // If our transform couldn't do multiple blocks at once, let CryptoStream
            // handle the chunking.
            using (MemoryStream messageStream = new MemoryStream())
            using (CryptoStream cryptoStream =
                new CryptoStream(messageStream, transform, CryptoStreamMode.Write))
            {
                cryptoStream.Write(input, inputOffset, inputLength);
                cryptoStream.FlushFinalBlock();
                return messageStream.ToArray();
            }
        }

        /// <summary>
        /// Open a properly configured <see cref="SymmetricAlgorithm"/> conforming to the
        /// scheme identified by <paramref name="aeCipher"/>.
        /// </summary>
        /// <param name="aeCipher">The cipher mode to open.</param>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <returns>
        /// A SymmetricAlgorithm object with the right key, cipher mode, and padding
        /// mode; or <c>null</c> on unknown algorithms.
        /// </returns>
        private static SymmetricAlgorithm GetCipher(AeCipher aeCipher, byte[] masterKey)
        {
            SymmetricAlgorithm symmetricAlgorithm;

            switch (aeCipher)
            {
                case AeCipher.Aes256CbcPkcs7:
                    symmetricAlgorithm = Aes.Create();
                    // While 256-bit, CBC, and PKCS7 are all the default values for these
                    // properties, being explicit helps comprehension more than it hurts
                    // performance.
                    symmetricAlgorithm.KeySize = 256;
                    symmetricAlgorithm.Mode = CipherMode.CBC;
                    symmetricAlgorithm.Padding = PaddingMode.PKCS7;
                    break;
                default:
                    // An algorithm we don't understand
                    throw new CryptographicException();
            }

            // Instead of using the master key directly, derive a key for our chosen
            // HMAC algorithm based upon the master key.
            //
            // Since none of the symmetric encryption algorithms currently in .NET
            // support key sizes greater than 256-bit, we can use HMACSHA256 with
            // NIST SP 800-108 5.1 (Counter Mode KDF) to derive a value that is
            // no smaller than the key size, then Array.Resize to trim it down as
            // needed.

            using (HMAC hmac = new HMACSHA256(masterKey))
            {
                // i=1, Label=ASCII(cipher)
                byte[] cipherKey = hmac.ComputeHash(
                    new byte[] { 1, 99, 105, 112, 104, 101, 114 });

                // Resize the array to the desired keysize. KeySize is in bits,
                // and Array.Resize wants the length in bytes.
                Array.Resize(ref cipherKey, symmetricAlgorithm.KeySize / 8);

                symmetricAlgorithm.Key = cipherKey;
            }

            return symmetricAlgorithm;
        }

        /// <summary>
        /// Open a properly configured <see cref="HMAC"/> conforming to the scheme
        /// identified by <paramref name="aeMac"/>.
        /// </summary>
        /// <param name="aeMac">The message authentication mode to open.</param>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <returns>
        /// An HMAC object with the proper key, or <c>null</c> on unknown algorithms.
        /// </returns>
        private static HMAC GetMac(AeMac aeMac, byte[] masterKey)
        {
            HMAC hmac;

            switch (aeMac)
            {
                case AeMac.HMACSHA256:
                    hmac = new HMACSHA256();
                    break;
                case AeMac.HMACSHA384:
                    hmac = new HMACSHA384();
                    break;
                default:
                    // An algorithm we don't understand
                    throw new CryptographicException();
            }

            // Instead of using the master key directly, derive a key for our chosen
            // HMAC algorithm based upon the master key.
            // Since the output size of the HMAC is the same as the ideal key size for
            // the HMAC, we can use the master key over a fixed input once to perform
            // NIST SP 800-108 5.1 (Counter Mode KDF):
            hmac.Key = masterKey;

            // i=1, Context=ASCII(MAC)
            byte[] newKey = hmac.ComputeHash(new byte[] { 1, 77, 65, 67 });

            hmac.Key = newKey;
            return hmac;
        }

        // A simple helper method to ensure that the offset (writePos) always moves
        // forward with new data.
        private static void Append(byte[] newData, byte[] combinedData, ref int writePos)
        {
            Buffer.BlockCopy(newData, 0, combinedData, writePos, newData.Length);
            writePos += newData.Length;
        }

        /// <summary>
        /// Compare the contents of two arrays in an amount of time which is only
        /// dependent on <paramref name="length"/>.
        /// </summary>
        /// <param name="a">An array to compare to <paramref name="b"/>.</param>
        /// <param name="aOffset">
        /// The starting position within <paramref name="a"/> for comparison.
        /// </param>
        /// <param name="b">An array to compare to <paramref name="a"/>.</param>
        /// <param name="bOffset">
        /// The starting position within <paramref name="b"/> for comparison.
        /// </param>
        /// <param name="length">
        /// The number of bytes to compare between <paramref name="a"/> and
        /// <paramref name="b"/>.</param>
        /// <returns>
        /// <c>true</c> if both <paramref name="a"/> and <paramref name="b"/> have
        /// sufficient length for the comparison and all of the applicable values are the
        /// same in both arrays; <c>false</c> otherwise.
        /// </returns>
        /// <remarks>
        /// An "insufficient data" <c>false</c> response can happen early, but otherwise
        /// a <c>true</c> or <c>false</c> response take the same amount of time.
        /// </remarks>
        [MethodImpl(MethodImplOptions.NoInlining | MethodImplOptions.NoOptimization)]
        private static bool CryptographicEquals(
            byte[] a,
            int aOffset,
            byte[] b,
            int bOffset,
            int length)
        {
            Debug.Assert(a != null);
            Debug.Assert(b != null);
            Debug.Assert(length >= 0);

            int result = 0;

            if (a.Length - aOffset < length || b.Length - bOffset < length)
            {
                return false;
            }

            unchecked
            {
                for (int i = 0; i < length; i++)
                {
                    // Bitwise-OR of subtraction has been found to have the most
                    // stable execution time.
                    //
                    // This cannot overflow because bytes are 1 byte in length, and
                    // result is 4 bytes.
                    // The OR propagates all set bytes, so the differences are only
                    // present in the lowest byte.
                    result = result | (a[i + aOffset] - b[i + bOffset]);
                }
            }

            return result == 0;
        }
    }
}
```
