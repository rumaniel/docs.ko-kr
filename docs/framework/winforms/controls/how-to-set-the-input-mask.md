---
title: '방법: 입력 마스크 설정'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.MaskPropertyEditor
helpviewer_keywords:
- MaskedTextBox control [Windows Forms]
ms.assetid: 779b3a12-cd74-4e58-b46e-04983bda5b2c
ms.openlocfilehash: 06dee48765653ac7a659246cc3dfe865c795ca21
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949144"
---
# <a name="how-to-set-the-input-mask"></a>방법: 입력 마스크 설정
마스킹된 텍스트 상자 컨트롤은 사용자 입력을 허용 하거나 거부 하는 선언적 구문을 지 원하는 향상 된 텍스트 상자 컨트롤입니다. Mask 속성을 설정 하 여 응용 프로그램에 사용자 지정 유효성 검사 논리를 작성 하지 않고 허용 가능한 사용자 입력을 지정할 수 있습니다. 자세한 내용은 <xref:System.Windows.Forms.MaskedTextBox> 클래스의 설명 섹션을 참조 하세요.  
  
## <a name="setting-the-mask-property-manually"></a>수동으로 Mask 속성 설정  
 Mask 속성이 지 원하는 문자에 대해 잘 알고 있는 경우 해당 문자를 수동으로 입력할 수 있습니다. Mask 속성이 지 원하는 문자에 대 한 요약은 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 속성의 설명 섹션을 참조 하세요.  
  
### <a name="to-set-the-mask-property-manually"></a>Mask 속성을 수동으로 설정 하려면  
  
1. **디자인** 뷰에서 a <xref:System.Windows.Forms.MaskedTextBox>를 선택 합니다.  
  
2. **속성** 창에서 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 속성을 찾습니다.  
  
3. 원하는 마스크를 입력 합니다. 예를 들어 `###`과 같이 입력합니다.  
  
## <a name="using-the-input-mask-dialog-box"></a>입력 마스크 대화 상자 사용  
 입력 마스크 대화 상자는 미리 정의 된 입력 마스크를 제공 합니다. 미리 정의 된 마스크를 변경 하거나 사용자 고유의 마스크를 수동으로 입력할 수도 있습니다.  
  
### <a name="to-open-the-input-mask-dialog-box"></a>입력 마스크 대화 상자를 열려면  
  
1. **디자인** 뷰에서 a <xref:System.Windows.Forms.MaskedTextBox>를 선택 합니다.  
  
    1. 스마트 태그를 클릭 하 여 **MaskedTextBox 작업** 패널을 엽니다.  
  
    2. **마스크 설정**을 클릭 합니다.  
  
     \- 또는 -  
  
    1. **속성** 창에서 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 속성을 선택 합니다.  
  
    2. 속성 값 열에서 줄임표 단추를 클릭 합니다.  
  
     **입력 마스크** 대화 상자가 나타납니다.  
  
### <a name="to-use-the-input-mask-dialog-box"></a>입력 마스크 대화 상자를 사용 하려면  
  
1. 필드 목록에서 미리 정의 된 마스크 중 하나를 클릭 합니다.  
  
2. 필드 **마스크** 상자에서 미리 정의 된 마스크를 편집 합니다.  
  
3. 필드 **마스크** 상자에 새 마스크를 입력 합니다. 즉, 미리 정의 된 마스크 중 하나를 사용할 필요가 없습니다.  
  
    > [!NOTE]
    > 미리 보기 상자에는 <xref:System.Windows.Forms.MaskedTextBox>사용자에 게 표시 되는 문자가 표시 됩니다. 이러한 문자는 사용자가 데이터를 올바르게 입력 하는 데 도움이 되는 지침입니다.  
  
4. **ValidatingType 사용** 확인란을 선택 하거나 선택 취소 합니다. **ValidatingType 사용** 확인란은 사용자가 데이터 입력을 확인 하는 데 데이터 형식을 사용할지 여부를 지정 합니다. 자세한 내용은 <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> 속성을 참조하세요.  
  
5. **확인**을 클릭합니다.  
  
     마스크는 **속성** 창의 **mask** 속성에 입력 됩니다.  
  
## <a name="see-also"></a>참고자료

- [연습: MaskedTextBox 컨트롤 사용](walkthrough-working-with-the-maskedtextbox-control.md)
