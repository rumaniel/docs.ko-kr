---
title: '방법: 논리적 트리 재정의'
ms.date: 03/30/2017
helpviewer_keywords:
- overriding the logical tree [WPF]
- logical tree [WPF], overriding
ms.assetid: 0ae4d074-8113-4b06-b4fa-e0f39d4967a6
ms.openlocfilehash: bf3459fff1a90326794d6713dd39c73596b0e960
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768448"
---
# <a name="how-to-override-the-logical-tree"></a>방법: 논리적 트리 재정의
대부분의 경우에서 필요하지 않지만 고급 제어 작성자에는 논리적 트리 재정의 옵션이 있습니다.  
  
## <a name="example"></a>예제  
 이 예제는 설명 서브 클래스 하는 방법을 <xref:System.Windows.Controls.StackPanel> 패널 하나만 있을 수 있습니다 하는 단일 자식 요소를 렌더링만 하는 동작을 적용할이 경우에 논리적 트리를 재정의 하 합니다. 이는 실제적으로 원하는 동작이 아닐 수 있지만 요소의 정상적인 논리적 트리를 재정의하기 위한 시나리오를 보여 주는 수단으로 여기에 표시됩니다.  
  
 [!code-csharp[LogicalOverride#SingletonPanel](~/samples/snippets/csharp/VS_Snippets_Wpf/LogicalOverride/CSharp/SDKSampleLibrary/class1.cs#singletonpanel)]  
  
 논리적 트리에 대한 자세한 내용은 [WPF의 트리](trees-in-wpf.md)를 참조하세요.
