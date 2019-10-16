---
title: 세 가지 범주의 그래픽 서비스
ms.date: 03/30/2017
helpviewer_keywords:
- imaging
- graphics [Windows Forms], categories
- 2-D vector graphics
- vector graphics
- typography
ms.assetid: 068c0ef3-f6ee-4d58-a7b6-eb2531ead408
ms.openlocfilehash: a69fa7a1ccad353c879731de05dc47f0d6ae8795
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505236"
---
# <a name="three-categories-of-graphics-services"></a>세 가지 범주의 그래픽 서비스
Windows Forms의 그래픽 제공은 다음 세 가지 광범위 한 범주에 속합니다.  
  
- 2 차원 (2-d) 벡터 그래픽  
  
- 이미징  
  
- 입력 체계  
  
## <a name="2-d-vector-graphics"></a>2 차원 벡터 그래픽  
 2 차원 벡터 그래픽은 기본 형식입니다. 선, 곡선 및 도형; 등 좌표계의 점 집합으로 지정 됩니다. 예를 들어 직선 두 끝점으로 지정 된 및 사각형 왼쪽 위 구석에 해당 하 고 너비와 높이 지정 하는 숫자의 쌍의 위치를 제공 하는 지점으로 지정 됩니다. 간단한 경로 직선으로 연결 된 점의 배열에 의해 지정 됩니다. 베 지 어 스플라인을 지정 되는 정교한 곡선에서 4 개의 제어점입니다.  
  
 GDI + 자체, 기본 형식 그리는 방법에 대 한 정보를 저장 하는 클래스 및 드로잉을 실제로 수행 하는 클래스를 제공 클래스와 구조체는 기본 형식에 대 한 정보를 저장 하는 합니다. 예를 들어 합니다 <xref:System.Drawing.Rectangle> 구조; 사각형의 크기와 위치를 저장 합니다 <xref:System.Drawing.Pen> 선 색, 선 두께 및 선 스타일에 대 한 정보를 저장 하는 클래스 및 <xref:System.Drawing.Graphics> 클래스에 선, 사각형, 경로 그리기 위한 메서드 및 다른 수치입니다. 또한 여러 <xref:System.Drawing.Brush> 하는 방법에 대 한 정보를 저장 하는 클래스 수치 닫히고 경로 색 또는 패턴을 사용 하 여 채워집니다.  
  
 그래픽 명령 시퀀스는 벡터 이미지 메타 파일에 기록할 수 있습니다. GDI + 제공은 <xref:System.Drawing.Imaging.Metafile> 기록, 표시 및 메타 파일을 저장 하는 클래스입니다. 사용 하 여 합니다 <xref:System.Drawing.Imaging.MetafileHeader> 고 <xref:System.Drawing.Imaging.MetaHeader> 클래스 메타 파일 헤더에 저장 된 데이터를 검사할 수 있습니다.  
  
## <a name="imaging"></a>이미징  
 특정 종류의 그림 어렵거나 벡터 그래픽 기술을 사용 하 여 표시 됩니다. 예를 들어, 도구 모음 단추에서 사진과 아이콘으로 표시 되는 그림은 선 및 곡선 컬렉션으로 지정 하기 어렵습니다. 붐비는 야구 경기장 고해상도 디지털 사진 벡터 기법을 사용 하 여 만들려는 훨씬 더 어렵습니다. 이 유형의 이미지는 화면에 있는 각 점의 색을 나타내는 숫자의 배열 하는 비트맵으로 저장 됩니다. GDI + 제공은 <xref:System.Drawing.Bitmap> 표시, 조작 및 비트맵 저장에 대 한 클래스입니다.  
  
## <a name="typography"></a>입력 체계  
 입력 체계에는 다양 한 글꼴, 크기 및 스타일의에서 텍스트 표시 됩니다. GDI +이 복잡 한 작업에 대 한 광범위 한 지원을 제공합니다. GDI +의 새로운 기능 중 하나는 부드러운 모양이 LCD 화면에서 렌더링 되는 텍스트를 제공 하는 하위 픽셀 앤티 앨리어싱입니다.  
  
 Windows Forms에서 GDI 기능을 사용 하 여 텍스트를 그리는 옵션을 제공 하는 또한 해당 <xref:System.Windows.Forms.TextRenderer> 클래스입니다.  
  
## <a name="see-also"></a>참고자료

- [그래픽 개요](graphics-overview-windows-forms.md)
- [GDI + 관리 코드 정보](about-gdi-managed-code.md)
- [관리되는 그래픽 클래스 사용](using-managed-graphics-classes.md)
