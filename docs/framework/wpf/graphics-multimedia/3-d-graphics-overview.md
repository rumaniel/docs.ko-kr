---
title: 3차원 그래픽 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 3-D graphics [WPF]
- graphics [WPF], 3-D
ms.assetid: 67f31ed4-e36b-4b02-9889-dcce245d7afc
ms.openlocfilehash: 48f14ff145ad35dae3ba960191d34360cbec6173
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67664096"
---
# <a name="3-d-graphics-overview"></a>3차원 그래픽 개요
<a name="introduction"></a> 3 차원 기능 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 개발자가 그리기, 변환 및 태그 및 프로시저 코드로 3 차원 그래픽 애니메이션을 적용할 수 있도록 합니다. 개발자는 다양 한 컨트롤을 만들거나 복잡 한 데이터를 제공, 응용 프로그램 인터페이스의 사용자 환경을 개선 하려면 2d 및 3d 그래픽을 결합할 수 있습니다. 3 차원 지원 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 갖춘 게임 개발 플랫폼을 제공 하도록 설계 되지 않았습니다. 이 항목에서 3 차원 기능의 개요를 제공 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 그래픽 시스템입니다.  

<a name="threed_in_2d"></a>   
## <a name="3-d-in-a-2-d-container"></a>2차원 컨테이너의 3차원  
 3 차원 그래픽 콘텐츠 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 요소에 캡슐화 되어 <xref:System.Windows.Controls.Viewport3D>, 2 차원 요소 구조에 참여할 수 있는 합니다. 그래픽 시스템 처리 <xref:System.Windows.Controls.Viewport3D> 의 다른 많은 요소 처럼 2 차원 시각적 요소로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다. <xref:System.Windows.Controls.Viewport3D> 창으로 함수-뷰포트-3 차원 장면에 있습니다. 보다 정확히 말해 이는 3차원 장면이 프로젝션되는 표면입니다.  
  
 기존의 2 차원 응용 프로그램에서 사용 하 여 <xref:System.Windows.Controls.Viewport3D> Grid 나 Canvas와 같은 다른 컨테이너 요소와 마찬가지로 합니다.  사용할 수 있지만 <xref:System.Windows.Controls.Viewport3D> 다른 2 차원 그리기 개체와 동일한 장면 그래프에서 내에서 2 차원 및 3 차원 개체를 상호 침투할 수 없습니다는 <xref:System.Windows.Controls.Viewport3D>합니다.  이 항목에서는 내에서 3 차원 그래픽을 그리는 방법을 중점적는 <xref:System.Windows.Controls.Viewport3D>합니다.  
  
<a name="coord_space"></a>   
## <a name="3-d-coordinate-space"></a>3차원 좌표 공간  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 2 차원 그래픽 좌표계는 렌더링 영역 (일반적으로 화면)의 왼쪽 위에서 원점을 찾습니다. 2차원 시스템에서 양의 x-축 값은 오른쪽으로 진행되고 양의 y-축 값은 아래로 진행됩니다.  하지만 3 차원 좌표계에서 원본에 렌더링 영역의 중앙 양의 x-축 값은 오른쪽으로 진행 되지만 양의 y-축 값은 대신 위로 진행 및 원본에서 바깥쪽으로 진행 하는 양의 z-축 값 에서 뷰어를 포함 합니다.  
  
 ![좌표계](./media/coordsystem-1.png "CoordSystem-1")  
기존의 2차원 및 3차원 좌표계 표현  
  
 이러한 축으로 정의되는 공간은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 3차원 개체에 대한 고정 참조 프레임입니다. 이 공간에서 모델을 빌드하고 이를 보기 위한 광원과 카메라를 만들 때는 변환 적용 시 각 모델에 대해 만드는 로컬 참조 프레임을 이 고정 참조 프레임 또는 "월드 공간"과 구분하면 유용합니다. 또한 월드 공간의 개체는 광원 및 카메라 설정에 따라 완전히 다르게 보이거나 전혀 보이지 않을 수 있지만 카메라의 위치는 월드 공간에서 개체의 위치를 변경하지 않습니다.  
  
<a name="cameras"></a>   
## <a name="cameras-and-projections"></a>카메라 및 프로젝션  
 2 차원에서 작업 하는 개발자가 익숙한 2 차원 화면에서 그리기 기본 형식을 배치 합니다. 3 차원 장면의 만들 때 3 차원 개체의 2 차원 표현을 작성 하 고 실제로는 고려해 야 합니다. 3 차원 장면을 보는 관점에 따라 다르게 보이는 때문에 해당 시점을 지정 해야 합니다. <xref:System.Windows.Media.Media3D.Camera> 클래스를 사용 하면이 관점 3 차원 장면에 대 한를 지정할 수 있습니다.  
  
 3 차원 장면 2 차원 화면에 표시 됩니다 하는 방법을 이해 하는 다른 방법은 장면을 보기 표면에 프로젝션으로 설명 하 여 것입니다. <xref:System.Windows.Media.Media3D.ProjectionCamera> 다른 프로젝션 및 보는 3 차원 모델을 표시 하는 방법을 변경 하려면 해당 속성을 지정할 수 있습니다. <xref:System.Windows.Media.Media3D.PerspectiveCamera> 는 장면을 단축 하는 프로젝션을 지정 합니다.  즉,는 <xref:System.Windows.Media.Media3D.PerspectiveCamera> 소실점 원근감을 제공 합니다.  장면 좌표 공간에서의 카메라 위치, 카메라의 방향 및 시야, 장면의 "위쪽" 방향을 정의하는 벡터를 지정할 수 있습니다. 다음 다이어그램은 <xref:System.Windows.Media.Media3D.PerspectiveCamera>의 프로젝션 합니다.  
  
 <xref:System.Windows.Media.Media3D.ProjectionCamera.NearPlaneDistance%2A> 하 고 <xref:System.Windows.Media.Media3D.ProjectionCamera.FarPlaneDistance%2A> 의 속성 <xref:System.Windows.Media.Media3D.ProjectionCamera> 카메라 프로젝션의 범위를 제한 합니다. 카메라는 장면의 어느 위치에나 배치될 수 있으므로 카메라가 실제로 모델 내 또는 모델에 매우 가깝게 배치될 수 있으며 이로 인해 개체를 제대로 구별하기가 어려워집니다.  <xref:System.Windows.Media.Media3D.ProjectionCamera.NearPlaneDistance%2A> 초과 하는 개체를 그릴 수 없는 최소 거리를 지정할 수 있습니다.  반대로, <xref:System.Windows.Media.Media3D.ProjectionCamera.FarPlaneDistance%2A> 지나면 개체를 그릴 수 없는, 장면에서 인식할 수 없는 너무 멀리 떨어진 곳에 개체를 포함 하지 않도록 보장 하는 카메라의 거리를 지정할 수 있습니다.  
  
 ![카메라 설정](./media/coordsystem-6.png "CoordSystem 6")  
카메라 위치  
  
 <xref:System.Windows.Media.Media3D.OrthographicCamera> 2 차원 시각적 화면에 3 차원 모델의 직교 프로젝션을 지정합니다. 다른 카메라와 마찬가지로 이는 위치, 보기 방향 및 "위쪽" 방향을 지정합니다. 와 달리 <xref:System.Windows.Media.Media3D.PerspectiveCamera>그러나 <xref:System.Windows.Media.Media3D.OrthographicCamera> 원근 단축법을 포함 하지 않는 프로젝션을 설명 합니다. 즉, <xref:System.Windows.Media.Media3D.OrthographicCamera> 는 카메라에서 지점에서 만나는 것이 아니라 평행한 보기 상자를 설명 합니다. 다음 이미지를 사용 하 여 표시 된 대로 동일한 모델을 보여 줍니다 <xref:System.Windows.Media.Media3D.PerspectiveCamera> 고 <xref:System.Windows.Media.Media3D.OrthographicCamera>입니다.  
  
 ![직교 및 원근 프로젝션](./media/camera-projections4.png "Camera_projections4")  
원근 및 직교 프로젝션  
  
 다음 코드에서는 일반적인 카메라 설정을 보여 줍니다.  
  
 [!code-csharp[3dgallery_procedural_snip#Basic3DShapeCodeExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Basic3DShapeExample.cs#basic3dshapecodeexampleinline1)]
 [!code-vb[3dgallery_procedural_snip#Basic3DShapeCodeExampleInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/basic3dshapeexample.vb#basic3dshapecodeexampleinline1)]  
  
<a name="models_meshes"></a>   
## <a name="model-and-mesh-primitives"></a>모델 및 메시 기본 형식  
  
 <xref:System.Windows.Media.Media3D.Model3D> 제네릭 3 차원 개체를 나타내는 추상 기본 클래스가입니다. 3 차원 장면의 빌드하려면를 보려면 개체 및 장면 그래프를 구성 하는 개체에서 파생 <xref:System.Windows.Media.Media3D.Model3D>합니다. 현재는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용 하 여 기 하 도형을 모델링 지원 <xref:System.Windows.Media.Media3D.GeometryModel3D>합니다. <xref:System.Windows.Media.Media3D.GeometryModel3D.Geometry%2A> 이 모델의 속성은 메시 기본입니다.  
  
 모델을 빌드하려면 먼저 기본 형식 또는 메시를 빌드합니다. 3 차원 기본 형식은 단일 3 차원 엔터티를 구성 하는 꼭 짓 점의 컬렉션입니다. 가장 간단한 닫힌된 그림에서 모델링 하는 기본 요소를 제공 하는 대부분의 3 차원 시스템: 세 가지 꼭 짓 점 정의한 삼각형입니다.  삼각형의 세 점은 같은 평면에 있으므로 메시라는 보다 복잡한 도형을 모델링하기 위해 계속해서 삼각형을 추가할 수 있습니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 3 차원 시스템에서 현재 제공는 <xref:System.Windows.Media.Media3D.MeshGeometry3D> 클래스 모든 기 하 도형을 지정할 수 있습니다 않으며, 현재 및 입방 형과 같은 미리 정의 된 지원 3 차원 기본 형식입니다. 만들기를 시작을 <xref:System.Windows.Media.Media3D.MeshGeometry3D> 으로 삼각형 꼭 짓 점 목록을 지정 하 여 해당 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> 속성입니다. 로 지정 된 각 꼭 짓 점에 <xref:System.Windows.Media.Media3D.Point3D>합니다.  [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]에서는 이 속성을 각 꼭짓점의 좌표를 나타내는 세 숫자가 그룹화된 목록으로 지정합니다. 해당 기하 도형에 따라 메시는 여러 개의 삼각형으로 구성될 수 있고 그 중 일부는 같은 모퉁이(꼭짓점)를 공유할 수 있습니다. 메시를 올바르게 그리려면 어떤 삼각형에 어떤 꼭짓점이 공유되는지에 대한 정보를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에 제공해야 합니다. 통해 삼각형 인덱스 목록을 지정 하 여이 정보를 제공 하는 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> 속성입니다. 이 목록에 지정 된 요소는 순서를 지정 된 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> 목록 삼각형을 결정 합니다.  
  
 [!code-xaml[basic3d#Basic3DXAML3DN3](~/samples/snippets/xaml/VS_Snippets_Wpf/Basic3D/XAML/Window1.xaml#basic3dxaml3dn3)]  
  
 앞의 예제에는 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> 목록은 큐브 모양의 메시를 정의 하는 8 개 꼭지점을 지정 합니다. <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> 속성에는 3 개의 인덱스를 12 개 그룹의 목록을 지정 합니다.  목록의 각 숫자에 오프셋을 나타냅니다는 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> 목록입니다.  예를 들어, 처음 세 개의 꼭 짓 점을 지정 된는 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> 목록 됩니다 (1,1,0) (0,1,0) 및 (0,0,0). 지정 된 첫 3 개의 인덱스를 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A> 목록에는 0, 2 및 1, 첫 번째에 해당 하는 세 번째, 두 번째 점에는 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A> 목록. 그 결과 큐브 모델을 구성하는 첫 번째 삼각형은 (1,1,0)에서 (0,1,0) 및 (0,0,0)으로 이어지고 나머지 11개의 삼각형도 이와 비슷하게 결정됩니다.  
  
 계속 모델에 대 한 값을 지정 하 여 정의할 수는 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A> 고 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> 속성입니다.  모델의 표면을 렌더링하려면 지정된 임의의 삼각형에서 해당 표면이 어느 방향을 바라보고 있는지에 대한 정보를 그래픽 시스템에 제공해야 합니다. 그래픽 시스템은 이 정보를 사용하여 모델에 대한 조명 계산을 수행할 수 있습니다. 즉, 광원 쪽 표면이 광원 반대쪽 표면보다 밝게 나타납니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 위치 좌표를 사용하여 기본 법선 벡터를 결정할 수 있지만 다른 법선 벡터를 지정하여 곡선 표면의 모양을 대략적으로 나타낼 수도 있습니다.  
  
 합니다 <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> 속성의 컬렉션을 지정 <xref:System.Windows.Point>메시의 꼭 짓 점에 질감이 그려지는 방법을 결정 하는 좌표를 매핑하는 방법을 그래픽 시스템에 알려주는 합니다. <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A> 0과 1 사이의 값으로 지정 됩니다.  마찬가지로 <xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A> 속성, 질감 좌표를 기본값이 되지만 예를 들어 반복 패턴의 일부를 포함 하는 질감의 매핑을 제어 하는 다른 질감 좌표를 설정 하도록 선택할 수 있습니다 그래픽 시스템을 계산할 수 있습니다. 질감 좌표에 대한 자세한 내용은 다음 항목 또는 Managed Direct3D SDK를 참조하세요.  
  
 다음 예제에서는 프로시저 코드로 큐브 모델의 한 면을 만드는 방법을 보여 줍니다. 큐브 전체를 단일 GeometryModel3D로 그릴 수 있지만 이 예제에서는 나중에 각 면에 별도의 질감을 적용하기 위해 큐브 면을 고유한 모델로 그립니다.  
  
 [!code-csharp[3doverview#3DOverview3DN6](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn6)]
 [!code-vb[3doverview#3DOverview3DN6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn6)]  
  
 [!code-csharp[3doverview#3DOverview3DN7](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn7)]
 [!code-vb[3doverview#3DOverview3DN7](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn7)]  
  
<a name="materials"></a>   
## <a name="applying-materials-to-the-model"></a>모델에 재질 적용  
  
 메시가 3차원 개체로 보이도록 만들려면 카메라로 비추고 프로젝션할 수 있도록 해당 꼭짓점과 삼각형으로 정의된 표면에 질감을 적용해야 합니다. 2 차원에서 사용 하 여는 <xref:System.Windows.Media.Brush> 화면 영역에 색, 패턴, 그라데이션 또는 기타 시각적 콘텐츠를 적용 하는 클래스입니다.  3 차원 개체의 모양을 것 인데, 조명 모델의 뿐 아니라 색 또는 패턴을 적용 하는 함수입니다. 실제 개체는 표면의 품질에 따라 빛을 다르게 반사합니다. 광택이 나거나 빛나는 표면은 거칠거나 윤기 없는 표면과 다르게 보이며 어떤 개체는 빛을 흡수하는 것처럼 보이는 반면 다른 개체는 빛이 납니다. 적용할 수 있는 동일한 브러시 2 차원 개체에 적용할 수 있는 3 차원 개체 있지만 직접 적용할 수 없습니다.  
  
 모델의 표면의 특징을 정의할 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용 하는 <xref:System.Windows.Media.Media3D.Material> 추상 클래스입니다. Material의 구체적 하위 클래스는 모델 표면의 일부 모양 특성을 결정하며 이들 각각은 SolidColorBrush, TileBrush 또는 VisualBrush를 전달할 수 있는 Brush 속성도 제공합니다.  
  
- <xref:System.Windows.Media.Media3D.DiffuseMaterial> 브러시는 모델 처럼 모델에 적용 됩니다 지정 합니다. 브러시를 사용 하 여 2 차원 모델에 직접 유사 가장 DiffuseMaterial을 사용 하 여 모델의 표면은 빛나는 것 처럼 빛을 반영 하지 않습니다.  
  
- <xref:System.Windows.Media.Media3D.SpecularMaterial> 하드 또는 반짝이 하이라이트를 반사할 수 있는 모델의 표면 인 것 처럼 브러시가 모델에 적용할 수를 지정 합니다. 에 대 한 값을 지정 하 여 하려는 질감에이 반사 품질 또는 "빛나는 정도 설정할 수 있습니다는 <xref:System.Windows.Media.Media3D.SpecularMaterial.SpecularPower%2A> 속성입니다.  
  
- <xref:System.Windows.Media.Media3D.EmissiveMaterial> 모델와 같은 브러시의 색으로 빛을 내보내는 것 처럼 질감이 적용 되도록 지정할 수 있습니다. 그러나 이로 인해 모델이 광원이 되는 것은 아니며 DiffuseMaterial 또는 SpecularMaterial을 사용하여 질감을 표현할 때와는 다른 방식으로 섀도잉에 참여합니다.  
  
 보다 나은 성능,의 뒷면을 <xref:System.Windows.Media.Media3D.GeometryModel3D> (카메라에서 모델의 반대쪽에 있기 때문에 보이지 않는 면)은 장면에서 선별 됩니다.  지정 하는 <xref:System.Windows.Media.Media3D.Material> 평면과 같이 모델의 뒷면에 적용 하려면 모델의 설정 <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> 속성입니다.  
  
 빛이 나거나 반사되는 효과와 같은 일부 표면 품질을 얻으려면 모델에 여러 개의 서로 다른 브러시를 연속으로 적용해야 할 수 있습니다. 적용 하 고 사용 하 여 여러 재질을 재사용할 수 있습니다는 <xref:System.Windows.Media.Media3D.MaterialGroup> 클래스입니다. MaterialGroup의 자식이 맨 먼저 적용되어 여러 렌더링 패스에서 지속됩니다.  
  
 다음 코드 예제에서는 브러시로 그리기 및 단색 3 차원 모델에 적용 하는 방법을 보여 줍니다.  
  
 [!code-xaml[basic3d#Basic3DXAML3DN5](~/samples/snippets/xaml/VS_Snippets_Wpf/Basic3D/XAML/Window1.xaml#basic3dxaml3dn5)]  
  
 [!code-xaml[3doverview#3DOverview3DN9](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/app.xaml#3doverview3dn9)]  
  
 [!code-csharp[3doverview#3DOverview3DN8](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn8)]
 [!code-vb[3doverview#3DOverview3DN8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn8)]  
  
<a name="lights"></a>   
## <a name="illuminating-the-scene"></a>장면 비추기  
 3 차원 그래픽의 광원의 실제 수행: 표면이 보이도록 만듭니다. 보다 정확히 말해 광원은 프로젝션에 포함될 장면의 부분을 결정합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 광원 개체는 다양한 명암 효과를 만들며 여러 실제 광원의 동작을 기반으로 모델링됩니다. 장면에 하나 이상의 광원을 포함하지 않으면 모델이 보이지 않습니다.  
  
 다음 광원은 기본 클래스에서 파생 <xref:System.Windows.Media.Media3D.Light>:  
  
- <xref:System.Windows.Media.Media3D.AmbientLight>: 모든 개체 위치나 방향 관계 없이 균일 하 게 비추는 주변 광원을 제공 합니다.  
  
- <xref:System.Windows.Media.Media3D.DirectionalLight>: 비춥니다 것 처럼 비춥니다.  방향성 광원이는 <xref:System.Windows.Media.Media3D.DirectionalLight.Direction%2A> Vector3D 하지만 지정 된 위치가 없고로 지정 합니다.  
  
- <xref:System.Windows.Media.Media3D.PointLight>: 광원이 가까이 있는 것 처럼 비춥니다. PointLight는 위치가 있으며 해당 위치에서 빛을 발합니다. 장면의 개체는 광원과 관련된 해당 위치 및 거리에 따라 비춰집니다. <xref:System.Windows.Media.Media3D.PointLightBase> 노출 된 <xref:System.Windows.Media.Media3D.PointLightBase.Range%2A> 초과 모델 비춰 지지 조명에서 거리를 결정 하는 속성입니다. 또한 PointLight는 거리에 따라 광원의 강도가 감소되는 방식을 결정하는 감쇠 속성도 노출합니다. 광원 감쇠에 대해 상수, 선형 또는 정방형 보간을 지정할 수 있습니다.  
  
- <xref:System.Windows.Media.Media3D.SpotLight>: <xref:System.Windows.Media.Media3D.PointLight>에서 상속됩니다. SpotLight는 PointLight와 유사하게 비추며 위치와 방향이 모두 있습니다. 설정한 원뿔 모양 영역에 광원을 프로젝션 <xref:System.Windows.Media.Media3D.SpotLight.InnerConeAngle%2A> 고 <xref:System.Windows.Media.Media3D.SpotLight.OuterConeAngle%2A> 속성을 각도로 지정 합니다.  
  
 광원은 <xref:System.Windows.Media.Media3D.Model3D> 개체를 변환 및 조명 속성, 위치, 색, 방향 및 범위를 포함 하 여 애니메이션을 적용할 수 있도록 합니다.  
  
 [!code-xaml[hittest3d#HitTest3D3DN6](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml#hittest3d3dn6)]  
  
 [!code-csharp[basic3d#Basic3D3DN11](~/samples/snippets/csharp/VS_Snippets_Wpf/Basic3D/CSharp/Window1.xaml.cs#basic3d3dn11)]
 [!code-vb[basic3d#Basic3D3DN11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Basic3D/visualbasic/window1.xaml.vb#basic3d3dn11)]  
  
 [!code-csharp[basic3d#Basic3D3DN12](~/samples/snippets/csharp/VS_Snippets_Wpf/Basic3D/CSharp/Window1.xaml.cs#basic3d3dn12)]
 [!code-vb[basic3d#Basic3D3DN12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Basic3D/visualbasic/window1.xaml.vb#basic3d3dn12)]  
  
 [!code-csharp[basic3d#Basic3D3DN13](~/samples/snippets/csharp/VS_Snippets_Wpf/Basic3D/CSharp/Window1.xaml.cs#basic3d3dn13)]
 [!code-vb[basic3d#Basic3D3DN13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Basic3D/visualbasic/window1.xaml.vb#basic3d3dn13)]  
  
<a name="transforms"></a>   
## <a name="transforming-models"></a>모델 변환  
 모델을 만들 때 모델에는 장면에서의 특정 위치가 지정됩니다. 장면에서 이러한 모델을 이동하거나, 회전하거나, 크기를 변경하기 위해 모델 자체를 정의하는 꼭짓점을 변경하는 것은 비효율적입니다.  대신 2차원에서와 같이 모델에 변환을 적용합니다.  
  
 각 모델 개체에는 <xref:System.Windows.Media.Media3D.Model3D.Transform%2A> 속성이 있는 이동, 방향을 다시 지정 하거나 모델의 크기를 조정 합니다.  변환을 적용할 때는 변환에 의해 지정된 벡터 또는 값이 무엇이든 실제적으로 모델의 모든 점을 오프셋합니다. 즉, 모델이 정의된 좌표 공간("모델 공간")은 변환하지만 장면 전체("월드 공간")의 좌표계에서 모델의 기하 도형을 구성하는 값은 변경하지 않습니다.  
  
 모델 변환에 대한 자세한 내용은 [3차원 변환 개요](3-d-transformations-overview.md)를 참조하세요.  
  
<a name="animations"></a>   
## <a name="animating-models"></a>모델에 애니메이션 효과 주기  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 3차원 구현은 2차원 그래픽과 동일한 타이밍 및 애니메이션 시스템에 참여합니다. 즉, 3차원 장면에 애니메이션 효과를 주려면 해당 모델의 속성에 애니메이션 효과를 줍니다. 기본 형식의 속성에 직접 애니메이션 효과를 줄 수도 있지만 일반적으로 모델의 위치나 모양을 변경하는 변환에 애니메이션 효과를 주는 것이 보다 쉽습니다. 변환을 적용할 수 있으므로 <xref:System.Windows.Media.Media3D.Model3DGroup> 개별 모델 뿐만 아니라 개체 Model3DGroup의 자식 및 다른 애니메이션 집합을 자식 개체의 그룹에 한 애니메이션 집합을 적용할 수 있습니다. 장면의 조명 속성에 애니메이션 효과를 주어 다양한 시각적 효과를 얻을 수도 있습니다. 마지막으로 카메라 위치 또는 시야에 애니메이션 효과를 주어 프로젝션 자체에 애니메이션 효과를 주도록 선택할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 타이밍 및 애니메이션 시스템에 대한 배경 정보는 [애니메이션 개요](animation-overview.md), [Storyboard 개요](storyboards-overview.md) 및 [Freezable 개체 개요](../advanced/freezable-objects-overview.md) 항목을 참조하세요.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 개체에 애니메이션 효과를 주려면 타임라인을 만들고 애니메이션(시간이 지남에 따른 일부 속성 값의 변경)을 정의한 다음 애니메이션을 적용할 속성을 지정합니다. 3 차원 장면에 있는 모든 개체의 자식 이므로 <xref:System.Windows.Controls.Viewport3D>, 장면에 적용 하려는 모든 애니메이션의 대상 속성은 Viewport3D의 속성입니다.  
  
 모델이 제자리에서 비틀거리는 것처럼 보이게 만든다고 가정합니다. 적용 하도록 선택할 수 있습니다는 <xref:System.Windows.Media.Media3D.RotateTransform3D> 모델에의 한 벡터에서 다른 벡터로 회전 축에 애니메이션을 적용 합니다. 다음 코드 예제에서는 RotateTransform3D가 TransformGroup이 있는 모델에 적용된 여러 변환 중 하나라는 가정 하에 변환의 Rotation3D에 대한 Axis 속성에 Vector3DAnimation을 적용하는 방법을 보여 줍니다.  
  
 [!code-csharp[3doverview#3DOverview3DN1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn1)]
 [!code-vb[3doverview#3DOverview3DN1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn1)]  
  
 [!code-csharp[3doverview#3DOverview3DN3](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn3)]
 [!code-vb[3doverview#3DOverview3DN3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn3)]  
  
 [!code-csharp[3doverview#3DOverview3DN4](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn4)]
 [!code-vb[3doverview#3DOverview3DN4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn4)]  
  
 [!code-csharp[3doverview#3DOverview3DN5](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn5)]
 [!code-vb[3doverview#3DOverview3DN5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn5)]  
  
<a name="animations1"></a>   
## <a name="add-3-d-content-to-the-window"></a>창에 3차원 콘텐츠 추가  
 장면을 렌더링에 모델과 광원을 추가 <xref:System.Windows.Media.Media3D.Model3DGroup>, 설정한 합니다 <xref:System.Windows.Media.Media3D.Model3DGroup> 으로 <xref:System.Windows.Media.Media3D.ModelVisual3D.Content%2A> 의 <xref:System.Windows.Media.Media3D.ModelVisual3D>입니다. 추가 <xref:System.Windows.Media.Media3D.ModelVisual3D> 에 <xref:System.Windows.Controls.Viewport3D.Children%2A> 의 컬렉션을 <xref:System.Windows.Controls.Viewport3D>합니다. 카메라를 추가 합니다 <xref:System.Windows.Controls.Viewport3D> 설정 하 여 해당 <xref:System.Windows.Controls.Viewport3D.Camera%2A> 속성입니다.  
  
 마지막으로 추가 된 <xref:System.Windows.Controls.Viewport3D> 창에 있습니다. 경우는 <xref:System.Windows.Controls.Viewport3D> 설정 하 여 Viewport3D의 크기를 지정 하는 캔버스와 같은 레이아웃 요소의 내용으로 포함 되어 해당 <xref:System.Windows.FrameworkElement.Height%2A> 및 <xref:System.Windows.FrameworkElement.Width%2A> 속성 (에서 상속 되며, <xref:System.Windows.FrameworkElement>).  
  
 [!code-xaml[hostingwpfusercontrolinwf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Viewport3D>
- <xref:System.Windows.Media.Media3D.PerspectiveCamera>
- <xref:System.Windows.Media.Media3D.DirectionalLight>
- <xref:System.Windows.Media.Media3D.Material>
- [3차원 변환 개요](3-d-transformations-overview.md)
- [WPF 3D 성능 최대화](maximize-wpf-3d-performance.md)
- [방법 항목](3-d-graphics-how-to-topics.md)
- [WPF에서 Shape 및 기본 그리기 개요](shapes-and-basic-drawing-in-wpf-overview.md)
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
