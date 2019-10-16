---
title: ICLRStrongName 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRStrongName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName
helpviewer_keywords:
- ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 2fac66fd-6b3b-4dbd-8baf-86038bd85526
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: abe967195694dd61b4af18fb4eebbc3caad2ef4f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771477"
---
# <a name="iclrstrongname-interface"></a>ICLRStrongName 인터페이스
강력한 이름의 어셈블리를 서명 하는 기본 전역 정적 함수를 제공 합니다. 모든 `ICLRStrongName` 메서드는 표준 COM HRESULTs를 반환 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetHashFromAssemblyFile 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromassemblyfile-method.md)|지정된 해시 알고리즘을 사용하여 지정된 어셈블리 파일의 해시를 가져옵니다.|  
|[GetHashFromAssemblyFileW 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromassemblyfilew-method.md)|지정된 해시 알고리즘을 사용하여 유니코드 문자열로 지정된 어셈블리 파일의 해시를 가져옵니다.|  
|[GetHashFromBlob 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromblob-method.md)|지정된 해시 알고리즘을 사용하여 지정된 메모리 주소에 있는 어셈블리의 해시를 가져옵니다.|  
|[GetHashFromFile 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromfile-method.md)|지정된 파일 내용에 대해 해시를 생성합니다.|  
|[GetHashFromFileW 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromfilew-method.md)|유니코드 문자열로 지정된 파일 내용에 대해 해시를 생성합니다.|  
|[GetHashFromHandle 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromhandle-method.md)|지정된 해시 알고리즘을 사용하여 지정된 파일 핸들로 파일 내용에 대해 해시를 생성합니다.|  
|[StrongNameCompareAssemblies 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamecompareassemblies-method.md)|두 어셈블리가 강력한 이름 서명에 의해서만 다른지 여부를 결정합니다.|  
|[StrongNameFreeBuffer 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md)|와 같은 강력한 이름의 메서드에 대 한 이전 호출을 사용 하 여 할당 된 메모리를 해제 [StrongNameGetPublicKey](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetpublickey-method.md)하십시오 [StrongNameTokenFromPublicKey](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfrompublickey-method.md), 또는 [StrongNameSignatureGeneration ](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegeneration-method.md).|  
|[StrongNameGetBlob 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblob-method.md)|지정된 주소에 있는 실행 파일의 이진 표현으로 지정된 버퍼를 채웁니다.|  
|[StrongNameGetBlobFromImage 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblobfromimage-method.md)|지정된 메모리 주소에 있는 어셈블리 이미지의 이진 표현을 가져옵니다.|  
|[StrongNameGetPublicKey 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetpublickey-method.md)|퍼블릭/퍼블릭 키 쌍에서 퍼블릭 키를 가져옵니다.|  
|[StrongNameHashSize 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamehashsize-method.md)|지정된 해시 알고리즘을 사용하여 해시에 필요한 버퍼 크기를 가져옵니다.|  
|[StrongNameKeyDelete 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeydelete-method.md)|지정된 키 컨테이너를 삭제합니다.|  
|[StrongNameKeyGen 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeygen-method.md)|강력한 이름 사용을 위한 새 퍼블릭/프라이빗 키 쌍을 만듭니다.|  
|[StrongNameKeyGenEx 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeygenex-method.md)|강력한 이름 사용을 위해 지정된 키 크기로 새 퍼블릭/프라이빗 키 쌍을 생성합니다.|  
|[StrongNameKeyInstall 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeyinstall-method.md)|퍼블릭/프라이빗 키 쌍을 컨테이너로 가져옵니다.|  
|[StrongNameSignatureGeneration 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegeneration-method.md)|지정된 어셈블리에 대한 강력한 이름 서명을 생성합니다.|  
|[StrongNameSignatureGenerationEx 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegenerationex-method.md)|지정된 플래그에 따라 지정된 어셈블리에 대한 강력한 이름 서명을 생성합니다.|  
|[StrongNameSignatureSize 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturesize-method.md)|강력한 이름 서명의 크기를 반환합니다.|  
|[StrongNameSignatureVerification 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignatureverification-method.md)|제공된 경로의 어셈블리 매니페스트에 지정된 플래그에 따라 확인되는 강력한 이름 서명이 포함되는지 여부를 나타내는 값을 가져옵니다.|  
|[StrongNameSignatureVerificationEx 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignatureverificationex-method.md)|제공된 경로의 어셈블리 매니페스트에 강력한 이름 서명이 포함되는지 여부를 나타내는 값을 가져옵니다.|  
|[StrongNameSignatureVerificationFromImage 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignatureverificationfromimage-method.md)|메모리에 이미 매핑된 어셈블리가 연결된 공개 키에 유효한지 확인합니다.|  
|[StrongNameTokenFromAssembly 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfromassembly-method.md)|지정된 어셈블리 파일에서 강력한 이름 토큰을 만듭니다.|  
|[StrongNameTokenFromAssemblyEx 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfromassemblyex-method.md)|지정된 어셈블리 파일에서 강력한 이름 토큰을 만들고 공개 키를 반환합니다.|  
|[StrongNameTokenFromPublicKey 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfrompublickey-method.md)|공개 키를 나타내는 토큰을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 인스턴스를 가져올 수 있습니다 합니다 `ICLRStrongName` 를 호출 하 여 합니다 [iclrruntimeinfo:: Getinterface](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getinterface-method.md) 메서드를 사용 하 여 `CLSID_CLRStrongName` 및 `IID_ICLRStrongName` 매개 변수로 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
