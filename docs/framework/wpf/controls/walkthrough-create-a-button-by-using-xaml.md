---
title: '연습: XAML을 사용하여 단추 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [WPF]
ms.assetid: 138c41c4-1759-4bbf-8d77-77031a06a8a0
ms.openlocfilehash: 3f85d7d454247694d084ac68780f830c4301b6c7
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332792"
---
# <a name="walkthrough-create-a-button-by-using-xaml"></a>연습: XAML을 사용하여 단추 만들기

이 연습의 목표는 Windows Presentation Foundation (WPF) 응용 프로그램에서 사용 하기 위한 애니메이션 된 단추를 만드는 방법을 설명 하는 것입니다. 이 연습에서는 스타일 및 템플릿을 사용 하 여 단추 선언에서 코드를 다시 사용 하 고 단추 논리를 분리 하는 데 사용할 수 있는 사용자 지정 된 단추 리소스를 만듭니다. 이 연습은 완전히 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]으로 작성 됩니다.

> [!IMPORTANT]
> 이 연습에서는 Microsoft Visual Studio에 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]을 입력 하거나 복사 하 여 붙여 넣는 방법으로 응용 프로그램을 만드는 단계를 안내 합니다. 디자인 도구 (Microsoft Expression Blend)를 사용 하 여 동일한 응용 프로그램을 만드는 방법을 알아보려면 [Microsoft Expression blend를 사용 하 여 단추 만들기](walkthrough-create-a-button-by-using-microsoft-expression-blend.md)를 참조 하세요.

다음 그림에서는 완료 된 단추를 보여 줍니다.

XAML(./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5") 를 ![사용 하 여 만든 사용자 지정 단추]

## <a name="create-basic-buttons"></a>기본 단추 만들기

먼저 새 프로젝트를 만들고 창에 몇 가지 단추를 추가 해 보겠습니다.

### <a name="to-create-a-new-wpf-project-and-add-buttons-to-the-window"></a>새 WPF 프로젝트를 만들고 창에 단추를 추가 하려면

1. Visual Studio를 시작합니다.

2. **새 WPF 프로젝트를 만듭니다.** **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. **Windows 응용 프로그램 (WPF)** 템플릿을 찾고 프로젝트 이름을 "AnimatedButton"로 합니다. 그러면 응용 프로그램에 대 한 해골을 만듭니다.

3. **기본 기본 단추 추가:** 이 연습에 필요한 모든 파일은 템플릿에서 제공 됩니다. 솔루션 탐색기에서 두 번 클릭 하 여 Window1 파일을 엽니다. 기본적으로는 <xref:System.Windows.Controls.Grid> 요소가 Window1에 있습니다. @No__t-0 요소를 제거 하 고 다음 강조 표시 된 코드를 Window1에 복사 하 여 붙여 넣는 방법으로 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 페이지에 몇 가지 단추를 추가 합니다.

    ```xaml
    <Window x:Class="AnimatedButton.Window1"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      Title="AnimatedButton" Height="300" Width="300"
      Background="Black">
      <!-- Buttons arranged vertically inside a StackPanel. -->
      <StackPanel HorizontalAlignment="Left">
          <Button>Button 1</Button>
          <Button>Button 2</Button>
          <Button>Button 3</Button>
      </StackPanel>
    </Window>
    ```

     F5 키를 눌러 응용 프로그램을 실행 합니다. 다음 그림과 같은 단추 집합이 표시 됩니다.

     ![세 가지 기본 단추](./media/custom-button-animatedbutton-1.gif "custom_button_AnimatedButton_1")

     이제 기본 단추를 만들었으므로 Window1 .xaml 파일에서 작업을 완료 합니다. 연습의 나머지 부분에서는 app.xaml 파일에 중점을 두고 단추에 대 한 스타일 및 템플릿을 정의 합니다.

## <a name="set-basic-properties"></a>기본 속성 설정

다음으로 이러한 단추의 몇 가지 속성을 설정 하 여 단추 모양과 레이아웃을 제어 해 보겠습니다. 단추에 대해 개별적으로 속성을 설정 하는 대신 리소스를 사용 하 여 전체 응용 프로그램에 대 한 단추 속성을 정의 합니다. 응용 프로그램 리소스는 웹 페이지에 대 한 CSS (외부 CSS 스타일시트)와 개념적으로 유사 합니다. 그러나이 연습의 끝에서 볼 수 있듯이 리소스는 CSS (CSS 스타일시트) 보다 훨씬 더 강력 합니다. 리소스에 대해 자세히 알아보려면 [XAML 리소스](../advanced/xaml-resources.md)를 참조 하세요.

### <a name="to-use-styles-to-set-basic-properties-on-the-buttons"></a>스타일을 사용 하 여 단추에 대 한 기본 속성을 설정 하려면

1. **응용 프로그램 리소스 블록을 정의 합니다.** App.xaml을 열고 다음 강조 표시 된 태그를 추가 합니다 (아직 없는 경우).

    ```xaml
    <Application x:Class="AnimatedButton.App"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      StartupUri="Window1.xaml"
      >
      <Application.Resources>
        <!-- Resources for the entire application can be defined here. -->
      </Application.Resources>
    </Application>
    ```

     리소스 범위는 리소스를 정의 하는 위치에 따라 결정 됩니다. App.xaml 파일의 `Application.Resources`에서 리소스를 정의 하면 응용 프로그램의 어디에서 나 리소스를 사용할 수 있습니다. 리소스의 범위를 정의 하는 방법에 대 한 자세한 내용은 [XAML 리소스](../advanced/xaml-resources.md)를 참조 하세요.

2. **스타일을 만들고 기본 속성 값을 정의 합니다.** @No__t-0 블록에 다음 태그를 추가 합니다. 이 태그는 응용 프로그램의 모든 단추에 적용 되는 <xref:System.Windows.Style>을 만들고 단추의 @no__t 1을 90로 설정 하 고 <xref:System.Windows.FrameworkElement.Margin%2A>를 10으로 설정 합니다.

    ```xaml
    <Application.Resources>
      <Style TargetType="Button">
        <Setter Property="Width" Value="90" />
        <Setter Property="Margin" Value="10" />
      </Style>
    </Application.Resources>
    ```

     @No__t-0 속성은 스타일이 <xref:System.Windows.Controls.Button> 형식의 모든 개체에 적용 되도록 지정 합니다. 각 <xref:System.Windows.Setter>은 <xref:System.Windows.Style>에 대해 다른 속성 값을 설정 합니다. 따라서이 시점에서 응용 프로그램의 모든 단추 너비는 90이 고 여백은 10입니다.  F5 키를 눌러 응용 프로그램을 실행 하면 다음 창이 표시 됩니다.

     ![너비가 90이 고 여백이 10 custom_button_AnimatedButton_2 인 단추](./media/custom-button-animatedbutton-2.gif "")

     대상 개체를 미세 조정 하 고, 복잡 한 속성 값을 지정 하 고, 다른 스타일의 입력으로 스타일을 사용 하는 다양 한 방법을 포함 하 여 스타일을 사용 하 여 더 많은 작업을 수행할 수 있습니다. 자세한 내용은 [스타일 지정 및 템플릿](styling-and-templating.md)을 참조하세요.

3. **스타일 속성 값을 리소스에 설정 합니다.** 리소스를 사용 하면 일반적으로 정의 된 개체 및 값을 다시 사용할 수 있습니다. 코드를 모듈식으로 만들기 위해 리소스를 사용 하 여 복잡 한 값을 정의 하는 데 특히 유용 합니다. 다음 강조 표시 된 태그를 app.xaml에 추가 합니다.

    ```xaml
    <Application.Resources>
      <LinearGradientBrush x:Key="GrayBlueGradientBrush" StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>
      <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />
        <Setter Property="Width" Value="80" />
        <Setter Property="Margin" Value="10" />
      </Style>
    </Application.Resources>
    ```

     @No__t-0 블록 바로 아래에 "GrayBlueGradientBrush" 라는 리소스를 만들었습니다. 이 리소스는 가로 그라데이션을 정의 합니다. 이 리소스는 <xref:System.Windows.Controls.Control.Background%2A> 속성에 대 한 단추 스타일 setter 내부를 포함 하 여 응용 프로그램의 어디에서 나 속성 값으로 사용할 수 있습니다. 이제 모든 단추에이 그라데이션의 <xref:System.Windows.Controls.Control.Background%2A> 속성 값이 있습니다.

     F5 키를 눌러 애플리케이션을 실행합니다. 다음과 같이 표시 됩니다.

     ![그라데이션 배경이](./media/custom-button-animatedbutton-3.gif "custom_button_AnimatedButton_3") 단추

## <a name="create-a-template-that-defines-the-look-of-the-button"></a>단추의 모양을 정의 하는 템플릿을 만듭니다.

이 섹션에서는 단추의 모양 (표시)을 사용자 지정 하는 템플릿을 만듭니다. 단추 프레젠테이션은 사각형 및 기타 구성 요소를 비롯 한 여러 개체로 구성 되어 단추에 고유한 모양을 제공 합니다.

지금까지 응용 프로그램에서 단추가 표시 되는 방식에 대 한 제어는 단추의 속성을 변경 하는 것으로 제한 되었습니다. 단추의 모양을 크게 변경 하려면 어떻게 해야 하나요? 템플릿을 사용 하면 개체의 표시를 효과적으로 제어할 수 있습니다. 템플릿은 스타일 내에서 사용할 수 있으므로 스타일이 적용 되는 모든 개체에 템플릿을 적용할 수 있습니다 (이 연습에서는 단추).

### <a name="to-use-the-template-to-define-the-look-of-the-button"></a>템플릿을 사용 하 여 단추의 모양을 정의 하려면

1. **템플릿 설정:** @No__t-0과 같은 컨트롤에는 <xref:System.Windows.Controls.Control.Template%2A> 속성이 있으므로 <xref:System.Windows.Setter>을 사용 하 여 <xref:System.Windows.Style>에서 설정한 다른 속성 값과 마찬가지로 템플릿 속성 값을 정의할 수 있습니다. 다음 강조 표시 된 태그를 단추 스타일에 추가 합니다.

    ```xaml
    <Application.Resources>
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"
        StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>
      <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />
        <Setter Property="Width" Value="80" />
        <Setter Property="Margin" Value="10" />
        <Setter Property="Template">
          <Setter.Value>
            <!-- The button template is defined here. -->
          </Setter.Value>
        </Setter>
      </Style>
    </Application.Resources>
    ```

2. **변경 단추 프레젠테이션:** 이 시점에서 템플릿을 정의 해야 합니다. 다음 강조 표시 된 태그를 추가 합니다. 이 태그는 모퉁이가 둥근 두 개의 <xref:System.Windows.Shapes.Rectangle> 요소를 지정 하 고 그 뒤에 <xref:System.Windows.Controls.DockPanel>을 사용 합니다. @No__t-0은 단추의 <xref:System.Windows.Controls.ContentPresenter>을 호스트 하는 데 사용 됩니다. @No__t-0은 단추의 내용을 표시 합니다. 이 연습에서는 콘텐츠가 텍스트 ("Button 1", "Button 2", "Button 3")입니다. 모든 템플릿 구성 요소 (사각형과 <xref:System.Windows.Controls.DockPanel>)는 <xref:System.Windows.Controls.Grid>의 내부에 배치 됩니다.

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="Button">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}" ClipToBounds="True">
          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}" RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />
          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20" Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />
          <!-- Present Content (text) of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20" Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>
      </ControlTemplate>
    </Setter.Value>
    ```

     F5 키를 눌러 애플리케이션을 실행합니다. 다음과 같이 표시 됩니다.

     ![3 개의 단추가 있는 창](./media/custom-button-animatedbutton-4.gif)

3. **템플릿에 glasseffect를 추가 합니다.** 다음에는 유리를 추가 합니다. 먼저 투명 효과 그라데이션 효과를 만드는 일부 리소스를 만듭니다. @No__t-0 블록 내의 아무 곳에 나 이러한 그라데이션 리소스를 추가 합니다.

    ```xaml
    <Application.Resources>
      <GradientStopCollection x:Key="MyGlassGradientStopsResource">
        <GradientStop Color="WhiteSmoke" Offset="0.2" />
        <GradientStop Color="Transparent" Offset="0.4" />
        <GradientStop Color="WhiteSmoke" Offset="0.5" />
        <GradientStop Color="Transparent" Offset="0.75" />
        <GradientStop Color="WhiteSmoke" Offset="0.9" />
        <GradientStop Color="Transparent" Offset="1" />
      </GradientStopCollection>
      <LinearGradientBrush x:Key="MyGlassBrushResource"
        StartPoint="0,0" EndPoint="1,1" Opacity="0.75"
        GradientStops="{StaticResource MyGlassGradientStopsResource}" />
    <!-- Styles and other resources below here. -->
    ```

     이러한 리소스는 단추 템플릿의 <xref:System.Windows.Controls.Grid>에 삽입 하는 사각형에 대해 <xref:System.Windows.Shapes.Shape.Fill%2A>으로 사용 됩니다. 템플릿에 다음 강조 표시 된 태그를 추가 합니다.

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="{x:Type Button}">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}"
          ClipToBounds="True">

        <!-- Outer Rectangle with rounded corners. -->
        <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />

        <!-- Inner Rectangle with rounded corners. -->
        <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20"
          Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />

        <!-- Glass Rectangle -->
        <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch"
          StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"
          Fill="{StaticResource MyGlassBrushResource}"
          RenderTransformOrigin="0.5,0.5">
          <Rectangle.Stroke>
            <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
              <LinearGradientBrush.GradientStops>
                <GradientStop Offset="0.0" Color="LightBlue" />
                <GradientStop Offset="1.0" Color="Gray" />
              </LinearGradientBrush.GradientStops>
            </LinearGradientBrush>
          </Rectangle.Stroke>
          <!-- These transforms have no effect as they are declared here.
          The reason the transforms are included is to be targets
          for animation (see later). -->
          <Rectangle.RenderTransform>
            <TransformGroup>
              <ScaleTransform />
              <RotateTransform />
            </TransformGroup>
          </Rectangle.RenderTransform>
          <!-- A BevelBitmapEffect is applied to give the button a "Beveled" look. -->
          <Rectangle.BitmapEffect>
            <BevelBitmapEffect />
          </Rectangle.BitmapEffect>
        </Rectangle>

        <!-- Present Text of the button. -->
        <DockPanel Name="myContentPresenterDockPanel">
          <ContentPresenter x:Name="myContentPresenter" Margin="20"
            Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
        </DockPanel>
      </Grid>
    </ControlTemplate>
    </Setter.Value>
    ```

     "GlassCube"의 `x:Name` 속성이 있는 사각형의 <xref:System.Windows.UIElement.Opacity%2A>은 0 이므로 샘플을 실행할 때 맨 위에 오버레이 사각형이 표시 되지 않습니다. 이는 나중에 사용자가 단추를 사용 하 여 상호 작용할 때 템플릿에 트리거를 추가 하기 때문입니다. 그러나 <xref:System.Windows.UIElement.Opacity%2A> 값을 1로 변경 하 고 응용 프로그램을 실행 하 여 이제 단추가 어떻게 표시 되는지 확인할 수 있습니다. 다음 그림을 참조하세요. 다음 단계로 진행 하기 전에 <xref:System.Windows.UIElement.Opacity%2A>을 다시 0으로 변경 합니다.

     XAML(./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5") 를 ![사용 하 여 만든 사용자 지정 단추]

## <a name="create-button-interactivity"></a>단추 대화형 작업 만들기

이 섹션에서는 속성 트리거와 이벤트 트리거를 만들어 속성 값을 변경 하 고 단추 위로 마우스 포인터를 이동 하 고를 클릭 하는 등의 사용자 동작에 대 한 응답으로 애니메이션을 실행 합니다.

대화형 작업을 추가 하는 쉬운 방법 (마우스 위로, 마우스-leave, 클릭 등)은 템플릿 또는 스타일 내에서 트리거를 정의 하는 것입니다. @No__t-0을 만들려면 다음과 같이 "condition" 속성을 정의 합니다. 단추 <xref:System.Windows.UIElement.IsMouseOver%2A> 속성 값이 `true`과 같습니다. 그런 다음 트리거 조건이 true 일 때 발생 하는 setter (동작)를 정의 합니다.

### <a name="to-create-button-interactivity"></a>단추 대화형 작업을 만들려면

1. **템플릿 트리거 추가:** 강조 표시 된 태그를 템플릿에 추가 합니다.

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="{x:Type Button}">
        <Grid Width="{TemplateBinding Width}"
          Height="{TemplateBinding Height}" ClipToBounds="True">

          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />

          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"
            VerticalAlignment="Stretch" Stroke="Transparent"
            StrokeThickness="20"
            Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20"
          />

          <!-- Glass Rectangle -->
          <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"
            VerticalAlignment="Stretch"
            StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"
            Fill="{StaticResource MyGlassBrushResource}"
            RenderTransformOrigin="0.5,0.5">
            <Rectangle.Stroke>
              <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
                <LinearGradientBrush.GradientStops>
                  <GradientStop Offset="0.0" Color="LightBlue" />
                  <GradientStop Offset="1.0" Color="Gray" />
                </LinearGradientBrush.GradientStops>
              </LinearGradientBrush>
            </Rectangle.Stroke>

            <!-- These transforms have no effect as they
                 are declared here.
                 The reason the transforms are included is to be targets
                 for animation (see later). -->
            <Rectangle.RenderTransform>
              <TransformGroup>
                <ScaleTransform />
                <RotateTransform />
              </TransformGroup>
            </Rectangle.RenderTransform>

              <!-- A BevelBitmapEffect is applied to give the button a
                   "Beveled" look. -->
            <Rectangle.BitmapEffect>
              <BevelBitmapEffect />
            </Rectangle.BitmapEffect>
          </Rectangle>

          <!-- Present Text of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20"
              Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>

        <ControlTemplate.Triggers>       <!-- Set action triggers for the buttons and define            what the button does in response to those triggers. -->     </ControlTemplate.Triggers>
      </ControlTemplate>
    </Setter.Value>
    ```

2. **속성 트리거 추가:** @No__t-0 블록에 강조 표시 된 태그를 추가 합니다.

    ```xaml
    <ControlTemplate.Triggers>

      <!-- Set properties when mouse pointer is over the button. -->   <Trigger Property="IsMouseOver" Value="True">     <!-- Below are three property settings that occur when the           condition is met (user mouses over button).  -->     <!-- Change the color of the outer rectangle when user           mouses over it. -->     <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <!-- Sets the glass opacity to 1, therefore, the           glass "appears" when user mouses over it. -->     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />     <!-- Makes the text slightly blurry as though you           were looking at it through blurry glass. -->     <Setter Property="ContentPresenter.BitmapEffect"        TargetName="myContentPresenter">       <Setter.Value>         <BlurBitmapEffect Radius="1" />       </Setter.Value>     </Setter>   </Trigger>

    <ControlTemplate.Triggers/>
    ```

     F5 키를 눌러 응용 프로그램을 실행 하 고 단추 위에 마우스 포인터를 놓으면 효과를 확인 합니다.

3. **포커스 트리거를 추가 합니다.** 다음으로, 단추에 포커스가 있을 때 (예: 사용자가 클릭 한 후) 사례를 처리 하는 비슷한 setter를 추가 합니다.

    ```xaml
    <ControlTemplate.Triggers>

      <!-- Set properties when mouse pointer is over the button. -->
      <Trigger Property="IsMouseOver" Value="True">

        <!-- Below are three property settings that occur when the
             condition is met (user mouses over button).  -->
        <!-- Change the color of the outer rectangle when user          mouses over it. -->
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />

        <!-- Sets the glass opacity to 1, therefore, the          glass "appears" when user mouses over it. -->
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />

        <!-- Makes the text slightly blurry as though you were          looking at it through blurry glass. -->
        <Setter Property="ContentPresenter.BitmapEffect"       TargetName="myContentPresenter">
          <Setter.Value>
            <BlurBitmapEffect Radius="1" />
          </Setter.Value>
        </Setter>
      </Trigger>
      <!-- Set properties when button has focus. -->   <Trigger Property="IsFocused" Value="true">     <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />     <Setter Property="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />   </Trigger>

    </ControlTemplate.Triggers>
    ```

     F5 키를 눌러 응용 프로그램을 실행 하 고 단추 중 하나를 클릭 합니다. 단추는 여전히 포커스를 가지 므로 클릭 하면 강조 표시 됩니다. 다른 단추를 클릭 하면 마지막 단추를 클릭 하면 포커스가 사라집니다.

4. @No__t-1 **및** <xref:System.Windows.UIElement.MouseLeave> **에 대 한 애니메이션을 추가 합니다** **.**   다음으로 트리거에 일부 애니메이션을 추가 합니다. @No__t-0 블록 내의 아무 곳에 나 다음 태그를 추가 합니다.

    ```xaml
    <!-- Animations that start when mouse enters and leaves button. -->
    <EventTrigger RoutedEvent="Mouse.MouseEnter">
      <EventTrigger.Actions>
        <BeginStoryboard Name="mouseEnterBeginStoryboard">
          <Storyboard>
          <!-- This animation makes the glass rectangle shrink in the X direction. -->
            <DoubleAnimation Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)"
              By="-0.1" Duration="0:0:0.5" />
            <!-- This animation makes the glass rectangle shrink in the Y direction. -->
            <DoubleAnimation
            Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)"
              By="-0.1" Duration="0:0:0.5" />
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
    <EventTrigger RoutedEvent="Mouse.MouseLeave">
      <EventTrigger.Actions>
        <!-- Stopping the storyboard sets all animated properties back to default. -->
        <StopStoryboard BeginStoryboardName="mouseEnterBeginStoryboard" />
      </EventTrigger.Actions>
    </EventTrigger>
    ```

     마우스 포인터를 단추 위로 이동할 때 투명 효과 사각형이 축소 되 고 포인터가 벗어나면 정상 크기로 돌아갑니다.

     포인터가 단추 위로 이동할 때 (<xref:System.Windows.UIElement.MouseEnter> 이벤트가 발생 하는 경우) 두 개의 애니메이션이 트리거됩니다. 이러한 애니메이션은 X 및 Y 축을 따라 투명 효과 사각형을 축소 합니다. @No__t-0 요소의 속성 (<xref:System.Windows.Media.Animation.Timeline.Duration%2A> 및 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>)을 확인 합니다. @No__t-0은 애니메이션이 0.5 초 이상 발생 하도록 지정 하 고 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>은 투명 효과를 10% 축소 하도록 지정 합니다.

     두 번째 이벤트 트리거 (<xref:System.Windows.UIElement.MouseLeave>)는 단순히 첫 번째 트리거를 중지 합니다. @No__t-0을 중지 하면 애니메이션을 적용 하는 모든 속성이 해당 기본값으로 돌아갑니다. 따라서 사용자가 포인터를 단추 밖으로 움직이면 단추가 단추 위로 마우스 포인터를 이동 하기 전의 상태로 돌아갑니다. 애니메이션에 대 한 자세한 내용은 [애니메이션 개요](../graphics-multimedia/animation-overview.md)를 참조 하세요.

5. **단추를 클릭 하면에 대 한 애니메이션을 추가 합니다.** 마지막 단계는 사용자가 단추를 클릭할 때에 대 한 트리거를 추가 하는 것입니다. @No__t-0 블록 내의 아무 곳에 나 다음 태그를 추가 합니다.

    ```xaml
    <!-- Animation fires when button is clicked, causing glass to spin.  -->
    <EventTrigger RoutedEvent="Button.Click">
      <EventTrigger.Actions>
        <BeginStoryboard>
          <Storyboard>
            <DoubleAnimation Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[1].(RotateTransform.Angle)"
              By="360" Duration="0:0:0.5" />
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
    ```

     F5 키를 눌러 응용 프로그램을 실행 하 고 단추 중 하나를 클릭 합니다. 단추를 클릭 하면 투명 직사각형이 회전 합니다.

## <a name="summary"></a>요약
 이 연습에서는 다음 연습을 수행 했습니다.

- @No__t-0을 개체 형식 (<xref:System.Windows.Controls.Button>)으로 지정 합니다.

- @No__t-0을 사용 하 여 전체 응용 프로그램의 단추에 대해 제어 되는 기본 속성입니다.

- @No__t-0 setter의 속성 값에 사용할 그라데이션과 같은 리소스를 만들었습니다.

- 단추에 템플릿을 적용 하 여 전체 응용 프로그램에서 단추의 모양을 사용자 지정 했습니다.

- 사용자 동작에 대 한 응답으로 단추에 대 한 사용자 지정 동작 (예: <xref:System.Windows.UIElement.MouseEnter>, <xref:System.Windows.UIElement.MouseLeave>, <xref:System.Windows.Controls.Primitives.ButtonBase.Click>)-애니메이션 효과를 포함 합니다.

## <a name="see-also"></a>참조

- [Microsoft Expression Blend를 사용하여 단추 만들기](walkthrough-create-a-button-by-using-microsoft-expression-blend.md)
- [스타일 지정 및 템플릿](styling-and-templating.md)
- [애니메이션 개요](../graphics-multimedia/animation-overview.md)
- [단색 및 그라데이션을 사용한 그리기 개요](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [비트맵 효과 개요](../graphics-multimedia/bitmap-effects-overview.md)
