---
title: 데이터 및 데이터 개체
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data transfer [WPF], drag-and-drop
- DataFormats class [WPF]
- DataObject class [WPF]
ms.assetid: 5967d557-1867-420f-a524-ae3af78402da
ms.openlocfilehash: 4b948a64a14df7ea79b54b810f734056d57ef406
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964859"
---
# <a name="data-and-data-objects"></a>데이터 및 데이터 개체
끌어서 놓기 작업의 일부로 전송 되는 데이터는 데이터 개체에 저장 됩니다.  개념적으로 데이터 개체는 다음 쌍 중 하나 이상으로 구성 됩니다.  
  
- 실제 데이터를 포함 하는입니다.<xref:System.Object>  
  
- 해당 데이터 형식 식별자입니다.  
  
 데이터 자체는 기본 <xref:System.Object>으로 표현할 수 있는 모든 항목으로 구성 될 수 있습니다.  해당 데이터 형식은 데이터의 형식에 대 <xref:System.Type> 한 힌트를 제공 하는 문자열 또는입니다.  데이터 개체는 여러 데이터/데이터 형식 쌍 호스팅을 지원 합니다. 이렇게 하면 단일 데이터 개체가 여러 형식으로 데이터를 제공할 수 있습니다.  
  
<a name="Data_and_Data_Objects"></a>   
## <a name="data-objects"></a>데이터 개체  
 모든 데이터 개체는 <xref:System.Windows.IDataObject> 인터페이스를 구현 해야 하며,이 인터페이스는 데이터 전송을 사용 하 고 용이 하 게 하는 다음과 같은 표준 메서드 집합을 제공 합니다.  
  
|메서드|요약|  
|------------|-------------|  
|<xref:System.Windows.IDataObject.GetData%2A>|지정된 된 데이터 형식의 데이터 개체를 검색 합니다.|  
|<xref:System.Windows.IDataObject.GetDataPresent%2A>|지정 된 형식의 데이터 또는 지정된 된 형식으로 변환할 수 있는지 여부를 확인 합니다.|  
|<xref:System.Windows.IDataObject.GetFormats%2A>|이 데이터 개체에 데이터가 저장 되거나 변환 될 수 있는 형식의 목록을 반환 합니다.|  
|<xref:System.Windows.IDataObject.SetData%2A>|이 데이터 개체에 지정된 된 데이터를 저장 합니다.|  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]클래스에서의 <xref:System.Windows.IDataObject> 기본 구현을 제공 합니다. <xref:System.Windows.DataObject> Stock <xref:System.Windows.DataObject> 클래스는 일반적인 많은 데이터 전송 시나리오에 충분 합니다.  
  
 비트맵, CSV, 파일, HTML, RTF, 문자열, 텍스트, 오디오와 같은 미리 정의 된 여러 가지 형식이 있습니다. 에서 제공 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]하는 <xref:System.Windows.DataFormats> 미리 정의 된 데이터 형식에 대 한 자세한 내용은 클래스 참조 항목을 참조 하세요.  
  
 데이터 개체에는 데이터를 추출 하는 동안 한 형식으로 저장 된 데이터를 다른 형식으로 자동으로 변환 하는 기능이 포함 되어 있습니다. 이 기능을 자동 변환 이라고 합니다. 데이터 개체에서 사용할 수 있는 데이터 형식을 쿼리 하는 <xref:System.Windows.DataObject.GetFormats%28System.Boolean%29> 경우 또는 <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> 메서드를 호출 하 고 매개 변수를 `autoConvert` 로 `false`지정 하 여 네이티브 데이터 형식에서 자동으로 변환할 수 있는 데이터 형식을 필터링 할 수 있습니다.  <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%2CSystem.Boolean%29> 메서드를 사용 하 여 데이터 개체에 데이터를 추가 하는 경우 `autoConvert` 매개 변수를로 `false`설정 하 여 데이터 자동 변환을 금지할 수 있습니다.  
  
<a name="Working_with_Data_Objects"></a>   
## <a name="working-with-data-objects"></a>데이터 개체 작업  
 이 섹션에서는 데이터 개체를 만들고 사용 하는 일반적인 방법에 대해 설명 합니다.  
  
### <a name="creating-new-data-objects"></a>새 데이터 개체 만들기  
 클래스 <xref:System.Windows.DataObject> 는 단일 데이터/데이터 형식 쌍을 사용 하 <xref:System.Windows.DataObject> 여 새 인스턴스를 쉽게 채울 몇 가지 오버 로드 된 생성자를 제공 합니다.  
  
 다음 예제 코드에서는 새 데이터 개체를 만들고 오버 로드 된 생성자 <xref:System.Windows.DataObject.%23ctor%2A>(<xref:System.Windows.DataObject.%23ctor(System.String,System.Object)>) 중 하나를 사용 하 여 문자열 및 지정 된 데이터 형식을 사용 하 여 데이터 개체를 초기화 합니다.  이 경우 데이터 형식은 문자열로 지정 됩니다. 클래스 <xref:System.Windows.DataFormats> 는 미리 정의 된 형식 문자열 집합을 제공 합니다. 저장 된 데이터의 자동 변환은 기본적으로 허용 됩니다.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
 데이터 개체를 만드는 코드의 추가 예제는 [데이터 개체 만들기](how-to-create-a-data-object.md)를 참조 하세요.  
  
### <a name="storing-data-in-multiple-formats"></a>여러 형식으로 데이터 저장  
 단일 데이터 개체는 여러 형식으로 데이터를 저장할 수 있습니다.   단일 데이터 개체 내에서 여러 데이터 형식을 전략적으로 사용 하면 단일 데이터 형식만 표현할 수 있는 것 보다 더 광범위 한 놓기 대상에서 데이터 개체를 사용할 수 있습니다.  일반적으로 끌기 소스는 잠재적 놓기 대상에서 사용할 수 있는 데이터 형식에 대해 독립적 이어야 합니다.  
  
 다음 예제에서는 <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> 메서드를 사용 하 여 여러 형식의 데이터를 데이터 개체에 추가 하는 방법을 보여 줍니다.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
### <a name="querying-a-data-object-for-available-formats"></a>사용 가능한 형식에 대 한 데이터 개체 쿼리  
 단일 데이터 개체에는 임의의 수의 데이터 형식이 포함 될 수 있기 때문에 데이터 개체에는 사용 가능한 데이터 형식 목록을 검색 하는 기능이 포함 되어 있습니다.  
  
 다음 예제 코드에서는 <xref:System.Windows.DataObject.GetFormats%2A> 오버 로드를 사용 하 여 데이터 개체에서 사용할 수 있는 모든 데이터 형식 (네이티브 및 자동 변환)을 나타내는 문자열의 배열을 가져옵니다.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
 데이터 개체에서 사용 가능한 데이터 형식을 쿼리 하는 코드의 추가 예제는 [데이터 개체의 데이터 형식 나열](how-to-list-the-data-formats-in-a-data-object.md)을 참조 하세요.  데이터 개체를 쿼리하여 특정 데이터 형식이 있는지 확인 하는 예는 데이터 [개체에 데이터 형식이 있는지 확인](how-to-determine-if-a-data-format-is-present-in-a-data-object.md)을 참조 하세요.  
  
### <a name="retrieving-data-from-a-data-object"></a>데이터 개체에서 데이터 검색  
 특정 형식의 데이터 개체에서 데이터를 검색 하는 작업에는 <xref:System.Windows.DataObject.GetData%2A> 메서드 중 하나를 호출 하 고 원하는 데이터 형식을 지정 하는 작업이 포함 됩니다.  <xref:System.Windows.DataObject.GetDataPresent%2A> 메서드 중 하나를 사용 하 여 특정 데이터 형식이 있는지 확인할 수 있습니다.  <xref:System.Windows.DataObject.GetData%2A>의 데이터를 반환 합니다 <xref:System.Object>. 데이터 형식에 따라이 개체를 유형별 컨테이너로 캐스팅할 수 있습니다.  
  
 다음 예제 코드에서는 <xref:System.Windows.DataObject.GetDataPresent%28System.String%29> 오버 로드를 사용 하 여 지정 된 데이터 형식을 사용할 수 있는지 여부를 확인 합니다 (네이티브 또는 자동 변환). 지정 된 형식을 사용할 수 있는 경우이 예제에서는 메서드를 <xref:System.Windows.DataObject.GetData%28System.String%29> 사용 하 여 데이터를 검색 합니다.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
 데이터 개체에서 데이터를 검색 하는 코드의 추가 예제는 [특정 데이터 형식으로 데이터 검색](how-to-retrieve-data-in-a-particular-data-format.md)을 참조 하세요.  
  
### <a name="removing-data-from-a-data-object"></a>데이터 개체에서 데이터 제거  
 데이터를 데이터 개체에서 직접 제거할 수 없습니다.  데이터 개체에서 데이터를 효과적으로 제거 하려면 다음 단계를 수행 합니다.  
  
1. 유지 하려는 데이터만 포함 하는 새 데이터 개체를 만듭니다.  
  
2. 이전 데이터 개체에서 새 데이터 개체로 원하는 데이터를 "복사" 합니다.  데이터를 복사 하려면 <xref:System.Windows.DataObject.GetData%2A> 메서드 중 하나를 사용 하 여 원시 데이터가 포함 <xref:System.Object> 된를 검색 한 <xref:System.Windows.DataObject.SetData%2A> 다음 메서드 중 하나를 사용 하 여 새 데이터 개체에 데이터를 추가 합니다.  
  
3. 이전 데이터 개체를 새 개체로 바꿉니다.  
  
> [!NOTE]
> 메서드 <xref:System.Windows.DataObject.SetData%2A> 는 데이터를 데이터 개체에만 추가 하 고 데이터와 데이터 형식이 이전 호출과 정확히 동일한 경우에도 데이터를 바꾸지 않습니다. 동일한 <xref:System.Windows.DataObject.SetData%2A> 데이터 및 데이터 형식에 대해를 두 번 호출 하면 데이터/데이터 형식이 데이터 개체에 두 번 표시 됩니다.
