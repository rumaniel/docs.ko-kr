---
title: 리플렉션 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: d991bc0f-d16a-4ac5-9351-70e5c5b9891b
ms.openlocfilehash: 6d1206d84dec4202a7dad8f03c3d88c8a97ff5ba
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972115"
---
# <a name="reflection-visual-basic"></a>리플렉션 (Visual Basic)
리플렉션은 어셈블리, 모듈 및 형식을 설명하는 개체(<xref:System.Type> 형식)를 제공합니다. 리플렉션을 사용하면 동적으로 형식 인스턴스를 만들거나, 형식을 기존 개체에 바인딩하거나, 기존 개체에서 형식을 가져와 해당 메서드를 호출하거나, 필드 및 속성에 액세스할 수 있습니다. 코드에서 특성을 사용하는 경우 리플렉션은 특성에 대한 액세스를 제공합니다. 자세한 내용은 [특성](../../../standard/attributes/index.md)을 참조하세요.  
  
 다음은 정적 메서드 `GetType`(`Object` 기본 클래스의 모든 형식에 상속됨)을 사용하여 변수 형식을 가져오는 간단한 리플렉션 예제입니다.  
  
```vb  
' Using GetType to obtain type information:  
Dim i As Integer = 42  
Dim type As System.Type = i.GetType()  
System.Console.WriteLine(type)  
```  
  
 출력은 다음과 같습니다.  
  
 `System.Int32`  
  
 다음 예제에서는 리플렉션을 사용하여 로드된 어셈블리의 전체 이름을 가져옵니다.  
  
```vb  
' Using Reflection to get information from an Assembly:  
Dim info As System.Reflection.Assembly = GetType(System.Int32).Assembly  
System.Console.WriteLine(info)  
```  
  
 출력은 다음과 같습니다.  
  
 `mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
## <a name="reflection-overview"></a>리플렉션 개요  
 리플렉션은 다음과 같은 상황에서 유용합니다.  
  
- 프로그램 메타데이터의 특성에 액세스해야 하는 경우. 자세한 내용은 [특성에 저장된 정보 검색](../../../standard/attributes/retrieving-information-stored-in-attributes.md)을 참조하세요.  
  
- 어셈블리에서 형식을 검사하고 인스턴스화하려는 경우.  
  
- 런타임에 새 형식을 빌드하려는 경우. <xref:System.Reflection.Emit>의 클래스를 사용합니다.  
  
- 런타임에 바인딩을 수행하고 런타임에 생성된 형식의 메서드에 액세스하려는 경우. [동적으로 형식 로드 및 사용](../../../framework/reflection-and-codedom/dynamically-loading-and-using-types.md) 항목을 참조하세요.  
  
## <a name="related-sections"></a>관련 단원  
 추가 정보  
  
- [리플렉션](../../../framework/reflection-and-codedom/reflection.md)  
  
- [형식 정보 보기](../../../framework/reflection-and-codedom/viewing-type-information.md)  
  
- [리플렉션 및 제네릭 형식](../../../framework/reflection-and-codedom/reflection-and-generic-types.md)  
  
- <xref:System.Reflection.Emit>  
  
- [특성에 저장된 정보 검색](../../../standard/attributes/retrieving-information-stored-in-attributes.md)  
  
## <a name="see-also"></a>참고자료

- [Visual Basic 프로그래밍 가이드](../../../visual-basic/programming-guide/index.md)
- [.NET 어셈블리](../../../standard/assembly/index.md)
