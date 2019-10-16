---
title: COM 클래스 예제 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- examples [C#], COM classes
- COM, exposing Visual C# objects to
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
ms.openlocfilehash: 461d5a2afb197596c1c52daeeca0583b7b5e9693
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589148"
---
# <a name="example-com-class-c-programming-guide"></a>COM 클래스 예제(C# 프로그래밍 가이드)
다음은 COM 개체로 노출되는 클래스의 예제입니다. 이 코드를 .cs 파일에 배치하고 프로젝트에 추가한 후 **COM Interop 등록** 속성을 **True**로 설정합니다. 자세한 내용은 [방법: COM Interop에 대한 구성 요소 등록](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w29wacsy(v=vs.100))을 참조하세요.
  
 Visual C# 개체를 COM에 노출하려면 클래스 인터페이스, 필요한 경우 이벤트 인터페이스 및 클래스 자체를 선언해야 합니다. 클래스 멤버가 COM에 표시되려면 다음 규칙을 따라야 합니다.  
  
- 클래스는 public이어야 합니다.  
  
- 속성, 메서드 및 이벤트는 public이어야 합니다.  
  
- 속성 및 메서드는 클래스 인터페이스에서 선언되어야 합니다.  
  
- 이벤트는 이벤트 인터페이스에서 선언되어야 합니다.  
  
 이러한 인터페이스에 선언되지 않은 다른 public 멤버는 COM에 표시되지 않지만 다른 .NET Framework 개체에 표시됩니다.  
  
 속성 및 메서드를 COM에 노출하려면 클래스 인터페이스에서 선언하고 `DispId` 특성을 사용하여 표시한 후 클래스에서 구현해야 합니다. 멤버가 인터페이스에서 선언되는 순서는 COM vtable에 사용되는 순서입니다.  
  
 클래스에서 이벤트를 노출하려면 이벤트 인터페이스에서 선언하고 `DispId` 특성을 사용하여 표시해야 합니다. 클래스는 이 인터페이스를 구현하지 않아야 합니다.  
  
 클래스는 클래스 인터페이스를 구현합니다. 둘 이상의 인터페이스를 구현할 수 있지만 첫 번째 구현이 기본 클래스 인터페이스가 됩니다. 여기에서 COM에 노출된 메서드 및 속성을 구현합니다. 이러한 메서드 및 속성은 public으로 표시되어야 하며 클래스 인터페이스의 선언과 일치해야 합니다. 또한 여기에서 클래스에 의해 발생된 이벤트를 선언합니다. 이러한 이벤트는 public으로 표시되어야 하며 이벤트 인터페이스의 선언과 일치해야 합니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csProgGuideInterop#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInterop/CS/ExampleCOM.cs#8)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [상호 운용성](./index.md)
- [프로젝트 디자이너, 빌드 페이지(C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)
