---
title: FontDialog 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- FontDialog
helpviewer_keywords:
- Font dialog box [Windows Forms], Windows Forms
- Font dialog box
- FontDialog component [Windows Forms], about FontDialog component
ms.assetid: daf46e57-1b4b-4b7a-bad0-b50ca7ba75dc
ms.openlocfilehash: 7f140807bf4b42e530302190042e729c59248e7f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61789313"
---
# <a name="fontdialog-component-overview-windows-forms"></a>FontDialog 구성 요소 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.FontDialog> 구성 요소는 표준 Windows 미리 구성 된 대화 상자 **글꼴** 시스템에 현재 설치 된 글꼴을 노출 하는 데 사용 되는 대화 상자. 글꼴 선택 대화 상자를 직접 구성 하는 대신에 대 한 간단한 솔루션으로 Windows 기반 응용 프로그램 내에서 사용 합니다.  
  
 기본적으로 대화 상자 글꼴에 대 한 목록 상자에 표시 글꼴 스타일 및 크기 취소선과 Underline;과 같은 효과 대 한 확인란 스크립트에 대 한 드롭다운 목록 및 샘플 글꼴 표시 되는 방식입니다. (스크립트 참조에 지정 된 글꼴을 사용할 수 있는 다양 한 문자 스크립트 예를 들어 일본어 또는 히브리어.) 글꼴 대화 상자를 표시 하려면 호출을 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드.  
  
## <a name="key-properties"></a>키 속성  
 구성 요소에 다양 한 모양을 구성 하는 속성입니다. 대화 상자 선택 항목을 설정 하는 속성은 <xref:System.Windows.Forms.FontDialog.Font%2A> 고 <xref:System.Windows.Forms.FontDialog.Color%2A>입니다. 합니다 <xref:System.Windows.Forms.FontDialog.Font%2A> 글꼴, 스타일, 크기, 스크립트 및 효과; 속성 설정 예를 들어 `Arial, 10pt, style=Italic, Strikeout`합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.FontDialog>
- [FontDialog 구성 요소](fontdialog-component-windows-forms.md)
