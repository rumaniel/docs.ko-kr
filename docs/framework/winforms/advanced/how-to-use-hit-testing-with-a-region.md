---
title: '방법: 영역에 적중 테스트 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit tests [Windows Forms], using regions
- regions [Windows Forms], hit testing
ms.assetid: 3a4c07cb-a40a-4d14-ad35-008f531910a8
ms.openlocfilehash: 136f15f1364fb2aed791b4a61d0f11411b055967
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778874"
---
# <a name="how-to-use-hit-testing-with-a-region"></a>방법: 영역에 적중 테스트 사용
적중 횟수 테스트의 목적은 커서 아이콘 단추 등의 지정 된 개체에 대해 인지 여부를 확인 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 사각형 영역을 결합 하 여 더하기 모양의 영역을 만듭니다. 가정 변수의 `point` 최신 클릭의 위치를 저장 합니다. 코드 확인 여부를 `point` 더하기 모양의 지역에 있습니다. 요점은 (적중) 지역의 경우 지역 불투명 빨강 브러시를 사용 하 여 채워집니다. 그렇지 않으면 지역 빨간색 반투명 브러시를 사용 하 여 채워집니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.MiscLegacyTopics#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Region>
- [GDI+의 영역](regions-in-gdi.md)
- [방법: 클리핑 영역 사용](how-to-use-clipping-with-a-region.md)
