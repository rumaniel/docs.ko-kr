---
title: '연습: 암호화 애플리케이션 만들기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [NET Framework], example
- cryptography [NET Framework], cryptographic application example
- cryptography [NET Framework], application example
ms.assetid: abf48c11-1e72-431d-9562-39cf23e1a8ff
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ee6dafa8578c59d23908bf0e184091bb4ceaeb45
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895293"
---
# <a name="walkthrough-creating-a-cryptographic-application"></a>연습: 암호화 애플리케이션 만들기
이 연습에서는 콘텐츠를 암호화 및 암호 해독하는 방법을 보여 줍니다. 코드 예제는 Windows Forms 응용 프로그램용으로 설계되었습니다. 이 응용 프로그램은 스마트 카드 사용과 같은 실제 시나리오를 보여 주지 않습니다. 대신, 암호화 및 암호 해독의 기초를 보여 줍니다.  
  
 이 연습에서는 암호화에 대한 다음 지침을 사용합니다.  
  
- 대칭 알고리즘인 <xref:System.Security.Cryptography.RijndaelManaged> 클래스를 사용하여 자동으로 생성된 해당 <xref:System.Security.Cryptography.SymmetricAlgorithm.Key%2A> 및 <xref:System.Security.Cryptography.SymmetricAlgorithm.IV%2A>를 통해 데이터를 암호화 및 암호 해독합니다.  
  
- 비대칭 알고리즘인 <xref:System.Security.Cryptography.RSACryptoServiceProvider>를 사용하여 <xref:System.Security.Cryptography.RijndaelManaged>를 통해 암호화된 데이터에 대한 키를 암호화 및 암호 해독합니다. 비대칭 알고리즘은 키와 같은 적은 양의 데이터에 가장 적합합니다.  
  
    > [!NOTE]
    > 암호화된 콘텐츠를 다른 사용자와 교환하는 대신 컴퓨터에서 데이터를 보호하려는 경우 <xref:System.Security.Cryptography.ProtectedData> 또는 <xref:System.Security.Cryptography.ProtectedMemory> 클래스를 사용하는 것이 좋습니다.  
  
 다음 표에는 이 항목의 암호화 작업이 요약되어 있습니다.  
  
|작업|설명|  
|----------|-----------------|  
|Windows Forms 응용 프로그램 만들기|응용 프로그램을 실행하는 데 필요한 컨트롤을 나열합니다.|  
|전역 개체 선언|<xref:System.Windows.Forms.Form> 클래스의 전역 컨텍스트를 사용하도록 문자열 경로 변수, <xref:System.Security.Cryptography.CspParameters> 및 <xref:System.Security.Cryptography.RSACryptoServiceProvider>를 선언합니다.|  
|비대칭 키 만들기|비대칭 공개 및 개인 키 값 쌍을 만들고 키 컨테이너 이름을 할당합니다.|  
|파일 암호화|암호화를 위해 파일을 선택할 수 있는 대화 상자를 표시하고 파일을 암호화합니다.|  
|파일 암호 해독|암호 해독을 위해 암호화된 파일을 선택할 수 있는 대화 상자를 표시하고 파일을 암호 해독합니다.|  
|개인 키 가져오기|키 컨테이너 이름을 사용하여 전체 키 쌍을 가져옵니다.|  
|공개 키 내보내기|public 매개 변수만 사용하여 키를 XML 파일에 저장합니다.|  
|공개 키 가져오기|XML 파일의 키를 키 컨테이너에 로드합니다.|  
|애플리케이션 테스트|이 응용 프로그램을 테스트하기 위한 절차를 나열합니다.|  
  
## <a name="prerequisites"></a>전제 조건  
 이 연습을 완료하려면 다음 구성 요소가 필요합니다.  
  
- <xref:System.IO> 및 <xref:System.Security.Cryptography> 네임스페이스에 대한 참조  
  
## <a name="creating-a-windows-forms-application"></a>Windows Forms 응용 프로그램 만들기  
 이 연습의 대다수 코드 예제는 단추 컨트롤에 대한 이벤트 처리기로 설계되었습니다. 다음 표에서는 샘플 응용 프로그램에 필요한 컨트롤 및 코드 예제와 일치하는 데 필요한 이름을 보여 줍니다.  
  
|Control|이름|텍스트 속성(필요에 따라)|  
|-------------|----------|---------------------------------|  
|<xref:System.Windows.Forms.Button>|`buttonEncryptFile`|파일 암호화|  
|<xref:System.Windows.Forms.Button>|`buttonDecryptFile`|파일 암호 해독|  
|<xref:System.Windows.Forms.Button>|`buttonCreateAsmKeys`|키 만들기|  
|<xref:System.Windows.Forms.Button>|`buttonExportPublicKey`|공개 키 내보내기|  
|<xref:System.Windows.Forms.Button>|`buttonImportPublicKey`|공개 키 가져오기|  
|<xref:System.Windows.Forms.Button>|`buttonGetPrivateKey`|개인 키 가져오기|  
|<xref:System.Windows.Forms.Label>|`label1`|키가 설정 되지 않음|  
|<xref:System.Windows.Forms.OpenFileDialog>|`openFileDialog1`||  
|<xref:System.Windows.Forms.OpenFileDialog>|`openFileDialog2`||  
  
 이벤트 처리기를 만들려면 Visual Studio 디자이너에서 해당 단추를 두 번 클릭합니다.  
  
## <a name="declaring-global-objects"></a>전역 개체 선언  
 폼의 생성자에 다음 코드를 추가합니다. 사용자 환경 및 기본 설정에 맞게 문자열 변수를 편집합니다.  
  
 [!code-csharp[CryptoWalkThru#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#1)]
 [!code-vb[CryptoWalkThru#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#1)]  
  
## <a name="creating-an-asymmetric-key"></a>비대칭 키 만들기  
 이 작업은 <xref:System.Security.Cryptography.RijndaelManaged> 키를 암호화 및 암호 해독하는 비대칭 키를 만듭니다. 이 키는 콘텐츠를 암호화하는 데 사용되었으며 레이블 컨트롤에 키 컨테이너 이름을 표시합니다.  
  
 `Create Keys` 단추(`buttonCreateAsmKeys_Click`)에 대한 `Click` 이벤트 처리기로 다음 코드를 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#2)]
 [!code-vb[CryptoWalkThru#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#2)]  
  
## <a name="encrypting-a-file"></a>파일 암호화  
 이 작업에는 `Encrypt File` 단추에 대 한 이벤트 처리기 메서드 (`buttonEncryptFile_Click`) 및 `EncryptFile` 메서드에 대 한 두 가지 메서드가 포함 됩니다. 첫 번째 메서드는 파일을 선택할 수 있는 대화 상자를 표시하고 암호화를 수행하는 두 번째 메서드에 파일 이름을 전달합니다.  
  
 암호화된 콘텐츠, 키 및 IV가 모두 하나의 <xref:System.IO.FileStream>에 저장되며, 이를 암호화 패키지라고 합니다.  
  
 `EncryptFile` 메서드는 다음 작업을 수행합니다.  
  
1. <xref:System.Security.Cryptography.RijndaelManaged> 대칭 알고리즘을 만들어 콘텐츠를 암호화합니다.  
  
2. <xref:System.Security.Cryptography.RSACryptoServiceProvider> 개체를 만들어 <xref:System.Security.Cryptography.RijndaelManaged> 키를 암호화합니다.  
  
3. <xref:System.Security.Cryptography.CryptoStream> 개체를 사용하여 소스 파일의 <xref:System.IO.FileStream>을 바이트 블록 단위로 암호화된 파일의 대상 <xref:System.IO.FileStream> 개체로 읽고 암호화합니다.  
  
4. 암호화된 키 및 IV의 길이를 확인하고 해당 길이 값의 바이트 배열을 만듭니다.  
  
5. 암호화된 패키지에 키, IV 및 해당 길이 값을 씁니다.  
  
 암호화 패키지는 다음 형식을 사용합니다.  
  
- 키 길이, 0-3바이트  
  
- IV 길이, 4-7바이트  
  
- 암호화된 키  
  
- IV  
  
- 암호화 텍스트  
  
 키 및 IV의 길이를 사용하여 파일을 암호 해독하는 데 사용할 수 있는 암호화 패키지의 모든 부분에 대한 시작 지점 및 길이를 확인할 수 있습니다.  
  
 `Encrypt File` 단추(`buttonEncryptFile_Click`)에 대한 `Click` 이벤트 처리기로 다음 코드를 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#3)]
 [!code-vb[CryptoWalkThru#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#3)]  
  
 다음 `EncryptFile` 메서드를 폼에 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#5)]
 [!code-vb[CryptoWalkThru#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#5)]  
  
## <a name="decrypting-a-file"></a>파일 암호 해독  
 이 작업에는 `Decrypt File` 단추에 대한 이벤트 처리기 메서드(`buttonDecryptFile_Click`) 및 `DecryptFile` 메서드의 두 메서드가 필요합니다. 첫 번째 메서드는 파일을 선택할 수 있는 대화 상자를 표시하고 암호 해독을 수행하는 두 번째 메서드에 파일 이름을 전달합니다.  
  
 `Decrypt` 메서드는 다음 작업을 수행합니다.  
  
1. <xref:System.Security.Cryptography.RijndaelManaged> 대칭 알고리즘을 만들어 콘텐츠를 암호 해독합니다.  
  
2. 암호화된 패키지 <xref:System.IO.FileStream>의 처음 8바이트를 바이트 배열로 읽어 암호화된 키 및 IV의 길이를 가져옵니다.  
  
3. 암호화 패키지에서 바이트 배열로 키 및 IV를 추출합니다.  
  
4. <xref:System.Security.Cryptography.RSACryptoServiceProvider> 개체를 만들어 <xref:System.Security.Cryptography.RijndaelManaged> 키를 암호 해독합니다.  
  
5. <xref:System.Security.Cryptography.CryptoStream> 개체를 사용하여 <xref:System.IO.FileStream> 암호화 패키지의 암호화 텍스트 섹션을 바이트 블록 단위로 암호 해독된 파일의 <xref:System.IO.FileStream> 개체로 읽고 암호 해독합니다. 이 작업을 완료하면 암호 해독이 완료됩니다.  
  
 `Decrypt File` 단추에 대한 `Click` 이벤트 처리기로 다음 코드를 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#4)]
 [!code-vb[CryptoWalkThru#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#4)]  
  
 다음 `DecryptFile` 메서드를 폼에 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#6)]
 [!code-vb[CryptoWalkThru#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#6)]  
  
## <a name="exporting-a-public-key"></a>공개 키 내보내기  
 이 작업은 `Create Keys` 단추를 사용하여 만든 키를 파일에 저장합니다. public 매개 변수만 내보냅니다.  
  
 이 작업은 Bob이 파일을 암호화할 수 있도록 Alice가 Bob에게 공개 키를 제공하는 시나리오를 시뮬레이트합니다. Bob과 해당 공개 키를 가진 다른 사용자는 private 매개 변수가 있는 전체 키 쌍이 없기 때문에 파일을 암호 해독할 수 없습니다.  
  
 `Export Public Key` 단추(`buttonExportPublicKey_Click`)에 대한 `Click` 이벤트 처리기로 다음 코드를 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#8](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#8)]
 [!code-vb[CryptoWalkThru#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#8)]  
  
## <a name="importing-a-public-key"></a>공개 키 가져오기  
 이 작업은 `Export Public Key` 단추를 사용하여 만든 public 매개 변수만 있는 키를 로드하고 키 컨테이너 이름으로 설정합니다.  
  
 이 작업은 Bob이 파일을 암호화할 수 있도록 public 매개 변수만 있는 Alice의 키를 Bob이 로드하는 시나리오를 시뮬레이트합니다.  
  
 `Import Public Key` 단추(`buttonImportPublicKey_Click`)에 대한 `Click` 이벤트 처리기로 다음 코드를 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#9](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#9)]
 [!code-vb[CryptoWalkThru#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#9)]  
  
## <a name="getting-a-private-key"></a>개인 키 가져오기  
 이 작업은 키 컨테이너 이름을 `Create Keys` 단추를 사용하여 만든 키의 이름으로 설정합니다. 키 컨테이너는 private 매개 변수가 있는 전체 키 쌍을 포함합니다.  
  
 이 작업은 Alice가 개인 키를 사용하여 Bob이 암호화한 파일을 암호 해독하는 시나리오를 시뮬레이트합니다.  
  
 `Get Private Key` 단추(`buttonGetPrivateKey_Click`)에 대한 `Click` 이벤트 처리기로 다음 코드를 추가합니다.  
  
 [!code-csharp[CryptoWalkThru#7](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#7)]
 [!code-vb[CryptoWalkThru#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#7)]  
  
## <a name="testing-the-application"></a>애플리케이션 테스트  
 응용 프로그램을 빌드한 후 다음과 같은 테스트 시나리오를 수행합니다.  
  
#### <a name="to-create-keys-encrypt-and-decrypt"></a>키를 만들고 암호화 및 암호 해독하려면  
  
1. `Create Keys` 단추를 클릭합니다. 레이블이 키 이름을 표시하고 전체 키 쌍임을 보여 줍니다.  
  
2. `Export Public Key` 단추를 클릭합니다. 공개 키 매개 변수를 내보내는 경우 현재 키가 변경되지 않습니다.  
  
3. `Encrypt File` 단추를 클릭하고 파일을 선택합니다.  
  
4. `Decrypt File` 단추를 클릭하고 방금 암호화한 파일을 선택합니다.  
  
5. 방금 암호 해독한 파일을 검사합니다.  
  
6. 응용 프로그램을 닫고 다음 시나리오에서 지속형 키 컨테이너 검색을 테스트하기 위해 다시 시작합니다.  
  
#### <a name="to-encrypt-using-the-public-key"></a>공개 키를 사용하여 암호화하려면  
  
1. `Import Public Key` 단추를 클릭합니다. 레이블이 키 이름을 표시하고 public 전용임을 보여 줍니다.  
  
2. `Encrypt File` 단추를 클릭하고 파일을 선택합니다.  
  
3. `Decrypt File` 단추를 클릭하고 방금 암호화한 파일을 선택합니다. 암호 해독하려면 개인 키가 있어야 하므로 이 작업은 실패합니다.  
  
 이 시나리오에서는 다른 사용자를 위해 파일을 암호화할 공개 키만 있는 경우를 보여 줍니다. 일반적으로 해당 사용자는 공개 키만 제공하고 암호 해독을 위한 개인 키는 보유합니다.  
  
#### <a name="to-decrypt-using-the-private-key"></a>개인 키를 사용하여 암호 해독하려면  
  
1. `Get Private Key` 단추를 클릭합니다. 레이블이 키 이름을 표시하고 전체 키 쌍인지 여부를 보여 줍니다.  
  
2. `Decrypt File` 단추를 클릭하고 방금 암호화한 파일을 선택합니다. 암호 해독을 위한 전체 키 쌍이 있으므로 이 작업은 성공합니다.  
  
## <a name="see-also"></a>참고자료

- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
