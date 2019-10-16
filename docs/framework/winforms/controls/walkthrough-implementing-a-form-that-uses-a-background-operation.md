---
title: '연습: 백그라운드 작업을 사용하는 양식 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [Windows Forms], forms
- BackgroundWorker component
- background tasks
- forms [Windows Forms], multithreading
- threading [Windows Forms], walkthroughs
- forms [Windows Forms], background operations
- threading [Windows Forms], background operations
- background operations
ms.assetid: 4691b796-9200-471a-89c3-ba4c7cc78c03
ms.openlocfilehash: 60421d6ba634bd7b4107f1c9998fbbe158417c83
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66423842"
---
# <a name="walkthrough-implementing-a-form-that-uses-a-background-operation"></a>연습: 백그라운드 작업을 사용하는 양식 구현

를 완료 하려면 시간이 오래 걸리는 작업을 해야 하 고 원하지 않는 사용자 인터페이스 (UI) 응답을 중지 하거나 차단 하도록을 사용할 수는 <xref:System.ComponentModel.BackgroundWorker> 다른 스레드에서 작업을 실행 하는 클래스입니다.

이 연습에 사용 하는 방법을 보여 줍니다는 <xref:System.ComponentModel.BackgroundWorker> "백그라운드"에서 시간이 오래 걸리는 계산을 수행 하는 클래스 사용자 인터페이스의 응답성을 유지 하는 동안.  완료하면 피보나치 수를 비동기적으로 계산하는 애플리케이션이 생깁니다. 큰 피보나치 수를 계산하는 데는 상당한 시간이 걸릴 수도 있지만 이 지연으로 주 UI 스레드가 중단되지 않으며 계산 중에도 폼이 응답하게 됩니다.

이 연습에서 설명하는 작업은 다음과 같습니다.

- Windows 기반 애플리케이션 만들기

- 만들기는 <xref:System.ComponentModel.BackgroundWorker> 폼에서

- 비동기 이벤트 처리기 추가

- 진행률 보고 및 취소에 대한 지원 추가

이 예제에서 사용 되는 코드의 전체 목록은 참조 하세요. [방법: 백그라운드 작업을 사용 하는 폼 구현](how-to-implement-a-form-that-uses-a-background-operation.md)합니다.

## <a name="create-a-form-that-uses-a-background-operation"></a>백그라운드 작업을 사용 하는 폼 만들기

1. Visual Studio에서 이라는 Windows 기반 응용 프로그램 프로젝트를 만듭니다 `BackgroundWorkerExample` (**파일** > **New** > **프로젝트**  >  **시각적 C#**  하거나 **Visual Basic** > **클래식 데스크톱** > **Windows Forms 응용 프로그램**).

2. **솔루션 탐색기**에서 **Form1**을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **이름 바꾸기**를 선택합니다. 파일 이름을 `FibonacciCalculator`로 변경합니다. 코드 요소 '`Form1`'에 대한 모든 참조 이름을 변경할지 묻는 메시지가 표시되면 **예** 단추를 클릭합니다.

3. 끌어서를 <xref:System.Windows.Forms.NumericUpDown> 에서 제어 합니다 **도구 상자** 폼입니다. 설정 된 <xref:System.Windows.Forms.NumericUpDown.Minimum%2A> 속성을 `1` 하며 <xref:System.Windows.Forms.NumericUpDown.Maximum%2A> 속성을 `91`입니다.

4. 두 개의 추가 <xref:System.Windows.Forms.Button> 폼에 컨트롤을 합니다.

5. 첫 번째 이름 바꾸기 <xref:System.Windows.Forms.Button> 제어 `startAsyncButton` 설정 된 <xref:System.Windows.Forms.Control.Text%2A> 속성을 `Start Async`입니다. 두 번째 이름을 바꿀 <xref:System.Windows.Forms.Button> 컨트롤 `cancelAsyncButton`를 설정 합니다 <xref:System.Windows.Forms.Control.Text%2A> 속성을 `Cancel Async`합니다. 설정 해당 <xref:System.Windows.Forms.Control.Enabled%2A> 속성을 `false`입니다.

6. 둘 다에 대해 이벤트 처리기를 만들고 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Click> 이벤트입니다. 자세한 내용은 [방법: 디자이너를 사용 하 여 이벤트 처리기를 만들](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/zwwsdtbk(v=vs.100))합니다.

7. 끌어서를 <xref:System.Windows.Forms.Label> 에서 제어 합니다 **도구 상자** 폼 하 고 이름을 `resultLabel`입니다.

8. 끌어서를 <xref:System.Windows.Forms.ProgressBar> 에서 제어 합니다 **도구 상자** 폼입니다.

## <a name="create-a-backgroundworker-with-the-designer"></a>디자이너로 BackgroundWorker를 만들려면

만들 수 있습니다 합니다 <xref:System.ComponentModel.BackgroundWorker> 를 사용 하 여 비동기 작업에는 **Windows** **Forms 디자이너**합니다.

**구성 요소** 탭을 **도구 상자**를 끌어를 <xref:System.ComponentModel.BackgroundWorker> 폼에.

## <a name="add-asynchronous-event-handlers"></a>비동기 이벤트 처리기를 추가 합니다.

에 대 한 이벤트 처리기를 추가할 준비가 된 <xref:System.ComponentModel.BackgroundWorker> 구성 요소의 비동기 이벤트입니다. 백그라운드로 실행되는 시간이 많이 소요되는 작업(예: 피보나치 수 계산)은 이러한 이벤트 처리기 중 하나에 의해 호출됩니다.

1. 에 **속성** 창 사용 하 여를 <xref:System.ComponentModel.BackgroundWorker> 구성 요소가 여전히 선택를 클릭 합니다 **이벤트** 단추. 두 번 클릭 합니다 <xref:System.ComponentModel.BackgroundWorker.DoWork> 및 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 이벤트를 이벤트 처리기를 만듭니다. 이벤트 처리기를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 디자이너를 사용 하 여 이벤트 처리기를 만들](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/zwwsdtbk(v=vs.100))합니다.

2. 사용자 폼에서 `ComputeFibonacci`라는 새 메서드를 만듭니다. 이 메서드는 실제 작업을 수행하며 백그라운드에서 실행됩니다. 이 코드는 피보나치 알고리즘의 재귀적 구현을 보여 줍니다. 이는 매우 비효율적이며, 큰 숫자를 완성하는 데 기하급수적으로 긴 시간이 소요됩니다. 여기서는 애플리케이션에서 오랜 지연을 유발할 수 있는 작업을 보여 주기 위해 설명 용도로 사용됩니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#10)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#10)]
     [!code-vb[System.ComponentModel.BackgroundWorker#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#10)]

3. 에 <xref:System.ComponentModel.BackgroundWorker.DoWork> 이벤트 처리기 호출을 추가 합니다 `ComputeFibonacci` 메서드. 에 대 한 첫 번째 매개 변수를 사용 `ComputeFibonacci` 에서 합니다 <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> 의 속성을 <xref:System.ComponentModel.DoWorkEventArgs>입니다. <xref:System.ComponentModel.BackgroundWorker> 및 <xref:System.ComponentModel.DoWorkEventArgs> 매개 변수는 나중에 사용할 진행률 보고 및 취소를 지원 합니다. 반환 값을 할당 `ComputeFibonacci` 에 <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> 의 속성을 <xref:System.ComponentModel.DoWorkEventArgs>. 이 결과 사용할 수 있습니다는 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 이벤트 처리기입니다.

    > [!NOTE]
    > 합니다 <xref:System.ComponentModel.BackgroundWorker.DoWork> 이벤트 처리기를 참조 하지 않습니다 합니다 `backgroundWorker1` 인스턴스 변수를 직접이 이벤트 처리기의 특정 인스턴스에 결합은이 처럼 <xref:System.ComponentModel.BackgroundWorker>합니다. 대신에 대 한 참조를 <xref:System.ComponentModel.BackgroundWorker> 이 발생 하는 이벤트에서 복구 되는 `sender` 매개 변수입니다. 둘 이상의 폼 호스트 하는 경우이 중요 <xref:System.ComponentModel.BackgroundWorker>합니다. 사용자 인터페이스 개체를 조작 하지 않아야 이기도 하 <xref:System.ComponentModel.BackgroundWorker.DoWork> 이벤트 처리기입니다. 대신, 사용자 인터페이스를 통해 통신 합니다 <xref:System.ComponentModel.BackgroundWorker> 이벤트입니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]

4. 에 `startAsyncButton` 컨트롤의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기에서 비동기 작업을 시작 하는 코드를 추가 합니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#13](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#13)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#13](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#13)]
     [!code-vb[System.ComponentModel.BackgroundWorker#13](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#13)]

5. 에 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 이벤트 처리기를 계산의 결과 할당 합니다 `resultLabel` 컨트롤.

     [!code-cpp[System.ComponentModel.BackgroundWorker#6](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#6)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#6)]

## <a name="adding-progress-reporting-and-support-for-cancellation"></a>진행률 보고 및 취소에 대한 지원 추가

시간이 오래 소요되는 비동기 작업의 경우 사용자에게 진행률을 보고하고 사용자가 작업을 취소하도록 할 수 있습니다. <xref:System.ComponentModel.BackgroundWorker> 클래스에 백그라운드 작업이 수행 될 때 진행률을 게시할 수 있는 이벤트를 제공 합니다. 또한 작업자 코드에 대 한 호출을 검색할 수 있는 플래그가 제공 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 자체를 방해 합니다.

### <a name="implement-progress-reporting"></a>진행률 보고를 구현 합니다.

1. **속성** 창에서 `backgroundWorker1`을 선택합니다. 설정 된 <xref:System.ComponentModel.BackgroundWorker.WorkerReportsProgress%2A> 하 고 <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> 속성을 `true`입니다.

2. `FibonacciCalculator` 폼에서 변수 두 개를 선언합니다. 진행률을 추적하는 데 사용됩니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#14](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#14)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#14](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#14)]
     [!code-vb[System.ComponentModel.BackgroundWorker#14](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#14)]

3. <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 이벤트에 대한 이벤트 처리기를 추가합니다. 에 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 이벤트 처리기, 업데이트를 <xref:System.Windows.Forms.ProgressBar> 사용 하 여를 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> 의 속성을 <xref:System.ComponentModel.ProgressChangedEventArgs> 매개 변수입니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#7](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#7)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#7)]

### <a name="implement-support-for-cancellation"></a>취소에 대 한 구현 지원

1. 에 `cancelAsyncButton` 컨트롤의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기에서 비동기 작업을 취소 하는 코드를 추가 합니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#4)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#4)]

2. `ComputeFibonacci` 메서드의 다음 코드 조각은 진행률을 보고하고 취소를 지원합니다.

     [!code-cpp[System.ComponentModel.BackgroundWorker#11](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#11)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#11)]
     [!code-vb[System.ComponentModel.BackgroundWorker#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#11)]
    [!code-cpp[System.ComponentModel.BackgroundWorker#12](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#12)]
    [!code-csharp[System.ComponentModel.BackgroundWorker#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#12)]
    [!code-vb[System.ComponentModel.BackgroundWorker#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#12)]

## <a name="checkpoint"></a>검사점

이 시점에서 피보나치 계산기 애플리케이션을 컴파일하여 실행할 수 있습니다.

키를 눌러 **F5** 를 컴파일하고 응용 프로그램을 실행 합니다.

계산 백그라운드에서 실행 되는 동안 표시 됩니다는 <xref:System.Windows.Forms.ProgressBar> 완료 될 때까지 계산 진행률이 표시 됩니다. 보류 중인 작업도 취소할 수 있습니다.

작은 숫자에 대한 계산은 매우 빠르지만 큰 수에 대한 계산은 상당한 지연이 나타납니다. 값을 30 이상 입력하면 컴퓨터 속도에 따라 몇 초의 지연이 나타납니다. 값이 40을 넘으면 계산을 완료하는 데 몇 분 또는 몇 시간이 소요될 수 있습니다. 계산기가 큰 피보나치 수를 계산하는 동안 폼을 자유롭게 움직이고, 최소화 및 최대화하며, 해제할 수도 있습니다. 주 UI 스레드가 계산이 완료되기를 기다리지 않기 때문입니다.

## <a name="next-steps"></a>다음 단계

사용 하는 폼 구현 했으므로 <xref:System.ComponentModel.BackgroundWorker> 백그라운드에서 계산을 실행 하는 구성 요소가 비동기 작업에 대 한 다른 가능성을 살펴볼 수 있습니다.

- 사용 하 여 <xref:System.ComponentModel.BackgroundWorker> 여러 동시 작업에 대 한 개체입니다.

- 다중 스레드 응용 프로그램을 디버깅 하려면 참조 [방법: 스레드 창 사용](/visualstudio/debugger/how-to-use-the-threads-window)합니다.

- 비동기 프로그래밍 모델을 지원하는 사용자 고유의 구성 요소를 구현합니다. 자세한 내용은 [이벤트 기반 비동기 패턴 개요](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)를 참조하세요.

    > [!CAUTION]
    > 모든 종류의 다중 스레딩을 사용할 때는 매우 심각하고 복잡한 버그에 잠재적으로 노출됩니다. 다중 스레딩을 사용하는 솔루션을 구현하기 전에 [관리되는 스레딩을 구현하는 최선의 방법](../../../standard/threading/managed-threading-best-practices.md)을 참조하세요.

## <a name="see-also"></a>참고자료

- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- [관리되는 스레딩](../../../standard/threading/index.md)
- [관리되는 스레딩을 구현하는 최선의 방법](../../../standard/threading/managed-threading-best-practices.md)
- [이벤트 기반 비동기 패턴 개요](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
- [방법: 백그라운드 작업을 사용하는 양식 구현](how-to-implement-a-form-that-uses-a-background-operation.md)
- [연습: 백그라운드에서 작업 실행](walkthrough-running-an-operation-in-the-background.md)
- [BackgroundWorker 구성 요소](backgroundworker-component.md)
