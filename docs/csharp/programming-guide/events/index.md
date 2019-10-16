---
title: 이벤트 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- classes [C#], events
- C# language, events
- events [C#]
ms.assetid: a8e51b22-d294-44fb-9539-0072f06c4cb3
ms.openlocfilehash: 7a8a8e6b6a393f151d69d1879f475e04f44df5fa
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590375"
---
# <a name="events-c-programming-guide"></a>이벤트(C# 프로그래밍 가이드)
[클래스](../../language-reference/keywords/class.md) 나 개체에서는 특정 상황이 발생할 때 이벤트를 통해 다른 클래스나 개체에 이를 알려줄 수 있습니다. 이벤트를 보내거나 *발생시키는*클래스를 *게시자* 라고 하며 이벤트를 받거나 *처리하는*클래스를 *구독자*라고 합니다.  
  
 일반적인 C# Windows Forms 또는 웹 애플리케이션, 단추 및 목록 상자 같은 컨트롤에 의해 발생하는 이벤트를 구독합니다. 컨트롤이 게시하는 이벤트를 찾아보고 처리할 이벤트를 선택하려면 Visual C# IDE(통합 개발 환경)를 사용할 수 있습니다. IDE는 빈 이벤트 처리기 메서드 및 이벤트를 구독하기 위한 코드를 자동으로 추가하는 편리한 방법을 제공합니다. 자세한 내용은 [방법: 이벤트 구독 및 구독 취소](./how-to-subscribe-to-and-unsubscribe-from-events.md)를 참조하세요.  
  
## <a name="events-overview"></a>이벤트 개요  
 이벤트에는 다음과 같은 속성이 있습니다.  
  
- 게시자는 이벤트 발생 시기를 결정합니다. 구독자는 이벤트에 대한 응답으로 수행할 작업을 결정합니다.  
  
- 한 이벤트에는 여러 구독자가 있을 수 있습니다. 구독자는 여러 게시자의 여러 이벤트를 처리할 수 있습니다.  
  
- 구독자가 없는 이벤트는 발생하지 않습니다.  
  
- 이벤트는 일반적으로 그래픽 사용자 인터페이스에서 단추 클릭이나 메뉴 선택 같은 사용자 작업을 표시하는 데 사용됩니다.  
  
- 이벤트에 여러 구독자가 있는 경우 이벤트 처리기는 이벤트가 발생할 때 동기적으로 호출됩니다. 이벤트를 비동기적으로 호출하려면 [Calling Synchronous Methods Asynchronously](../../../standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)를 참조하세요.  
  
- .NET Framework 클래스 라이브러리에서 이벤트는 <xref:System.EventHandler> 대리자 및 <xref:System.EventArgs> 기본 클래스를 기반으로 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 자세한 내용은 다음을 참조하세요.  
  
- [방법: 이벤트 구독 및 구독 취소](./how-to-subscribe-to-and-unsubscribe-from-events.md)  
  
- [방법: .NET Framework 지침을 따르는 이벤트 게시](./how-to-publish-events-that-conform-to-net-framework-guidelines.md)  
  
- [방법: 파생 클래스에서 기본 클래스 이벤트 발생](./how-to-raise-base-class-events-in-derived-classes.md)  
  
- [방법:  인터페이스 이벤트 구현](./how-to-implement-interface-events.md)  
  
- [방법: 사용자 지정 이벤트 접근자 구현](./how-to-implement-custom-event-accessors.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [이벤트](~/_csharplang/spec/classes.md#events)를 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.
  
## <a name="featured-book-chapters"></a>중요 설명서 장  
 [대리자, Events, and Lambda Expressions](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518994%28v=orm.10%29) 에 [ C# 3.0 Cookbook, Third Edition: 250 개 이상의 솔루션에 대 한 C# 3.0 프로그래머](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518995%28v=orm.10%29)  
  
 [대리자 및 이벤트](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652490%28v=orm.10%29) 에 [학습 C# 3.0. 기본 사항 마스터 C# 3.0](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652493%28v=orm.10%29)  
  
## <a name="see-also"></a>참고 항목

- <xref:System.EventHandler>
- [C# 프로그래밍 가이드](../index.md)
- [대리자](../delegates/index.md)
- [Windows Forms에서 이벤트 처리기 만들기](../../../framework/winforms/creating-event-handlers-in-windows-forms.md)
