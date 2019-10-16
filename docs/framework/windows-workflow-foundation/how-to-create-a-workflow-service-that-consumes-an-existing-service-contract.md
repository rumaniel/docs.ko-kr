---
title: '방법: 기존 서비스 계약을 사용하는 워크플로 서비스 만들기'
ms.date: 03/30/2017
ms.assetid: 11d11b59-acc4-48bf-8e4b-e97b516aa0a9
ms.openlocfilehash: 6d7fa8c9faa84efc84243387cd27aa264f6155eb
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989618"
---
# <a name="how-to-create-a-workflow-service-that-consumes-an-existing-service-contract"></a>방법: 기존 서비스 계약을 사용하는 워크플로 서비스 만들기
.NET Framework 4.5는 계약 중심 워크플로 개발의 형태로 웹 서비스와 워크플로 간에 더 나은 통합 기능을 제공 합니다. 계약 중심 워크플로 개발 도구를 사용하면 코드에서 계약을 먼저 디자인할 수 있습니다. 그러면 이 도구는 계약의 작업을 위해 도구 상자에 활동 템플릿을 자동으로 생성합니다.  
  
> [!NOTE]
> 이 항목에서는 계약 중심 워크플로 서비스를 만들기 위한 단계별 지침을 제공합니다. 계약 중심 워크플로 서비스 개발에 대 한 자세한 내용은 [첫 번째 워크플로 서비스 개발 계약](contract-first-workflow-service-development.md)을 참조 하세요.  
  
### <a name="creating-the-workflow-project"></a>워크플로 프로젝트 만들기  
  
1. Visual Studio에서 **파일**, **새 프로젝트**를 차례로 선택 합니다. **템플릿** 트리의 **C#** 노드 아래에서 Wcf 노드를 선택 하 고 **wcf 워크플로 서비스 응용 프로그램** 템플릿을 선택 합니다.  
  
2. 새 프로젝트 `ContractFirst` 의 이름을로 하 고 **확인을**클릭 합니다.  
  
### <a name="creating-the-service-contract"></a>서비스 계약 만들기  
  
1. **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**...을 차례로 선택 합니다. 왼쪽에서 **코드** 노드를 선택 하 고 오른쪽의 **클래스** 템플릿을 선택 합니다. 새 클래스 `IBookService` 의 이름을로, **확인을**클릭 합니다.  
  
2. 표시되는 코드 창의 맨 위에서 `System.Servicemodel`에 Using 문을 추가합니다.  
  
    ```csharp  
    using System.ServiceModel;  
    ```  
  
3. 샘플 클래스 정의를 다음과 같은 인터페이스 정의로 변경합니다.  
  
    ```csharp  
    [ServiceContract]  
        public interface IBookService  
        {  
            [OperationContract]  
            void Buy(string bookName);  
  
            [OperationContract(IsOneWay=true)]  
            void Checkout();  
        }  
    ```  
  
4. **Ctrl + Shift + B**를 눌러 프로젝트를 빌드합니다.  
  
### <a name="importing-the-service-contract"></a>서비스 계약 가져오기  
  
1. **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **서비스 계약 가져오기**를 선택 합니다. **\<현재 프로젝트 >** 아래에서 모든 하위 노드를 열고 **ibookservice**를 선택 합니다. **확인**을 클릭합니다.  
  
2. 작업이 성공적으로 완료되었음을 알리는 대화 상자가 열리고 프로젝트가 빌드된 후 생성된 활동이 도구 상자에 나타납니다. **확인**을 클릭합니다.  
  
3. 가져온 활동이 도구 상자에 표시 되도록 **Ctrl + Shift + B**를 눌러 프로젝트를 빌드합니다.  
  
4. **솔루션 탐색기**에서 .xamlx을 엽니다. 워크플로 서비스가 디자이너에 표시됩니다.  
  
5. **Sequence** 활동을 선택 합니다. 속성 창 **에서 ...** **구현 된 Edcontract** 속성의 단추입니다. 표시 되는 **형식 컬렉션 편집기** 창에서 **형식** 드롭다운을 클릭 하 고 **형식 찾아보기** ...를 선택 합니다. 엔트리의. **.Net 형식 찾아보기 및 선택** 대화 상자의  **\<현재 프로젝트 >** 아래에서 모든 하위 노드를 열고 **ibookservice**를 선택 합니다. **확인**을 클릭합니다. **형식 컬렉션 편집기** 대화 상자에서 **확인**을 클릭 합니다.  
  
6. **ReceiveRequest** 및 **sendresponse** 활동을 선택 하 고 삭제 합니다.  
  
7. 도구 상자에서 **Buy_ReceiveAndSendReply** 및 **Checkout_Receive** 활동을 **순차적 서비스** 활동으로 끌어 옵니다.
