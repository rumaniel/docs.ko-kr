---
title: Windows Forms에서 지원하는 데이터 소스
ms.date: 03/30/2017
helpviewer_keywords:
- collections [Windows Forms], binding to
- OLE DB providers [Windows Forms], Windows Forms
- DataTable class [Windows Forms], binding and Windows Forms
- Windows Forms, data binding
- DataView class [Windows Forms], binding and Windows Forms
- DataViewManager class [Windows Forms], binding and Windows Forms
- Windows Forms, source data
- arrays [Windows Forms]
- data sources [Windows Forms]
- data providers [Windows Forms]
- DataSet class [Windows Forms], binding and Windows Forms
- data [Windows Forms], data providers
ms.assetid: 3d2c43f6-462b-4d35-9c86-13e9afe012e1
ms.openlocfilehash: 6782261953fb5df94498deefb261407a2f0ba33a
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65882391"
---
# <a name="data-sources-supported-by-windows-forms"></a>Windows Forms에서 지원하는 데이터 소스
일반적으로 데이터 바인딩은 데 사용 된 응용 프로그램 내에서 데이터베이스에 저장 된 데이터를 활용 합니다. Windows Forms 데이터 바인딩에 특정 최소 요구 사항이 충족 된다면 배열 및 컬렉션 등의 다른 구조에 있는 데이터 뿐만 아니라 데이터베이스에서 데이터를 액세스할 수 있습니다.  
  
## <a name="structures-to-bind-to"></a>바인딩할 구조  
 Windows Forms에 바인딩할 수 있습니다 다양 한 구조의 간단한에서 ADO.NET 데이터 테이블 (복잡 한 바인딩) 같은 복잡 한 목록에 개체 (단순 바인딩). 단순 바인딩 Windows Forms 단순 개체에서 공용 속성 바인딩을 지원합니다. Windows Forms 목록 기반 바인딩을 개체 지 일반적으로 필요 합니다 <xref:System.Collections.IList> 인터페이스 또는 <xref:System.ComponentModel.IListSource> 인터페이스입니다. 또한를 통해 바인딩하는 경우는 <xref:System.Windows.Forms.BindingSource> 구성 요소를 지 원하는 개체를 바인딩할 수 있습니다는 <xref:System.Collections.IEnumerable> 인터페이스입니다. 데이터 바인딩과 관련 된 인터페이스에 대 한 자세한 내용은 참조 하세요. [데이터 바인딩과 관련 인터페이스](interfaces-related-to-data-binding.md)합니다.  
  
 다음은 Windows Forms에 바인딩할 수 있습니다 구조를 보여 줍니다.  
  
 <xref:System.Windows.Forms.BindingSource>  
 <xref:System.Windows.Forms.BindingSource> 는 가장 일반적인 Windows Forms 데이터 원본 및 데이터 원본 및 Windows Forms 컨트롤 간의 프록시 역할입니다. 일반 <xref:System.Windows.Forms.BindingSource> 사용 패턴에 컨트롤을 바인딩하는 <xref:System.Windows.Forms.BindingSource> 바인딩하고 <xref:System.Windows.Forms.BindingSource> 데이터 원본 (예를 들어, ADO.NET 데이터 테이블 또는 비즈니스 개체)에 있습니다. <xref:System.Windows.Forms.BindingSource> 및 데이터 바인딩 지원의 수준을 향상 시킬 수 있는 서비스를 제공 합니다. 그러나 예를 들어, Windows Forms 기반 목록 컨트롤 같은 합니다 <xref:System.Windows.Forms.DataGridView> 및 <xref:System.Windows.Forms.ComboBox> 직접 바인딩할 수 없습니다 <xref:System.Collections.IEnumerable> 데이터 원본을 통해 바인딩에서이 시나리오를 설정할 수 있습니다.를 <xref:System.Windows.Forms.BindingSource>. 이 경우에 <xref:System.Windows.Forms.BindingSource> 데이터 원본에는 변환는 <xref:System.Collections.IList>.  
  
 단순 개체  
 Windows Forms를 사용 하 여 개체를 인스턴스에서 공용 속성에 데이터 바인딩 컨트롤 속성을 지원 합니다 <xref:System.Windows.Forms.Binding> 형식입니다. Windows Forms에서는 바인딩 목록 기반 컨트롤을 같은 <xref:System.Windows.Forms.ListControl> 때 개체 인스턴스는 <xref:System.Windows.Forms.BindingSource> 사용 됩니다.  
  
 배열 또는 컬렉션  
 를 데이터 소스로 작동 하려면 목록을 구현 해야 합니다는 <xref:System.Collections.IList> 인터페이스; 하나 예로 배열을 인스턴스의 수는 <xref:System.Array> 클래스입니다. 배열에 대 한 자세한 내용은 참조 하세요. [방법: (Visual Basic) 개체의 배열을 만들어](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/487y7874(v=vs.100))합니다.  
  
 일반적으로 사용 해야 <xref:System.ComponentModel.BindingList%601> 데이터 바인딩에 대 한 개체의 목록을 만들 때. <xref:System.ComponentModel.BindingList%601> 제네릭 버전이 <xref:System.ComponentModel.IBindingList> 인터페이스입니다. 합니다 <xref:System.ComponentModel.IBindingList> 인터페이스를 확장 합니다 <xref:System.Collections.IList> 속성, 메서드 및 양방향 데이터 바인딩을 위해 필요한 이벤트를 추가 하 여 인터페이스입니다.  
  
 <xref:System.Collections.IEnumerable>  
 만 지 원하는 데이터 소스에 Windows Forms 컨트롤을 바인딩할 수 있습니다 합니다 <xref:System.Collections.IEnumerable> 인터페이스를 통해 바인딩된 경우를 <xref:System.Windows.Forms.BindingSource> 구성 요소입니다.  
  
 ADO.NET 데이터 개체  
 ADO.NET에 대 한 바인딩에 적합 한 데이터 구조를 많이 제공합니다. 각 해당 숙련도 및 복잡성에 따라 다릅니다.  
  
- <xref:System.Data.DataColumn>. <xref:System.Data.DataColumn> 는의 필수 구성 요소를 <xref:System.Data.DataTable>를 열 수를 하나의 테이블을 구성 합니다. 각 <xref:System.Data.DataColumn> 에 <xref:System.Data.DataColumn.DataType%2A> 열 (예를 들어, 자동차를 설명 하는 테이블에 있는 자동차의 제조업체)에 저장 된 데이터의 종류를 결정 하는 속성입니다. 바인딩할 수 있습니다 단순 컨트롤 (같은 <xref:System.Windows.Forms.TextBox> 컨트롤의 <xref:System.Windows.Forms.Control.Text%2A> 속성) 데이터 테이블 내의 열입니다.  
  
- <xref:System.Data.DataTable>. <xref:System.Data.DataTable> 행 및 열으로 ADO.NET 사용 하 여 테이블의 표현입니다. 두 컬렉션을 포함 하는 데이터 테이블: <xref:System.Data.DataColumn>합니다 (해당 테이블에 입력할 수 있는 데이터 종류 결정)는 지정된 된 테이블의 데이터 열을 나타내는 및 <xref:System.Data.DataRow>, 지정된 된 테이블의 데이터 행을 나타내는입니다. 바인딩할 수 있습니다 복합 컨트롤을 데이터 테이블에 포함 된 정보 (바인딩 등의 <xref:System.Windows.Forms.DataGridView> 컨트롤을 데이터 테이블에). 그러나에 바인딩하는 경우는 <xref:System.Data.DataTable>, 테이블의 기본 보기에 실제로 바인딩는 합니다.  
  
- <xref:System.Data.DataView>. <xref:System.Data.DataView> 필터링 하거나 정렬할 수 있는 단일 데이터 테이블의 사용자 지정 뷰입니다. 데이터 보기는 "스냅숏" 복합 바인딩된 컨트롤에서 사용 하는 데이터입니다. 단순 바인딩 또는 복합 바인딩할 데이터 뷰의 데이터 따르면 깨끗 하 고 업데이트 하는 데이터 원본 대신 데이터의 고정된 "그림"을 바인딩하는 알고 있어야 합니다.  
  
- <xref:System.Data.DataSet>. <xref:System.Data.DataSet> 는 테이블, 관계 및 제약 조건 데이터베이스의 데이터의 컬렉션입니다. 단순 바인딩 또는 복잡 한 바인딩 데이터 집합 내의 데이터에 따르면 기본값으로 바인딩하는 유의 <xref:System.Data.DataViewManager> 에 대 한는 <xref:System.Data.DataSet> (다음 글머리 기호 참조).  
  
- <xref:System.Data.DataViewManager>. <xref:System.Data.DataViewManager> 전체 사용자 지정 뷰입니다 <xref:System.Data.DataSet>비슷합니다는 <xref:System.Data.DataView>, 비슷하지만 관계가 포함 합니다. 사용 하 여는 <xref:System.Data.DataViewManager.DataViewSettings%2A> 컬렉션을 설정할 수 있습니다 기본 필터 및 모든 보기에 대 한 정렬 옵션을 <xref:System.Data.DataViewManager> 에 지정된 된 테이블에 대 한 합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms 데이터 바인딩의 변경 알림](change-notification-in-windows-forms-data-binding.md)
- [데이터 바인딩 및 Windows Forms](data-binding-and-windows-forms.md)
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
