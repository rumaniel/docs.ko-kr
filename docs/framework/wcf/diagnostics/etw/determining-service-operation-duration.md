---
title: 서비스 작업 기간 확인
ms.date: 03/30/2017
ms.assetid: e8a93a2c-2c20-48b3-8986-57e90e9aa908
ms.openlocfilehash: 06a4c2da7b702fa4fbc1469576c118b790803339
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291428"
---
# <a name="determining-service-operation-duration"></a>서비스 작업 기간 확인
WCF (Windows Communication Foundation) 응용 프로그램에서 분석 추적을 사용 하는 경우 이벤트 로그를 검사 하 여 서비스 작업에 대 한 실행 기간을 쉽게 확인할 수 있습니다.  이 항목에서는 서비스 작업을 완료하는 데 소요되는 시간을 확인하는 방법을 보여 줍니다.  
  
### <a name="determining-service-operation-execution-duration"></a>서비스 작업 실행 기간 확인  
  
1. **시작**, **실행**을 차례로 클릭 하 고 `eventvwr.exe`를 입력 하 여 이벤트 뷰어를 엽니다.  
  
2. 분석 추적을 사용 하도록 설정 하지 않은 경우 **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-** 응용 프로그램을 확장 합니다. **보기**, **분석 및 디버그 로그 표시**를 선택 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다. 서비스 작업이 실행된 후 추적 내용을 볼 수 있도록 이벤트 뷰어를 열어 둡니다.  
  
3. 그런 다음 서비스 프로젝트 및 서비스와 상호 작용 하는 클라이언트 프로젝트를 포함 하는 WCF 응용 프로그램을 엽니다.  초보자를 위한 [자습서](../../getting-started-tutorial.md)에 따라 이러한 응용 프로그램을 만들 수 있습니다.  WCF 샘플을 설치한 경우 자습서에서 만든 완료 된 프로젝트를 포함 하는 [시작](../../samples/getting-started-sample.md)을 열 수 있습니다.  
  
4. **F5**키를 눌러 서버 응용 프로그램을 실행 합니다. **클라이언트** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **디버그**, **새 인스턴스 시작**을 차례로 선택 하 여 클라이언트 응용 프로그램을 실행 합니다.  
  
5. 이벤트 뷰어에서 분석 로그를 새로 고친 다음 이벤트 ID를 기준으로 이벤트를 정렬합니다.  이벤트 ID가 [214-OperationCompleted](214-operationcompleted.md)인 이벤트를 찾습니다.  이 이벤트는 완료된 작업과 해당 작업의 기간을 보여 줍니다.  다음 이벤트는 Add 작업의 기간을 보여 줍니다.  
  
    ```output  
    An OperationInvoker completed the call to the 'Add' method.  The method call duration was '3' ms.  
    ```
