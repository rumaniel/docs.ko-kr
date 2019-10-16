---
title: 동적 개체 작업(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- dynamic objects [Visual Basic]
ms.assetid: bdee2a00-07ff-46f9-86dd-fdac9b99cc97
ms.openlocfilehash: ea7d7aae1cd79a0243a9c721b5e3958fba82f84f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61973188"
---
# <a name="working-with-dynamic-objects-visual-basic"></a>동적 개체 작업(Visual Basic)
동적 개체는 또 다른 방법은 이외의 `Object` 런타임에 개체에 런타임에 바인딩 형식입니다. 동적 개체에 정의 된 동적 인터페이스를 사용 하 여 런타임에 속성 및 메서드와 같은 멤버를 노출 합니다 <xref:System.Dynamic> 네임 스페이스입니다. 클래스를 사용할 수는 <xref:System.Dynamic> 형식 또는 정적 형식과 일치 하지 않는 데이터 구조를 사용 하는 개체를 만들 네임 스페이스입니다. IronPython 및 IronRuby와 같은 동적 언어에서 정의 되는 동적 개체를 사용할 수도 있습니다. 동적 개체를 만들거나 동적 언어로 정의 된 동적 개체를 사용 하는 방법을 보여주는 예제를 보려면 [연습: 동적 개체 만들기 및 사용](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)하십시오 <xref:System.Dynamic.DynamicObject>, 또는 <xref:System.Dynamic.ExpandoObject>합니다.  
  
 Visual Basic 개체를 동적 언어 런타임 및 IronPython 및 IronRuby와 같은 동적 언어에서 사용 하 여 바인딩합니다는 <xref:System.Dynamic.IDynamicMetaObjectProvider> 인터페이스입니다. 구현 하는 클래스의 예는 `IDynamicMetaObjectProvider` 인터페이스는 합니다 <xref:System.Dynamic.DynamicObject> 및 <xref:System.Dynamic.ExpandoObject> 클래스입니다.  
  
 런타임에 바인딩된 호출을 구현 하는 개체 하려고 하는 경우는 `IDynamicMetaObjectProvider` 인터페이스를 해당 인터페이스를 사용 하 여 동적 개체를 Visual Basic 바인딩합니다. 구현 하지 않는 개체에 런타임에 바인딩된 호출 하는 경우는 `IDynamicMetaObjectProvider` 인터페이스를 또는 경우에 대 한 호출을 `IDynamicMetaObjectProvider` 인터페이스가 실패 하면, Visual Basic의 Visual Basic 런타임은 런타임에 바인딩 기능을 사용 하 여 개체에 바인딩합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Dynamic.DynamicObject>
- <xref:System.Dynamic.ExpandoObject>
- [연습: 동적 개체 만들기 및 사용](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)
- [초기 바인딩 및 런타임에 바인딩](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
