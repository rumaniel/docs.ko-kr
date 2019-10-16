---
title: '방법: 명령줄에서 Windows Forms 응용 프로그램 만들기'
ms.date: 03/14/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, application development from command line
- Windows Forms, getting started
- Windows Forms, creating basic form
ms.assetid: 45ad3f8b-1c26-4c9f-91a9-3bb0759a47a4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da7fdab1cf67ffd47acb75533fcfdb89664c86d3
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834817"
---
# <a name="how-to-create-a-windows-forms-application-from-the-command-line"></a>방법: 명령줄에서 Windows Forms 응용 프로그램 만들기

다음 절차에서는 명령줄에서 Windows Forms 애플리케이션을 만들고 실행하기 위해 완료해야 하는 기본 단계를 설명합니다. Visual Studio에서는 이러한 절차가 광범위하게 지원됩니다.  [또한 연습: WPF](../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)에서 Windows Forms 컨트롤 호스팅.
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-create-the-form"></a>폼을 만들려면  
  
1. 빈 코드 파일에 다음 `Imports` 또는 `using` 문을 입력 합니다.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BasicForm#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#2)]  
  
2. Form 클래스에서 상속 되는 `Form1` 이라는 클래스를 선언 합니다.
  
     [!code-csharp[System.Windows.Forms.BasicForm#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BasicForm#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#3)]  
  
3. 에 대해 `Form1`매개 변수가 없는 생성자를 만듭니다.
  
     이후 절차에서 생성자에 더 많은 코드를 추가합니다.
  
     [!code-csharp[System.Windows.Forms.BasicForm#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.BasicForm#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#4)]  
  
4. 클래스에 `Main` 메서드를 추가합니다.
  
    1. C# 하 여 Windows Forms 응용 프로그램이 단일 스레드 아파트 인지 지정 합니다. `Main` <xref:System.STAThreadAttribute> (Visual Basic를 사용 하 여 개발 된 Windows forms 응용 프로그램은 기본적으로 단일 스레드 아파트 모델을 사용 하므로 Visual Basic에서는이 특성이 필요 하지 않습니다.)  
  
    2. 을 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 호출 하 여 응용 프로그램에 운영 체제 스타일을 적용 합니다.  
  
    3. 폼 인스턴스를 만들고 실행합니다.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.BasicForm#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#5)]  
  
#### <a name="to-compile-and-run-the-application"></a>애플리케이션을 컴파일하고 실행하려면  
  
1. .NET Framework 명령 프롬프트에서 `Form1` 클래스를 만든 디렉터리로 이동합니다.  
  
2. 폼을 컴파일합니다.  
  
    - 을 사용 C#하는 경우 다음을 입력 합니다.`csc form1.cs`  
  
         `-or-`  
  
    - Visual Basic를 사용 하는 경우 다음을 입력 합니다.`vbc form1.vb`  
  
3. 명령 프롬프트에서 다음을 입력 합니다.`Form1.exe`  
  
## <a name="adding-a-control-and-handling-an-event"></a>컨트롤 추가 및 이벤트 처리

이전 절차의 단계에서는 컴파일 및 실행되는 기본 Windows Form을 만드는 방법만 보여 주었습니다. 다음 절차에서는 컨트롤을 만들고 폼에 추가한 다음 컨트롤에 대한 이벤트를 처리하는 방법을 보여 줍니다. Windows Forms에 추가할 수 있는 컨트롤에 대 한 자세한 내용은 [Windows Forms 컨트롤](./controls/index.md)을 참조 하세요.
  
 Windows Forms 애플리케이션을 만드는 방법을 이해하는 것은 물론 이벤트 기반 프로그래밍 및 사용자 입력을 처리하는 방법도 이해해야 합니다. 자세한 내용은 [Windows Forms에서 이벤트 처리기 만들기](creating-event-handlers-in-windows-forms.md)및 [사용자 입력 처리](./controls/handling-user-input.md) 를 참조 하세요.  
  
#### <a name="to-declare-a-button-control-and-handle-its-click-event"></a>단추 컨트롤을 선언하고 해당 click 이벤트를 처리하려면  
  
1. `button1`이라는 단추 컨트롤을 선언합니다.  
  
2. 생성자에서 단추를 만들고 해당 <xref:System.Windows.Forms.Control.Size%2A>, <xref:System.Windows.Forms.Control.Location%2A> 및 <xref:System.Windows.Forms.Control.Text%2A> 속성을 설정합니다.  
  
3. 폼에 단추를 추가합니다.  
  
     다음 코드 예제에서는 단추 컨트롤을 선언 하는 방법을 보여 줍니다.
  
     [!code-csharp[System.Windows.Forms.FormWithButton#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.FormWithButton#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#2)]  
  
4. 단추에 대한 <xref:System.Windows.Forms.Control.Click> 이벤트를 처리할 메서드를 만듭니다.  
  
5. click 이벤트 처리기에서 "Hello World" 메시지와 함께 <xref:System.Windows.Forms.MessageBox>를 표시합니다.  
  
     다음 코드 예제에서는 단추 컨트롤의 click 이벤트를 처리 하는 방법을 보여 줍니다.
  
     [!code-csharp[System.Windows.Forms.FormWithButton#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.FormWithButton#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#3)]  
  
6. 만든 메서드에 <xref:System.Windows.Forms.Control.Click> 이벤트를 연결합니다.  
  
     다음 코드 예제에서는 이벤트를 메서드에 연결하는 방법을 보여 줍니다.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.FormWithButton#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#4)]  
  
7. 이전 절차에서 설명한 대로 애플리케이션을 컴파일 및 실행합니다.  
  
## <a name="example"></a>예제  
 
다음 코드 예제는 이전 절차의 전체 예제입니다.
  
 [!code-csharp[System.Windows.Forms.FormWithButton#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.FormWithButton#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Forms.Form>
- <xref:System.Windows.Forms.Control>
- [Windows Forms의 모양 변경](changing-the-appearance-of-windows-forms.md)
- [Windows Forms 애플리케이션 강화](./advanced/index.md)
- [Windows Forms 시작](getting-started-with-windows-forms.md)
