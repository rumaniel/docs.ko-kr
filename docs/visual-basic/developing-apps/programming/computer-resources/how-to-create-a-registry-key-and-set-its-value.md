---
title: '방법: Visual Basic에서 레지스트리 키 만들기 및 해당 값 설정'
ms.date: 07/20/2015
f1_keywords:
- RegistryKey.CreateSubKey
- RegistryKey.SetValue
helpviewer_keywords:
- registry keys [Visual Basic], creating
- registry [Visual Basic], adding values
- registry [Visual Basic], adding keys
- registry keys [Visual Basic], setting values
- examples [Visual Basic], registry
ms.assetid: d3e40f74-c283-480c-ab18-e5e9052cd814
ms.openlocfilehash: 84fc824ad5911621c679d70f480d9b5e83c095ad
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054128"
---
# <a name="how-to-create-a-registry-key-and-set-its-value-in-visual-basic"></a>방법: Visual Basic에서 레지스트리 키 만들기 및 해당 값 설정

`My.Computer.Registry` 개체의 `CreateSubKey` 메서드를 사용하여 레지스트리 키를 만들 수 있습니다.

## <a name="procedure"></a>프로시저

### <a name="to-create-a-registry-key"></a>레지스트리 키를 만들려면

- 키를 배치할 하이브와 키 이름을 지정하여 `CreateSubKey` 메서드를 사용합니다. `Subkey` 매개 변수는 대/소문자를 구분하지 않습니다. 이 예제에서는 HKEY_CURRENT_USER 아래에 레지스트리 키 `MyTestKey`를 만듭니다.

    [!code-vb[VbResourceTasks#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#17)]

### <a name="to-create-a-registry-key-and-set-a-value-in-it"></a>레지스트리 키를 만들고 키에 값을 설정하려면

1. 키를 배치할 하이브와 키 이름을 지정하여 `CreateSubkey` 메서드를 사용합니다. 이 예제에서는 HKEY_CURRENT_USER 아래에 레지스트리 키 `MyTestKey`를 만듭니다.

    [!code-vb[VbResourceTasks#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#17)]

2. `SetValue` 메서드를 사용하여 값을 설정합니다. 이 예제에서는 문자열 값 "MyTestKeyValue"를 "This is a test value"로 설정합니다.

    [!code-vb[VbResourceTasks#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#14)]

## <a name="example"></a>예

이 예제에서는 HKEY_CURRENT_USER 아래에 레지스트리 키 `MyTestKey`를 만든 다음 문자열 값 `MyTestKeyValue`를 `This is a test value`로 설정합니다.

[!code-vb[VbResourceTasks#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#15)]

## <a name="robust-programming"></a>강력한 프로그래밍

레지스트리 구조를 검사하여 키에 적합한 위치를 찾습니다. 예를 들어 현재 사용자의 HKEY_CURRENT_USER\Software 키를 열고 회사 이름으로 키를 만들 수 있습니다. 그런 다음 회사 키에 레지스트리 값을 추가합니다.

웹 애플리케이션에서 레지스트리를 읽는 경우 현재 사용자는 웹 애플리케이션에 구현된 인증 및 가장에 따라 결정됩니다.

로컬 컴퓨터(<xref:Microsoft.Win32.Registry.LocalMachine>)보다 사용자 폴더(<xref:Microsoft.Win32.Registry.CurrentUser>)에 데이터를 쓰는 것이 더 안전합니다.

레지스트리 값을 만들 때 해당 값이 이미 있는 경우 수행할 작업을 결정해야 합니다. 다른 악성 프로세스에서 값을 이미 만들고 액세스했을 수도 있습니다. 레지스트리 값에 데이터를 넣으면 다른 프로세스에서 해당 데이터를 사용할 수 있습니다. 이를 방지하려면 <xref:Microsoft.Win32.RegistryKey.GetValue%2A> 메서드를 사용합니다. 키가 아직 없는 경우 `Nothing`이 반환됩니다.

레지스트리 키가 ACL(액세스 제어 목록)로 보호된 경우에도 비밀(예: 암호)을 레지스트리에 일반 텍스트로 저장하는 것은 안전하지 않습니다.

다음 조건에서 예외가 발생합니다.

- 키의 이름이 `Nothing`인 경우(<xref:System.ArgumentNullException>)

- 사용자에게 레지스트리 키를 만들 수 있는 권한이 없는 경우(<xref:System.Security.SecurityException>)

- 키 이름이 255자 제한을 초과하는 경우(<xref:System.ArgumentException>)

- 키가 닫힌 경우(<xref:System.IO.IOException>)

- 레지스트리 키가 읽기 전용인 경우(<xref:System.UnauthorizedAccessException>)

## <a name="net-framework-security"></a>.NET Framework 보안

이 프로세스를 실행하려면 어셈블리에 <xref:System.Security.Permissions.RegistryPermission> 클래스에서 부여한 권한 수준이 필요합니다. 부분 신뢰 컨텍스트에서 실행하는 경우 프로세스가 권한 부족으로 인해 예외를 throw할 수 있습니다. 마찬가지로, 사용자에게 설정을 만들거나 쓸 수 있는 올바른 ACL이 있어야 합니다. 예를 들어 코드 액세스 보안 권한이 있는 로컬 애플리케이션에는 운영 체제 권한이 없을 수 있습니다. 자세한 내용은 [코드 액세스 보안 기본 사항](../../../../framework/misc/code-access-security-basics.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy.CurrentUser%2A>
- <xref:Microsoft.Win32.RegistryKey.CreateSubKey%2A>
- [레지스트리 읽기 및 쓰기](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
- [코드 액세스 보안 기본 사항](../../../../framework/misc/code-access-security-basics.md)
