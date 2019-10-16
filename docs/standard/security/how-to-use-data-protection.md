---
title: '방법: 데이터 보호 사용'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DPAPI
- encryption [.NET Framework], data protection API
- data [.NET Framework], decryption
- ProtectedMemory class, about ProtectedMemory class
- ProtectedData class, about ProtectedData class
- cryptography [.NET Framework], data protection API
- data protection API [.NET Framework]
- decryption
- data [.NET Framework], encryption
ms.assetid: 606698b0-cb1a-42ca-beeb-0bea34205d20
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1dc8c75d3c8c91d974388779528deff16453d852
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64602547"
---
# <a name="how-to-use-data-protection"></a>방법: 데이터 보호 사용
.NET Framework는 현재 사용자 계정 또는 컴퓨터의 정보를 사용하여 데이터를 암호화할 수 있게 해주는 DPAPI(데이터 보호 API)에 대한 액세스를 제공합니다.  DPAPI를 사용하는 경우 명시적으로 암호화 키를 생성 및 저장하는 어려운 문제가 완화됩니다.  
  
 <xref:System.Security.Cryptography.ProtectedMemory> 클래스를 사용하여 메모리 내 바이트 배열을 암호화합니다.  이 기능은 Microsoft Windows XP 이상의 운영 체제에서 사용할 수 있습니다.  현재 프로세스에서 암호화된 메모리가 현재 프로세스에서만, 모든 프로세스에서 또는 동일한 사용자 컨텍스트에서 암호 해독할 수 있도록 지정할 수 있습니다.  <xref:System.Security.Cryptography.ProtectedMemory> 옵션에 대한 자세한 내용은 <xref:System.Security.Cryptography.MemoryProtectionScope> 열거형을 참조하세요.  
  
 <xref:System.Security.Cryptography.ProtectedData> 클래스를 사용하여 바이트 배열 복사본을 암호화합니다. 이 기능은 Microsoft Windows 2000 이상의 운영 체제에서 사용할 수 있습니다.  현재 사용자 계정에서 암호화된 데이터가 동일한 사용자 계정에 의해서만 암호 해독될 수 있도록 지정하거나, 현재 사용자 계정에서 암호화된 데이터가 컴퓨터의 모든 계정에 의해 암호 해독될 수 있도록 지정할 수 있습니다.  <xref:System.Security.Cryptography.ProtectedData> 옵션에 대한 자세한 내용은 <xref:System.Security.Cryptography.DataProtectionScope> 열거형을 참조하세요.  
  
### <a name="to-encrypt-in-memory-data-using-data-protection"></a>데이터 보호를 사용하여 메모리 내 데이터를 암호화하려면  
  
1. 암호화할 바이트 배열, 엔트로피 및 메모리 보호 범위를 전달하는 동안 정적 <xref:System.Security.Cryptography.ProtectedMemory.Protect%2A> 메서드를 호출합니다.  
  
### <a name="to-decrypt-in-memory-data-using-data-protection"></a>데이터 보호를 사용하여 메모리 내 데이터를 암호 해독하려면  
  
1. 암호 해독할 바이트 배열 및 메모리 보호 범위를 전달하는 동안 정적 <xref:System.Security.Cryptography.ProtectedMemory.Unprotect%2A> 메서드를 호출합니다.  
  
### <a name="to-encrypt-data-to-a-file-or-stream-using-data-protection"></a>데이터 보호를 사용하여 파일 또는 스트림에 데이터를 암호화하려면  
  
1. 임의 엔트로피를 만듭니다.  
  
2. 암호화할 바이트 배열, 엔트로피 및 데이터 보호 범위를 전달하는 동안 정적 <xref:System.Security.Cryptography.ProtectedData.Protect%2A> 메서드를 호출합니다.  
  
3. 파일 또는 스트림에 암호화된 데이터를 씁니다.  
  
### <a name="to-decrypt-data-from-a-file-or-stream-using-data-protection"></a>데이터 보호를 사용하여 파일 또는 스트림에서 데이터를 암호 해독하려면  
  
1. 파일 또는 스트림에서 암호화된 데이터를 읽습니다.  
  
2. 암호 해독할 바이트 배열 및 데이터 보호 범위를 전달하는 동안 정적 <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A> 메서드를 호출합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 두 가지 형태의 암호화 및 암호 해독을 보여 줍니다.  먼저 코드 예제에서 메모리 내 바이트 배열을 암호화한 다음 암호 해독합니다.  그런 다음 코드 예제에서 바이트 배열의 복사본을 암호화하고 파일에 저장한 다음 파일에서 다시 데이터를 로드하고 데이터를 암호 해독합니다.  이 예제에서는 원본 데이터, 암호화된 데이터 및 암호 해독된 데이터를 표시합니다.  
  
 [!code-csharp[DPAPI-HowTO#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DPAPI-HowTO/cs/sample.cs#1)]
 [!code-vb[DPAPI-HowTO#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DPAPI-HowTO/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- `System.Security.dll`에 대한 참조를 포함합니다.  
  
- <xref:System>, <xref:System.IO>, <xref:System.Security.Cryptography> 및 <xref:System.Text> 네임스페이스를 포함합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography.ProtectedMemory>
- <xref:System.Security.Cryptography.ProtectedData>
