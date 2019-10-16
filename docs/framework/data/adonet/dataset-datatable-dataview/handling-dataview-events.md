---
title: DataView 이벤트 처리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5675663-fc91-4e0d-87a9-481b25b64c0f
ms.openlocfilehash: c36c68b0375e7d03aac36de7d02b2c9579ea9316
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784592"
---
# <a name="handling-dataview-events"></a>DataView 이벤트 처리
<xref:System.Data.DataView.ListChanged>의 <xref:System.Data.DataView> 이벤트를 사용하여 뷰가 업데이트되었는지 확인할 수 있습니다. 이벤트를 발생시키는 업데이트에는 원본으로 사용하는 테이블에서의 행 추가, 삭제 또는 수정과 원본으로 사용하는 테이블 스키마에서의 열 추가 또는 삭제, 그리고 부모 또는 자식 관계의 변경이 포함됩니다. 또한 **ListChanged** 이벤트는 새 정렬 순서나 필터의 적용으로 인해 보고 있는 행의 목록이 현저 하 게 변경 되었는지 여부를 알려줍니다.  
  
 **ListChanged** 이벤트는 <xref:System.ComponentModel> 네임 스페이스의 **listchangedeventhandler** 대리자를 구현 하 고 개체를 <xref:System.ComponentModel.ListChangedEventArgs> 입력으로 사용 합니다. **ListChangedEventArgs** 개체의 **listchangedtype** 속성에서 열거형 값 <xref:System.ComponentModel.ListChangedType> 을 사용 하 여 발생 하는 변경 유형을 확인할 수 있습니다. 행 추가, 삭제 또는 이동과 관련 된 변경 내용에 대해서는 **ListChangedEventArgs** 개체의 **NewIndex** 속성을 사용 하 여 추가 되거나 이동한 행의 새 인덱스와 삭제 된 행의 이전 인덱스에 액세스할 수 있습니다. 이동 된 행의 경우 이동한 행의 이전 인덱스는 **ListChangedEventArgs** 개체의 **oldindex** 속성을 사용 하 여 액세스할 수 있습니다.  
  
 또한 **DataViewManager** 는 테이블이 추가 되거나 제거 된 경우 또는 기본 **데이터 집합**의 **관계** 컬렉션이 변경 된 경우 알리도록 **ListChanged** 이벤트를 노출 합니다.  
  
 다음 코드 예제에서는 **ListChanged** 이벤트 처리기를 추가 하는 방법을 보여 줍니다.  
  
```vb  
AddHandler custView.ListChanged, _  
  New System.ComponentModel.ListChangedEventHandler( _  
  AddressOf OnListChanged)  
  
Private Shared Sub OnListChanged( _  
  sender As Object, args As System.ComponentModel.ListChangedEventArgs)  
  Console.WriteLine("ListChanged:")  
  Console.WriteLine(vbTab & "    Type = " & _  
    System.Enum.GetName(args.ListChangedType.GetType(), _  
    args.ListChangedType))  
  Console.WriteLine(vbTab & "OldIndex = " & args.OldIndex)  
  Console.WriteLine(vbTab & "NewIndex = " & args.NewIndex)  
End Sub  
```  
  
```csharp  
custView.ListChanged  += new   
  System.ComponentModel.ListChangedEventHandler(OnListChanged);  
  
protected static void OnListChanged(object sender,   
  System.ComponentModel.ListChangedEventArgs args)  
{  
  Console.WriteLine("ListChanged:");  
  Console.WriteLine("\t    Type = " + args.ListChangedType);  
  Console.WriteLine("\tOldIndex = " + args.OldIndex);  
  Console.WriteLine("\tNewIndex = " + args.NewIndex);  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataView>
- <xref:System.ComponentModel.ListChangedEventHandler>
- [DataView](dataviews.md)
- [ADO.NET 개요](../ado-net-overview.md)
