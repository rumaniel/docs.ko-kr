---
title: '연습: 부분 신뢰 시나리오에서 코드 내보내기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- reflection emit, anonymously hosted dynamic methods
- partial trust, reflection
- partial trust, emitting dynamic methods
- reflection emit, partial trust scenarios
- anonymously hosted dynamic methods [.NET Framework]
- emitting dynamic assemblies,partial trust scenarios
- reflection emit, dynamic methods
- dynamic methods
ms.assetid: c45be261-2a9d-4c4e-9bd6-27f0931b7d25
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 002434cf51b221a456c8752b5b1388912f875a28
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045748"
---
# <a name="walkthrough-emitting-code-in-partial-trust-scenarios"></a>연습: 부분 신뢰 시나리오에서 코드 내보내기

리플렉션 내보내기에는 완전 또는 부분 신뢰에서 동일한 API 집합이 사용되지만 일부 기능의 경우 부분적으로 신뢰할 수 있는 코드에 특수 권한이 필요합니다. 또한 리플렉션 내보내기에는 부분 신뢰와 함께 보안 투명 어셈블리에서 사용되도록 디자인된 익명으로 호스트되는 동적 메서드의 기능이 있습니다.

> [!NOTE]
> .NET Framework 3.5 이전에는 코드 내보내기에는 <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>이 필요했습니다. 이 권한은 기본적으로 `FullTrust` 및 `Intranet` 명명된 권한 집합에 포함되지만 `Internet` 권한 집합에는 포함되지 않습니다. 따라서 <xref:System.Security.SecurityCriticalAttribute> 특성이 있고 <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit>에 대해 <xref:System.Security.PermissionSet.Assert%2A> 메서드를 실행한 경우에만 부분 신뢰 영역에서 라이브러리를 사용할 수 있었습니다. 코딩 오류가 있을 경우 보안 허점이 발생할 수 있으므로 이러한 라이브러리는 신중한 보안 검토가 필요합니다. .NET Framework 3.5에서는 코드 생성이 기본적으로 권한 있는 작업이 아니기 때문에 보안 요구를 실행하지 않고 부분 신뢰 시나리오에서 코드를 내보낼 수 있습니다. 즉, 생성된 코드에 코드를 내보내는 어셈블리보다 많은 권한이 없습니다. 따라서 코드를 내보내는 라이브러리가 보안상 투명할 수 있으며 <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit>를 어설션할 필요가 없으므로 보안 라이브러리 작성 시 철저한 보안 검토가 필요하지 않습니다.

이 연습에서는 다음 작업을 수행합니다.

- [부분적으로 신뢰할 수 있는 코드를 테스트하기 위한 간단한 샌드박스 설정](#Setting_up).

  > [!IMPORTANT]
  > 부분 신뢰에서 코드를 간단하게 실험하는 방법입니다. 실제로 신뢰할 수 없는 위치에서 나오는 코드를 실행하려면 [방법: 샌드박스에서 부분적으로 신뢰할 수 있는 코드 실행](../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)을 참조하세요.

- [부분적으로 신뢰할 수 있는 애플리케이션 도메인에서 코드 실행](#Running_code).

- [익명으로 호스트된 동적 메서드를 사용하여 부분 신뢰에서 코드 내보내기 및 실행](#Using_methods).

부분 신뢰 시나리오의 코드 내보내기에 대한 자세한 내용은 [리플렉션 내보내기의 보안 문제점](security-issues-in-reflection-emit.md)을 참조하세요.

이러한 절차에 표시된 코드의 전체 목록을 보려면 이 연습의 끝부분에 있는 [예제 섹션](#Example)을 참조하세요.

<a name="Setting_up"></a>

## <a name="setting-up-partially-trusted-locations"></a>부분적으로 신뢰할 수 있는 위치 설정

다음 두 절차는 부분 신뢰를 사용하여 코드를 테스트할 수 있는 위치를 설정하는 방법을 보여 줍니다.

- 첫 번째 절차는 코드에 인터넷 권한이 부여되는 샌드박스가 적용된 애플리케이션 도메인을 만드는 방법을 보여 줍니다.

- 두 번째 절차는 동일하거나 낮은 신뢰 수준 어셈블리의 전용 데이터에 액세스할 수 있도록 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그와 함께 <xref:System.Security.Permissions.ReflectionPermission>을 부분적으로 신뢰할 수 있는 애플리케이션 도메인에 추가하는 방법을 보여 줍니다.

### <a name="creating-sandboxed-application-domains"></a>샌드박스가 적용된 애플리케이션 도메인 만들기

어셈블리가 부분 신뢰로 실행되는 애플리케이션 도메인을 만들려면 <xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=nameWithType> 메서드 오버로드를 사용하여 애플리케이션 도메인을 만드는 방식으로 어셈블리에 부여되는 권한 집합을 지정해야 합니다. 권한 집합을 지정하는 가장 쉬운 방법은 보안 정책에서 명명된 권한 집합을 검색하는 것입니다.

다음 절차에서는 코드를 부분 신뢰로 실행하는 샌드박스가 적용된 애플리케이션 도메인을 만들어 내보낸 코드가 public 형식의 public 멤버에만 액세스할 수 있는 시나리오를 테스트합니다. 이후 절차에서는 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess>를 추가하여 내보낸 코드가 동일하거나 낮은 수준의 권한이 부여된 어셈블리의 public이 아닌 형식 및 멤버에 액세스할 수 있는 시나리오를 테스트하는 방법을 보여 줍니다.

#### <a name="to-create-an-application-domain-with-partial-trust"></a>부분 신뢰를 사용하여 애플리케이션 도메인을 만들려면

1. 샌드박스가 적용된 애플리케이션 도메인에서 어셈블리에 부여할 권한 집합을 만듭니다. 이 경우 인터넷 영역의 권한 집합이 사용됩니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#2)]
    [!code-vb[HowToEmitCodeInPartialTrust#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#2)]

2. <xref:System.AppDomainSetup> 개체를 만들어 애플리케이션 경로를 통해 애플리케이션 도메인을 초기화합니다.

    > [!IMPORTANT]
    > 간단히 설명하기 위해 이 코드 예제에서는 현재 폴더를 사용합니다. 실제로 인터넷에서 나오는 코드를 실행하려면 [방법: 샌드박스에서 부분적으로 신뢰할 수 있는 코드 실행](../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)의 설명대로 신뢰할 수 없는 코드에 별도의 폴더를 사용합니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#3)]
    [!code-vb[HowToEmitCodeInPartialTrust#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#3)]

3. 애플리케이션 도메인을 만들어 애플리케이션 도메인 설정 정보 및 애플리케이션 도메인에서 실행되는 모든 어셈블리의 권한 집합을 지정합니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#5)]
    [!code-vb[HowToEmitCodeInPartialTrust#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#5)]

    <xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=nameWithType> 메서드 오버로드의 마지막 매개 변수를 사용하여 애플리케이션 도메인의 권한 집합이 아닌 완전 신뢰가 부여되는 어셈블리 집합을 지정할 수 있습니다. 애플리케이션에서 사용하는 .NET Framework 어셈블리는 글로벌 어셈블리 캐시에 있으므로 해당 어셈블리를 지정할 필요가 없습니다. 전역 어셈블리 캐시의 어셈블리는 항상 완전히 신뢰할 수 있습니다. 이 매개 변수를 사용하여 전역 어셈블리 캐시에 없는 강력한 이름의 어셈블리를 지정할 수 있습니다.

### <a name="adding-restrictedmemberaccess-to-sandboxed-domains"></a>샌드박스가 적용된 도메인에 RestrictedMemberAccess 추가

호스트 애플리케이션에서는 익명으로 호스트된 동적 메서드가 코드를 내보내는 어셈블리의 신뢰 수준과 같거나 낮은 신뢰 수준을 가진 어셈블리의 전용 데이터에 액세스할 수 있습니다. JIT(Just-In-Time) 표시 유형 확인을 건너뛰는 이 제한된 기능을 사용할 수 있도록 호스트 애플리케이션에서는 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>(RMA) 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission> 개체를 권한 집합에 추가합니다.

예를 들어 호스트에서는 인터넷 애플리케이션에 인터넷 권한과 RMA를 부여할 수 있으므로 인터넷 애플리케이션은 자체 어셈블리의 전용 데이터에 액세스하는 코드를 내보낼 수 있습니다. 액세스는 같거나 낮은 신뢰 수준의 어셈블리로 제한되므로 인터넷 애플리케이션은 .NET Framework 어셈블리와 같이 완전히 신뢰할 수 있는 어셈블리의 멤버에 액세스할 수 없습니다.

> [!NOTE]
> 권한 상승을 방지하기 위해 익명으로 호스트된 동적 메서드가 생성될 때 내보내는 어셈블리에 대한 스택 정보가 포함됩니다. 메서드가 호출되면 스택 정보가 확인됩니다. 따라서 완전히 신뢰할 수 있는 코드에서 호출되는 익명으로 호스트된 동적 메서드는 계속해서 내보내는 어셈블리의 신뢰 수준으로 제한됩니다.

#### <a name="to-create-an-application-domain-with-partial-trust-plus-rma"></a>부분 신뢰 및 RMA를 사용하여 애플리케이션 도메인을 만들려면

1. <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess>(RMA) 플래그가 있는 새 <xref:System.Security.Permissions.ReflectionPermission> 개체를 만들고 <xref:System.Security.PermissionSet.SetPermission%2A?displayProperty=nameWithType> 메서드를 사용하여 권한 집합에 권한을 추가합니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#7)]
    [!code-vb[HowToEmitCodeInPartialTrust#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#7)]

    <xref:System.Security.PermissionSet.AddPermission%2A> 메서드는 권한 집합에 권한을 추가합니다(권한이 포함되지 않은 경우). 권한이 이미 권한 집합에 포함된 경우 지정된 플래그가 기존 권한에 추가됩니다.

    > [!NOTE]
    > RMA는 익명으로 호스트된 동적 메서드의 기능입니다. 일반 동적 메서드가 JIT 표시 유형 확인을 건너뛰면 내보낸 코드에 완전 신뢰가 필요합니다.

2. 애플리케이션 도메인을 만들어 애플리케이션 도메인 설정 정보 및 권한 집합을 지정합니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#8)]
    [!code-vb[HowToEmitCodeInPartialTrust#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#8)]

<a name="Running_code"></a>

## <a name="running-code-in-sandboxed-application-domains"></a>샌드박스가 적용된 애플리케이션 도메인에서 코드 실행

다음 절차에서는 애플리케이션 도메인에서 실행할 수 있는 메서드를 사용하여 클래스를 정의하는 방법, 도메인에서 클래스 인스턴스를 만드는 방법 및 해당 메서드를 실행하는 방법을 설명합니다.

#### <a name="to-define-and-execute-a-method-in-an-application-domain"></a>애플리케이션 도메인에서 메서드를 정의 및 실행하려면

1. <xref:System.MarshalByRefObject>에서 파생된 클래스를 정의합니다. 이 작업을 통해 다른 애플리케이션 도메인에서 클래스 인스턴스를 만들고 애플리케이션 도메인 경계에 걸쳐 메서드 호출을 실행할 수 있습니다. 이 예제에서 클래스 이름은 `Worker`입니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#10)]
    [!code-vb[HowToEmitCodeInPartialTrust#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#10)]

2. 실행할 코드가 포함된 public 메서드를 정의합니다. 이 예제에서 코드는 간단한 동적 메서드를 내보내고, 대리자를 만들어 메서드를 실행하고, 대리자를 호출합니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#11)]
    [!code-vb[HowToEmitCodeInPartialTrust#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#11)]

3. 기본 프로그램에서 어셈블리의 표시 이름을 가져옵니다. 이 이름은 샌드박스가 적용된 애플리케이션 도메인에서 `Worker` 클래스의 인스턴스를 만들 때 사용됩니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#14)]
    [!code-vb[HowToEmitCodeInPartialTrust#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#14)]

4. 기본 프로그램에서 이 연습의 [첫 번째 절차](#Setting_up)에 설명된 대로 샌드박스가 적용된 애플리케이션 도메인을 만듭니다. `SimpleEmitDemo` 메서드는 public 메서드만 사용하므로 `Internet` 권한 집합에 권한을 추가할 필요가 없습니다.

5. 기본 프로그램에서 샌드박스가 적용된 애플리케이션 도메인에서 `Worker` 클래스의 인스턴스를 만듭니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#12)]
    [!code-vb[HowToEmitCodeInPartialTrust#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#12)]

    <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> 메서드는 대상 애플리케이션 도메인에서 개체를 만들고 개체의 속성과 메서드를 호출하는 데 사용될 수 있는 프록시를 반환합니다.

    > [!NOTE]
    > Visual Studio에서 이 코드를 사용하는 경우 네임스페이스를 포함하도록 클래스의 이름을 변경해야 합니다. 기본적으로 네임스페이스는 프로젝트의 이름입니다. 예를 들어 프로젝트가 "PartialTrust"이면 클래스 이름은 "PartialTrust.Worker"입니다.

6. `SimpleEmitDemo` 메서드를 호출하는 코드를 추가합니다. 호출은 애플리케이션 도메인 경계에서 마샬링되고 코드는 샌드박스가 적용된 애플리케이션 도메인에서 실행됩니다.

    [!code-csharp[HowToEmitCodeInPartialTrust#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#13)]
    [!code-vb[HowToEmitCodeInPartialTrust#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#13)]

<a name="Using_methods"></a>

## <a name="using-anonymously-hosted-dynamic-methods"></a>익명으로 호스트된 동적 메서드 사용

익명으로 호스트된 동적 메서드는 시스템에서 제공되는 투명 어셈블리와 연결됩니다. 따라서 메서드에 포함된 코드는 투명합니다. 반면, 일반 동적 메서드는 기존 모듈과 연결되고(직접 지정되거나 연결된 형식에서 유추됨) 해당 모듈의 보안 수준을 사용해야 합니다.

> [!NOTE]
> 익명 호스팅을 제공하는 어셈블리와 동적 메서드를 연결하는 유일한 방법은 다음 절차에 설명된 생성자를 사용하는 것입니다. 익명 호스팅 어셈블리에서는 모듈을 명시적으로 지정할 수 없습니다.

일반 동적 메서드는 연결된 모듈의 internal 멤버 또는 연결된 형식의 private 멤버에 액세스할 수 있습니다. 익명으로 호스트된 동적 메서드는 다른 코드에서 분리되므로 전용 데이터에 액세스할 수 없습니다. 하지만 JIT 표시 유형 확인을 건너뛰어 전용 데이터에 대한 액세스 권한을 얻는 제한된 기능이 있습니다. 이 기능은 코드를 내보내는 어셈블리의 신뢰 수준과 같거나 낮은 신뢰 수준을 가진 어셈블리로 제한됩니다.

권한 상승을 방지하기 위해 익명으로 호스트된 동적 메서드가 생성될 때 내보내는 어셈블리에 대한 스택 정보가 포함됩니다. 메서드가 호출되면 스택 정보가 확인됩니다. 완전히 신뢰할 수 있는 코드에서 호출되는 익명으로 호스트된 동적 메서드는 계속해서 메서드를 내보낸 어셈블리의 신뢰 수준으로 제한됩니다.

#### <a name="to-use-anonymously-hosted-dynamic-methods"></a>익명으로 호스트된 동적 메서드를 사용하려면

- 연결된 모듈 또는 형식을 지정하지 않는 생성자를 사용하여 익명으로 호스트된 동적 메서드를 만듭니다.

  [!code-csharp[HowToEmitCodeInPartialTrust#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#15)]
  [!code-vb[HowToEmitCodeInPartialTrust#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#15)]

  public 형식 및 메서드만 사용하는 익명으로 호스트된 동적 메서드의 경우 제한된 멤버 액세스가 필요하지 않고 JIT 표시 유형 확인을 건너뛸 필요가 없습니다.

  동적 메서드를 내보내기 위한 특수 권한이 필요하지 않지만, 내보낸 코드에는 코드에서 사용하는 형식 및 메서드에 필요한 권한이 있어야 합니다. 예를 들어 내보낸 코드가 파일에 액세스하는 메서드를 호출할 경우 <xref:System.Security.Permissions.FileIOPermission>이 필요합니다. 신뢰 수준에 권한이 포함되지 않은 경우 내보낸 코드가 실행될 때 보안 예외가 throw됩니다. 여기 표시된 코드는 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 메서드만 사용하는 동적 메서드를 내보냅니다. 따라서 코드는 부분적으로 신뢰할 수 있는 위치에서 실행할 수 있습니다.

- 또는 <xref:System.Reflection.Emit.DynamicMethod.%23ctor%28System.String%2CSystem.Type%2CSystem.Type%5B%5D%2CSystem.Boolean%29> 생성자를 사용하고 `restrictedSkipVisibility` 매개 변수를 `true`로 지정하여 JIT 표시 유형 확인을 건너뛰는 제한된 기능을 가진 익명으로 호스트된 동적 메서드를 만듭니다.

  [!code-csharp[HowToEmitCodeInPartialTrust#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#16)]
  [!code-vb[HowToEmitCodeInPartialTrust#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#16)]

  익명으로 호스트된 동적 메서드는 내보내는 어셈블리의 신뢰 수준과 같거나 낮은 신뢰 수준을 가진 어셈블리의 전용 데이터에만 액세스할 수 있도록 제한됩니다. 예를 들어 인터넷 신뢰로 실행되고 있는 동적 메서드는 인터넷 신뢰로 실행되고 있는 다른 어셈블리의 전용 데이터에 액세스할 수 있지만 .NET Framework 어셈블리의 전용 데이터에는 액세스할 수 없습니다. .NET Framework 어셈블리는 글로벌 어셈블리 캐시에 설치되고 항상 완전히 신뢰할 수 있습니다.

  익명으로 호스트된 동적 메서드는 호스트 애플리케이션에서 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그로 <xref:System.Security.Permissions.ReflectionPermission>을 부여하는 경우에만 JIT 표시 유형 확인을 건너뛰는 이 제한된 기능을 사용할 수 있습니다. 메서드가 호출될 때 이 권한이 필요합니다.

  > [!NOTE]
  > 동적 메서드가 생성될 때 내보내는 어셈블리의 호출 스택 정보가 포함됩니다. 따라서 메서드를 호출하는 어셈블리가 아닌 내보내는 어셈블리에 대한 권한이 필요합니다. 이렇게 하면 내보낸 코드가 높은 권한으로 실행되지 않습니다.

  이 연습의 끝부분에 있는 [전체 코드 예제](#Example)는 제한된 멤버 액세스의 사용 및 제한 사항을 보여 줍니다. `Worker` 클래스에는 표시 유형 확인을 건너뛰는 제한된 기능을 사용하거나 사용하지 않고 익명으로 호스트된 동적 메서드를 만들 수 있는 메서드가 포함되며 예제에서는 다양한 신뢰 수준을 가진 애플리케이션 도메인에서 이 메서드를 실행한 결과를 보여 줍니다.

  > [!NOTE]
  > 표시 유형 확인을 건너뛰는 제한된 기능은 익명으로 호스트된 동적 메서드의 기능입니다. 일반 동적 메서드가 JIT 표시 유형 확인을 건너뛸 경우 완전 신뢰가 부여되어야 합니다.

<a name="Example"></a>

## <a name="example"></a>예제

### <a name="description"></a>설명

다음 코드 예제는 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess> 플래그를 사용하여 대상 멤버가 코드를 내보내는 어셈블리와 같거나 낮은 신뢰 수준에 있는 경우에만 익명으로 호스트된 동적 메서드가 JIT 표시 유형 확인을 건너뛰도록 하는 방법을 보여 줍니다.

예제에서는 애플리케이션 도메인 경계에서 마샬링될 수 있는 `Worker` 클래스를 정의합니다. 클래스에는 동적 메서드를 내보내고 실행하는 두 개의 `AccessPrivateMethod` 메서드 오버로드가 있습니다. 첫 번째 오버로드는 `Worker` 클래스의 private `PrivateMethod` 메서드를 호출하는 동적 메서드를 내보내며 JIT 표시 유형 확인 여부에 관계없이 동적 메서드를 내보낼 수 있습니다. 두 번째 오버로드는 <xref:System.String> 클래스의 `internal` 속성(Visual Basic의 `Friend` 속성)에 액세스하는 동적 메서드를 내보냅니다.

예제에서는 도우미 메서드를 사용하여 `Internet` 권한으로 제한된 권한 집합을 만들고 나서 <xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=nameWithType> 메서드 오버로드로 애플리케이션 도메인을 만들어 도메인에서 실행되는 모든 코드가 이 권한 집합을 사용하도록 지정합니다. 예제에서는 애플리케이션 도메인에서 `Worker` 클래스 인스턴스를 만들고 `AccessPrivateMethod` 메서드를 두 번 실행합니다.

- `AccessPrivateMethod` 메서드가 처음 실행될 때 JIT 표시 유형 확인이 실행됩니다. JIT 표시 유형 확인을 실행하면 동적 메서드가 private 메서드에 액세스할 수 없으므로 동적 메서드는 호출 시 실패합니다.

- `AccessPrivateMethod` 메서드가 두 번째로 실행될 때는 JIT 표시 유형 확인을 건너뜁니다. `Internet` 권한 집합은 표시 유형 확인을 건너뛸 충분한 권한을 부여하지 않으므로 동적 메서드는 컴파일 시 실패합니다.

예제에서는 <xref:System.Security.Permissions.ReflectionPermission>을 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>와 함께 권한 집합에 추가합니다. 예제에서는 그다음에 두 번째 도메인을 만들어 도메인에서 실행되는 모든 코드에 새 권한 집합의 권한이 부여되도록 지정합니다. 예제에서는 새 애플리케이션 도메인에서 `Worker` 클래스 인스턴스를 만들고 `AccessPrivateMethod` 메서드의 오버로드를 둘 다 실행합니다.

- `AccessPrivateMethod` 메서드의 첫 번째 오버로드가 실행되고 JIT 표시 유형 확인을 건너뜁니다. 코드를 내보내는 어셈블리가 private 메서드를 포함하는 어셈블리와 같기 때문에 동적 메서드가 성공적으로 컴파일 및 실행됩니다. 따라서 신뢰 수준이 같습니다. `Worker` 클래스를 포함하는 애플리케이션에 여러 어셈블리가 있는 경우에는 모든 어셈블리의 신뢰 수준이 같으므로 모든 해당 어셈블리에 대해 동일한 프로세스가 성공합니다.

- `AccessPrivateMethod` 메서드의 두 번째 오버로드가 실행되고 다시 JIT 표시 유형 확인을 건너뜁니다. 이때 동적 메서드는 <xref:System.String> 클래스의 `internal` `FirstChar` 속성에 액세스하려고 하므로 동적 메서드가 컴파일 시 실패합니다. <xref:System.String> 클래스를 포함하는 어셈블리는 완전히 신뢰할 수 있습니다. 따라서 이 어셈블리는 코드를 내보내는 어셈블리보다 신뢰 수준이 높습니다.

이 비교는 신뢰할 수 있는 코드의 보안을 손상시키지 않고 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>를 사용하여 부분적으로 신뢰할 수 있는 코드가 다른 부분적으로 신뢰할 수 있는 코드의 표시 유형 확인을 건너뛰는 방법을 보여 줍니다.

### <a name="code"></a>코드

[!code-csharp[HowToEmitCodeInPartialTrust#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#1)]
[!code-vb[HowToEmitCodeInPartialTrust#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#1)]

## <a name="compiling-the-code"></a>코드 컴파일

- Visual Studio에서 이 코드 예제를 빌드하는 경우 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> 메서드에 클래스를 전달할 때 네임스페이스를 포함하도록 해당 클래스의 이름을 변경해야 합니다. 기본적으로 네임스페이스는 프로젝트의 이름입니다. 예를 들어 프로젝트가 "PartialTrust"이면 클래스 이름은 "PartialTrust.Worker"입니다.

## <a name="see-also"></a>참고 항목

- [리플렉션 내보내기의 보안 문제점](security-issues-in-reflection-emit.md)
- [방법: 샌드박스에서 부분적으로 신뢰할 수 있는 코드 실행](../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)
