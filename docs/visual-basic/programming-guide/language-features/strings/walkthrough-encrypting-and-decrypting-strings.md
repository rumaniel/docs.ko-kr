---
title: Visual Basic에서 문자열 암호화 및 암호 해독
ms.date: 07/20/2015
helpviewer_keywords:
- encryption [Visual Basic], strings
- strings [Visual Basic], encrypting
- decryption [Visual Basic], strings
- strings [Visual Basic], decrypting
ms.assetid: 1f51e40a-2f88-43e2-a83e-28a0b5c0d6fd
ms.openlocfilehash: ee8691fedb537d1aa588eaac61624b445da64d1f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69944420"
---
# <a name="walkthrough-encrypting-and-decrypting-strings-in-visual-basic"></a>연습: Visual Basic에서 문자열 암호화 및 암호 해독
이 연습에서는 클래스를 <xref:System.Security.Cryptography.DESCryptoServiceProvider> 사용 하 여 삼중 데이터 암호화 표준 (<xref:System.Security.Cryptography.TripleDES>) 알고리즘의 CSP (암호화 서비스 공급자) 버전을 사용 하 여 문자열을 암호화 하 고 해독 하는 방법을 보여 줍니다. 첫 번째 단계는 3DES 알고리즘을 캡슐화 하 고 암호화 된 데이터를 base-64로 인코딩된 문자열로 저장 하는 간단한 래퍼 클래스를 만드는 것입니다. 그런 다음이 래퍼는 공개적으로 액세스할 수 있는 텍스트 파일에 개인 사용자 데이터를 안전 하 게 저장 하는 데 사용 됩니다.  
  
 암호화를 사용 하 여 사용자 비밀 (예: 암호)을 보호 하 고 권한이 없는 사용자가 자격 증명을 읽을 수 없도록 할 수 있습니다. 이렇게 하면 권한 있는 사용자의 id가 도난당 하지 않도록 보호할 수 있으므로 사용자의 자산을 보호 하 고 부인 방지를 제공 합니다. 암호화는 권한이 없는 사용자가 액세스 하는 사용자의 데이터를 보호할 수도 있습니다.  
  
 자세한 내용은 [암호화 서비스](../../../../standard/security/cryptographic-services.md)를 참조하세요.  
  
> [!IMPORTANT]
> Rijndael (현재 AES(Advanced Encryption Standard) [AES] 이라고 함) 및 3DES (Triple Data Encryption Standard) 알고리즘은 더 많은 계산을 많이 하므로 DES 보다 더 높은 보안을 제공 합니다. 자세한 내용은 <xref:System.Security.Cryptography.DES> 및 <xref:System.Security.Cryptography.Rijndael>를 참조하세요.  
  
### <a name="to-create-the-encryption-wrapper"></a>암호화 래퍼를 만들려면  
  
1. 암호화 및 암호 해독 메서드를 캡슐화 하는 클래스를만듭니다.`Simple3Des`  
  
     [!code-vb[VbVbalrStrings#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#38)]  
  
2. 암호화 네임 스페이스의 가져오기를 `Simple3Des` 클래스를 포함 하는 파일의 시작 부분에 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#77](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#77)]  
  
3. `Simple3Des` 클래스에서 3des 암호화 서비스 공급자를 저장할 전용 필드를 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#39)]  
  
4. 지정 된 키의 해시에서 지정 된 길이의 바이트 배열을 만드는 전용 메서드를 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#41)]  
  
5. 3DES 암호화 서비스 공급자를 초기화 하는 생성자를 추가 합니다.  
  
     매개 `key` 변수는 및 `EncryptData` `DecryptData` 메서드를 제어 합니다.  
  
     [!code-vb[VbVbalrStrings#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#40)]  
  
6. 문자열을 암호화 하는 공용 메서드를 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#42)]  
  
7. 문자열을 해독 하는 공용 메서드를 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#43)]  
  
     이제 래퍼 클래스를 사용 하 여 사용자 자산을 보호할 수 있습니다. 이 예제에서는 공개적으로 액세스할 수 있는 텍스트 파일에 개인 사용자 데이터를 안전 하 게 저장 하는 데 사용 됩니다.  
  
### <a name="to-test-the-encryption-wrapper"></a>암호화 래퍼를 테스트 하려면  
  
1. 별도의 클래스에서 래퍼 `EncryptData` 메서드를 사용 하 여 문자열을 암호화 하 고 사용자의 내 문서 폴더에 쓰는 메서드를 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#78)]  
  
2. 사용자의 내 문서 폴더에서 암호화 된 문자열을 읽고 래퍼 `DecryptData` 메서드를 사용 하 여 문자열의 암호를 해독 하는 메서드를 추가 합니다.  
  
     [!code-vb[VbVbalrStrings#79](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#79)]  
  
3. `TestEncoding` 및`TestDecoding` 메서드를 호출 하는 사용자 인터페이스 코드를 추가 합니다.  
  
4. 애플리케이션을 실행합니다.  
  
     응용 프로그램을 테스트할 때 잘못 된 암호를 입력 하면 데이터의 암호를 해독 하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography>
- <xref:System.Security.Cryptography.DESCryptoServiceProvider>
- <xref:System.Security.Cryptography.DES>
- <xref:System.Security.Cryptography.TripleDES>
- <xref:System.Security.Cryptography.Rijndael>
- [Cryptographic Services](../../../../standard/security/cryptographic-services.md)
