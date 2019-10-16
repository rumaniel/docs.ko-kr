---
title: 편집 범위 사용
ms.date: 03/30/2017
ms.assetid: 79306f9e-318b-4687-9863-8b93d1841716
ms.openlocfilehash: 386c94e5c6761bb704efc9e48723d0e91a4aaf6b
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037795"
---
# <a name="using-editing-scope"></a>편집 범위 사용
이 샘플에서는 단일 원자 단위에서 실행 취소될 수 있도록 일련의 변경 내용을 일괄 처리하는 방법을 보여 줍니다. 기본적으로 활동 디자이너 작성자가 수행하는 동작은 실행 취소/다시 실행 시스템에 자동으로 통합됩니다.  
  
## <a name="demonstrates"></a>세부 항목  
 범위 편집과 실행 취소 및 다시 실행  
  
## <a name="discussion"></a>토론  
 이 샘플에서는 단일 작업 단위 내에서 <xref:System.Activities.Presentation.Model.ModelItem> 트리에 대한 일련의 변경 내용을 일괄 처리하는 방법을 보여 줍니다. WPF 디자이너에서 직접 <xref:System.Activities.Presentation.Model.ModelItem> 값에 바인딩할 때 변경 내용이 자동으로 적용됩니다. 이 샘플에서는 단일 변경 내용이 아닌 일괄 처리할 여러 개의 변경 내용을 명령적 코드를 통해 처리할 때 수행해야 하는 작업을 보여 줍니다.  
  
 이 샘플에서는 세 가지 활동이 추가됩니다. 편집을 시작하면 <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A>의 인스턴스에서 <xref:System.Activities.Presentation.Model.ModelItem>가 호출됩니다. 이 편집 범위 내의 <xref:System.Activities.Presentation.Model.ModelItem> 트리에 대한 변경 내용이 일괄 처리됩니다. <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A> 명령은 이 인스턴스를 제어하는 데 사용할 수 있는 <xref:System.Activities.Presentation.Model.EditingScope>를 반환합니다. <xref:System.Activities.Presentation.Model.EditingScope.OnComplete%2A> 또는 <xref:System.Activities.Presentation.Model.EditingScope.OnRevert%2A>를 호출하여 편집 범위를 커밋하거나 되돌릴 수 있습니다.  
  
 여러 개의 변경 내용 집합을 더 큰 편집 범위의 일부로 추적하고 개별적으로 제어할 수 있도록<xref:System.Activities.Presentation.Model.EditingScope> 개체를 중첩할 수도 있습니다. 이 기능을 사용할 수 있는 시나리오는 모든 변경 내용이 단일 원자 단위 작업으로 처리될 여러 대화 상자의 변경 내용을 개별적으로 커밋하거나 되돌려야 하는 경우입니다. 이 샘플에서는 편집 범위가 <xref:System.Collections.ObjectModel.ObservableCollection%601> 형식의 <xref:System.Activities.Presentation.Model.ModelEditingScope>을 사용하여 누적됩니다. 디자인 화면에서 중첩 한도를 확인할 수 있도록 <xref:System.Collections.ObjectModel.ObservableCollection%601>이 사용됩니다.  
  
## <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 샘플을 빌드하고 실행한 다음 왼쪽의 단추를 사용하여 워크플로를 수정합니다.  
  
2. **편집 범위 열기**를 클릭 합니다.  
  
    1. 이 명령은 편집 범위를 만들어 편집 스택에 푸시하는 <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A>를 호출합니다.  
  
    2. 그러면 선택한 <xref:System.Activities.Presentation.Model.ModelItem>에 세 개의 활동이 추가됩니다. <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A>를 사용하여 편집 범위를 열지 않았다면 디자이너 캔버스에 세 개의 새 활동이 나타납니다. 이 작업은 <xref:System.Activities.Presentation.Model.EditingScope> 내에서 여전히 보류 중이므로 디자이너가 아직 업데이트되지 않았습니다.  
  
3. 편집 범위 **닫기** 를 눌러 편집 범위를 커밋합니다. 그러면 디자이너에 세 개의 활동이 나타납니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\UsingEditingScope`
