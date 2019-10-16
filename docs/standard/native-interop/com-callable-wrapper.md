---
title: CCW
ms.date: 10/23/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CCW
- COM interop, COM wrappers
- COM wrappers
- callable wrappers
- interoperation with unmanaged code, COM wrappers
- COM callable wrappers
ms.assetid: d04be3b5-27b9-4f5b-8469-a44149fabf78
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ebfc8f79303f89b092dd0fb38237dffffe0a93ba
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353910"
---
# <a name="com-callable-wrapper"></a>CCW

COM 클라이언트가.NET 개체를 호출할 때 공용 언어 런타임에서는 관리되는 개체 및 개체에 대한 COM 호출 가능 래퍼(CCW)를 만듭니다. .NET 개체를 직접 참조할 수는 없으며, COM 클라이언트는 CCW를 관리되는 개체에 대한 프록시로 사용합니다.

런타임에서는 서비스를 요청하는 COM 클라이언트 수와 관계없이 관리되는 개체에 대한 CCW를 하나만 만듭니다. 다음 그림과 같이 INew 인터페이스를 노출하는 CCW에 대한 참조가 여러 COM 클라이언트에 포함될 수 있습니다. 반대로 CCW에는 인터페이스를 구현하고 수집된 가비지인 관리되는 개체에 대한 참조 하나가 포함됩니다. COM 및 .NET 클라이언트는 둘 다 동시에 같은 관리되는 개체에 대한 요청을 수행할 수 있습니다.

![INew를 공개하는 CCW에 대한 참조를 포함하는 여러 COM 클라이언트.](./media/com-callable-wrapper/com-callable-wrapper-clients.gif)

COM 호출 가능 래퍼는 .NET 런타임 내에서 실행되는 다른 클래스에 표시되지 않습니다. 주요 용도는 관리 및 비관리 코드 간의 호출을 마샬링하는 것이지만 CCW는 래핑하고 있는 관리되는 개체의 개체 ID 및 개체 수명도 관리합니다.

## <a name="object-identity"></a>개체 ID

런타임에서는 런타임에 필요에 따라 개체가 메모리 내에서 이동할 수 있도록 하는 가비지 수집된 힙에서 .NET 개체에 대한 메모리를 할당합니다. 반면 런타임에서는 수집되지 않은 힙에서 CCW에 대한 메모리를 할당하므로 COM 클라이언트가 래퍼를 직접 참조할 수 있습니다.

## <a name="object-lifetime"></a>개체 수명

CCW는 래핑하고 있는 .NET 클라이언트와 달리 기존 COM 방식으로 참조 횟수가 계산됩니다. CCW의 참조 횟수가 0에 도달하면 래퍼는 관리되는 개체에 대한 참조를 해제합니다. 남은 참조가 없는 관리되는 개체는 다음 가비지 수집 주기 동안 수집됩니다.

## <a name="simulating-com-interfaces"></a>COM 인터페이스 시뮬레이션

CCW는 COM에 표시되는 인터페이스 데이터 형식 및 반환 값을 모두 COM의 인터페이스 기반 조작 적용과 일치하는 방식으로 COM 클라이언트에 노출합니다. COM 클라이언트의 경우 .NET 개체에서 메서드를 호출하는 것은 COM 개체에서 메서드를 호출하는 것과 같습니다.

이 원활한 접근 방식을 만들기 위해 CCW는 **IUnknown** 및 **IDispatch**와 같은 기존 COM 인터페이스를 만듭니다. 다음 그림과 같이 CCW는 래핑하고 있는 .NET 개체에 대한 단일 참조를 유지 관리합니다. COM 클라이언트 및 .NET 개체 둘 다는 CCW의 프록시 및 스텁 생성을 통해 상호 작용합니다.

![CCW에서 COM 인터페이스를 제작하는 방법을 보여 주는 다이어그램입니다.](./media/com-callable-wrapper/com-callable-wrapper-interfaces.gif)

관리되는 환경에서 클래스에 의해 명시적으로 구현되는 인터페이스를 노출하는 것 외에도 .NET 런타임은 개체 대신에 다음 표에 나열된 COM 인터페이스의 구현을 제공합니다. .NET 클래스는 이러한 인터페이스의 자체 구현을 제공하여 기본 동작을 재정의할 수 있습니다. 그러나 런타임에서는 항상 **IUnknown** 및 **IDispatch** 인터페이스에 대한 구현을 제공합니다.

|인터페이스|설명|
|---------------|-----------------|
|**IDispatch**|입력할 런타임 바인딩을 위한 메커니즘을 제공합니다.|
|**IErrorInfo**|오류, 소스, 도움말 파일, 도움말 컨텍스트에 대한 설명과 오류를 정의한 인터페이스의 GUID를 제공합니다(.NET 클래스의 경우 항상 **GUID_NULL**).|
|**IProvideClassInfo**|COM 클라이언트가 관리되는 클래스에 의해 구현된 **ITypeInfo** 인터페이스에 액세스할 수 있도록 합니다. COM에서 가져오지 않은 유형의 경우 .NET Core에서 `COR_E_NOTSUPPORTED`를 반환합니다. |
|**ISupportErrorInfo**|관리 개체에서 **IErrorInfo** 인터페이스를 지원할지 여부를 COM 클라이언트가 결정하도록 합니다. 지원하도록 하면 클라이언트가 최신 예외 개체에 대한 포인터를 가져올 수 있습니다. 관리되는 모든 형식이 **IErrorInfo** 인터페이스를 지원합니다.|
|**ITypeInfo**(.NET Framework만 해당)|Tlbexp.exe에서 생성된 형식 정보와 똑같은 클래스에 대한 형식 정보를 제공합니다.|
|**IUnknown**|COM 클라이언트가 CCW 수명을 관리하고 형식 강제 변환을 제공하는 데 사용하는 **IUnknown** 인터페이스의 표준 구현을 제공합니다.|

 관리되는 클래스는 다음 표에 설명된 COM 인터페이스를 제공할 수도 있습니다.

|인터페이스|설명|
|---------------|-----------------|
|(\_*classname*) 클래스 인터페이스|관리되는 개체에서 명시적으로 노출되는 모든 공용 인터페이스, 메서드, 속성 및 필드를 노출하는, 런타임에서 노출되고 명시적으로 정의되지 않는 인터페이스입니다.|
|**IConnectionPoint** 및 **IConnectionPointContainer**|대리자 기반 이벤트(이벤트 구독자를 등록하기 위한 인터페이스)의 소스가 되는 개체에 대한 인터페이스입니다.|
|**IDispatchEx**(.NET Framework만 해당)|클래스가 **IExpando**를 구현하는 경우 런타임에서 제공되는 인터페이스입니다. **IDispatchEx** 인터페이스는 **IDispatch**와 달리 멤버의 대/소문자 구분 호출, 열거형, 추가, 삭제를 가능하게 하는 **IDispatch** 인터페이스의 확장입니다.|
|**IEnumVARIANT**|클래스가 **IEnumerable**을 구현하는 경우 컬렉션에서 개체를 열거하는 컬렉션 형식 클래스에 대한 인터페이스입니다.|

## <a name="introducing-the-class-interface"></a>클래스 인터페이스 소개

관리 코드에서 명시적으로 정의되지 않은 클래스 인터페이스는 .NET 개체에서 명시적으로 노출되는 모든 공용 메서드, 속성, 필드, 이벤트를 노출하는 인터페이스입니다. 이 인터페이스는 이중 인터페이스이거나 디스패치 전용 인터페이스입니다. 클래스 인터페이스는 앞에 밑줄이 추가된 .NET 클래스 자체의 이름을 수신합니다. 예를 들어 Mammal 클래스의 클래스 인터페이스는 \_Mammal입니다.

파생 클래스의 클래스 인터페이스는 기본 클래스의 모든 공용 메서드, 속성 및 필드도 노출합니다. 파생 클래스는 각 기본 클래스의 클래스 인터페이스도 노출합니다. 예를 들어 System.Object를 확장하는 MammalSuperclass 클래스를 Mammal 클래스가 확장하면 .NET 개체는 \_Mammal, \_MammalSuperclass 및 \_Object라는 세 개의 인터페이스를 COM 클라이언트에 노출합니다.

예를 들어 다음 .NET 클래스를 예로 들어 봅니다.

```vb
' Applies the ClassInterfaceAttribute to set the interface to dual.
<ClassInterface(ClassInterfaceType.AutoDual)> _
' Implicitly extends System.Object.
Public Class Mammal
    Sub Eat()
    Sub Breathe()
    Sub Sleep()
End Class
```

```csharp
// Applies the ClassInterfaceAttribute to set the interface to dual.
[ClassInterface(ClassInterfaceType.AutoDual)]
// Implicitly extends System.Object.
public class Mammal
{
    public void Eat() {}
    public void Breathe() {}
    public void Sleep() {}
}
```

COM 클라이언트는 `_Mammal`이라는 클래스 인터페이스의 포인터를 가져올 수 있습니다. .NET Framework에서 [형식 라이브러리 내보내기 프로그램(Tlbexp.exe)](../../framework/tools/tlbexp-exe-type-library-exporter.md) 도구를 사용하여 `_Mammal` 인터페이스 정의를 포함하는 유형 라이브러리를 생성합니다. 형식 라이브러리 내보내기 프로그램은 .NET Core에서는 지원되지 않습니다. `Mammal` 클래스가 인터페이스를 하나 이상 구현하면 인터페이스가 coclass 아래에 표시됩니다.

```console
[odl, uuid(…), hidden, dual, nonextensible, oleautomation]
interface _Mammal : IDispatch
{
    [id(0x00000000), propget] HRESULT ToString([out, retval] BSTR*
        pRetVal);
    [id(0x60020001)] HRESULT Equals([in] VARIANT obj, [out, retval]
        VARIANT_BOOL* pRetVal);
    [id(0x60020002)] HRESULT GetHashCode([out, retval] short* pRetVal);
    [id(0x60020003)] HRESULT GetType([out, retval] _Type** pRetVal);
    [id(0x6002000d)] HRESULT Eat();
    [id(0x6002000e)] HRESULT Breathe();
    [id(0x6002000f)] HRESULT Sleep();
}
[uuid(…)]
coclass Mammal
{
    [default] interface _Mammal;
}
```

클래스 인터페이스 생성은 선택 사항입니다. 기본적으로 COM interop는 형식 라이브러리로 내보내는 각 클래스에 대한 디스패치 전용 인터페이스를 생성합니다. <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>를 클래스에 적용하여 이 인터페이스의 자동 만들기를 방지하거나 수정할 수 있습니다. 클래스 인터페이스를 사용하면 관리되는 클래스를 COM에 간편하게 노출할 수 있지만 사용이 제한됩니다.

> [!CAUTION]
> 고유 인터페이스를 명시적으로 정의하지 않고 클래스 인터페이스를 사용하면 관리되는 클래스의 미래 버전 관리가 복잡해질 수 있습니다. 클래스 인터페이스를 사용하기 전에 다음 지침을 참조하세요.

### <a name="define-an-explicit-interface-for-com-clients-to-use-rather-than-generating-the-class-interface"></a>클래스 인터페이스를 사용하는 대신 COM 클라이언트가 사용할 명시적 인터페이스를 정의하세요.

COM interop는 클래스 인터페이스를 자동으로 생성하므로 클래스에 대한 사무 버전 변경으로 공용 언어 런타임에서 노출하는 클래스 인터페이스의 레이아웃이 변경될 수 있습니다. 일반적으로 COM 클라이언트는 인터페이스 레이아웃에서 변경 내용을 처리하도록 준비되지 않으므로 클래스의 멤버를 변경하면 COM 클라이언트가 중단됩니다.

이 지침은 COM 클라이언트에 노출되는 인터페이스를 변경할 수 없어야 한다는 개념을 적용합니다. 실수로 인터페이스 레이아웃을 다시 정렬함으로써 COM 클라이언트가 중단되는 위험을 줄이려면 인터페이스를 명시적으로 정의하여 클래스에 대한 모든 변경 내용과 인터페이스 레이아웃을 분리합니다.

**ClassInterfaceAttribute**를 사용하여 클래스 인터페이스의 자동 생성을 해제하고 다음 코드 조각과 같이 클래스에 대한 명시적 인터페이스를 구현합니다.

```vb
<ClassInterface(ClassInterfaceType.None)>Public Class LoanApp
    Implements IExplicit
    Sub M() Implements IExplicit.M
…
End Class
```

```csharp
[ClassInterface(ClassInterfaceType.None)]
public class LoanApp : IExplicit
{
    int IExplicit.M() { return 0; }
}
```

**ClassInterfaceType.None** 값은 클래스 메타데이터가 형식 라이브러리에 노출될 때 클래스 인터페이스가 생성되지 않도록 방지합니다. 이전 예제에서 COM 클라이언트는 `IExplicit` 인터페이스를 통해서만 `LoanApp` 클래스에 액세스할 수 있습니다.

### <a name="avoid-caching-dispatch-identifiers-dispids"></a>디스패치 식별자(DispId)를 캐시하지 마세요.

클래스 인터페이스 사용은 스크립팅된 클라이언트, Microsoft Visual Basic 6.0 클라이언트 또는 인터페이스 멤버의 DispId를 캐시하지 않는 런타임에 바인딩된 클라이언트에 적용할 수 있는 옵션입니다. DispId로 런타임 바인딩을 가능하게 하는 인터페이스 멤버를 구별합니다.

클래스 인터페이스에 대한 DispId 생성은 인터페이스에서 멤버의 위치에 기반을 둡니다. 멤버 순서를 변경하고 클래스를 형식 라이브러리로 내보내면 클래스 인터페이스에서 생성된 DispId가 변경됩니다.

클래스 인터페이스를 사용할 때 런타임에 바인딩된 COM 클라이언트의 중단을 방지하려면 **ClassInterfaceAttribute** 및 **ClassInterfaceType.AutoDispatch** 값을 적용합니다. 이 값은 디스패치 전용 클래스 인터페이스를 구현하지만 형식 라이브러리에서 인터페이스 설명을 생략합니다. 인터페이스 설명이 없으면 클라이언트가 컴파일 타임에 DispId를 캐시할 수 없습니다. 이 형식이 클래스 인터페이스의 기본 인터페이스 형식이지만 특정 값을 명시적으로 적용할 수 있습니다.

```vb
<ClassInterface(ClassInterfaceType.AutoDispatch)> Public Class LoanApp
    Implements IAnother
    Sub M() Implements IAnother.M
…
End Class
```

```csharp
[ClassInterface(ClassInterfaceType.AutoDispatch)]
public class LoanApp
{
    public int M() { return 0; }
}
```

런타임에 인터페이스 멤버의 DispId를 가져오려고 COM 클라이언트는 **IDispatch.GetIdsOfNames**를 호출합니다. 인터페이스에서 메서드를 호출하려면 반환된 DispId를 인수로 **IDispatch.Invoke**에 전달합니다.

### <a name="restrict-using-the-dual-interface-option-for-the-class-interface"></a>클래스 인터페이스의 이중 인터페이스 옵션 사용을 제한하세요.

이중 인터페이스를 사용하면 COM 클라이언트에서 인터페이스 멤버를 초기에 바인딩하고 런타임에 바인딩할 수 있습니다. 디자인 타임이나 테스트 중에는 클래스 인터페이스를 이중으로 설정하는 것이 유용할 수 있습니다. 수정되지 않는 관리되는 클래스(및 해당 기본 클래스)에도 이 옵션을 적용할 수 있습니다. 이외의 경우에는 클래스 인터페이스를 이중으로 설정하지 마세요.

드물지만 자동으로 생성된 이중 인터페이스가 적절할 수 있지만 버전과 관련해서 복잡해지는 경우가 더 많습니다. 예를 들어 파생 클래스의 클래스 인터페이스를 사용하는 COM 클라이언트는 기본 클래스가 변경될 때 쉽게 중단될 수 있습니다. 타사에서 기본 클래스를 제공할 경우 클래스 인터페이스의 레이아웃을 제어할 수 없습니다. 또한 디스패치 전용 인터페이스와 달리 이중 인터페이스(**ClassInterfaceType.AutoDual**)는 내보낸 형식 라이브러리에서 클래스 인터페이스의 설명을 제공합니다. 이 설명은 런타임에 바인딩된 클라이언트가 컴파일 시간에 DispId를 캐시하도록 권장합니다.

### <a name="ensure-that-all-com-event-notifications-are-late-bound"></a>모든 COM 이벤트 알림이 런타임에 바인딩되는지 확인합니다.

기본적으로 COM 형식 정보는 관리되는 어셈블리에 직접 포함되므로 PIA(주 interop 어셈블리)가 필요하지 않습니다. 그러나 포함 형식 정보의 제한 사항 중 하나는 초기 바인딩된 vtable 호출에 의한 COM 이벤트 알림 전송을 지원하지 않고 런타임에 바인딩된 `IDispatch::Invoke` 호출만 지원합니다.

애플리케이션에 COM 이벤트 인터페이스 메서드에 대한 초기 바인딩된 호출이 필요한 경우 Visual Studio에서 **Interop 형식 포함** 속성을 `true`로 설정하거나 프로젝트 파일에 다음 요소를 포함할 수 있습니다.

```xml
<EmbedInteropTypes>True</EmbedInteropTypes>
```

## <a name="see-also"></a>참조

- <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>
- [COM 래퍼](com-wrappers.md)
- [.NET Framework 구성 요소를 COM에 노출](../../framework/interop/exposing-dotnet-components-to-com.md)
- [.NET Core 구성 요소를 COM에 노출](../../core/native-interop/expose-components-to-com.md)
- [상호 운용할 .NET 형식의 정규화](qualify-net-types-for-interoperation.md)
- [런타임 호출 가능 래퍼](runtime-callable-wrapper.md)
