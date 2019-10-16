---
title: '완화: 새로운 64비트 JIT 컴파일러'
ms.date: 03/30/2017
helpviewer_keywords:
- JIT compiler, 64-bit
- JIT compilation, 64-bit
- RyuJIT compiler
ms.assetid: 0332dabc-72c5-4bdc-8975-20d717802b17
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 07f9ae01fae5e4badbc13670ee56a2f05e303c0c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779357"
---
# <a name="mitigation-new-64-bit-jit-compiler"></a>완화: 새로운 64비트 JIT 컴파일러
.NET Framework 4.6부터는 런타임에 Just-In-Time 컴파일을 위한 새로운 64비트 JIT 컴파일러가 포함됩니다. 이 변경 내용은 32비트 JIT 컴파일러를 사용하는 컴파일에는 영향을 주지 않습니다.  
  
## <a name="unexpected-behavior-or-exceptions"></a>예기치 않은 동작이나 예외  
 경우에 따라 새로운 64비트 JIT 컴파일러를 사용하여 컴파일을 수행하면 이전 64비트 JIT 컴파일러로 컴파일한 코드를 실행할 때 확인되지 않던 런타임 예외 또는 동작이 발생합니다. 알려진 차이점은 다음과 같습니다.  
  
> [!IMPORTANT]
> .NET Framework 4.6.2와 함께 릴리스된 새로운 64비트 컴파일러에서 이러한 모든 알려진 문제가 해결되었습니다. Windows 업데이트에 포함된 .NET Framework 4.6 및 4.6.1의 서비스 릴리스에서도 대부분의 문제가 해결되었습니다. 사용 중인 Windows 버전이 최신 버전인지 확인하거나 .NET Framework 4.6.2로 업그레이드하여 이러한 문제를 제거할 수 있습니다.  
  
- 특정 상황에서 최적화가 설정된 릴리스 빌드에서 Unboxing 작업으로 인해 <xref:System.NullReferenceException>이 throw될 수 있습니다.  
  
- 일부 경우에는 큰 메서드 본문의 프로덕션 코드가 실행될 때 <xref:System.StackOverflowException>이 throw될 수 있습니다.  
  
- 특정 상황에서 메서드에 전달된 구조체가 릴리스 빌드에서 값 형식이 아닌 참조 형식으로 처리됩니다. 이 문제의 징후 중 하나는 컬렉션의 개별 항목이 예기치 않은 순서로 표시되는 것입니다.  
  
- 특정 상황에서 최적화가 사용되도록 설정되어 있을 경우 <xref:System.UInt16> 값을 높은 비트의 집합과 비교하면 결과가 잘못됩니다.  
  
- 배열 값을 초기화할 때와 같은 특정 상황에서 <xref:System.Reflection.Emit.OpCodes.Initblk?displayProperty=nameWithType> IL 명령에 따라 메모리가 초기화되면 잘못된 값이 사용될 수 있습니다. 이로 인해 처리되지 않은 예외 또는 잘못된 출력이 발생할 수 있습니다.  
  
- 드물게 특정한 상황에서 컴파일러 최적화가 사용되도록 설정되면 조건부 비트 테스트가 잘못된 <xref:System.Boolean> 값을 반환하거나 예외를 throw할 수 있습니다.  
  
- 특정 상황에서 `try` 블록을 시작하기 전에 `if` 문을 사용해서 조건을 테스트한 후에 `try` 블록을 종료하고 `catch` 또는 `finally` 블록에서 동일한 조건을 평가하면 새로운 64비트 JIT 컴파일러는 코드를 최적화할 때 `catch` 또는 `finally` 블록에서 `if` 조건을 제거합니다. 결과적으로 `catch` 또는 `finally` 블록에서 `if` 문 내의 코드가 무조건적으로 실행됩니다.  
  
<a name="General"></a>   
## <a name="mitigation-of-known-issues"></a>알려진 문제 완화  
 위에 나열된 문제가 발생하는 경우 다음 중 하나를 수행하여 해결할 수 있습니다.  
  
- .NET Framework 4.6.2로 업그레이드합니다. .NET Framework 4.6.2에 포함된 새로운 64비트 컴파일러는 이러한 각각의 알려진 문제를 해결합니다.  
  
- Windows 업데이트를 실행하여 사용 중인 Windows 버전을 최신 상태로 유지합니다. .NET Framework 4.6 및 4.6.1에 대한 서비스 업데이트는 unboxing 작업의 <xref:System.NullReferenceException>을 제외하고 이러한 각 문제를 해결합니다.  
  
- 이전 64비트 JIT 컴파일러를 사용하여 컴파일합니다. 방법에 대한 자세한 내용은 [기타 문제 완화](#Other) 섹션을 참조하세요.  
  
<a name="Other"></a>   
## <a name="mitigation-of-other-issues"></a>기타 문제 완화  
 이전 64비트 JIT 컴파일러 및 새로운 64비트 JIT 컴파일러를 사용하여 컴파일한 코드 또는 둘 다 새로운 64비트 JIT 컴파일러를 사용하여 컴파일한 앱의 디버그 버전 및 릴리스 버전 간 동작에서 다른 차이가 발생하는 경우 다음을 수행하여 이전 64비트 JIT 컴파일러로 앱을 컴파일할 수 있습니다.  
  
- 애플리케이션별로 [\<useLegacyJit&gt;](../configure-apps/file-schema/runtime/uselegacyjit-element.md) 요소를 애플리케이션의 구성 파일에 추가할 수 있습니다. 다음은 새로운 64비트 JIT 컴파일러를 사용하는 컴파일을 사용하지 않도록 설정하고, 대신 레거시 64비트 JIT 컴파일러를 사용합니다.  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>  
        <runtime>  
           <useLegacyJit enabled="1" />  
        </runtime>  
    </configuration>  
    ```  
  
- 사용자별로 레지스트리의 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework` 키에 `useLegacyJit`라는 `REG_DWORD` 값을 추가할 수 있습니다. 값이 1이면 레거시 64비트 JIT 컴파일러가 사용되도록 설정되고 값이 0이면 새로운 64비트 JIT 컴파일러가 사용되도록 설정됩니다.  
  
- 컴퓨터별로 레지스트리의 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework` 키에 `useLegacyJit`라는 `REG_DWORD` 값을 추가할 수 있습니다. 값이 1이면 레거시 64비트 JIT 컴파일러가 사용되도록 설정되고 값이 0이면 새로운 64비트 JIT 컴파일러가 사용되도록 설정됩니다.  
  
 [Microsoft Connect](https://connect.microsoft.com/VisualStudio)에 버그를 보고하여 문제를 알릴 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [런타임 변경 내용](runtime-changes-in-the-net-framework-4-6.md)
- [\<useLegacyJit> 요소](../configure-apps/file-schema/runtime/uselegacyjit-element.md)
