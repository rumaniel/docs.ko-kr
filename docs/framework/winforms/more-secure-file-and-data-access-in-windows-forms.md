---
title: Windows Forms의 파일 및 데이터 액세스 추가 보안
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [Windows Forms], file access
- registry [Windows Forms]
- data access [Windows Forms]
- database access (Windows Forms security)
- data [Windows Forms], secure access
- file access [Windows Forms]
- security [Windows Forms], data access
ms.assetid: 3cd3e55b-2f5e-40dd-835d-f50f7ce08967
ms.openlocfilehash: 94b165757de636b2570798a21fd7c483264e37c5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949946"
---
# <a name="more-secure-file-and-data-access-in-windows-forms"></a>Windows Forms의 파일 및 데이터 액세스 추가 보안
.NET Framework는 사용 권한을 사용 하 여 리소스와 데이터를 보호 합니다. 애플리케이션이 데이터를 일거나 쓸 수 있는 위치는 애플리케이션에 부여된 권한에 따라 달라집니다. 애플리케이션이 부분 신뢰 환경에서 실행되는 경우 데이터에 대한 액세스 권한이 없거나 데이터에 액세스하는 방법을 변경해야 할 수 있습니다.  
  
 보안 제한이 발생할 경우 다음 두가지 옵션이 있습니다. 권한을 어설션(애플리케이션에 부여되었다고 가정)하거나 부분 신뢰에서 작동하도록 작성된 기능 버전을 사용합니다. 다음 섹션에서는 부분 신뢰 환경에서 실행 중인 애플리케이션에서 파일, 데이터베이스 및 레지스트리 액세스 작업을 수행하는 방법을 설명합니다.  
  
> [!NOTE]
> 기본적으로 ClickOnce 배포를 생성 하는 도구는 해당 배포를 실행 하는 컴퓨터에서 완전 신뢰를 요청 하는 배포를 기본적으로 수행 합니다. 부분 신뢰로 실행 되는의 보안 이점을 강화 하려면 Visual Studio 또는 Windows SDK 도구 (Mage.exe 또는 Mageui.exe) 중 하나에서이 기본값을 변경 해야 합니다. Windows Forms 보안에 대 한 자세한 내용과 응용 프로그램의 적절 한 신뢰 수준을 결정 하는 방법에 대 한 자세한 내용은 [Windows Forms 개요의 보안](security-in-windows-forms-overview.md)을 참조 하세요.  
  
## <a name="file-access"></a>파일 액세스  
 클래스 <xref:System.Security.Permissions.FileIOPermission> 는 .NET Framework에서 파일 및 폴더 액세스를 제어 합니다. 기본적으로 보안 시스템은 로컬 인트라넷 및 인터넷 영역과 같은 부분 신뢰 환경에 <xref:System.Security.Permissions.FileIOPermission>을 부여하지 않습니다. 그러나 애플리케이션의 디자인을 수정하거나 다른 메서드를 사용하여 파일에 액세스하는 경우 파일 액세스가 필요한 애플리케이션이 여전히 이러한 환경에서 작동할 수 있습니다. 기본적으로 로컬 인트라넷 영역에는 동일한 사이트 액세스 및 동일한 디렉터리 액세스를 포함하고, 원본 사이트에 다시 연결하고, 설치 디렉터리에서 읽을 수 있는 권한이 부여됩니다. 기본적으로 인터넷 영역에는 원본 사이트에 다시 연결할 수 있는 권한만 부여됩니다.  
  
### <a name="user-specified-files"></a>사용자 지정 파일  
 파일 액세스 권한 없음을 처리하는 한 가지 방법은 <xref:System.Windows.Forms.OpenFileDialog> 또는 <xref:System.Windows.Forms.SaveFileDialog> 클래스를 통해 특정 파일 정보를 제공하라는 메시지를 사용자에게 표시하는 것입니다. 이 사용자 상호 작용은 애플리케이션이 악의적으로 개인 파일을 로드하거나 중요한 파일을 덮어쓸 수 없도록 합니다. <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 및 <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> 메서드는 사용자가 지정한 파일에 대한 파일 스트림을 열어 읽기 및 쓰기 파일 액세스를 제공합니다. 메서드는 파일 경로가 표시되지 않도록 하여 사용자 파일 보호를 돕습니다.  
  
> [!NOTE]
> 이러한 권한은 애플리케이션이 인터넷 영역 또는 인트라넷 영역에 있는지에 따라 달라집니다. 인터넷 영역 애플리케이션은 <xref:System.Windows.Forms.OpenFileDialog>만 사용할 수 있는 반면 인트라넷 애플리케이션은 무제한 파일 대화 상자 권한이 있습니다.  
  
 <xref:System.Security.Permissions.FileDialogPermission> 클래스는 애플리케이션에서 사용할 수 있는 파일 형식 대화 상자를 지정합니다. 다음 표에서는 각 <xref:System.Windows.Forms.FileDialog> 클래스를 사용하는 데 필요한 값을 보여 줍니다.  
  
|클래스|필요한 액세스 값|  
|-----------|---------------------------|  
|<xref:System.Windows.Forms.OpenFileDialog>|<xref:System.Security.Permissions.FileDialogPermissionAccess.Open>|  
|<xref:System.Windows.Forms.SaveFileDialog>|<xref:System.Security.Permissions.FileDialogPermissionAccess.Save>|  
  
> [!NOTE]
> <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 메서드가 실제로 호출될 때까지 특정 권한이 요청되지 않습니다.  
  
 파일 대화 상자를 표시할 수 있는 권한은 애플리케이션에 <xref:System.Windows.Forms.FileDialog>, <xref:System.Windows.Forms.OpenFileDialog> 및 <xref:System.Windows.Forms.SaveFileDialog> 클래스의 모든 멤버에 대한 모든 권한을 부여하지 않습니다. 각 메서드를 호출 하는 데 필요한 정확한 사용 권한은 .NET Framework 클래스 라이브러리 설명서에서 해당 메서드에 대 한 참조 항목을 참조 하세요.  
  
 다음 코드 예제에서는 <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> 메서드를 사용하여 사용자 지정 파일을 <xref:System.Windows.Forms.RichTextBox> 컨트롤에 엽니다. 예제를 사용하려면 <xref:System.Security.Permissions.FileDialogPermission> 및 연결된 <xref:System.Security.Permissions.FileDialogPermissionAttribute.Open%2A> 열거형 값이 필요합니다. 예제에서는 <xref:System.Security.SecurityException>을 처리하여 저장 기능을 사용하지 않도록 설정할지 여부를 확인하는 방법을 보여 줍니다. 이 예제를 사용하려면 <xref:System.Windows.Forms.Form>에 `ButtonOpen`이라는 <xref:System.Windows.Forms.Button> 컨트롤과 `RtfBoxMain`이라는 <xref:System.Windows.Forms.RichTextBox> 컨트롤이 있어야 합니다.  
  
> [!NOTE]
> 저장 기능에 대한 프로그래밍 논리는 예제에 표시되어 있지 않습니다.  
  
```vb  
Private Sub ButtonOpen_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles ButtonOpen.Click   
  
    Dim editingFileName as String = ""  
    Dim saveAllowed As Boolean = True  
  
    ' Displays the OpenFileDialog.  
    If (OpenFileDialog1.ShowDialog() = DialogResult.OK) Then  
        Dim userStream as System.IO.Stream  
        Try   
            ' Opens the file stream for the file selected by the user.  
            userStream =OpenFileDialog1.OpenFile()   
            Me.RtfBoxMain.LoadFile(userStream, _  
                RichTextBoxStreamType.PlainText)  
        Finally  
            userStream.Close()  
        End Try  
  
        ' Tries to get the file name selected by the user.  
        ' Failure means that the application does not have  
        ' unrestricted permission to the file.  
        Try   
            editingFileName = OpenFileDialog1.FileName  
        Catch ex As Exception  
            If TypeOf ex Is System.Security.SecurityException Then   
                ' The application does not have unrestricted permission   
                ' to the file so the save feature will be disabled.  
                saveAllowed = False   
            Else   
                Throw ex  
            End If  
        End Try  
    End If  
End Sub  
```  
  
```csharp  
private void ButtonOpen_Click(object sender, System.EventArgs e)   
{  
    String editingFileName = "";  
    Boolean saveAllowed = true;  
  
    // Displays the OpenFileDialog.  
    if (openFileDialog1.ShowDialog() == DialogResult.OK)   
    {  
        // Opens the file stream for the file selected by the user.  
        using (System.IO.Stream userStream = openFileDialog1.OpenFile())   
        {  
            this.RtfBoxMain.LoadFile(userStream,  
                RichTextBoxStreamType.PlainText);  
            userStream.Close();  
        }  
  
        // Tries to get the file name selected by the user.  
        // Failure means that the application does not have  
        // unrestricted permission to the file.  
        try   
        {  
            editingFileName = openFileDialog1.FileName;  
        }   
        catch (Exception ex)   
        {  
            if (ex is System.Security.SecurityException)   
            {  
                // The application does not have unrestricted permission   
                // to the file so the save feature will be disabled.  
                saveAllowed = false;   
            }   
            else   
            {  
                throw ex;  
            }  
        }  
    }  
}  
```  
  
> [!NOTE]
> 시각적 개체 C#에서 이벤트 처리기를 사용 하도록 설정 하는 코드를 추가 해야 합니다. 이전 예제의 코드를 사용하여 다음 코드에서는 이벤트 처리기 `this.ButtonOpen.Click += newSystem.Windows.Forms.EventHandler(this.ButtonOpen_Click);`를 사용하도록 설정하는 방법을 보여 줍니다.  
  
### <a name="other-files"></a>Other Files  
 애플리케이션 설정을 유지해야 하는 경우와 같이 사용자가 지정하지 않는 파일을 읽거나 써야 하는 경우가 있습니다. 로컬 인트라넷 및 인터넷 영역에서는 로컬 파일에 데이터를 저장할 수 있는 권한이 애플리케이션에 없습니다. 그러나 애플리케이션은 격리된 스토리지에 데이터를 저장할 수 있습니다. 격리된 스토리지는 데이터가 저장된 실제 디렉터리 위치를 포함하는 하나 이상의 격리된 스토리지 파일(스토리지라고 함)이 포함된 추상 데이터 컴파트먼트(특정 스토리지 위치가 아님)입니다. <xref:System.Security.Permissions.FileIOPermission>과 같은 파일 액세스 권한은 필요하지 않습니다. 대신, <xref:System.Security.Permissions.IsolatedStoragePermission> 클래스는 격리된 스토리지에 대한 권한을 제어합니다. 기본적으로 로컬 인트라넷 및 인터넷 영역에서 실행 중인 애플리케이션은 격리된 스토리지를 사용하여 데이터를 저장할 수 있습니다. 그러나 디스크 할당량과 같은 설정이 달라질 수 있습니다. 격리 된 저장소에 대 한 자세한 내용은 [격리 된 저장소](../../standard/io/isolated-storage.md)를 참조 하세요.  
  
 다음 예제에서는 격리된 스토리지를 사용하여 스토리지에 있는 파일에 데이터를 씁니다. 예제를 사용하려면 <xref:System.Security.Permissions.IsolatedStorageFilePermission> 및 <xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByUser> 열거형 값이 필요합니다. 예제에서는 <xref:System.Windows.Forms.Button> 컨트롤의 특정 속성 값을 읽고 격리된 스토리지의 파일에 쓰는 방법을 보여 줍니다. `Read` 함수는 애플리케이션이 시작된 후에 호출되고 `Write` 함수는 애플리케이션이 종료되기 전에 호출됩니다. 이 `Read` 예제를 사용 하려면 및 `Write` 함수가 <xref:System.Windows.Forms.Button> 이라는 `MainButton`컨트롤이 포함 <xref:System.Windows.Forms.Form> 된의 멤버로 존재 해야 합니다.  
  
```vb  
' Reads the button options from the isolated storage. Uses Default values   
' for the button if the options file does not exist.  
Public Sub Read()   
    Dim isoStore As System.IO.IsolatedStorage.IsolatedStorageFile = _  
        System.IO.IsolatedStorage.IsolatedStorageFile. _   
        GetUserStoreForDomain()  
  
    Dim filename As String = "options.txt"  
    Try  
        ' Checks to see if the options.txt file exists.  
        If (isoStore.GetFileNames(filename).GetLength(0) <> 0) Then  
  
            ' Opens the file because it exists.  
            Dim isos As New System.IO.IsolatedStorage.IsolatedStorageFileStream _   
                 (filename, IO.FileMode.Open,isoStore)  
            Dim reader as System.IO.StreamReader  
            Try   
                reader = new System.IO.StreamReader(isos)  
  
                ' Reads the values stored.  
                Dim converter As System.ComponentModel.TypeConverter  
                converter = System.ComponentModel.TypeDescriptor.GetConverter _   
                    (GetType(Color))  
  
                Me.MainButton.BackColor = _   
                        CType(converter.ConvertFromString _   
                         (reader.ReadLine()), Color)  
                me.MainButton.ForeColor = _  
                        CType(converter.ConvertFromString _   
                         (reader.ReadLine()), Color)  
  
                converter = System.ComponentModel.TypeDescriptor.GetConverter _   
                    (GetType(Font))  
                me.MainButton.Font = _  
                        CType(converter.ConvertFromString _   
                         (reader.ReadLine()), Font)  
  
            Catch ex As Exception  
                Debug.WriteLine("Cannot read options " + _  
                    ex.ToString())  
            Finally  
                reader.Close()  
            End Try  
        End If  
  
    Catch ex As Exception  
        Debug.WriteLine("Cannot read options " + ex.ToString())  
    End Try  
End Sub  
  
' Writes the button options to the isolated storage.  
Public Sub Write()   
    Dim isoStore As System.IO.IsolatedStorage.IsolatedStorageFile = _  
        System.IO.IsolatedStorage.IsolatedStorageFile. _   
        GetUserStoreForDomain()  
  
    Dim filename As String = "options.txt"  
    Try   
        ' Checks if the file exists, and if it does, tries to delete it.  
        If (isoStore.GetFileNames(filename).GetLength(0) <> 0) Then  
            isoStore.DeleteFile(filename)  
        End If  
    Catch ex As Exception  
        Debug.WriteLine("Cannot delete file " + ex.ToString())  
    End Try  
  
    ' Creates the options.txt file and writes the button options to it.  
    Dim writer as System.IO.StreamWriter  
    Try   
        Dim isos As New System.IO.IsolatedStorage.IsolatedStorageFileStream _   
             (filename, IO.FileMode.CreateNew, isoStore)  
  
        writer = New System.IO.StreamWriter(isos)  
        Dim converter As System.ComponentModel.TypeConverter  
  
        converter = System.ComponentModel.TypeDescriptor.GetConverter _   
           (GetType(Color))  
        writer.WriteLine(converter.ConvertToString( _  
            Me.MainButton.BackColor))  
        writer.WriteLine(converter.ConvertToString( _  
            Me.MainButton.ForeColor))  
  
        converter = System.ComponentModel TypeDescriptor.GetConverter _   
           (GetType(Font))  
        writer.WriteLine(converter.ConvertToString( _  
            Me.MainButton.Font))  
  
    Catch ex as Exception  
        Debug.WriteLine("Cannot write options " + ex.ToString())  
  
    Finally  
        writer.Close()  
    End Try  
End Sub  
```  
  
```csharp  
// Reads the button options from the isolated storage. Uses default values   
// for the button if the options file does not exist.  
public void Read()   
{  
    System.IO.IsolatedStorage.IsolatedStorageFile isoStore =   
        System.IO.IsolatedStorage.IsolatedStorageFile.  
        GetUserStoreForDomain();  
  
    string filename = "options.txt";  
    try  
    {  
        // Checks to see if the options.txt file exists.  
        if (isoStore.GetFileNames(filename).GetLength(0) != 0)   
        {  
            // Opens the file because it exists.  
            System.IO.IsolatedStorage.IsolatedStorageFileStream isos =   
                new System.IO.IsolatedStorage.IsolatedStorageFileStream  
                    (filename, System.IO.FileMode.Open,isoStore);  
            System.IO.StreamReader reader = null;  
            try   
            {  
                reader = new System.IO.StreamReader(isos);  
  
                // Reads the values stored.  
                TypeConverter converter ;  
                converter = TypeDescriptor.GetConverter(typeof(Color));  
  
                this.MainButton.BackColor =   
                 (Color)(converter.ConvertFromString(reader.ReadLine()));  
                this.MainButton.ForeColor =   
                 (Color)(converter.ConvertFromString(reader.ReadLine()));  
  
                converter = TypeDescriptor.GetConverter(typeof(Font));  
                this.MainButton.Font =   
                  (Font)(converter.ConvertFromString(reader.ReadLine()));  
            }  
            catch (Exception ex)  
            {   
                System.Diagnostics.Debug.WriteLine  
                     ("Cannot read options " + ex.ToString());  
            }  
            finally  
            {  
                reader.Close();  
            }  
        }  
    }   
    catch (Exception ex)   
    {  
        System.Diagnostics.Debug.WriteLine  
            ("Cannot read options " + ex.ToString());  
    }  
}  
  
// Writes the button options to the isolated storage.  
public void Write()   
{  
    System.IO.IsolatedStorage.IsolatedStorageFile isoStore =   
        System.IO.IsolatedStorage.IsolatedStorageFile.  
        GetUserStoreForDomain();  
  
    string filename = "options.txt";  
    try   
    {  
        // Checks if the file exists and, if it does, tries to delete it.  
        if (isoStore.GetFileNames(filename).GetLength(0) != 0)   
        {  
            isoStore.DeleteFile(filename);  
        }  
    }  
    catch (Exception ex)   
    {  
        System.Diagnostics.Debug.WriteLine  
            ("Cannot delete file " + ex.ToString());  
    }  
  
    // Creates the options file and writes the button options to it.  
    System.IO.StreamWriter writer = null;  
    try   
    {  
        System.IO.IsolatedStorage.IsolatedStorageFileStream isos = new   
            System.IO.IsolatedStorage.IsolatedStorageFileStream(filename,   
            System.IO.FileMode.CreateNew,isoStore);  
  
        writer = new System.IO.StreamWriter(isos);  
        TypeConverter converter ;  
  
        converter = TypeDescriptor.GetConverter(typeof(Color));  
        writer.WriteLine(converter.ConvertToString(  
            this.MainButton.BackColor));  
        writer.WriteLine(converter.ConvertToString(  
            this.MainButton.ForeColor));  
  
        converter = TypeDescriptor.GetConverter(typeof(Font));  
        writer.WriteLine(converter.ConvertToString(  
            this.MainButton.Font));  
  
    }  
    catch (Exception ex)  
    {   
        System.Diagnostics.Debug.WriteLine  
           ("Cannot write options " + ex.ToString());  
    }  
    finally  
    {  
        writer.Close();  
    }  
}  
```  
  
## <a name="database-access"></a>데이터베이스 액세스  
 데이터베이스에 액세스하는 데 필요한 권한은 데이터베이스 공급자에 따라 다릅니다. 그러나 적절한 권한으로 실행 중인 애플리케이션만 데이터 연결을 통해 데이터베이스에 액세스할 수 있습니다. 데이터베이스에 액세스 하는 데 필요한 권한에 대 한 자세한 내용은 [코드 액세스 보안 및 ADO.NET](../data/adonet/code-access-security.md)을 참조 하세요.  
  
 부분 신뢰로 애플리케이션을 실행하려 하므로 데이터베이스에 직접 액세스할 수 없는 경우 데이터에 액세스하는 대체 방법으로 웹 서비스를 사용할 수 있습니다. 웹 서비스는 네트워크를 통해 프로그래밍 방식으로 액세스할 수 있는 소프트웨어입니다. 웹 서비스를 통해 애플리케이션은 코드 그룹 영역 간에 데이터를 공유할 수 있습니다. 기본적으로 로컬 인트라넷 및 인터넷 영역의 애플리케이션에는 동일한 서버에서 호스트된 웹 서비스를 호출할 수 있게 해주는 원본 사이트 액세스 권한이 부여됩니다. 자세한 내용은 ASP.NET AJAX 또는 [Windows Communication Foundation](../wcf/index.md) [의 웹 서비스를](https://docs.microsoft.com/previous-versions/aspnet/bb398785(v=vs.100)) 참조 하세요.  
  
## <a name="registry-access"></a>레지스트리 액세스  
 <xref:System.Security.Permissions.RegistryPermission> 클래스는 운영 체제 레지스트리에 대한 액세스를 제어합니다. 기본적으로 로컬에서 실행 중인 애플리케이션만 레지스트리에 액세스할 수 있습니다.  <xref:System.Security.Permissions.RegistryPermission>은 레지스트리 액세스 시도 권한만 애플리케이션에 부여합니다. 운영 체제가 여전히 레지스트리에 대한 보안을 적용하므로 액세스가 성공한다는 보장은 없습니다.  
  
 부분 신뢰에서는 레지스트리에 액세스할 수 없으므로 다른 데이터 저장 방법을 찾아야 할 수도 있습니다. 애플리케이션 설정을 저장하는 경우 레지스트리 대신 격리된 스토리지를 사용합니다. 격리된 스토리지를 사용하여 다른 애플리케이션 관련 파일을 저장할 수도 있습니다. 또한 기본적으로 애플리케이션에 원본 사이트 액세스 권한이 부여되므로 서버 또는 원본 사이트에 대한 전역 애플리케이션 정보를 저장할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 인쇄 추가 보안](more-secure-printing-in-windows-forms.md)
- [Windows Forms의 추가 보안 고려 사항](additional-security-considerations-in-windows-forms.md)
- [Windows Forms의 보안 개요](security-in-windows-forms-overview.md)
- [Windows Forms 보안](windows-forms-security.md)
- [Mage.exe(매니페스트 생성 및 편집 도구)](../tools/mage-exe-manifest-generation-and-editing-tool.md)
- [MageUI.exe(매니페스트 생성 및 편집 도구, 그래픽 클라이언트)](../tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)
