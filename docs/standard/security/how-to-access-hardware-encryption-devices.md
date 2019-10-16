---
title: '방법: 하드웨어 암호화 디바이스에 액세스'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- encryption
- key card
- cryptography
- hardware encryption
- CspParameters
ms.assetid: b0e734df-6eb4-4b16-b48c-6f0fe82d5f17
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9c16c994e3976fb3ee569799461db1d1789a6186
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64654386"
---
# <a name="how-to-access-hardware-encryption-devices"></a>방법: 하드웨어 암호화 디바이스에 액세스
<xref:System.Security.Cryptography.CspParameters> 클래스를 사용하여 하드웨어 암호화 디바이스에 액세스할 수 있습니다. 예를 들어 이 클래스를 사용하여 스마트 카드, 하드웨어 난수 생성기 또는 특정 암호화 알고리즘의 하드웨어 구현과 애플리케이션을 통합할 수 있습니다.  
  
 <xref:System.Security.Cryptography.CspParameters> 클래스는 제대로 설치된 하드웨어 암호화 디바이스에 액세스하는 CSP(암호화 서비스 공급자)를 만듭니다.  레지스트리 편집기 (Regedit.exe)를 사용 하 여 다음 레지스트리 키를 검사 하 여 CSP의 가용성을 확인할 수 있습니다.  HKEY_LOCAL_MACHINE\Software\Microsoft\Cryptography\Defaults\Provider.  
  
### <a name="to-sign-data-using-a-key-card"></a>키 카드를 사용하여 데이터에 서명하려면  
  
1. 정수 공급자 형식과 공급자 이름을 생성자에 전달하여 <xref:System.Security.Cryptography.CspParameters> 클래스의 새 인스턴스를 만듭니다.  
  
2. 새로 만든 <xref:System.Security.Cryptography.CspParameters> 개체의 <xref:System.Security.Cryptography.CspParameters.Flags%2A> 속성에 적절한 플래그를 전달합니다.  예를 들어 <xref:System.Security.Cryptography.CspProviderFlags.UseDefaultKeyContainer> 플래그를 전달합니다.  
  
3. <xref:System.Security.Cryptography.CspParameters> 개체를 생성자에 전달하여 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 클래스(예: <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스)의 새 인스턴스를 만듭니다.  
  
4. `Sign` 메서드 중 하나를 사용하여 데이터에 서명하고 `Verify` 메서드 중 하나를 사용하여 데이터를 확인합니다.  
  
### <a name="to-generate-a-random-number-using-a-hardware-random-number-generator"></a>하드웨어 난수 생성기를 사용하여 난수를 생성하려면  
  
1. 정수 공급자 형식과 공급자 이름을 생성자에 전달하여 <xref:System.Security.Cryptography.CspParameters> 클래스의 새 인스턴스를 만듭니다.  
  
2. <xref:System.Security.Cryptography.CspParameters> 개체를 생성자에 전달하여 <xref:System.Security.Cryptography.RNGCryptoServiceProvider>의 새 인스턴스를 만듭니다.  
  
3. <xref:System.Security.Cryptography.RNGCryptoServiceProvider.GetBytes%2A> 또는 <xref:System.Security.Cryptography.RNGCryptoServiceProvider.GetNonZeroBytes%2A> 메서드를 사용하여 난수를 만듭니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 스마트 카드를 사용하여 데이터에 서명하는 방법을 보여 줍니다.  코드 예제에서는 스마트 카드를 노출하는 <xref:System.Security.Cryptography.CspParameters> 개체를 만든 다음 CSP를 사용하여 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 개체를 초기화합니다.  그런 다음 일부 데이터에 서명하고 확인합니다.  
  
 [!code-cpp[Cryptography.SmartCardCSP#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Cryptography.SmartCardCSP/CPP/Cryptography.SmartCardCSP.cpp#1)]
 [!code-csharp[Cryptography.SmartCardCSP#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Cryptography.SmartCardCSP/CS/example.cs#1)]
 [!code-vb[Cryptography.SmartCardCSP#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Cryptography.SmartCardCSP/VB/example.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- <xref:System> 및 <xref:System.Security.Cryptography> 네임스페이스를 포함합니다.  
  
- 스마트 카드 판독기 및 드라이버가 컴퓨터에 설치되어 있어야 합니다.  
  
- 카드 판독기와 관련된 정보를 사용하여 <xref:System.Security.Cryptography.CspParameters> 개체를 초기화해야 합니다.  자세한 내용은 카드 판독기 설명서를 참조하세요.
