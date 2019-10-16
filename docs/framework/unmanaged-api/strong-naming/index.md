---
title: 강력한 이름 지정(관리되지 않는 API 참조)
ms.date: 03/30/2017
helpviewer_keywords:
- strong naming [.NET Framework], using the unmanaged API
- native API reference [.NET Framework], strong naming
- unmanaged API reference [.NET Framework], strong naming
ms.assetid: 428c68b6-a7b4-44be-b280-75905f46612c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a697d96864f336982c05b5bcc7c48efef2df0f6a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799210"
---
# <a name="strong-naming-unmanaged-api-reference"></a>강력한 이름 지정(관리되지 않는 API 참조)
강력한 이름 API를 통해 클라이언트는 어셈블리에 대한 강력한 이름 서명을 관리할 수 있습니다.  
  
 강력한 이름을 사용하여 어셈블리에 서명하면 어셈블리 매니페스트를 포함하는 파일에 공개 키 암호화가 추가됩니다. 강력한 이름 서명은 참조가 해결될 때 이름의 고유성을 확인하고, 이름 스푸핑을 방지하며, 호출자에게 고유한 ID를 제공합니다. 그러나 강력한 이름과 관련된 신뢰 수준이 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
> [!NOTE]
> 이러한 모든 함수는 .NET Framework 4부터는 사용되지 않습니다. 권장된 대안은 [ICLRStrongName](../hosting/iclrstrongname-interface.md) 인터페이스를 참조하세요.  
  
 [GetHashFromAssemblyFile 함수](gethashfromassemblyfile-function.md)  
 지정된 해시 알고리즘을 사용하여 지정된 어셈블리 파일의 해시를 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [GetHashFromAssemblyFileW 함수](gethashfromassemblyfilew-function.md)  
 지정된 해시 알고리즘을 사용하여 유니코드 문자열로 지정된 어셈블리 파일의 해시를 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [GetHashFromBlob 함수](gethashfromblob-function.md)  
 지정된 해시 알고리즘을 사용하여 지정된 메모리 주소에 있는 어셈블리의 해시를 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [GetHashFromFile 함수](gethashfromfile-function.md)  
 지정된 파일 내용에 대해 해시를 생성합니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [GetHashFromFileW 함수](gethashfromfilew-function.md)  
 유니코드 문자열로 지정된 파일 내용에 대해 해시를 생성합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [GetHashFromHandle 함수](gethashfromhandle-function.md)  
 지정된 해시 알고리즘을 사용하여 지정된 파일 핸들로 파일 내용에 대해 해시를 생성합니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameCompareAssemblies 함수](strongnamecompareassemblies-function.md)  
 두 어셈블리가 강력한 이름 서명에 의해서만 다른지 여부를 결정합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameErrorInfo 함수](strongnameerrorinfo-function.md)  
 강력한 이름 함수 중 하나에 의해 발생하는 마지막 오류 코드를 가져옵니다.  
  
 [StrongNameFreeBuffer 함수](strongnamefreebuffer-function.md)  
 [StrongNameGetPublicKey](strongnamegetpublickey-function.md), [StrongNameTokenFromPublicKey](strongnametokenfrompublickey-function.md) 또는 [StrongNameSignatureGeneration](strongnamesignaturegeneration-function.md)과 같은 강력한 이름 함수에 대한 이전 호출로 할당된 메모리를 해제합니다.   .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameGetBlob 함수](strongnamegetblob-function.md)  
 지정된 주소에 있는 실행 파일의 이진 표현으로 지정된 버퍼를 채웁니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameGetBlobFromImage 함수](strongnamegetblobfromimage-function.md)  
 지정된 메모리 주소에 있는 어셈블리 이미지의 이진 표현을 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameGetPublicKey 함수](strongnamegetpublickey-function.md)  
 퍼블릭/퍼블릭 키 쌍에서 퍼블릭 키를 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameHashSize 함수](strongnamehashsize-function.md)  
 지정된 해시 알고리즘을 사용하여 해시에 필요한 버퍼 크기를 가져옵니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameKeyDelete 함수](strongnamekeydelete-function.md)  
 지정된 키 컨테이너를 삭제합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameKeyGen 함수](strongnamekeygen-function.md)  
 강력한 이름 사용을 위한 새 퍼블릭/프라이빗 키 쌍을 만듭니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameKeyGenEx 함수](strongnamekeygenex-function.md)  
 강력한 이름 사용을 위해 지정된 키 크기로 새 퍼블릭/프라이빗 키 쌍을 생성합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameKeyInstall 함수](strongnamekeyinstall-function.md)  
 퍼블릭/프라이빗 키 쌍을 컨테이너로 가져옵니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameSignatureGeneration 함수](strongnamesignaturegeneration-function.md)  
 지정된 어셈블리에 대한 강력한 이름 서명을 생성합니다.   .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameSignatureGenerationEx 함수](strongnamesignaturegenerationex-function.md)  
 지정된 플래그에 따라 지정된 어셈블리에 대한 강력한 이름 서명을 생성합니다.    .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameSignatureSize 함수](strongnamesignaturesize-function.md)  
 강력한 이름 서명의 크기를 반환합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameSignatureVerification 함수](strongnamesignatureverification-function.md)  
 제공된 경로의 어셈블리 매니페스트에 지정된 플래그에 따라 확인되는 강력한 이름 서명이 포함되는지 여부를 나타내는 값을 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameSignatureVerificationEx 함수](strongnamesignatureverificationex-function.md)  
 제공된 경로의 어셈블리 매니페스트에 강력한 이름 서명이 포함되는지 여부를 나타내는 값을 가져옵니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameSignatureVerificationFromImage 함수](strongnamesignatureverificationfromimage-function.md)  
 메모리에 이미 매핑된 어셈블리가 연결된 공개 키에 유효한지 확인합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameTokenFromAssembly 함수](strongnametokenfromassembly-function.md)  
 지정된 어셈블리 파일에서 강력한 이름 토큰을 만듭니다.  .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameTokenFromAssemblyEx 함수](strongnametokenfromassemblyex-function.md)  
 지정된 어셈블리 파일에서 강력한 이름 토큰을 만들고 공개 키를 반환합니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [StrongNameTokenFromPublicKey 함수](strongnametokenfrompublickey-function.md)  
 공개 키를 나타내는 토큰을 가져옵니다. .NET Framework 4부터 사용되지 않습니다.  
  
 [PublicKeyBlob 구조체](publickeyblob-structure.md)  
 퍼블릭/프라이빗 키 쌍의 퍼블릭 키를 이진 형식으로 나타냅니다.  
  
## <a name="see-also"></a>참고 항목

- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
- [관리되지 않는 API 참조](../index.md)
