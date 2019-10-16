---
title: '방법: Windows Forms ProgressBar 컨트롤에서 표시하는 값 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ProgressBar control [Windows Forms], setting value displayed
- progress controls [Windows Forms], setting value displayed
ms.assetid: 0e5010ad-1e9a-4271-895e-5a3d24d37a26
ms.openlocfilehash: 2e0134206ba3ebdce35f5374cbad575e34483d58
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956088"
---
# <a name="how-to-set-the-value-displayed-by-the-windows-forms-progressbar-control"></a>방법: Windows Forms ProgressBar 컨트롤에서 표시하는 값 설정
> [!IMPORTANT]
> <xref:System.Windows.Forms.ToolStripProgressBar> 컨트롤은 <xref:System.Windows.Forms.ProgressBar> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.ProgressBar> 컨트롤을 계속 유지하도록 선택할 수 있습니다.  
  
 .NET Framework는 <xref:System.Windows.Forms.ProgressBar> 컨트롤 내에 지정 된 값을 표시 하는 여러 가지 방법을 제공 합니다. 선택 하는 방법은 현재 작업 또는 해결 중인 문제에 따라 달라 집니다. 다음 표에서는 선택할 수 있는 방법을 보여 줍니다.  
  
|접근 방식|Description|  
|--------------|-----------------|  
|<xref:System.Windows.Forms.ProgressBar> 컨트롤의 값을 직접 설정 합니다.|이 방법은 데이터 원본에서 레코드를 읽는 것과 같이 측정 된 항목의 합계를 알고 있는 작업에 유용 합니다. 또한 값을 한 번 또는 두 번 설정 해야 하는 경우이 작업을 수행 하는 쉬운 방법입니다. 마지막으로 진행률 표시줄에 표시 되는 값을 줄여야 하는 경우이 프로세스를 사용 합니다.|  
|고정 값 <xref:System.Windows.Forms.ProgressBar> 으로 표시를 늘립니다.|이 방법은 경과 된 시간 또는 알려진 합계에서 처리 된 파일 수와 같은 최소 및 최대 사이의 단순 카운트를 표시 하는 경우에 유용 합니다.|  
|표시 되 <xref:System.Windows.Forms.ProgressBar> 는 값에 따라 표시를 늘립니다.|이 방법은 표시 된 값을 다른 값으로 변경 해야 하는 경우에 유용 합니다. 예를 들어 디스크에 일련의 파일을 쓰는 동안 소비 되는 하드 디스크 공간의 크기를 보여 줍니다.|  
  
 진행률 표시줄에 표시 되는 값을 설정 하는 가장 직접적인 방법은 속성을 <xref:System.Windows.Forms.ProgressBar.Value%2A> 설정 하는 것입니다. 디자인 타임 또는 런타임에이 작업을 수행할 수 있습니다.  
  
### <a name="to-set-the-progressbar-value-directly"></a>ProgressBar 값을 직접 설정 하려면  
  
1. 컨트롤의 <xref:System.Windows.Forms.ProgressBar> <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 및<xref:System.Windows.Forms.ProgressBar.Maximum%2A> 값을 설정 합니다.  
  
2. 코드에서 설정 된 최소값과 최대값 사이의 <xref:System.Windows.Forms.ProgressBar.Value%2A> 정수 값으로 컨트롤의 속성을 설정 합니다.  
  
    > [!NOTE]
    > <xref:System.Windows.Forms.ProgressBar.Value%2A> 속성 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 을 및 <xref:System.ArgumentException> 속성으로 설정 된 경계 밖으로 설정 하면 컨트롤이 예외를 throw 합니다. <xref:System.Windows.Forms.ProgressBar.Maximum%2A>  
  
     다음 코드 예제에서는 <xref:System.Windows.Forms.ProgressBar> 값을 직접 설정 하는 방법을 보여 줍니다. 이 코드는 데이터 소스에서 레코드를 읽고 데이터 레코드를 읽을 때마다 진행률 표시줄과 레이블을 업데이트 합니다. 이 예에서는 폼에 <xref:System.Windows.Forms.Label> 컨트롤 <xref:System.Windows.Forms.ProgressBar> , 컨트롤 및 및 `LastName` 필드가 있는 `FirstName` 라는 `CustomerRow` 행이 있는 데이터 테이블이 있어야 합니다.  
  
    ```vb  
    Public Sub CreateNewRecords()  
       ' Sets the progress bar's Maximum property to  
       ' the total number of records to be created.  
       ProgressBar1.Maximum = 20  
  
       ' Creates a new record in the dataset.  
       ' NOTE: The code below will not compile, it merely  
       ' illustrates how the progress bar would be used.  
       Dim anyRow As CustomerRow = DatasetName.ExistingTable.NewRow  
       anyRow.FirstName = "Stephen"  
       anyRow.LastName = "James"  
       ExistingTable.Rows.Add(anyRow)  
  
       ' Increases the value displayed by the progress bar.  
       ProgressBar1.Value += 1  
       ' Updates the label to show that a record was read.  
       Label1.Text = "Records Read = " & ProgressBar1.Value.ToString()  
    End Sub  
    ```  
  
    ```csharp  
    public void createNewRecords()  
    {  
       // Sets the progress bar's Maximum property to  
       // the total number of records to be created.  
       progressBar1.Maximum = 20;  
  
       // Creates a new record in the dataset.  
       // NOTE: The code below will not compile, it merely  
       // illustrates how the progress bar would be used.  
       CustomerRow anyRow = DatasetName.ExistingTable.NewRow();  
       anyRow.FirstName = "Stephen";  
       anyRow.LastName = "James";  
       ExistingTable.Rows.Add(anyRow);  
  
       // Increases the value displayed by the progress bar.  
       progressBar1.Value += 1;  
       // Updates the label to show that a record was read.  
       label1.Text = "Records Read = " + progressBar1.Value.ToString();  
    }  
    ```  
  
     일정 한 간격으로 진행 되는 진행률을 표시 하는 경우 값을 설정한 다음 해당 간격 만큼 컨트롤의 값을 <xref:System.Windows.Forms.ProgressBar> 늘리는 메서드를 호출할 수 있습니다. 이는 진행률을 전체에 대 한 비율로 측정 하지 않는 타이머 및 기타 시나리오에 유용 합니다.  
  
### <a name="to-increase-the-progress-bar-by-a-fixed-value"></a>고정 값으로 진행률 표시줄을 늘리려면  
  
1. 컨트롤의 <xref:System.Windows.Forms.ProgressBar> <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 및<xref:System.Windows.Forms.ProgressBar.Maximum%2A> 값을 설정 합니다.  
  
2. 컨트롤의 <xref:System.Windows.Forms.ProgressBar.Step%2A> 속성을 진행률 표시줄에 표시 되는 값을 늘릴 크기를 나타내는 정수로 설정 합니다.  
  
3. 메서드를 <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> 호출 하 여 <xref:System.Windows.Forms.ProgressBar.Step%2A> 속성에 설정 된 양만큼 표시 되는 값을 변경 합니다.  
  
     다음 코드 예제에서는 진행률 표시줄이 복사 작업에서 파일 수를 유지 관리 하는 방법을 보여 줍니다.  
  
     다음 예제에서는 각 파일을 메모리로 읽어 온 총 파일 수를 반영 하도록 진행률 표시줄과 레이블이 업데이트 됩니다. 이 예제에서는 폼 <xref:System.Windows.Forms.Label> 에 컨트롤과 <xref:System.Windows.Forms.ProgressBar> 컨트롤이 있어야 합니다.  
  
    ```vb  
    Public Sub LoadFiles()  
       ' Sets the progress bar's minimum value to a number representing  
       ' no operations complete -- in this case, no files read.  
       ProgressBar1.Minimum = 0  
       ' Sets the progress bar's maximum value to a number representing  
       ' all operations complete -- in this case, all five files read.  
       ProgressBar1.Maximum = 5  
       ' Sets the Step property to amount to increase with each iteration.  
       ' In this case, it will increase by one with every file read.  
       ProgressBar1.Step = 1  
  
       ' Dimensions a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be copied into memory,  
       ' so the loop will execute 5 times.  
       For i = 0 To 4  
          ' Insert code to copy a file  
          ProgressBar1.PerformStep()  
          ' Update the label to show that a file was read.  
          Label1.Text = "# of Files Read = " & ProgressBar1.Value.ToString  
       Next i  
    End Sub  
    ```  
  
    ```csharp  
    public void loadFiles()  
    {  
       // Sets the progress bar's minimum value to a number representing  
       // no operations complete -- in this case, no files read.  
       progressBar1.Minimum = 0;  
       // Sets the progress bar's maximum value to a number representing  
       // all operations complete -- in this case, all five files read.  
       progressBar1.Maximum = 5;  
       // Sets the Step property to amount to increase with each iteration.  
       // In this case, it will increase by one with every file read.  
       progressBar1.Step = 1;  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be copied into memory,  
       // so the loop will execute 5 times.  
       for (int i = 0; i <= 4; i++)  
       {  
          // Inserts code to copy a file  
          progressBar1.PerformStep();  
          // Updates the label to show that a file was read.  
          label1.Text = "# of Files Read = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
     마지막으로 각 증가가 고유한 금액이 되도록 진행률 표시줄에 표시 되는 값을 늘릴 수 있습니다. 이 방법은 하드 디스크에 다양 한 크기의 파일을 기록 하거나 전체에 대 한 비율로 진행률을 측정 하는 등의 일련의 고유한 작업을 추적 하는 경우에 유용 합니다.  
  
### <a name="to-increase-the-progress-bar-by-a-dynamic-value"></a>동적 값으로 진행률 표시줄을 늘리려면  
  
1. 컨트롤의 <xref:System.Windows.Forms.ProgressBar> <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 및<xref:System.Windows.Forms.ProgressBar.Maximum%2A> 값을 설정 합니다.  
  
2. 지정한 정수로 <xref:System.Windows.Forms.ProgressBar.Increment%2A> 표시 되는 값을 변경 하려면 메서드를 호출 합니다.  
  
     다음 코드 예제에서는 진행률 표시줄이 복사 작업 중에 사용 된 디스크 공간 크기를 계산 하는 방법을 보여 줍니다.  
  
     다음 예제에서 각 파일이 하드 디스크에 기록 되 면 사용 가능한 하드 디스크 공간 크기를 반영 하도록 진행률 표시줄과 레이블이 업데이트 됩니다. 이 예제에서는 폼 <xref:System.Windows.Forms.Label> 에 컨트롤과 <xref:System.Windows.Forms.ProgressBar> 컨트롤이 있어야 합니다.  
  
    ```vb  
    Public Sub ReadFiles()  
       ' Sets the progress bar's minimum value to a number   
       ' representing the hard disk space before the files are read in.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example and  
       ' will not compile.  
       ProgressBar1.Minimum = AvailableDiskSpace()  
       ' Sets the progress bar's maximum value to a number   
       ' representing the total hard disk space.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example   
       ' and will not compile.  
       ProgressBar1.Maximum = TotalDiskSpace()  
  
       ' Dimension a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be written to the disk,  
       ' so it will execute the loop 5 times.  
       For i = 1 To 5  
          ' Insert code to read a file into memory and update file size.  
          ' Increases the progress bar's value based on the size of   
          ' the file currently being written.  
          ProgressBar1.Increment(FileSize)  
          ' Updates the label to show available drive space.  
          Label1.Text = "Current Disk Space Used = " &_   
          ProgressBar1.Value.ToString()  
       Next i  
    End Sub  
    ```  
  
    ```csharp  
    public void readFiles()  
    {  
       // Sets the progress bar's minimum value to a number   
       // representing the hard disk space before the files are read in.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example and   
       // will not compile.  
       progressBar1.Minimum = AvailableDiskSpace();  
       // Sets the progress bar's maximum value to a number   
       // representing the total hard disk space.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example   
       // and will not compile.  
       progressBar1.Maximum = TotalDiskSpace();  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be written  
       // to the disk, so it will execute the loop 5 times.  
       for (int i = 1; i<= 5; i++)  
       {  
          // Insert code to read a file into memory and update file size.  
          // Increases the progress bar's value based on the size of   
          // the file currently being written.  
          progressBar1.Increment(FileSize);  
          // Updates the label to show available drive space.  
          label1.Text = "Current Disk Space Used = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ProgressBar>
- <xref:System.Windows.Forms.ToolStripProgressBar>
- [ProgressBar 컨트롤 개요](progressbar-control-overview-windows-forms.md)
- [ProgressBar 컨트롤](progressbar-control-windows-forms.md)
