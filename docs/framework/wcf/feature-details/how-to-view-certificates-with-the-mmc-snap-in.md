---
title: '방법: MMC 스냅인을 사용 하 여 인증서 보기'
ms.date: 02/25/2019
helpviewer_keywords:
- certificates [WCF], viewing with the MMC snap-in
ms.assetid: 2b8782aa-ebb4-4ee7-974b-90299e356dc5
ms.openlocfilehash: 69f79b64250ff46524e7b4720d13351774875a3f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972733"
---
# <a name="how-to-view-certificates-with-the-mmc-snap-in"></a>방법: MMC 스냅인을 사용 하 여 인증서 보기
보안 클라이언트 또는 서비스를 만들 때 사용할 수 있습니다는 [인증서](working-with-certificates.md) 자격 증명으로 합니다. 예를 들어, 일반적인 자격 증명 형식은 X.509 인증서를 사용 하 여 만든는 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A?displayProperty=nameWithType> 메서드. 

세 가지 유형의 Windows 시스템에서 Microsoft Management Console (MMC) 사용 하 여 검사할 수 있는 인증서 저장소에는

- 로컬 컴퓨터: 로컬 장치 및 장치의 모든 사용자에 게 전역 인지 합니다.

- 현재 사용자: 저장소 장치에서 현재 사용자 계정에 로컬입니다.

- 서비스 계정: 저장소 장치에서 특정 서비스에 로컬입니다.

## <a name="view-certificates-in-the-mmc-snap-in"></a>MMC 스냅인에서 인증서 보기 

다음 절차에는 적절 한 인증서를 찾으려면 장치의 로컬 저장소를 검사 하는 방법을 보여 줍니다. 
  
1. 선택 **실행** 에서 합니다 **시작** 메뉴에서 누릅니다 *mmc*. 

    MMC에는 다음이 표시 됩니다. 
  
2. **파일** 메뉴에서 **스냅인 추가/제거**합니다. 
    
    합니다 **추가 / 스냅인 제거** 창이 나타납니다.
  
3. **사용 가능한 스냅인** 목록에서 선택 **인증서**을 선택한 후 **추가**합니다.  

    ![인증서 스냅인 추가](./media/mmc-add-certificate-snap-in.png)
  
4. 에 **인증서 스냅인** 창에서 **컴퓨터 계정**를 선택한 후 **다음**합니다. 
  
    필요에 따라 선택할 수 있습니다 **내 사용자 계정** 현재 사용자 또는 **서비스 계정** 특정 서비스에 대 한 합니다. 

    > [!NOTE]
    > 모르는 경우 관리자가 장치에 대 한, 사용자 계정에 대해서만 인증서를 관리할 수 있습니다.
  
5. 에 **컴퓨터 선택** 두십시오 창 **로컬 컴퓨터** 을 선택한 다음 선택 **마침**합니다.  
  
6. 에 **추가 또는 제거 스냅인** 창에서 **확인**합니다.  
  
    ![인증서 스냅인 추가](./media/mmc-certificate-snap-in-selected.png)

7. 선택 사항: **파일** 메뉴에서 **저장** 또는 **이름으로 저장** 나중에 사용할 MMC 콘솔 파일을 저장 합니다.  

8. MMC 스냅인에서 인증서를 보려면 선택 **콘솔 루트** 왼쪽된 창에서 확장 **인증서 (로컬 컴퓨터)** 합니다.

    각 유형의 인증서에 대 한 디렉터리 목록이 표시 됩니다. 각 인증서 디렉터리에서 보기, 내보내기,를 가져오고 해당 인증서를 삭제 합니다.

## <a name="view-certificates-with-the-certificate-manager-tool"></a>인증서 관리자 도구를 사용 하 여 인증서 보기

있습니다 수도 보기, 내보내기, 가져오기 및 인증서 관리자 도구를 사용 하 여 인증서를 삭제 합니다.

### <a name="to-view-certificates-for-the-local-device"></a>로컬 장치에 대 한 인증서를 보려면

1. 선택 **실행** 에서 **시작** 메뉴에서 누릅니다 *certlm.msc*합니다. 

    로컬 장치에 대 한 인증서 관리자 도구에는 다음이 표시 됩니다. 
  
2. 아래에서 인증서를 보려면 **인증서-로컬 컴퓨터** 왼쪽된 창에서 보려는 인증서 종류에 대 한 디렉터리를 확장 합니다.

### <a name="to-view-certificates-for-the-current-user"></a>현재 사용자에 대 한 인증서를 보려면

1. 선택 **실행** 에서 합니다 **시작** 메뉴에서 누릅니다 *certmgr.msc*. 

    현재 사용자에 대 한 인증서 관리자 도구에는 다음이 표시 됩니다. 
  
2. 아래에서 인증서를 보려면 **인증서-현재 사용자** 왼쪽된 창에서 보려는 인증서 종류에 대 한 디렉터리를 확장 합니다.

## <a name="see-also"></a>참고자료

- [인증서 작업](working-with-certificates.md)
- [방법: 개발 중 사용할 임시 인증서 만들기](how-to-create-temporary-certificates-for-use-during-development.md)
- [방법: 인증서의 지문 검색](how-to-retrieve-the-thumbprint-of-a-certificate.md)
