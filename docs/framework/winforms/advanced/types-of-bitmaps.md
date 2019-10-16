---
title: 비트맵의 유형
ms.date: 03/30/2017
helpviewer_keywords:
- jpeg files
- TIFF files
- gif files
- Graphics Interchange Format
- Joint Photographic Experts Group
- .jpeg files
- .gif files
- graphics [Windows Forms], file formats
- images [Windows Forms], file formats
- Portable Network Graphics
- .bmp files
- EXIF file format
- PNG files
- pictures [Windows Forms], file formats
- Tag Image File Format
- bitmaps [Windows Forms], file format
- Exchangeable Image File
ms.assetid: 6be085a2-2c13-47c8-b80a-c18b32777d8d
ms.openlocfilehash: 2243c9ce2d8ba741143d301c38e8b88d7b196c98
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914819"
---
# <a name="types-of-bitmaps"></a>비트맵의 유형
비트맵은 사각형의 픽셀 배열에서 각 픽셀의 색을 지정 하는 비트의 배열입니다. 개별 픽셀에 할당 되는 비트 수에 따라 해당 픽셀에 할당 될 수 있는 색의 수가 결정 됩니다. 예를 들어 각 픽셀이 4 비트로 표시 되는 경우 지정 된 픽셀에는 16 가지 다른 색 (2 ^ 4 = 16) 중 하나를 할당할 수 있습니다. 다음 표에서는 지정 된 비트 수로 표현 되는 픽셀에 할당할 수 있는 색 수의 몇 가지 예를 보여 줍니다.  
  
|픽셀당 비트 수|픽셀에 할당할 수 있는 색의 수|  
|--------------------|------------------------------------------------------|  
|1|2^1 = 2|  
|2|2^2 = 4|  
|4|2^4 = 16|  
|8|2^8 = 256|  
|16|2^16 = 65,536|  
|24|2^24 = 16,777,216|  
  
 비트맵을 저장 하는 디스크 파일은 일반적으로 픽셀당 비트 수, 각 행의 픽셀 수 및 배열의 행 수와 같은 정보를 저장 하는 하나 이상의 정보 블록을 포함 합니다. 이러한 파일에는 색상표 라고도 하는 색 테이블이 포함 될 수도 있습니다. 색 테이블은 비트맵의 숫자를 특정 색에 매핑합니다. 다음 그림에서는 비트맵 및 색 표와 함께 확대 된 이미지를 보여 줍니다. 각 픽셀은 4 비트 숫자로 표시 되므로 색 테이블에 2 ^ 4 = 16 색이 있습니다. 테이블의 각 색은 24 비트 숫자로 표시 됩니다. 빨강의 경우 8 비트, 녹색의 경우 8 비트, 파랑의 경우 8 비트 숫자는 16 진수 (기 수 16) 형식으로 표시 됩니다. A = 10, B = 11, C = 12, D = 13, E = 14, F = 15.  
  
 ![Bitmap 샘플](./media/aboutgdip03-art01.gif "AboutGdip03_Art01")  
  
 이미지의 행 3, 열 5에서 픽셀을 확인 합니다. 비트맵의 해당 숫자는 1입니다. 색 테이블은 1은 빨간색을 나타내므로 픽셀이 빨강 임을 나타냅니다. 비트맵의 맨 위 행에 있는 모든 항목은 3입니다. 색 테이블은 3이 blue를 나타내므로 이미지의 맨 위 행에 있는 모든 픽셀이 파란색 임을 나타냅니다.  
  
> [!NOTE]
> 일부 비트맵은 상향식 형식으로 저장 됩니다. 비트맵의 첫 번째 행에 있는 숫자는 이미지 아래쪽 행의 픽셀에 해당 합니다.  
  
 인덱스를 색 테이블에 저장 하는 비트맵을 색상표 인덱스 비트맵 이라고 합니다. 일부 비트맵에서는 색 테이블이 필요 하지 않습니다. 예를 들어 비트맵이 픽셀당 24 비트를 사용 하는 경우 비트맵은 색 테이블에 인덱스가 아닌 색을 저장할 수 있습니다. 다음 그림에서는 색 표를 사용 하는 대신 색을 직접 저장 하는 비트맵 (픽셀 당 24 비트)을 보여 줍니다. 이 그림에서는 해당 이미지의 확대 된 보기도 보여 줍니다. 비트맵에서 FFFFFF는 흰색, FF0000는 빨강, 00FF00는 녹색, 0000FF>MICROSOFT는 blue를 나타냅니다.  
  
 ![Bitmap 샘플](./media/aboutgdip03-art02.gif "AboutGdip03_Art02")  
  
## <a name="graphics-file-formats"></a>그래픽 파일 형식  
 비트맵을 디스크 파일에 저장 하는 데는 여러 가지 표준 형식이 있습니다. GDI +는 다음 단락에 설명 된 그래픽 파일 형식을 지원 합니다.  
  
### <a name="bmp"></a>BMP  
 BMP는 Windows에서 장치 독립적 및 응용 프로그램 독립적 이미지를 저장 하는 데 사용 하는 표준 형식입니다. 지정 된 BMP 파일의 픽셀 당 비트 수 (1, 4, 8, 15, 24, 32 또는 64)는 파일 헤더에 지정 됩니다. 픽셀당 24 비트의 BMP 파일은 일반적입니다. BMP 파일은 일반적으로 압축 되지 않으므로 인터넷을 통해 전송 하는 데 적합 하지 않습니다.  
  
### <a name="graphics-interchange-format-gif"></a>GIF(Graphics Interchange Format)  
 GIF는 웹 페이지에 표시 되는 이미지의 일반적인 형식입니다. Gif는 선 그리기, 단색 블록의 그림, 색 사이에 선명한 경계가 있는 그림 등에서 잘 작동 합니다. Gif는 압축 되지만 압축 프로세스에서 정보는 손실 되지 않습니다. 압축을 푼 이미지는 원래와 정확히 동일 합니다. GIF에서 색 하나를 투명 하 게 지정 하 여 이미지에 표시 되는 모든 웹 페이지의 배경색을 지정할 수 있습니다. GIF 이미지 시퀀스는 애니메이션 GIF를 형성 하기 위해 단일 파일에 저장할 수 있습니다. Gif는 픽셀당 최대 8 비트를 저장 하므로 256 색으로 제한 됩니다.  
  
### <a name="joint-photographic-experts-group-jpeg"></a>공동 사진 전문가 그룹 (JPEG)  
 JPEG는 스캔 한 사진과 같은 자연 스러운 장면에서 잘 작동 하는 압축 체계입니다. 일부 정보는 압축 프로세스에서 손실 되지만 종종 사용자 눈에 imperceptible 수 있습니다. Jpeg는 픽셀당 24 비트를 저장 하므로 1600만 개 보다 많은 색을 표시할 수 있습니다. Jpeg는 투명도 또는 애니메이션을 지원 하지 않습니다.  
  
 JPEG 이미지의 압축 수준은 구성 가능 하지만 더 높은 압축 수준 (작은 파일)으로 인해 정보가 손실 됩니다. 20:1 압축 비율은 종종 인간 눈동자에서 원래와 구별 하기 어려운 이미지를 생성 합니다. 다음 그림은 bmp 이미지와 해당 BMP 이미지에서 압축 된 두 개의 JPEG 이미지를 보여 줍니다. 첫 번째 JPEG의 압축 비율은 4:1이 고, 두 번째 JPEG의 압축 비율은 약 8:1입니다.  
  
 ![Filetype 샘플](./media/aboutgdip03-art03.gif "AboutGdip03_Art03")  
  
 JPEG 압축은 선 그리기, 단색 블록 및 선명한 경계의 경우 제대로 작동 하지 않습니다. 다음 그림에서는 두 개의 Jpeg와 GIF를 함께 사용 하는 BMP를 보여 줍니다. Jpeg와 GIF는 BMP에서 압축 되었습니다. 압축 비율은 GIF의 경우 4:1, 작은 JPEG의 경우 4:1, 큰 JPEG의 경우 8:3입니다. GIF는 선을 따라 선명한 경계를 유지 하지만 Jpeg는 경계를 흐리게 하는 경향이 있습니다.  
  
 ![Filetypes](./media/aboutgdip03-art03a.gif "AboutGdip03_Art03A")  
  
 JPEG는 파일 형식이 아니라 압축 스키마입니다. JPEG 파일 교환 형식 (.JFIF)은 JPEG 체계에 따라 압축 된 이미지를 저장 하 고 전송 하는 데 일반적으로 사용 되는 파일 형식입니다. 웹 브라우저에서 표시 되는 .JFIF 파일은 .jpg 확장명을 사용 합니다.  
  
### <a name="exchangeable-image-file-exif"></a>EXIF (교환 이미지 파일)  
 EXIF는 디지털 카메라에서 캡처한 사진에 사용 되는 파일 형식입니다. EXIF 파일은 JPEG 사양에 따라 압축 된 이미지를 포함 합니다. 또한 EXIF 파일에는 사진 (찍은 날짜, 셔터 속도, 노출 시간 등) 및 카메라에 대 한 정보 (제조업체, 모델 등)에 대 한 정보가 포함 되어 있습니다.  
  
### <a name="portable-network-graphics-png"></a>PNG(이동식 네트워크 그래픽)  
 PNG 형식은 GIF 형식의 많은 이점을 제공 하지만 GIF 이외의 기능도 제공 합니다. GIF 파일과 마찬가지로 PNG 파일은 정보의 손실 없이 압축 됩니다. PNG 파일은 픽셀당 8, 24 또는 48 비트 및 회색조 1, 2, 4, 8 또는 16 비트의 색을 저장할 수 있습니다. 이와 대조적으로, GIF 파일은 픽셀당 1, 2, 4 또는 8 비트만 사용할 수 있습니다. PNG 파일에는 픽셀의 색이 배경색과 혼합 되는 정도를 지정 하는 알파 값을 각 픽셀에 저장할 수도 있습니다.  
  
 PNG는 이미지를 점진적으로 표시 하는 기능 (즉, 이미지를 네트워크 연결을 통해 도착할 때 더 잘 근사치 더 나은 이미지를 표시 하는 기능)에서 GIF를 개선 합니다. PNG 파일은 다양 한 디스플레이 장치에서 이미지를 정확 하 게 렌더링할 수 있도록 감마 수정 및 색 수정 정보를 포함할 수 있습니다.  
  
### <a name="tag-image-file-format-tiff"></a>TIFF (태그 이미지 파일 형식)  
 TIFF는 다양 한 플랫폼 및 이미지 처리 응용 프로그램에서 지원 되는 유연 하 고 확장 가능한 형식입니다. TIFF 파일은 픽셀당 임의 수의 비트를 포함 하는 이미지를 저장할 수 있으며 다양 한 압축 알고리즘을 사용할 수 있습니다. 여러 이미지를 다중 페이지의 단일 TIFF 파일에 저장할 수 있습니다. 이미지와 관련 된 정보 (스캐너 제조업체, 호스트 컴퓨터, 압축 유형, 방향, 픽셀당 샘플 등)를 파일에 저장 하 고 태그를 사용 하 여 정렬할 수 있습니다. TIFF 형식은 승인 및 새 태그 추가에 필요에 따라 확장할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Image?displayProperty=nameWithType>
- <xref:System.Drawing.Bitmap?displayProperty=nameWithType>
- <xref:System.Drawing.Imaging.PixelFormat?displayProperty=nameWithType>
- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
