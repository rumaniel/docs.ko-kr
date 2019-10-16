---
title: '방법: Viewport3D의 적중 테스트'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 3-D visuals [WPF], hit-testing for
- hit tests [WPF], for 3-D visuals
- Viewport3D [WPF]
ms.assetid: 42bfbd99-c7c6-43f1-940b-90448faa412e
ms.openlocfilehash: 6eb68f4668c6ea5aa8728a81fac98409896f3fd2
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70373264"
---
# <a name="how-to-hit-test-in-a-viewport3d"></a>방법: Viewport3D의 적중 테스트

이 예제에서는에서 3D 시각적 개체에 대 한 적중 테스트 <xref:System.Windows.Controls.Viewport3D>를 진행 하는 방법을 보여 줍니다.

는 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 2d 및 3d 정보를 반환 하기 때문에 테스트 결과를 반복 하 여 3d 결과만 읽을 수 있습니다.

[!code-csharp[HitTest3D#HitTest3D3DN4](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn4)]
[!code-vb[HitTest3D#HitTest3D3DN4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn4)]

다음 <xref:System.Windows.Media.HitTestResultBehavior> 코드의는 적중 테스트 결과를 처리 하는 방법을 결정 합니다. `UpdateResultInfo`및 `UpdateMaterial` 은 로컬로 정의 된 메서드입니다.

[!code-csharp[HitTest3D#HitTest3D3DN5](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn5)]
[!code-vb[HitTest3D#HitTest3D3DN5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn5)]
