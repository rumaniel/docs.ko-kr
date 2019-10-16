---
title: Func 및 Action 제네릭 대리자에 가변성 사용(C#)
ms.date: 07/20/2015
ms.assetid: 1826774f-2b7a-470f-b110-17cfdd6abdae
ms.openlocfilehash: bbfc41fb8ab3e7d800f1eb03098e02056e694872
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659918"
---
# <a name="using-variance-for-func-and-action-generic-delegates-c"></a>Func 및 Action 제네릭 대리자에 가변성 사용(C#)
이러한 예제는 메서드를 다시 사용하고 코드의 유연성을 높이기 위해 `Func` 및 `Action` 제네릭 대리자에서 공변성(covariance) 및 반공변성(contravariance)을 사용하는 방법을 보여 줍니다.  
  
 공변성(covariance) 및 반공변성(contravariance)에 대한 자세한 내용은 [대리자에서의 분산(C#)](./variance-in-delegates.md)을 참조하세요.  
  
## <a name="using-delegates-with-covariant-type-parameters"></a>공변 형식 매개 변수가 있는 대리자 사용  
 다음 예제는 `Func` 대리자에서 공변성(covariance) 지원의 이점을 보여 줍니다. `FindByTitle` 메서드는 `String` 형식의 매개 변수를 가져오고 `Employee` 형식의 개체를 반환합니다. 그러나 `Employee`는 `Person`을 상속하므로 이 메서드를 `Func<String, Person>` 대리자에 할당할 수 있습니다.  
  
```csharp  
// Simple hierarchy of classes.  
public class Person { }  
public class Employee : Person { }  
class Program  
{  
    static Employee FindByTitle(String title)  
    {  
        // This is a stub for a method that returns  
        // an employee that has the specified title.  
        return new Employee();  
    }  
  
    static void Test()  
    {  
        // Create an instance of the delegate without using variance.  
        Func<String, Employee> findEmployee = FindByTitle;  
  
        // The delegate expects a method to return Person,  
        // but you can assign it a method that returns Employee.  
        Func<String, Person> findPerson = FindByTitle;  
  
        // You can also assign a delegate   
        // that returns a more derived type   
        // to a delegate that returns a less derived type.  
        findPerson = findEmployee;  
  
    }  
}  
```  
  
## <a name="using-delegates-with-contravariant-type-parameters"></a>반공변 형식 매개 변수가 있는 대리자 사용  
 다음 예제에서는 제네릭 `Action` 대리자에서 반공변성(contravariance) 지원의 이점을 보여 줍니다. `AddToContacts` 메서드는 `Person` 형식의 매개 변수를 사용합니다. 그러나 `Employee`는 `Person`을 상속하므로 이 메서드를 `Action<Employee>` 대리자에 할당할 수 있습니다.  
  
```csharp  
public class Person { }  
public class Employee : Person { }  
class Program  
{  
    static void AddToContacts(Person person)  
    {  
        // This method adds a Person object  
        // to a contact list.  
    }  
  
    static void Test()  
    {  
        // Create an instance of the delegate without using variance.  
        Action<Person> addPersonToContacts = AddToContacts;  
  
        // The Action delegate expects   
        // a method that has an Employee parameter,  
        // but you can assign it a method that has a Person parameter  
        // because Employee derives from Person.  
        Action<Employee> addEmployeeToContacts = AddToContacts;  
  
        // You can also assign a delegate   
        // that accepts a less derived parameter to a delegate   
        // that accepts a more derived parameter.  
        addEmployeeToContacts = addPersonToContacts;  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [공변성(Covariance) 및 반공변성(Contravariance)(C#)](./index.md)
- [제네릭](../../../../standard/generics/index.md)
