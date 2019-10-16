---
title: Wndows Presentation Foundation 클라이언트에서 데이터 바인딩
ms.date: 03/30/2017
ms.assetid: bb8c8293-5973-4aef-9b07-afeff5d3293c
ms.openlocfilehash: b0f1eb8ca154ab8e37a15b35097f746662511f7c
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928629"
---
# <a name="data-binding-in-a-windows-presentation-foundation-client"></a>Wndows Presentation Foundation 클라이언트에서 데이터 바인딩
이 샘플에서는 WPF(Windows Presentation Foundation) 클라이언트에서 데이터 바인딩을 사용하는 방법을 보여 줍니다. 이 샘플에서는 클라이언트에 반환할 앨범 배열을 임의로 생성 하는 WCF (Windows Communication Foundation) 서비스를 사용 합니다. 각 앨범에는 이름, 가격 및 앨범 트랙 목록이 있습니다. 앨범 트랙에는 이름과 기간이 있습니다. 서비스에서 반환 되는 정보는 WPF (Windows Presentation Foundation) 클라이언트에서 제공 하는 UI (사용자 인터페이스)에 자동으로 바인딩됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 데이터 바인딩을 사용하면 데이터 소스를 UI에 자동으로 바인딩할 수 있습니다. 이렇게 하면 데이터 개체나 데이터 개체 배열의 데이터로 각 UI 요소를 프로그래밍 방식으로 업데이트할 필요가 없으므로 프로그래밍 모델이 단순화됩니다. 단일 UI 요소에 개체를 바인딩하거나 `ListBox`와 같이 여러 입력을 허용하는 컨트롤에 배열을 바인딩할 수 있습니다. 다음 코드에서는 UI 요소의 `DataContext`에 데이터를 바인딩하는 방법을 보여 줍니다.  
  
```csharp  
// Event handler executed when call is complete  
void client_GetAlbumListCompleted(object sender, GetAlbumListCompletedEventArgs e)  
{  
    // This is on the UI thread, myPanel can be accessed directly  
    myPanel.DataContext = e.Result;   
}  
```  
  
 위 샘플에서 `DataContext`이라는 `grid` 레이아웃 요소에 대한 `myPanel`는 `GetAlbumList` 메서드가 반환하는 데이터로 설정됩니다. `DataContext`를 사용하여 요소는 바인딩에 사용되는 데이터 소스에 대한 정보뿐만 아니라 경로와 같은 바인딩의 다른 특성을 부모 요소로부터 상속할 수 있습니다. 서버의 데이터가 업데이트될 때마다 이 코드 줄이 실행되어야 합니다. 예를 들어, 이 코드 줄은 창이 초기화될 경우 및 새 앨범이 추가될 경우 실행됩니다.  
  
 다음 샘플 XAML 코드에서 `ListBox`는 `ItemsSource="{Binding }"`을 지정합니다.  
  
```xml  
<ListBox   
          ItemTemplate="{StaticResource AlbumStyle}"  
          ItemsSource="{Binding }"   
          IsSynchronizedWithCurrentItem="true" />  
```  
  
 이 샘플 코드는 최상위 UI 요소에 바인딩된 데이터가 이 컨트롤(즉, 앨범 배열)에도 바인딩되도록 지정합니다. 또한 `ItemTemplate="{StaticResource AlbumStyle}"`은 `ListBox`의 각 항목에 사용될 데이터 템플릿을 지정합니다. 데이터 템플릿을 정의하여 데이터의 형식을 지정하는 방법을 지정할 수도 있습니다. 이러한 데이터 템플릿을 애플리케이션의 다른 UI 요소에 다시 사용할 수 있으므로 데이터 템플릿을 한 곳에서 정의하고 유지 관리할 수 있다는 이점이 있습니다.  
  
 `AlbumStyle` 데이터 템플릿은 두 개의 `TextBlock`을 나란히 사용하여 그리드의 레이아웃을 지정합니다. 이러한 두 개체 중 하나는 앨범의 이름을 지정하고 다른 하나는 앨범의 트랙 수를 지정합니다.  
  
```xaml  
<DataTemplate x:Key="AlbumStyle">  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="260" />  
            <ColumnDefinition Width="60" />  
        </Grid.ColumnDefinitions>  
        <TextBlock Grid.Column="0" TextContent="{Binding Path=Title}" />  
        <TextBlock Grid.Column="1" TextContent="{Binding Path=Tracks#.Count}" HorizontalAlignment="Right" />  
    </Grid>  
</DataTemplate>  
```  
  
 다음 XAML 코드에서는 두 번째 `ListBox`를 만듭니다.  
  
```xaml  
<ListBox Grid.Row="2"   
            Grid.ColumnSpan="2"   
            ItemTemplate="{StaticResource TrackStyle}"  
            ItemsSource="{Binding Path=Tracks}" />  
```  
  
 이 코드에서는 `ItemsSource`의 경로를 지정합니다. 이는 이 컨트롤에 바인딩된 데이터가 최상위 데이터가 데이터가 아니라 `Tracks`라는 최상위 데이터의 속성이라는 것을 나타냅니다. 이 속성은 앨범 내에 포함된 트랙의 배열을 나타냅니다. 또한 `DataTemplate`이라는 다른 `TrackStyle`이 지정됩니다. `TrackStyle` 템플릿의 레이아웃은 `AlbumStyle` 템플릿의 레이아웃과 비슷하지만 `TextBlock`이 다른 속성에 바인딩됩니다. 이는 두 템플릿이 다른 데이터 개체와 함께 사용되기 때문입니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WPFDataBinding`  
