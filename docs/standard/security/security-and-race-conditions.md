---
title: 보안 및 경합 상태
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], race conditions
- race conditions
- secure coding, race conditions
- code security, race conditions
ms.assetid: ea3edb80-b2e8-4e85-bfed-311b20cb59b6
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 57ceaedc7c38ae70a0db5a7fd584a765a7474aff
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61933811"
---
# <a name="security-and-race-conditions"></a>보안 및 경합 상태
다른 문제 영역을 보안 허점을 경합 상태에 의해 악용 가능성이 있습니다. 여러 가지 방법으로이 발생할 수 있습니다. 다음에 나오는 하위 항목은 개발자가 피해 야 하는 주요 문제 중 일부를 간략하게 설명 합니다.  
  
## <a name="race-conditions-in-the-dispose-method"></a>Dispose 메서드에서 경합  
 클래스의 경우 **Dispose** 메서드 (자세한 내용은 참조 하세요. [가비지 수집](../../../docs/standard/garbage-collection/index.md))은 동기화 되지 않은 것 같습니다 내부 정리 코드 **Dispose** 실행할 수 있습니다 둘 다음 예제에서와 같이 번입니다.  
  
```vb  
Sub Dispose()  
    If Not (myObj Is Nothing) Then  
       Cleanup(myObj)  
       myObj = Nothing  
    End If  
End Sub  
```  
  
```csharp  
void Dispose()   
{  
    if (myObj != null)   
    {  
        Cleanup(myObj);  
        myObj = null;  
    }  
}  
```  
  
 때문에이 **Dispose** 구현은 동기화 되지 않은, 있기 `Cleanup` 첫 번째 스레드 및 하기 전에 두 번째 스레드가 호출 될 `_myObj` 로 설정 되어 **null**합니다. 이 보안 문제 인지에 따라 달라 집니다 때는 `Cleanup` 코드를 실행 합니다. 동기화 되지 않은 사용 하 여 중요 한 문제가 **Dispose** 구현 파일과 같은 리소스 핸들의 사용이 포함 됩니다. 메서드를 잘못 사용 될 보안 문제를 일으키는 핸들을 잘못 발생할 수 있습니다.  
  
## <a name="race-conditions-in-constructors"></a>생성자에서 경합 상태  
 일부 응용 프로그램에서는 다른 스레드가 해당 클래스 생성자가 완전히 실행 하려면 먼저 클래스 멤버에 액세스할 수 있습니다. 이 발생 하거나 필요한 경우에 스레드를 동기화 해야 하는 경우 보안 문제가 발생 하지는 되도록 모든 클래스 생성자를 검토 해야 합니다.  
  
## <a name="race-conditions-with-cached-objects"></a>캐시 된 개체를 사용 하 여 경합  
 보안 정보를 캐시 하거나 코드 액세스 보안을 사용 하는 코드 [Assert](../../../docs/framework/misc/using-the-assert-method.md) 작업 노출 될 수 있습니다 경합 클래스의 다른 부분을 적절 하 게 동기화 되지 않은 경우 다음 예와에서 같이 합니다.  
  
```vb  
Sub SomeSecureFunction()  
    If SomeDemandPasses() Then  
        fCallersOk = True  
        DoOtherWork()  
        fCallersOk = False  
    End If  
End Sub  
  
Sub DoOtherWork()  
    If fCallersOK Then  
        DoSomethingTrusted()  
    Else  
        DemandSomething()  
        DoSomethingTrusted()  
    End If  
End Sub  
```  
  
```csharp  
void SomeSecureFunction()   
{  
    if (SomeDemandPasses())   
    {  
        fCallersOk = true;  
        DoOtherWork();  
        fCallersOk = false;  
    }  
}  
void DoOtherWork()   
{  
    if (fCallersOK)   
    {  
        DoSomethingTrusted();  
    }  
    else   
    {  
        DemandSomething();  
        DoSomethingTrusted();  
    }  
}  
```  
  
 다른 경로가 없으면 `DoOtherWork` 동일한 개체를 사용 하 여 다른 스레드에서 호출 될 수 있는, 신뢰할 수 없는 호출자를 빠져나갈 수 있습니다.  
  
 코드 보안 정보를 캐시 하는 경우이 취약성에 대 한 검토 해야 합니다.  
  
## <a name="race-conditions-in-finalizers"></a>종료자에서 경합 상태  
 해당 종료자에서 해제 되는 정적 또는 관리 되지 않는 리소스를 참조 하는 개체에 경합 상태가 발생할 수 있습니다. 여러 개체 클래스의 종료자에서 조작 되는 리소스를 공유 하는 경우 개체는 해당 리소스에 대 한 모든 액세스를 동기화 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../../docs/standard/security/secure-coding-guidelines.md)
