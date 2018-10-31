---
title: 컬렉션에서 Culture를 구분하지 않는 문자열 작업 수행
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CaseInsensitiveComparer class, using
- CollectionsUtil.CreateCaseInsensitiveHashtable method
- culture-insensitive string operations, collections
- collections [.NET Framework], culture-insensitive string operations
- CaseInsensitiveHashCodeProvider class, using
- ArrayList.Sort method
- SortedList class, culture-insensitive string operations
- culture parameter
ms.assetid: 5cdc9396-a64b-4615-a1cd-b605db4c5983
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0e458f45fea8e2207ced930daebf10e653901fa7
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582803"
---
# <a name="performing-culture-insensitive-string-operations-in-collections"></a>컬렉션에서 Culture를 구분하지 않는 문자열 작업 수행
<xref:System.Collections> 네임스페이스에는 기본적으로 문화권 구분 동작을 제공하는 클래스 및 멤버가 있습니다. <xref:System.Collections.CaseInsensitiveComparer> 및 <xref:System.Collections.CaseInsensitiveHashCodeProvider> 클래스의 기본 생성자는 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 속성을 사용하여 새 인스턴스를 초기화합니다. <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType> 메서드의 모든 오버로드는 기본적으로 `Thread.CurrentCulture` 속성을 사용하여 <xref:System.Collections.Hashtable> 클래스의 새 인스턴스를 만듭니다. <xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> 메서드의 오버로드는 기본적으로 `Thread.CurrentCulture`를 사용하여 문화권 구분 정렬을 수행합니다. 문자열이 키로 사용될 경우 <xref:System.Collections.SortedList>의 정렬 및 조회는 `Thread.CurrentCulture`의 영향을 받을 수 있습니다. `Collections` 네임스페이스의 이러한 클래스 및 메서드에서 문화권을 구분하는 결과를 얻으려면 이 섹션에 제공된 사용 권장 사항을 따릅니다.  
  
 **참고** 비교 메서드에 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>를 전달하면 문화권을 구분하지 않는 비교가 수행됩니다. 그러나 파일 경로, 레지스트리 키 및 환경 변수 등과 같은 비언어적 비교는 수행되지 않습니다. 비교 결과에 따라 보안 결정을 지원하지도 않습니다. 비언어적 비교 또는 결과 기반 보안 의사 결정에 대한 지원의 경우는 응용 프로그램이 <xref:System.StringComparison> 값을 수락하는 비교 메서드를 사용해야 합니다. 그런 다음, 응용 프로그램이 <xref:System.StringComparison>을 전달해야 합니다.  
  
## <a name="using-the-caseinsensitivecomparer-and-caseinsensitivehashcodeprovider-classes"></a>CaseInsensitiveComparer 및 CaseInsensitiveHashCodeProvider 클래스 사용  
 `CaseInsensitiveHashCodeProvider` 및 `CaseInsensitiveComparer`에 대한 기본 생성자는 `Thread.CurrentCulture`를 사용하여 클래스의 새 인스턴스를 초기화함으로써 문화권 구분 동작을 발생합니다. 다음 코드 예제에서는 `CaseInsensitiveHashCodeProvider` 및 `CaseInsensitiveComparer`에 대해 기본 생성자를 사용하므로 문화권을 구분하는 `Hashtable`에 대한 생성자를 보여 줍니다.  
  
```vb  
internalHashtable = New Hashtable(CaseInsensitiveHashCodeProvider.Default, CaseInsensitiveComparer.Default)  
```  
  
```csharp  
internalHashtable = new Hashtable(CaseInsensitiveHashCodeProvider.Default, CaseInsensitiveComparer.Default);  
```  
  
 `CaseInsensitiveComparer` 및 `CaseInsensitiveHashCodeProvider` 클래스를 사용하여 문화권을 구분하지 않는 `Hashtable`을 만들려는 경우 `culture` 매개 변수를 수락하는 생성자를 사용하여 이러한 클래스의 새 인스턴스를 초기화합니다. `culture` 매개 변수의 경우 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>를 지정합니다. 다음 코드 예제에서는 문화권을 구분하지 않는 `Hashtable`에 대한 생성자를 보여 줍니다.  
  
```vb  
internalHashtable = New Hashtable(New  
    CaseInsensitiveHashCodeProvider(CultureInfo.InvariantCulture),  
    New CaseInsensitiveComparer(CultureInfo.InvariantCulture))  
```  
  
```csharp  
internalHashtable = new Hashtable(new CaseInsensitiveHashCodeProvider  
    (CultureInfo.InvariantCulture),   
    new CaseInsensitiveComparer(CultureInfo.InvariantCulture));  
```  
  
## <a name="using-the-collectionsutilcreatecaseinsensitivehashtable-method"></a>CollectionsUtil.CreateCaseInsensitiveHashtable 메서드 사용  
 `CollectionsUtil.CreateCaseInsensitiveHashTable` 메서드는 문자열의 대/소문자를 무시하는 `Hashtable` 클래스의 새 인스턴스를 만드는 데 유용한 바로 가기입니다. 그러나 `CollectionsUtil.CreateCaseInsensitiveHashTable` 메서드의 모든 오버로드는 `Thread.CurrentCulture` 속성을 사용하기 때문에 문화권을 구분합니다. 이 메서드를 사용하여 문화권을 구분하지 않는 `Hashtable`을 만들 수는 없습니다. 문화권을 구분하지 않는 `Hashtable`을 만들려면 `culture` 매개 변수를 수락하는 `Hashtable` 생성자를 사용합니다. `culture` 매개 변수의 경우 `CultureInfo.InvariantCulture`를 지정합니다. 다음 코드 예제에서는 문화권을 구분하지 않는 `Hashtable`에 대한 생성자를 보여 줍니다.  
  
```vb  
internalHashtable = New Hashtable(New  
    CaseInsensitiveHashCodeProvider(CultureInfo.InvariantCulture),  
    New CaseInsensitiveComparer(CultureInfo.InvariantCulture))  
```  
  
```csharp  
internalHashtable = new Hashtable(new CaseInsensitiveHashCodeProvider  
    (CultureInfo.InvariantCulture),   
    new CaseInsensitiveComparer(CultureInfo.InvariantCulture));  
```  
  
<a name="cpconperformingculture-insensitivestringoperationsincollectionsanchor1"></a>   
## <a name="using-the-sortedlist-class"></a>SortedList 클래스 사용  
 `SortedList`는 키를 기준으로 정렬되고 키와 인덱스로 액세스할 수 있는 키/값 쌍의 컬렉션을 나타냅니다. 문자열이 키인 경우에 `SortedList`를 사용하면 정렬 및 조회가 `Thread.CurrentCulture` 속성의 영향을 받을 수 있습니다. `SortedList`에서 문화권을 구분하지 않는 동작을 가져오려면 `comparer` 매개 변수를 수락하는 생성자 중 하나를 사용하여 `SortedList`를 만듭니다. `comparer` 매개 변수는 키를 비교할 때 사용할 <xref:System.Collections.IComparer> 구현을 지정합니다. 매개 변수의 경우 `CultureInfo.InvariantCulture`를 사용하는 사용자 지정 비교자 클래스를 지정하여 키를 비교합니다. 다음 예제에서는 `SortedList` 생성자에 대한 `comparer` 매개 변수로 지정할 수 있는 사용자 지정 문화권 비구분 비교자 클래스를 보여 줍니다.  
  
```vb  
Imports System  
Imports System.Collections  
Imports System.Globalization  
  
Friend Class InvariantComparer  
    Implements IComparer   
    Private m_compareInfo As CompareInfo  
    Friend Shared [Default] As New InvariantComparer()  
  
    Friend Sub New()  
        m_compareInfo = CultureInfo.InvariantCulture.CompareInfo  
    End Sub     
  
    Public Function Compare(a As Object, b As Object) As Integer _  
            Implements IComparer.Compare  
        Dim sa As String = CType(a, String)  
        Dim sb As String = CType(b, String)  
        If Not (sa Is Nothing) And Not (sb Is Nothing) Then  
            Return m_compareInfo.Compare(sa, sb)  
        Else  
            Return Comparer.Default.Compare(a, b)  
        End If  
    End Function  
End Class  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Globalization;  
  
internal class InvariantComparer : IComparer   
{  
    private CompareInfo m_compareInfo;  
    internal static readonly InvariantComparer Default = new  
        InvariantComparer();  
  
    internal InvariantComparer()   
    {  
        m_compareInfo = CultureInfo.InvariantCulture.CompareInfo;  
    }  
  
    public int Compare(Object a, Object b)  
    {  
        String sa = a as String;  
        String sb = b as String;  
        if (sa != null && sb != null)  
            return m_compareInfo.Compare(sa, sb);  
        else  
            return Comparer.Default.Compare(a,b);  
    }  
}  
```  
  
 일반적으로 사용자 지정 고정 비교자를 지정하지 않고 문자열에 대해 `SortedList`를 사용하는 경우 목록이 채워진 후에 수행한 `Thread.CurrentCulture` 변경 내용 때문에 목록이 무효화될 수 있습니다.  
  
## <a name="using-the-arraylistsort-method"></a>ArrayList.Sort 메서드 사용  
 `ArrayList.Sort` 메서드의 오버로드는 기본적으로 `Thread.CurrentCulture` 속성을 사용하여 문화권 구분 정렬을 수행합니다. 다른 정렬 순서로 인해 문화권마다 결과가 달라질 수 있습니다. 문화권 구분 동작을 제거하려면 `IComparer` 구현을 수락하는 이 메서드의 오버로드를 사용합니다. `comparer` 매개 변수의 경우 `CultureInfo.InvariantCulture`를 사용하는 사용자 지정 고정 비교자 클래스를 지정합니다. 사용자 지정 고정 비교자 클래스의 예는 [SortedList 클래스 사용](#cpconperformingculture-insensitivestringoperationsincollectionsanchor1)에 제공됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.CaseInsensitiveComparer>  
- <xref:System.Collections.CaseInsensitiveHashCodeProvider>  
- <xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType>  
- <xref:System.Collections.SortedList>  
- <xref:System.Collections.Hashtable>  
- <xref:System.Collections.IComparer>  
- [Culture의 영향을 받지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)  
- <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType>
