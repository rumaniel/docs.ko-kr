---
title: '방법: 애플리케이션 세션 간 설정 값 변경'
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], changing
- application settings [Windows Forms], between application sessions
ms.assetid: 1a85911f-97b2-476c-930b-83379edd890c
ms.openlocfilehash: 95e613cb280813cd75d887d3cf147d7c897bc2e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62004434"
---
# <a name="how-to-change-the-value-of-a-setting-between-application-sessions"></a>방법: 애플리케이션 세션 간 설정 값 변경
때때로 다음 응용 프로그램을 컴파일 및 배포 후 응용 프로그램 세션 간 설정 값을 변경 하는 것이 좋습니다. 예를 들어, 다음 올바른 데이터베이스 위치를 가리키도록 연결 문자열을 변경 하는 것이 좋습니다. 디자인 타임 도구를 사용할 수 없는 응용 프로그램을 컴파일 및 배포 후 하므로 파일에서 수동으로 설정 값을 변경 해야 합니다.  
  
### <a name="to-change-the-value-of-a-setting-between-application-sessions"></a>응용 프로그램 세션 간 설정 값을 변경 하려면  
  
1. Microsoft 메모장 또는 일부 다른 텍스트 또는 XML 편집기를 사용 하 여, 응용 프로그램과 연결 된.config 파일을 엽니다.  
  
2. 변경 하려면 설정에 대 한 항목을 찾습니다. 아래 예제와 비슷하게 표시 됩니다.  
  
    ```xml  
    <setting name="Setting1" serializeAs="String" >  
       <value>My Setting Value</value>  
    </setting>  
    ```  
  
3. 설정에 대 한 새 값을 입력 하 고 파일을 저장 합니다.  
  
## <a name="see-also"></a>참고자료

- [응용 프로그램 설정 및 사용자 설정 사용](using-application-settings-and-user-settings.md)
- [응용 프로그램 설정 개요](application-settings-overview.md)
