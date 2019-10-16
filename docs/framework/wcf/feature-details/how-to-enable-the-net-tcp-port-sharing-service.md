---
title: '방법: Net.TCP Port Sharing Service 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- port sharing [WCF]
- activation services [WCF]
ms.assetid: c9175af4-c27c-4765-bf45-b8f7528a7282
ms.openlocfilehash: 20db0ef427a5e791bd6b8dcef90bf7911ae0d4a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61772959"
---
# <a name="how-to-enable-the-nettcp-port-sharing-service"></a>방법: Net.TCP Port Sharing Service 사용
Windows Communication Foundation (WCF) Net.TCP Port Sharing Service 라는 Windows 서비스를 사용 하 여 여러 프로세스에서 TCP 포트를 공유할 수 있도록 합니다. 이 서비스는 WCF의 일부로 설치 되지만 서비스 보안 예방 조치로 서 기본적으로 사용 되지 않으며 따라서 수동으로 활성화 해야 처음 사용 하기 전에 합니다. 이 항목에서는 MMC(Microsoft Management Console) 스냅인을 사용하여 Net TCP Port Sharing Service를 구성하는 방법에 대해 설명합니다.  
  
 Net.TCP Port Sharing Service를 사용 하도록 설정 하 고 수동으로 시작 후 참조 [방법: 포트 공유를 사용 하도록 WCF 서비스 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md) 이 서비스를 사용 하도록 서비스를 구성 하는 방법에 대 한 정보에 대 한 합니다.  
  
 Net.tcp:// 포트 공유를 사용 하는 샘플에 대해서는 [Net.TCP Port Sharing 샘플](../../../../docs/framework/wcf/samples/net-tcp-port-sharing-sample.md)합니다.  
  
### <a name="to-enable-the-nettcp-port-sharing-service-using-mmc"></a>MMC를 사용하여 Net.TCP Port Sharing Service를 사용하려면  
  
1. 시작 메뉴에서 명령 프롬프트 창을 열고를 입력 하 여 서비스 관리 콘솔을 엽니다 `services.msc` 실행을 열고를 입력 하거나 `services.msc` 열기 상자에 있습니다.  
  
2. 에 **이름** 열의 서비스 목록 마우스 오른쪽 단추로 클릭 합니다 **Net.Tcp Port Sharing Service**, 선택한 **속성** 메뉴에서.  
  
3. 서비스의 수동 시작을 사용 하도록 설정 하는 **속성** 창 선택 합니다 **일반** 탭 및는 **시작 유형** 수동을 선택한 다음 를클릭**적용**합니다.  
  
4. 서비스 상태 영역에서 서비스를 시작 하려면 클릭 합니다 **시작** 단추입니다. 서비스 상태가 "시작됨"으로 표시되어야 합니다.  
  
5. 서비스 목록으로 돌아가려면 클릭 합니다 **확인**를 하 고 MMC 콘솔을 종료 합니다.  
  
## <a name="example"></a>예제  
  
## <a name="see-also"></a>참고자료

- [Net.TCP 포트 공유](../../../../docs/framework/wcf/feature-details/net-tcp-port-sharing.md)
- [Net.TCP Port Sharing Service 구성](../../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)
