---
title: '방법: PropertyNameChanged 패턴 적용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], property changes (using code)
- data binding [Windows Forms], custom controls
- PropertyNameChanged pattern [Windows Forms], applying
ms.assetid: aa47ddf6-5223-40c4-833f-a78992194836
ms.openlocfilehash: 01afa713e97206ea192ba55dc2affad20163f872
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665257"
---
# <a name="how-to-apply-the-propertynamechanged-pattern"></a>방법: PropertyNameChanged 패턴 적용
다음 코드 예제를 적용 하는 방법에 설명 합니다 *PropertyName*패턴을 사용자 지정 컨트롤을 합니다. Windows Forms 데이터 바인딩 엔진에서 사용 되는 사용자 지정 컨트롤을 구현 하는 경우이 패턴을 적용 합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.ChangeNotification#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ChangeNotification/CS/Form1.cs#3)]
 [!code-vb[System.Windows.Forms.ChangeNotification#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ChangeNotification/VB/Form1.vb#3)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이전 코드 예제를 컴파일하려면:  
  
- 빈 코드 파일에 코드를 붙여 넣습니다. 포함 된 Windows Form에 사용자 지정 컨트롤을 사용 해야는 `Main` 메서드.  
  
## <a name="see-also"></a>참고자료

- [방법: INotifyPropertyChanged 인터페이스 구현](how-to-implement-the-inotifypropertychanged-interface.md)
- [Windows Forms 데이터 바인딩의 변경 알림](change-notification-in-windows-forms-data-binding.md)
- [Windows Forms 데이터 바인딩](windows-forms-data-binding.md)
