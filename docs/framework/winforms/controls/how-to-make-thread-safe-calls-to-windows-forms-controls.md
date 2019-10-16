---
title: '방법: Windows Forms 컨트롤을 스레드로부터 안전 하 게 호출 합니다.'
ms.date: 02/19/2019
dev_langs:
- csharp
- vb
f1_keywords:
- EHInvalidOperation.WinForms.IllegalCrossThreadCall
helpviewer_keywords:
- thread safety [Windows Forms], calling controls [Windows Forms]
- calling controls [Windows Forms], thread safety [Windows Forms]
- CheckForIllegalCrossThreadCalls property [Windows Forms]
- Windows Forms controls [Windows Forms], multithreading
- BackgroundWorker class [Windows Forms], examples
- threading [Windows Forms], cross-thread calls
- controls [Windows Forms], multithreading
ms.assetid: 138f38b6-1099-4fd5-910c-390b41cbad35
ms.openlocfilehash: 78ad7b16d5220972a61848c0c80cd884afa842d9
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928613"
---
# <a name="how-to-make-thread-safe-calls-to-windows-forms-controls"></a>방법: Windows Forms 컨트롤을 스레드로부터 안전 하 게 호출 합니다.

다중 스레딩을 사용 하면 Windows Forms 앱의 성능을 향상 시킬 수 있지만 Windows Forms 컨트롤에 대 한 액세스는 기본적으로 스레드로부터 안전 하지 않습니다. 다중 스레딩을 통해 코드를 매우 심각 하 고 복잡 한 버그에 노출할 수 있습니다. 컨트롤을 조작 하는 두 개 이상의 스레드가 컨트롤을 일관 되지 않은 상태로 강제 적용 하 여 경합 상태, 교착 상태, 중단 또는 중단을 초래할 수 있습니다. 응용 프로그램에서 다중 스레딩을 구현 하는 경우에는 스레드로부터 안전한 방식으로 크로스 스레드 컨트롤을 호출 해야 합니다. 자세한 내용은 [관리 되는 스레딩 모범 사례](../../../standard/threading/managed-threading-best-practices.md)를 참조 하세요. 

해당 컨트롤을 만들지 않은 스레드에서 Windows Forms 제어를 안전 하 게 호출 하는 방법에는 두 가지가 있습니다. <xref:System.Windows.Forms.Control.Invoke%2A?displayProperty=fullName> 메서드를 사용 하 여 주 스레드에서 만든 대리자를 호출할 수 있습니다. 그러면이 대리자가 컨트롤을 호출 합니다. 또는 이벤트 기반 모델을 사용 <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>하 여 백그라운드 스레드에서 수행 된 작업을 결과에 대 한 보고에서 분리 하는를 구현할 수 있습니다. 

## <a name="unsafe-cross-thread-calls"></a>안전 하지 않은 크로스 스레드 호출

컨트롤을 만들지 않은 스레드에서 직접 호출 하는 것은 안전 하지 않습니다. 다음 코드 조각에서는 <xref:System.Windows.Forms.TextBox?displayProperty=nameWithType> 컨트롤에 대 한 안전 하지 않은 호출을 보여 줍니다. 이벤트 `Button1_Click` 처리기는 주 스레드의 <xref:System.Windows.Forms.TextBox.Text%2A?displayProperty=nameWithType> 속성 `WriteTextUnsafe` 을 직접 설정 하는 새 스레드를 만듭니다. 

```csharp
private void Button1_Click(object sender, EventArgs e)
{
    thread2 = new Thread(new ThreadStart(WriteTextUnsafe));
    thread2.Start();
}
private void WriteTextUnsafe()
{
    textBox1.Text = "This text was set unsafely.";
}
```

```vb
Private Sub Button1_Click(ByVal sender As Object, e As EventArgs) Handles Button1.Click
    Thread2 = New Thread(New ThreadStart(AddressOf WriteTextUnsafe))
    Thread2.Start()
End Sub

Private Sub WriteTextUnsafe()
    TextBox1.Text = "This text was set unsafely."
End Sub
```

Visual Studio 디버거는 메시지, 크로스 스레드 작업이 유효 하지 않은 <xref:System.InvalidOperationException> 상태로를 발생 시켜 **이러한 안전 하지 않은 스레드 호출을 검색 합니다. "" 컨트롤이 만들어진 스레드가 아닌 스레드에서 액세스 되었습니다.** 는 <xref:System.InvalidOperationException> Visual Studio 디버깅 중 안전 하지 않은 크로스 스레드 호출에 대해 항상 발생 하며, 앱 런타임에서 발생할 수 있습니다. 문제를 해결 해야 하지만 <xref:System.Windows.Forms.Control.CheckForIllegalCrossThreadCalls%2A?displayProperty=nameWithType> 속성을로 `false`설정 하 여 예외를 비활성화할 수 있습니다.

## <a name="safe-cross-thread-calls"></a>안전한 크로스 스레드 호출 

다음 코드 예제에서는 코드를 만들지 않은 스레드에서 Windows Forms 제어를 안전 하 게 호출 하는 두 가지 방법을 보여 줍니다. 

1. 컨트롤을 호출 하기 위해 주 스레드에서 대리자를 호출 하는 메서드입니다.<xref:System.Windows.Forms.Control.Invoke%2A?displayProperty=fullName> 
2. 이벤트 기반 모델을 제공 하는 구성요소입니다.<xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType> 

두 예제에서 백그라운드 스레드는 1 초 동안 대기 하 여 해당 스레드에서 수행 되는 작업을 시뮬레이션 합니다. 

C# 또는 Visual Basic 명령줄에서 .NET Framework 앱으로 이러한 예제를 빌드하고 실행할 수 있습니다. 자세한 내용은 [csc.exe를 사용한 명령줄 빌드](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md) 또는 [명령줄에서 빌드 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)를 참조 하세요. 

.Net core 3.0부터 .net core Windows Forms  *\<폴더 이름 > .csproj* 프로젝트 파일을 포함 하는 폴더에서 Windows .net core 앱으로 예제를 빌드하고 실행할 수도 있습니다. 

## <a name="example-use-the-invoke-method-with-a-delegate"></a>예제: 대리자와 함께 Invoke 메서드 사용

다음 예제에서는 Windows Forms 컨트롤을 스레드로부터 안전 하 게 호출 하는 패턴을 보여 줍니다. 이 메서드는 <xref:System.Windows.Forms.Control.InvokeRequired%2A?displayProperty=fullName> 컨트롤의 스레드 id를 호출 하는 스레드 id와 비교 하는 속성을 쿼리 합니다. 스레드 Id가 동일 하면 컨트롤을 직접 호출 합니다. 스레드 id가 다른 경우에는 기본 스레드에서 대리자 <xref:System.Windows.Forms.Control.Invoke%2A?displayProperty=nameWithType> 를 사용 하 여 메서드를 호출 합니다. 그러면이 메서드는 컨트롤에 대 한 실제 호출을 수행 합니다.

는 `SafeCallDelegate` 컨트롤 <xref:System.Windows.Forms.TextBox> 의<xref:System.Windows.Forms.TextBox.Text%2A> 속성을 설정할 수 있습니다. `WriteTextSafe` 메서드 쿼리입니다<xref:System.Windows.Forms.Control.InvokeRequired%2A>. <xref:System.Windows.Forms.Control.InvokeRequired%2A> `true` `SafeCallDelegate` 가 를반환하는경우를메서드에전달하여컨트롤에대한실제호출을수행합니다.`WriteTextSafe` <xref:System.Windows.Forms.Control.Invoke%2A> 가 <xref:System.Windows.Forms.Control.InvokeRequired%2A> 를 `false`반환 `WriteTextSafe` 하면를 <xref:System.Windows.Forms.TextBox.Text%2A?displayProperty=nameWithType> 직접 설정 합니다. 이벤트 처리기는 새 스레드를 만들고 메서드를 `WriteTextSafe` 실행 합니다. `Button1_Click` 

 [!code-csharp[ThreadSafeCalls#1](~/samples/snippets/winforms/thread-safe/example1/cs/Form1.cs)]
 [!code-vb[ThreadSafeCalls#1](~/samples/snippets/winforms/thread-safe/example1/vb/Form1.vb)]  

## <a name="example-use-a-backgroundworker-event-handler"></a>예제: BackgroundWorker 이벤트 처리기 사용

다중 스레딩을 구현 하는 쉬운 방법은 이벤트 구동 <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType> 모델을 사용 하는 구성 요소를 사용 하는 것입니다. 백그라운드 스레드는 주 스레드와 <xref:System.ComponentModel.BackgroundWorker.DoWork?displayProperty=nameWithType> 상호 작용 하지 않는 이벤트를 실행 합니다. 주 스레드는 주 스레드의 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged?displayProperty=nameWithType> 컨트롤 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted?displayProperty=nameWithType> 을 호출할 수 있는 및 이벤트 처리기를 실행 합니다.

를 사용 <xref:System.ComponentModel.BackgroundWorker>하 여 스레드로부터 안전한 호출을 수행 하려면 백그라운드 스레드에서 작업을 수행 하는 메서드를 만들어 <xref:System.ComponentModel.BackgroundWorker.DoWork> 이벤트에 바인딩합니다. 주 스레드에 다른 메서드를 만들어 백그라운드 작업의 결과를 보고 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 하거나 또는 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 이벤트에 바인딩합니다. 백그라운드 스레드를 시작 하려면를 호출 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A?displayProperty=nameWithType>합니다. 

이 예제에서는 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> 이벤트 처리기를 사용 하 여 <xref:System.Windows.Forms.TextBox> 컨트롤의 <xref:System.Windows.Forms.TextBox.Text%2A> 속성을 설정 합니다. 이벤트를 사용 하는 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 예제는를 <xref:System.ComponentModel.BackgroundWorker>참조 하십시오. 

 [!code-csharp[ThreadSafeCalls#2](~/samples/snippets/winforms/thread-safe/example2/cs/Form1.cs)]
 [!code-vb[ThreadSafeCalls#2](~/samples/snippets/winforms/thread-safe/example2/vb/Form1.vb)]  

## <a name="see-also"></a>참고자료

- <xref:System.ComponentModel.BackgroundWorker>
- [방법: 백그라운드에서 작업 실행](how-to-run-an-operation-in-the-background.md)
- [방법: 백그라운드 작업을 사용 하는 폼 구현](how-to-implement-a-form-that-uses-a-background-operation.md)
- [.NET Framework를 사용 하 여 사용자 지정 Windows Forms 컨트롤 개발](developing-custom-windows-forms-controls.md)
