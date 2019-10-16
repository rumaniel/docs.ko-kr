---
title: 해시 코드를 사용하여 데이터 무결성 보장
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generating hash
- verifying hash codes
- cryptography [.NET Framework], hash
- data integrity
- checking hash codes
- encryption [.NET Framework], hash
- hash
ms.assetid: 33660f33-b70f-4dca-8c87-ab35cfc2961a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 995f54e81a48fb3f809d99981ad135974544eb28
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353176"
---
# <a name="ensuring-data-integrity-with-hash-codes"></a>해시 코드를 사용하여 데이터 무결성 보장
해시 값을 데이터를 고유하게 식별하는 고정 길이 숫자 값입니다. 해시 값은 대용량 데이터를 훨씬 더 작은 숫자 값으로 나타내므로 디지털 서명과 함께 사용됩니다. 해시 값에 서명하는 것이 더 큰 값에 서명하는 것보다 더 효율적입니다. 해시 값은 안전하지 않은 채널을 통해 전송된 데이터의 무결성을 확인하는 데도 유용합니다. 수신된 데이터의 해시 값을 전송된 데이터의 해시 값과 비교하여 데이터가 변경되었는지 확인할 수 있습니다.  
  
 이 항목에서는 <xref:System.Security.Cryptography?displayProperty=nameWithType> 네임스페이스의 클래스를 사용하여 해시 코드를 생성하고 확인하는 방법을 설명합니다.  
  
## <a name="generating-a-hash"></a>해시 생성  
 관리되는 해시 클래스는 바이트 배열이나 관리되는 스트림 개체를 해시할 수 있습니다. 다음 예제에서는 SHA1 해시 알고리즘을 사용하여 문자열에 대한 해시 값을 만듭니다. 이 예제에서는 <xref:System.Text.UnicodeEncoding> 클래스를 사용하여 문자열을 <xref:System.Security.Cryptography.SHA1Managed> 클래스를 통해 해시된 바이트 배열로 변환합니다. 해시 값이 콘솔에 표시됩니다.  

 S h a 1의 충돌 문제로 인해 s h a 1 이상을 권장 합니다.
  
 [!code-csharp[GeneratingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/generatingahash/cs/program.cs#1)]
 [!code-vb[GeneratingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/generatingahash/vb/program.vb#1)]  
  
 이 코드는 다음 문자열을 콘솔에 표시합니다.  
  
 `59 4 248 102 77 97 142 201 210 12 224 93 25 41 100 197 213 134 130 135`  
  
## <a name="verifying-a-hash"></a>해시 확인  
 데이터를 해시 값과 비교하여 데이터 무결성을 확인할 수 있습니다. 일반적으로 데이터는 특정 시간에 해시되고 해시 값은 몇 가지 방법으로 보호됩니다. 나중에 데이터를 다시 해시하고 보호된 값과 비교할 수 있습니다. 해시 값이 일치하면 데이터가 변경되지 않은 것입니다. 값이 일치하지 않으면 데이터가 손상된 것입니다. 이 시스템이 작동하려면 보호된 해시를 암호화하거나 모든 신뢰할 수 없는 상대방으로부터 기밀로 유지해야 합니다.  
  
 다음 예제에서는 문자열의 이전 해시 값을 새 해시 값과 비교합니다. 이 예제에서는 해시 값의 각 바이트를 순환하고 비교를 수행합니다.  
  
 [!code-csharp[VerifyingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/verifyingahash/cs/program.cs#1)]
 [!code-vb[VerifyingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/verifyingahash/vb/program.vb#1)]  
  
 두 해시 값이 일치하면 이 코드는 다음 내용을 콘솔에 표시합니다.  
  
```console  
The hash codes match.  
```  
  
 일치하지 않으면 코드는 다음을 표시합니다.  
  
```console  
The hash codes do not match.  
```  
  
## <a name="see-also"></a>참조

- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
