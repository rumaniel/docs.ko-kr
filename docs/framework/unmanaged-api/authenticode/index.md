---
title: Authenticode(관리되지 않는 API 참조)
ms.date: 03/30/2017
ms.assetid: 7e8cc303-6e77-4116-aa8b-7ea297a3a467
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d2c0163d03a19a7bc00ae705fd633ef4f0880082
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70776561"
---
# <a name="authenticode-unmanaged-api-reference"></a>Authenticode(관리되지 않는 API 참조)
Authenticode XrML 라이센스 만들기 및 확인 모듈을 지원합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [_AxlGetIssuerPublicKeyHash 함수](axlgetissuerpublickeyhash-function.md)  
 지정한 인증서에 서명하는 데 사용되는 프라이빗 키에 연결된 퍼블릭 키의 SHA-1 해시를 검색합니다.  
  
 [_AxlPublicKeyBlobToPublicKeyToken 함수](axlpublickeyblobtopublickeytoken-function.md)  
 CSP PUBLICKEYBLOB 형식에서 강력한 이름 공개 키 토큰을 계산합니다.  
  
 [_AxlRSAKeyValueToPublicKeyToken 함수](axlrsakeyvaluetopublickeytoken-function.md)  
 모듈러스 및 지수를 강력한 이름 공개 키 토큰으로 변환합니다.  
  
 [CertFreeAuthenticodeSignerInfo 함수](certfreeauthenticodesignerinfo-function.md)  
 AXL_AUTHENTICODE_SIGNER_INFO 구조체에 할당된 리소스를 해제합니다.  
  
 [CertFreeAuthenticodeTimestamperInfo 함수](certfreeauthenticodetimestamperinfo-function.md)  
 AXL_AUTHENTICODE_TIMESTAMPER_INFO 구조체에 할당된 리소스를 해제합니다.  
  
 [CertTimestampAuthenticodeLicense 함수](certtimestampauthenticodelicense-function.md)  
 CertCreateAuthenticodeLicense에 의해 작성된 Authenticode XrML 라이선스에 타임스탬프를 적용합니다.  
  
 [CertVerifyAuthenticodeLicense 함수](certverifyauthenticodelicense-function.md)  
 Authenticode XrML 라이선스의 유효성을 확인합니다.  
  
 [AXL_AUTHENTICODE_SIGNER_INFO 구조체](axl-authenticode-signer-info-structure.md)  
 Authenticode 서명자 정보를 정의합니다.  
  
 [AXL_AUTHENTICODE_TIMESTAMPER_INFO 구조체](axl-authenticode-timestamper-info-structure.md)  
 Authenticode 타임스탬퍼 정보를 정의합니다.  
  
## <a name="see-also"></a>참고 항목

- [관리되지 않는 API 참조](../index.md)
