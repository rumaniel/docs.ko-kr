---
title: '방법: TreeView 또는 ListView 컨트롤에 사용자 지정 정보 추가(Windows Forms)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- ListItem
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- examples [Windows Forms], ListView control
- ListView control [Windows Forms], adding custom information
- TreeView control [Windows Forms], adding custom information
ms.assetid: 68be11de-1d5b-430e-901f-cfbe48d14b19
ms.openlocfilehash: f588a00c430eb1ae1f0cdcde6b7dd22f0c8671c5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956993"
---
# <a name="how-to-add-custom-information-to-a-treeview-or-listview-control-windows-forms"></a>방법: TreeView 또는 ListView 컨트롤에 사용자 지정 정보 추가(Windows Forms)
컨트롤의 파생 된 항목이 나 Windows Forms <xref:System.Windows.Forms.TreeView> 컨트롤에서 파생 노드를 만들 수 있습니다. <xref:System.Windows.Forms.ListView> 파생은 필드를 처리하는 사용자 지정 메서드 및 생성자뿐만 아니라 필요로 하는 모든 필드를 추가할 수 있습니다. 이 기능을 사용하여 각 트리 노드 또는 목록 항목에 고객 개체를 연결합니다. 여기에 있는 예제는 <xref:System.Windows.Forms.TreeView> 컨트롤에 대 한 것 이지만 <xref:System.Windows.Forms.ListView> 컨트롤에 동일한 방법을 사용할 수 있습니다.  
  
### <a name="to-derive-a-tree-node"></a>트리 노드를 파생하려면  
  
- 파일 경로를 기록 하는 사용자 지정 필드 <xref:System.Windows.Forms.TreeNode> 를 포함 하는 클래스에서 파생 된 새 노드 클래스를 만듭니다.  
  
    ```vb  
    Class myTreeNode  
       Inherits TreeNode  
  
       Public FilePath As String  
  
       Sub New(ByVal fp As String)  
          MyBase.New()  
          FilePath = fp  
          Me.Text = fp.Substring(fp.LastIndexOf("\"))  
       End Sub  
    End Class  
    ```  
  
    ```csharp  
    class myTreeNode : TreeNode  
    {  
       public string FilePath;  
  
       public myTreeNode(string fp)  
       {  
          FilePath = fp;  
          this.Text = fp.Substring(fp.LastIndexOf("\\"));  
       }  
    }  
    ```  
  
    ```cpp  
    ref class myTreeNode : public TreeNode  
    {  
    public:  
       System::String ^ FilePath;  
  
       myTreeNode(System::String ^ fp)  
       {  
          FilePath = fp;  
          this->Text = fp->Substring(fp->LastIndexOf("\\"));  
       }  
    };  
    ```  
  
### <a name="to-use-a-derived-tree-node"></a>파생된 트리 노드를 사용하려면  
  
1. 함수 호출에 대한 매개 변수로 새롭게 파생된 트리 노드를 사용할 수 있습니다.  
  
     아래 예제에서 텍스트 파일의 위치에 설정된 경로는 내 문서 폴더입니다. Windows 운영 체제를 실행하는 대부분 컴퓨터가 이 디렉터리에 포함된다고 가정할 수 있기 때문에 그렇습니다. 또한 최소한의 시스템 액세스 수준을 가진 사용자가 안전하게 애플리케이션을 실행할 수 있습니다.  
  
    ```vb  
    ' You should replace the bold text file   
    ' in the sample below with a text file of your own choosing.  
    TreeView1.Nodes.Add(New myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\ TextFile.txt ") )  
    ```  
  
    ```csharp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    treeView1.Nodes.Add(new myTreeNode(System.Environment.GetFolderPath
       (System.Environment.SpecialFolder.Personal)
       + @"\TextFile.txt") );  
    ```  
  
    ```cpp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    treeView1->Nodes->Add(new myTreeNode(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\TextFile.txt")));  
    ```  
  
2. 트리 노드가 전달 되 고이 노드가 <xref:System.Windows.Forms.TreeNode> 클래스로 형식화 된 경우에는 파생 클래스로 캐스팅 해야 합니다. 캐스팅은 개체의 한 유형에서 다른 유형으로의 명시적 변환입니다. 캐스팅에 대 한 자세한 내용은 [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md) (Visual Basic), [캐스팅 및 형식 변환](../../../csharp/programming-guide/types/casting-and-type-conversions.md) (시각적 개체 C#) 또는 [캐스트 연산자: ()](/cpp/cpp/cast-operator-parens) (시각적 개체 C++)를 참조 하세요.  
  
    ```vb  
    Public Sub TreeView1_AfterSelect(ByVal sender As Object, ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       Dim mynode As myTreeNode  
       mynode = CType(e.node, myTreeNode)  
       MessageBox.Show("Node selected is " & mynode.filepath)  
    End Sub  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,  
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       myTreeNode myNode = (myTreeNode)e.Node;  
       MessageBox.Show("Node selected is " + myNode.FilePath);  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          myTreeNode ^ myNode = safe_cast<myTreeNode^>(e->Node);  
          MessageBox::Show(String::Concat("Node selected is ",   
             myNode->FilePath));  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- [TreeView 컨트롤](treeview-control-windows-forms.md)
- [ListView 컨트롤](listview-control-windows-forms.md)
