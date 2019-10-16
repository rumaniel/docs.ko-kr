---
title: 페더레이션 시나리오에서 혼합 트러스트 프로토콜
ms.date: 03/30/2017
ms.assetid: d7b5fee9-2246-4b09-b8d7-9e63cb817279
ms.openlocfilehash: 18f486b9de83db48e186bb3856aff6cc6ccb56b1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64606503"
---
# <a name="mixing-trust-protocols-in-federated-scenarios"></a>페더레이션 시나리오에서 혼합 트러스트 프로토콜
페더레이션 클라이언트가 트러스트 버전이 다른 서비스 및 STS(보안 토큰 서비스)와 통신하는 시나리오가 있을 수 있습니다. 서비스 WSDL에 STS와 버전이 다른 WS-Trust 요소가 있는 `RequestSecurityTokenTemplate` 어설션이 포함될 수 있습니다. 이러한 경우 Windows Communication Foundation (WCF) 클라이언트에서 수신한 Ws-trust 요소를 변환 합니다.는 `RequestSecurityTokenTemplate` STS 트러스트 버전과 일치 하도록 합니다. WCF에는 일치 하지 않는 트러스트 버전을 표준 바인딩 용 으로만 처리합니다. WCF에서 인식 되는 모든 표준 알고리즘 매개 변수를 사용 하면 표준 바인딩의 일부인 합니다. 이 항목에서는 서비스와 STS 간의 다양 한 트러스트 설정 사용 하 여 WCF 동작을 설명 합니다.  
  
## <a name="rp-feb-2005-and-sts-feb-2005"></a>RP 2005년 2월 및 STS 2005년 2월  
 RP(신뢰 당사자)에 대한 WSDL에서는 `RequestSecurityTokenTemplate` 섹션 내에 다음 요소를 포함합니다.  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
 클라이언트 구성 파일에는 매개 변수 목록이 포함됩니다.  
  
 WCF는 클라이언트 및 서비스 매개 변수를 구분할 수 없습니다. 모든 매개 변수를 추가 하 고 보냅니다는 `RequestSecurityTokenTemplate` (RST).  
  
## <a name="rp-trust-13-and-sts-trust-13"></a>RP Trust 1.3 및 STS Trust 1.3  
 RP에 대한 WSDL에서는 `RequestSecurityTokenTemplate` 섹션 내에 다음 요소를 포함합니다.  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
- `KeyWrapAlgorithm`  
  
 클라이언트 구성 파일에는 RP에서 지정한 매개 변수를 래핑하는 `secondaryParameters` 요소가 포함됩니다.  
  
 WCF 제거 합니다 `EncryptionAlgorithm`, `CanonicalizationAlgorithm` 및 `KeyWrapAlgorithm` 요소 내에 있는 경우 rst의 최상위 요소에서는 `SecondaryParameters` 요소입니다. WCF 추가 `SecondaryParameters` 수정 되지 않은 나가는 RST 요소입니다.  
  
## <a name="rp-trust-feb-2005-and-sts-trust-13"></a>RP Trust 2005년 2월 및 STS Trust 1.3  
 RP에 대한 WSDL에서는 `RequestSecurityTokenTemplate` 섹션 내에 다음 요소를 포함합니다.  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
 클라이언트 구성 파일에는 매개 변수 목록이 포함됩니다.  
  
 클라이언트 구성 파일에서 WCF 서비스 및 클라이언트 매개 변수를 구분할 수 없습니다. 따라서 WCF 트러스트 버전 1.3 네임 스페이스에 모든 매개 변수를 변환합니다.  
  
 WCF 핸들은 `KeyType`, `KeySize`, 및 `TokenType` 다음과 같은 요소:  
  
- WSDL을 다운로드하고, 바인딩을 만들고, RP 매개 변수에서 `KeyType`, `KeySize` 및 `TokenType`을 할당합니다. 그런 다음 클라이언트 구성 파일이 생성됩니다.  
  
- 이제 클라이언트에서 구성 파일의 모든 매개 변수를 수정할 수 있습니다.  
  
- WCF 런타임 중에 지정 된 모든 매개 변수를 복사 합니다 `AdditionalTokenParameters` 제외 하 고 클라이언트 구성 파일의 섹션 `KeyType`, `KeySize` 고 `TokenType`이므로 이러한 매개 변수는 구성 파일 하는 동안에 필요 세대입니다.  
  
## <a name="rp-trust-13-and-sts-trust-feb-2005"></a>RP Trust 1.3 및 STS Trust 2005년 2월  
 RP에 대한 WSDL에서는 `RequestSecurityTokenTemplate` 섹션 내에 다음 요소를 포함합니다.  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
- `KeyWrapAlgorithm`  
  
 클라이언트 구성 파일에는 RP에서 지정한 매개 변수를 래핑하는 `secondaryParamters` 요소가 포함됩니다.  
  
 내에 지정 된 모든 매개 변수를 복사 하는 WCF는 `SecondaryParameters` 최상위 RST 요소로 섹션 하지만 2005 Ws-trust 네임 스페이스를 변환 하지 않습니다.
