---
title: 사용자 지정 특성 액세스
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- custom attributes, accessibility
- attributes [.NET Framework], accessing
- reflection, custom attributes
ms.assetid: 1d8e3398-00d8-47d5-a084-214f9859d3d7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5b8eafa4f3f8a3fd81772c4521f26323019d012c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046148"
---
# <a name="accessing-custom-attributes"></a>사용자 지정 특성 액세스
특성이 프로그램 요소와 연결된 후 리플렉션을 사용하여 특성의 존재 및 값을 쿼리할 수 있습니다. .NET Framework 버전 1.0 및 1.1에서 사용자 지정 특성은 실행 컨텍스트에서 검사됩니다. .NET Framework 버전 2.0에서는 실행을 위해 로드할 수 없는 코드를 검사하는 데 사용할 수 있는 새로운 로드 컨텍스트인 리플렉션 전용 컨텍스트를 제공합니다.  
  
## <a name="the-reflection-only-context"></a>리플렉션 전용 컨텍스트  
 리플렉션 전용 컨텍스트로 로드된 코드는 실행할 수 없습니다. 즉, 생성자를 실행할 필요가 없으므로 사용자 지정 특성의 인스턴스를 만들 수 없습니다. 리플렉션 전용 컨텍스트에서 사용자 지정 특성을 로드하고 검사하려면 <xref:System.Reflection.CustomAttributeData> 클래스를 사용합니다. static <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=nameWithType> 메서드의 적절한 오버로드를 사용하여 이 클래스의 인스턴스를 가져올 수 있습니다. [방법: 리플렉션 전용 컨텍스트에 어셈블리 로드](how-to-load-assemblies-into-the-reflection-only-context.md)를 참조하세요.  
  
## <a name="the-execution-context"></a>실행 컨텍스트  
 실행 컨텍스트에서 특성을 쿼리하는 기본 리플렉션 메서드는 <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType> 및 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>입니다.  
  
 사용자 지정 특성의 접근성은 연결된 어셈블리를 기준으로 확인됩니다. 이 확인은 사용자 지정 특성이 연결된 어셈블리의 형식에 대한 메서드가 사용자 지정 특성의 생성자를 호출할 수 있는지 확인하는 것과 같습니다.  
  
 <xref:System.Reflection.Assembly.GetCustomAttributes%28System.Boolean%29?displayProperty=nameWithType> 같은 메서드는 형식 인수의 표시 유형 및 접근성을 확인합니다. 사용자 정의 형식이 포함된 어셈블리의 코드만 **GetCustomAttributes**를 사용하여 해당 형식의 사용자 지정 특성을 검색할 수 있습니다.  
  
 다음 C# 예제는 일반적인 사용자 지정 특성 디자인 패턴입니다. 이 예제는 런타임 사용자 지정 특성 리플렉션 모델을 보여 줍니다.  
  
```csharp
System.DLL  
public class DescriptionAttribute : Attribute  
{  
}  
  
System.Web.DLL  
internal class MyDescriptionAttribute : DescriptionAttribute  
{  
}  
  
public class LocalizationExtenderProvider  
{  
    [MyDescriptionAttribute(...)]  
    public CultureInfo GetLanguage(...)  
    {  
    }  
}  
```  
  
 런타임에서 **GetLanguage** 메서드에 연결된 public 사용자 지정 특성 유형 <xref:System.ComponentModel.DescriptionAttribute>에 대한 사용자 지정 특성을 검색하려고 시도하는 경우에는 다음 작업을 수행합니다.  
  
1. 런타임은 **Type.GetCustomAttributes**(*type* 형식)에 대한 형식 인수 **DescriptionAttribute**가 public이고 이에 따라 표시되고 액세스 가능한지 확인합니다.  
  
2. 런타임은 **DescriptionAttribute**에서 파생된 사용자 정의 형식 **MyDescriptionAttribute**가 **GetLanguage**() 메서드에 연결된 경우 **System.Web.DLL** 어셈블리 내에서 표시되고 액세스 가능한지 확인합니다.  
  
3. 런타임은 **MyDescriptionAttribute**의 생성자가 **System.Web.DLL** 어셈블리 내에서 표시되고 액세스 가능한지 확인합니다.  
  
4. 런타임은 사용자 지정 특성 매개 변수를 사용하여 **MyDescriptionAttribute**의 생성자를 호출하고 새 개체를 호출자로 반환합니다.  
  
 사용자 지정 특성 리플렉션 모델에서는 형식이 정의된 어셈블리 외부에서 사용자 정의 형식의 인스턴스가 누수될 수 있습니다. 이것은 **RuntimeMethodInfo** 개체의 배열을 반환하는 <xref:System.Type.GetMethods%2A?displayProperty=nameWithType>와 같이 사용자 정의 형식의 인스턴스를 반환하는 런타임 시스템 라이브러리의 멤버와 다르지 않습니다. 클라이언트가 사용자 정의 사용자 지정 특성 유형 관련 정보를 검색하지 않게 하려면 유형의 멤버를 public이 아닌 멤버로 정의합니다.  
  
 다음 예제에서는 리플렉션을 사용하여 사용자 지정 특성에 대한 액세스 권한을 얻는 기본적인 방법을 보여 줍니다.  
  
 [!code-cpp[CustomAttributeData#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source2.cpp#2)]
 [!code-csharp[CustomAttributeData#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source2.cs#2)]
 [!code-vb[CustomAttributeData#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source2.vb#2)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>
- [형식 정보 보기](viewing-type-information.md)
- [리플렉션의 보안 고려 사항](security-considerations-for-reflection.md)
