---
title: '방법: 레지스트리에 키 만들기(Visual C#)'
ms.date: 07/20/2015
helpviewer_keywords:
- registry, adding keys and values [C#]
- registry keys, creating [C#]
- keys, creating in registry
ms.assetid: 8fa475b0-e01f-483a-9327-fd03488fdf5d
ms.openlocfilehash: a3a6af8eb493ce17ac73769decd1f60b903ae165
ms.sourcegitcommit: d88024e6d6d8b242feae5f4007a709379355aa24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49337612"
---
# <a name="how-to-create-a-key-in-the-registry-visual-c"></a>방법: 레지스트리에 키 만들기(Visual C#)
이 예제에서는 현재 사용자의 레지스트리, "Names" 키 아래에 "Name" 및 "Isabella" 값 쌍을 추가합니다.  
  
## <a name="example"></a>예  
  
```csharp  
Microsoft.Win32.RegistryKey key;  
key = Microsoft.Win32.Registry.CurrentUser.CreateSubKey("Names");  
key.SetValue("Name", "Isabella");  
key.Close();  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
-   코드를 복사하고 콘솔 응용 프로그램의 `Main` 메서드에 붙여넣습니다.  
  
-   `Names` 매개 변수를 레지스트리의 HKEY_CURRENT_USER 노드 바로 아래에 있는 키 이름으로 바꿉니다.  
  
-   `Name` 매개 변수를 Names 노드 바로 아래에 있는 값 이름으로 바꿉니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 레지스트리 구조를 검사하여 키에 적합한 위치를 찾습니다. 예를 들어 현재 사용자의 소프트웨어 키를 열고 회사 이름으로 키를 만들 수 있습니다. 그런 다음 회사 키에 레지스트리 값을 추가합니다.  
  
 다음 조건에서 예외가 발생할 수 있습니다.  
  
-   키 이름이 null인 경우  
  
-   사용자에게 레지스트리 키를 만들 수 있는 권한이 없는 경우  
  
-   키 이름이 255자 제한을 초과하는 경우  
  
-   키가 닫힌 경우  
  
-   레지스트리 키가 읽기 전용인 경우  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 로컬 컴퓨터(`Microsoft.Win32.Registry.LocalMachine`)보다 사용자 폴더(`Microsoft.Win32.Registry.CurrentUser`)에 데이터를 쓰는 것이 더 안전합니다.  
  
 레지스트리 값을 만들 때 해당 값이 이미 있는 경우 수행할 작업을 결정해야 합니다. 다른 악성 프로세스에서 값을 이미 만들고 액세스했을 수도 있습니다. 레지스트리 값에 데이터를 넣으면 다른 프로세스에서 해당 데이터를 사용할 수 있습니다. 이를 방지하려면 `Overload:Microsoft.Win32.RegistryKey.GetValue` 메서드를 재정의합니다. 키가 아직 없는 경우 null이 반환됩니다.  
  
 레지스트리 키가 ACL(액세스 제어 목록)로 보호된 경우에도 암호 등을 레지스트리에 일반 텍스트로 저장하는 것은 안전하지 않습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO?displayProperty=nameWithType>  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](../../../csharp/programming-guide/file-system/index.md)  
- [C#을 사용하여 레지스트리에서 읽기, 쓰기 및 삭제](https://www.codeproject.com/Articles/3389/Read-write-and-delete-from-registry-with-C)
