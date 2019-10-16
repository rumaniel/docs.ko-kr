---
title: Microsoft.Win32 네임스페이스를 사용하여 레지스트리 읽기 및 쓰기(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- registry [Visual Basic]
ms.assetid: 4a0dcce0-c27b-4199-baa8-ee4528da6a56
ms.openlocfilehash: bf0d6ae329c5a09986a4a7bf641fe6820387ff22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916564"
---
# <a name="reading-from-and-writing-to-the-registry-using-the-microsoftwin32-namespace-visual-basic"></a>Microsoft.Win32 네임스페이스를 사용하여 레지스트리 읽기 및 쓰기(Visual Basic)
`My.Computer.Registry`는 레지스트리에 대해 프로그래밍할 때 기본 요구를 충족해야 하지만, .NET Framework의 <xref:Microsoft.Win32> 네임스페이스에서 <xref:Microsoft.Win32.Registry> 및 <xref:Microsoft.Win32.RegistryKey> 클래스를 사용할 수도 있습니다.  
  
## <a name="keys-in-the-registry-class"></a>레지스트리 클래스의 키  
 <xref:Microsoft.Win32.Registry> 클래스는 하위 키 및 값에 액세스하기 위해 사용할 수 있는 기본 레지스트리 키를 제공합니다. 기본 키 자체는 읽기 전용입니다. 다음 표에서는 <xref:Microsoft.Win32.Registry> 클래스에서 사용되는 7개의 키를 나열하고 설명합니다.  
  
|**키**|**설명**|  
|-------------|---------------------|  
|<xref:Microsoft.Win32.Registry.ClassesRoot>|문서의 형식 및 그러한 형식과 관련된 속성을 정의합니다.|  
|<xref:Microsoft.Win32.Registry.CurrentConfig>|사용자와 관련되지 않은 하드웨어 구성 정보를 포함합니다.|  
|<xref:Microsoft.Win32.Registry.CurrentUser>|현재 사용자 기본 설정(예: 환경 변수)에 대한 정보를 포함합니다.|  
|<xref:Microsoft.Win32.Registry.DynData>|가상 디바이스 드라이버에서 사용하는 것과 같은 동적 레지스트리 데이터를 포함합니다.|  
|<xref:Microsoft.Win32.Registry.LocalMachine>|로컬 컴퓨터에 대한 구성 데이터를 유지하는 5개의 하위 키(하드웨어, SAM, 보안, 소프트웨어 및 시스템)를 포함합니다.|  
|<xref:Microsoft.Win32.Registry.PerformanceData>|소프트웨어 구성 요소에 대한 성능 정보를 포함합니다.|  
|<xref:Microsoft.Win32.Registry.Users>|기본 사용자 기본 설정에 대한 정보를 포함합니다.|  
  
> [!IMPORTANT]
> 로컬 컴퓨터(<xref:Microsoft.Win32.Registry.LocalMachine>)보다 현재 사용자(<xref:Microsoft.Win32.Registry.CurrentUser>)에게 데이터를 기록하는 것이 더 안전합니다. 만들고 있는 키가 전에 다른 프로세스(예: 악의적인 프로세스)로 만들어진 경우 일반적으로 "스쿼팅(squatting)"이라는 조건이 발생합니다. 이 문제가 발생하지 않도록 하려면 키가 존재하지 않을 경우 `Nothing`을 반환하는 메서드(예: <xref:Microsoft.Win32.RegistryKey.GetValue%2A>)를 사용합니다.  
  
## <a name="reading-a-value-from-the-registry"></a>레지스트리에서 값 읽기  
 다음 코드는 HKEY_CURRENT_USER에서 문자열을 읽는 방법을 보여 줍니다.  
  
 [!code-vb[VbResourceTasks#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#20)]  
  
 다음 코드는 문자열을 읽고, 늘리고, HKEY_CURRENT_USER에 씁니다.  
  
 [!code-vb[VbResourceTasks#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.SystemException>
- <xref:System.ApplicationException>
- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [Try...Catch...Finally 문](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
- [레지스트리 읽기 및 쓰기](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
- [보안 및 레지스트리](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)
