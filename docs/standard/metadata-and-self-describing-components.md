---
title: 메타데이터 및 자동 기술 구성 요소
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- runtime, metadata
- languages, interoperability
- portable executable files, metadata
- self-describing files
- metadata, about metadata
- common language runtime, metadata
- PE files, metadata
- components [.NET Framework], metadata
ms.assetid: 3dd13c5d-a508-455b-8dce-0a852882a5a7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1a35f4ffa88211d914dbf84c87da49fafa89a929
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353900"
---
# <a name="metadata-and-self-describing-components"></a>메타데이터 및 자동 기술 구성 요소

이전에 한 가지 언어로 작성된 소프트웨어 구성 요소(.exe 또는 .dll)는 다른 언어로 작성된 소프트웨어 구성 요소를 쉽게 사용할 수 없었습니다. COM은 이러한 문제를 해결하기 위한 단계를 제공했습니다. .NET Framework는 컴파일러가 모든 모듈과 어셈블리에 추가 선언 정보를 내보낼 수 있도록 하여 구성 요소 상호 운용성을 훨씬 더 쉽게 만듭니다. 메타데이터라고 하는 이 정보는 구성 요소가 아무런 문제 없이 원만하게 상호 작용할 수 있도록 하는 데 도움이 됩니다.

 메타데이터는 프로그램을 기술하는 이진 정보이며 공용 언어 런타임 PE 파일 또는 메모리에 저장됩니다. 코드를 PE 파일로 컴파일하면 메타데이터는 PE 파일의 한 부분에 삽입되고 해당 코드는 MSIL(Microsoft Intermediate Language)로 변환되어 파일의 다른 부분에 삽입됩니다. 모듈 또는 어셈블리에서 정의되고 참조된 모든 형식과 멤버는 메타데이터 내에 기술됩니다. 코드를 실행하면 런타임은 메타데이터를 메모리로 로드한 다음 참조하여 해당 코드의 클래스, 멤버, 상속 등에 대한 정보를 검색합니다.

 메타데이터는 언어와 무관하게 코드에 정의된 모든 형식과 멤버를 기술하며 다음과 같은 정보를 저장합니다.

- 어셈블리 기술 내용

  - ID(이름, 버전, 문화권, 공개 키)

  - 내보낸 형식

  - 이 어셈블리가 종속된 다른 어셈블리

  - 실행하는 데 필요한 보안 권한

- 형식 기술 내용

  - 이름, 표시 여부, 기본 클래스 및 구현된 인터페이스

  - 멤버(메서드, 필드, 속성, 이벤트, 중첩 형식)

- 특성.

  - 형식과 멤버를 수정하는 추가 설명적 요소

## <a name="benefits-of-metadata"></a>메타데이터의 이점

메타데이터는 더욱 간편한 프로그래밍 모델의 주요 요소이며 IDL(인터페이스 정의 언어) 파일, 헤더 파일 또는 구성 요소 참조의 외부 메서드를 사용하지 않아도 되게 합니다. 메타데이터를 사용하면 .NET Framework 언어는 개발자와 사용자 모두 알지 못한 채 언어와 무관하게 자동으로 자신을 기술할 수 있습니다. 또한 특성을 사용하여 메타데이터를 확장할 수 있습니다. 메타데이터는 다음과 같은 중요한 이점을 제공합니다.

- 자동 기술 파일

  공용 언어 런타임의 모듈과 어셈블리는 자동으로 기술됩니다. 모듈의 메타데이터에는 다른 모듈과 상호 작용하는 데 필요한 모든 요소가 있습니다. 메타데이터는 하나의 파일만 사용하여 정의와 구현을 모두 수행할 수 있도록 COM의 IDL 기능을 자동으로 제공합니다. 런타임 모듈과 어셈블리를 운영 체제에 등록할 필요도 없습니다. 결과적으로 런타임에 사용된 기술 내용은 항상 컴파일된 파일의 실제 코드를 반영하므로 애플리케이션의 안정성이 높아집니다.

- 언어 상호 운용성 및 간편해진 구성 요소 기반 디자인

  메타데이터는 다른 언어로 작성된 PE 파일에서 클래스를 상속하기 위해 컴파일된 코드에 대해 필요한 모든 정보를 제공하므로 명시적 마샬링을 고려하거나 사용자 지정 상호 운용성 코드를 사용할 필요 없이 관리되는 언어(공용 언어 런타임 기능이 있는 언어)로 작성된 클래스의 인스턴스를 만들 수 있습니다.

- 특성.

  .NET Framework에서는 특성이라고 하는 특정 종류의 메타데이터를 컴파일된 파일에 선언할 수 있습니다. 특성은 .NET Framework 전체에서 선언할 수 있으며 프로그램이 런타임에 동작하는 방식을 좀 더 자세하게 제어하기 위해 사용됩니다. 또한 사용자 지정 특성을 사용하여 사용자 지정 메타데이터를 .NET Framework 파일로 내보낼 수 있습니다. 자세한 내용은 [특성](../../docs/standard/attributes/index.md)을 참조하세요.

## <a name="metadata-and-the-pe-file-structure"></a>메타데이터 및 PE 파일 구조

메타데이터는 .NET Framework PE 파일의 한 섹션에 저장되고 MSIL은 PE 파일의 다른 섹션에 저장됩니다. PE 파일의 메타데이터 부분에는 테이블과 힙 데이터 구조가 있으며 MSIL 부분에는 MSIL 및 PE 파일의 메타데이터 부분을 참조하는 메타데이터 토큰이 있습니다. 예를 들어 [MSIL 디스어셈블러(Ildasm.exe)](../../docs/framework/tools/ildasm-exe-il-disassembler.md) 같은 도구를 사용하여 코드의 MSIL을 보는 경우 메타데이터 토큰을 발견할 수 있습니다.

### <a name="metadata-tables-and-heaps"></a>메타데이터 테이블 및 힙

각 메타데이터 테이블은 프로그램 요소에 대한 정보를 보유합니다. 예를 들어, 한 메타데이터 테이블은 코드의 클래스를 나타내고 다른 테이블은 필드를 나타내는 식입니다. 코드에 클래스가 10개 있는 경우 클래스 테이블은 각 클래스마다 행 하나씩, 모두 10개의 행을 가집니다. 메타데이터 테이블은 다른 테이블과 힙을 참조합니다. 예를 들어, 클래스의 메타데이터 테이블은 메서드의 테이블을 참조합니다.

또한 메타데이터는 문자열, blob, 사용자 문자열 및 GUID라고 하는 네 가지 힙 구조에 정보를 저장합니다. 형식과 멤버의 이름을 지정하는 데 사용되는 모든 문자열은 문자열 힙에 저장됩니다. 예를 들어, 메서드 테이블은 특정 메서드의 이름을 직접 저장하지 않지만 문자열 힙에 저장된 메서드의 이름을 가리킵니다.

### <a name="metadata-tokens"></a>메타데이터 토큰

메타데이터 테이블의 각 행은 메타데이터 토큰에 의해 PE 파일의 MSIL 부분에서 고유하게 식별됩니다. 메타데이터 토큰은 MSIL에 유지되고 특정 메타데이터 테이블을 참조하는 포인터와 개념적으로 비슷합니다.

메타데이터 토큰은 4바이트 숫자입니다. 최상위 바이트는 특정 토큰이 참조하는 메타데이터 테이블(메서드, 형식 등)을 나타내고 나머지 3바이트는 메타데이터 테이블의 행 중에서 현재 나타내고 있는 프로그래밍 요소에 해당하는 행을 지정합니다. C#에서 메서드를 정의하여 PE 파일로 컴파일하면 PE 파일의 MSIL 부분에 다음과 같은 메타데이터 토큰이 존재합니다.

`0x06000004`

최상위 바이트(`0x06`)는 이 토큰이 **MethodDef** 토큰임을 나타내고, 하위 3바이트(`000004`)는 공용 언어 런타임이 **MethodDef** 테이블의 넷째 행에서 이 메서드 정의를 기술하는 정보를 찾도록 지시합니다.

### <a name="metadata-within-a-pe-file"></a>PE 파일 내의 메타데이터

프로그램이 공용 언어 런타임으로 컴파일되면 해당 프로그램은 세 부분으로 구성되는 PE 파일로 변환됩니다. 다음 표에서는 각 부분의 내용을 설명합니다.

|PE 섹션|PE 섹션의 내용|
|----------------|----------------------------|
|PE 헤더|PE 파일의 주 섹션 인덱스 및 진입점 주소를 저장합니다.<br /><br /> 런타임은 이 정보를 사용하여 파일을 PE 파일로 식별하고 프로그램을 메모리로 로드하는 경우 실행 시작 위치를 결정합니다.|
|MSIL 명령|코드를 구성하는 MSIL 명령. 대부분의 MSIL 명령은 메타데이터 토큰을 동반합니다.|
|메타데이터|메타데이터 테이블과 힙. 런타임은 이 섹션을 사용하여 코드의 모든 형식과 멤버에 대한 정보를 기록합니다. 또한 사용자 지정 특성과 보안 정보도 포함되어 있습니다.|

## <a name="run-time-use-of-metadata"></a>메타데이터 런타임 사용

공용 언어 런타임에서 메타데이터 및 메타데이터의 역할을 더 잘 이해하려면 간단한 프로그램을 만들어 메타데이터가 런타임 주기에 어떤 영향을 주는지 실제로 나타내 보면 도움이 됩니다. 다음 코드 예제에서는 `MyApp`라는 클래스 내에서 두 가지 메서드를 보여 줍니다. `Main` 메서드는 프로그램 진입점이고 `Add` 메서드는 두 정수 인수의 합계를 반환합니다.

```vb
Public Class MyApp
   Public Shared Sub Main()
      Dim ValueOne As Integer = 10
      Dim ValueTwo As Integer = 20
      Console.WriteLine("The Value is: {0}", Add(ValueOne, ValueTwo))
   End Sub

   Public Shared Function Add(One As Integer, Two As Integer) As Integer
      Return (One + Two)
   End Function
End Class
```

```csharp
using System;
public class MyApp
{
   public static int Main()
   {
      int ValueOne = 10;
      int ValueTwo = 20;
      Console.WriteLine("The Value is: {0}", Add(ValueOne, ValueTwo));
      return 0;
   }
   public static int Add(int One, int Two)
   {
      return (One + Two);
   }
}
```

코드를 실행하면 런타임은 모듈을 메모리로 로드하고 이 클래스의 메타데이터를 참조합니다. 로드하고 나면 런타임은 메서드의 MSIL 스트림에 대해 광범위한 분석을 수행하여 이를 빠른 네이티브 기계어 명령으로 변환합니다. 런타임은 JIT(Just-In-Time) 컴파일러를 사용하여 MSIL 명령을 네이티브 기계어 코드 명령 메서드로 필요에 따라 한 번에 변환합니다.

다음 예제에서는 이전 코드의 `Main` 함수에서 생성된 MSIL 부분을 보여 줍니다. [MSIL 디스어셈블러(Ildasm.exe)](../../docs/framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 .NET Framework 애플리케이션에서 MSIL 및 메타데이터를 볼 수 있습니다.

```console
.entrypoint
.maxstack  3
.locals ([0] int32 ValueOne,
         [1] int32 ValueTwo,
         [2] int32 V_2,
         [3] int32 V_3)
IL_0000:  ldc.i4.s   10
IL_0002:  stloc.0
IL_0003:  ldc.i4.s   20
IL_0005:  stloc.1
IL_0006:  ldstr      "The Value is: {0}"
IL_000b:  ldloc.0
IL_000c:  ldloc.1
IL_000d:  call int32 ConsoleApplication.MyApp::Add(int32,int32) /* 06000003 */
```

JIT 컴파일러는 전체 메서드에 대한 MSIL을 읽고 이를 자세히 분석하여 해당 메서드에 대해 효과적인 네이티브 명령을 생성합니다. `IL_000d`에 `Add` 메서드에 대한 메타데이터 토큰(`/*` `06000003 */`)이 있고 런타임은 이 토큰을 사용하여 **MethodDef** 테이블의 셋째 행을 참조합니다.

다음 표에서는 `Add` 메서드를 나타내는 메타데이터 토큰에서 참조하는 **MethodDef** 테이블의 부분을 보여 줍니다. 이 어셈블리에는 고유한 값을 가지는 다른 메타데이터 테이블도 있지만 여기서는 이 테이블에 대해서만 설명합니다.

|행|RVA(Relevant Virtual Address)|ImplFlags|플래그|name<br /><br /> (문자열 힙을 가리킴)|Signature(blob 힙을 가리킴)|
|---------|--------------------------------------|---------------|-----------|-----------------------------------------|----------------------------------------|
|1|0x00002050|IL<br /><br /> 관리|Public<br /><br /> ReuseSlot<br /><br /> SpecialName<br /><br /> RTSpecialName<br /><br /> .ctor|.ctor (생성자)||
|2|0x00002058|IL<br /><br /> 관리|Public<br /><br /> 정적<br /><br /> ReuseSlot|주|문자열|
|3|0x0000208c|IL<br /><br /> 관리|Public<br /><br /> 정적<br /><br /> ReuseSlot|추가|int, int, int|

테이블의 각 열에는 코드에 대한 중요한 정보가 있습니다. **RVA**열을 사용하여 런타임은 이 메서드를 정의하는 MSIL의 시작 메모리 주소를 계산할 수 있습니다. **ImplFlags** 및 **Flags** 열은 메서드를 나타내는 비트마스크(예: 해당 메서드가 공용인지 아니면 전용인지를 나타냄)를 포함합니다. **Name** 열은 문자열 힙에서 메서드의 이름을 인덱싱하고 **Signature** 열은 blob 힙에서 메서드의 시그니처 정의를 인덱싱합니다.

런타임은 셋째 행의 **RVA** 열을 사용하여 원하는 오프셋 주소를 계산하고 이 주소를 JIT 컴파일러에 반환한 다음 새 주소로 계속합니다. JIT 컴파일러는 다른 메타데이터 토큰을 발견할 때까지 새 주소에서 MSIL을 계속 처리하며 프로세스를 반복합니다.

메타데이터를 사용하면 런타임은 코드를 로드하여 네이티브 기계어 명령으로 처리하는 데 필요한 모든 정보에 액세스할 수 있습니다. 이런 방식으로 메타데이터는 공용 형식 시스템과 함께 자동 기술 파일 및 언어 간 상속을 가능하게 합니다.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[특성](../../docs/standard/attributes/index.md)|특성을 적용하고, 사용자 지정 특성을 작성하고, 특성에 저장된 정보를 검색하는 방법에 대해 설명합니다.|
