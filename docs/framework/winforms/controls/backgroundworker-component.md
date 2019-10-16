---
title: BackgroundWorker 구성 요소
ms.date: 03/30/2017
helpviewer_keywords:
- BackgroundWorker component
- background tasks
- Asynchronous Pattern
- forms [Windows Forms], multithreading
- components [Windows Forms], asynchronous
- forms [Windows Forms], background operations
- threading [Windows Forms], background operations
- background operations
ms.assetid: bef7b0ab-ce57-475a-a2d6-fb8a702a9417
ms.openlocfilehash: 0baf54d27cf33eef7e4df7019ee98b42eba40205
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011803"
---
# <a name="backgroundworker-component"></a>BackgroundWorker 구성 요소
`BackgroundWorker` 양식이 나 컨트롤 작업을 비동기적으로 실행 하려면 구성 요소에 사용 하도록 설정 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [BackgroundWorker 구성 요소 개요](backgroundworker-component-overview.md)  
 에 대해 설명 합니다 `BackgroundWorker` 응용 프로그램의 주 UI 스레드가 아닌 다른 스레드에서 비동기적으로 ("백그라운드에서") 시간이 오래 걸리는 작업을 실행 하는 기능을 제공 하는 구성 요소입니다.  
  
 [연습: 백그라운드에서 작업 실행](walkthrough-running-an-operation-in-the-background.md)  
 사용 하는 방법에 설명 합니다 `BackgroundWorker` 별도 스레드에서 시간이 많이 걸리는 작업을 실행 하려면 디자이너에서 구성 요소입니다.  
  
 [방법: 백그라운드에서 작업 실행](how-to-run-an-operation-in-the-background.md)  
 사용 하는 방법에 설명 합니다 `BackgroundWorker` 구성 요소가 별도 스레드에서 시간이 많이 걸리는 작업을 실행 합니다.  
  
 [연습: 백그라운드 작업을 사용 하는 폼 구현](walkthrough-implementing-a-form-that-uses-a-background-operation.md)  
 수학적 계산을 비동기적으로 수행 하는 디자이너를 사용 하 여 응용 프로그램을 만듭니다.  
  
 [방법: 백그라운드 작업을 사용하는 양식 구현](how-to-implement-a-form-that-uses-a-background-operation.md)  
 수학적 계산을 비동기적으로 수행 하는 응용 프로그램을 만듭니다.  
  
 [방법: 백그라운드에서 파일 다운로드](how-to-download-a-file-in-the-background.md)  
 사용 하는 방법에 설명 합니다 `BackgroundWorker` 별도 스레드에서 파일을 다운로드 하는 구성 요소입니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ComponentModel.BackgroundWorker>  
 이 클래스를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
 <xref:System.ComponentModel.RunWorkerCompletedEventArgs>  
 에 대 한 데이터를 보유 하는 형식을 설명 합니다 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 이벤트입니다.  
  
 <xref:System.ComponentModel.ProgressChangedEventArgs>  
 에 대 한 데이터를 보유 하는 형식을 설명 합니다 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 이벤트입니다.  
  
## <a name="related-sections"></a>관련 단원  
 [이벤트 기반 비동기 패턴 개요](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 어떻게 비동기 패턴을 통해 사용할 수 있는 다중 스레드 응용 프로그램의 장점을 많은 복잡 한 다중 스레드 디자인에 내재 된 문제를 숨기면 설명 합니다.
