---
title: 필수 인수 및 오버로드 그룹
ms.date: 03/30/2017
ms.assetid: 4ca3ed06-b9af-4b85-8b70-88c2186aefa3
ms.openlocfilehash: 84384e90be0036036477d9b4249832f544e17d08
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989306"
---
# <a name="required-arguments-and-overload-groups"></a>필수 인수 및 오버로드 그룹
활동을 실행하기 위해 특정 인수를 바인딩하도록 활동을 구성할 수 있습니다. `RequiredArgument` 특성은 활동의 특정 인수가 필수 인수임을 나타내고 `OverloadGroup` 특성은 필수 인수 범주를 그룹화하는 데 사용됩니다. 활동 작성자는 특성을 사용하여 단순 활동 유효성 검사 구성 또는 복합 활동 유효성 검사 구성을 제공할 수 있습니다.  
  
## <a name="using-required-arguments"></a>필수 인수 사용  
 활동에서 `RequiredArgument` 특성을 사용하려면 <xref:System.Activities.RequiredArgumentAttribute>를 사용하여 원하는 인수를 나타냅니다. 이 예제에서는 두 필수 인수를 가진 `Add` 활동을 정의합니다.  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 XAML에서는 또한 <xref:System.Activities.RequiredArgumentAttribute>를 사용하여 필수 인수를 나타냅니다. 이 예제에서 `Add` 활동은 세 인수를 사용하여 정의되며 <xref:System.Activities.Statements.Assign%601> 활동을 사용하여 추가 작업을 수행합니다.  
  
```xaml  
<Activity x:Class="ValidationDemo.Add" ...>  
  <x:Members>  
    <x:Property Name="Operand1" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Operand2" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Result" Type="OutArgument(x:Int32)" />  
  </x:Members>  
  <Assign>  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:Int32">[Result]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:Int32">[Operand1 + Operand2]</InArgument>  
    </Assign.Value>  
  </Assign>  
</Activity>  
```  
  
 활동을 사용할 때 필수 인수가 바인딩되지 않을 경우 다음 유효성 검사 오류가 반환됩니다.  
  
 **필수 작업 인수 ' Operand1 '의 값이 제공 되지 않았습니다.**  
> [!NOTE]
> 유효성 검사 오류 및 경고를 확인 하 고 처리 하는 방법에 대 한 자세한 내용은 [활동 유효성 검사 호출](invoking-activity-validation.md)을 참조 하세요.  
  
## <a name="using-overload-groups"></a>오버로드 그룹 사용

오버로드 그룹은 활동에서 유효한 인수 조합을 나타내는 메서드를 제공합니다. 인수는 <xref:System.Activities.OverloadGroupAttribute>를 사용하여 그룹화됩니다. 각 그룹에는에 <xref:System.Activities.OverloadGroupAttribute>지정 된 이름이 지정 됩니다. 오버 로드 그룹에서 하나의 인수 집합만 바인딩되는 경우 활동이 유효 합니다. 다음 예제에서는 `CreateLocation` 클래스를 정의합니다.  
  
```csharp  
class CreateLocation: Activity  
{  
    [RequiredArgument]  
    public InArgument<string> Name { get; set; }  
  
    public InArgument<string> Description { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Latitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Longitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    [OverloadGroup("G3")]  
    public InArgument<string> Street { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> City { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> State { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G3")]  
    public InArgument<int> Zip { get; set; }                  
}  
```  
  
 이 활동의 목적은 미국 내 위치를 지정하는 데 있습니다. 활동 사용자는 세 인수 그룹 중 하나를 사용하여 위치를 지정할 수 있습니다. 유효한 인수 조합을 지정하기 위해 세 가지 오버로드 그룹이 정의됩니다. `G1`에는 `Latitude` 및 `Longitude` 인수가 포함됩니다. `G2`에는 `Street`, `City` 및 `State`가 포함됩니다. `G3`에는 `Street` 및 `Zip`이 포함됩니다. `Name`도 필수 인수이지만 오버로드 그룹에 속하지는 않습니다. 이 활동이 유효하려면 `Name`을 한 오버로드 그룹의 모든 인수와 함께 바인딩해야 합니다.  
  
 [데이터베이스 액세스 활동](./samples/database-access-activities.md) 샘플에서 가져온 다음 예제에서는 두 개의 오버 로드 그룹인 `ConnectionString` 및 `ConfigFileSectionName`가 있습니다. 이 활동이 유효하려면 `ProviderName`과 `ConnectionString` 인수가 바인딩되어 있거나 `ConfigName` 인수가 바인딩되어 있어야 하지만 둘 다가 바인딩되어서는 안 됩니다.  
  
```csharp  
public class DbUpdate: AsyncCodeActivity  
{  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
  
    [DependsOn("Parameters")]  
    public OutArgument<int> AffectedRecords { get; set; }       
}  
```  
  
 오버로드 그룹 사용을 정의할 경우  
  
- 오버로드 그룹은 다른 오버로드 그룹의 하위 집합 또는 이와 동등한 집합이 될 수 없습니다.  
  
    > [!NOTE]
    > 그러나 이 규칙에는 한 가지 예외가 있습니다. 오버로드 그룹이 다른 오버로드 그룹의 하위 집합이고, 하위 집합에 `RequiredArgument`가 `false`인 인수만 있을 경우 오버로드 그룹은 유효합니다.  
  
- 오버로드 그룹은 겹칠 수 있지만 그룹의 교집합에 오버로드 그룹 중 하나 또는 둘 다의 모든 필수 인수가 포함되는 경우 오류가 발생합니다. 이전 예제에서 `G2` 및 `G3` 오버로드 그룹은 겹쳤지만 교집합에 오버로드 그룹 중 하나 또는 둘 다의 모든 인수가 포함되지 않았으므로 유효했습니다.  
  
 오버로드 그룹에서 인수를 바인딩할 경우  
  
- 오버로드 그룹은 그룹의 모든 `RequiredArgument` 인수가 바인딩되는 경우 바인딩된 것으로 간주됩니다.  
  
- 그룹에 `RequiredArgument` 인수가 없고 하나 이상의 인수가 바인딩되는 경우 그룹은 바인딩된 것으로 간주됩니다.  
  
- 하나의 오버로드 그룹에 `RequiredArgument` 인수가 없는 경우가 아니면 오버로드 그룹이 바인딩되지 않은 경우 유효성 검사 오류가 발생합니다.  
  
- 두 개 이상의 오버로드 그룹이 바인딩되는 경우, 즉 한 오버로드 그룹의 모든 필수 인수가 바인딩되고 다른 오버로드 그룹의 인수도 바인딩되는 경우 오류가 발생합니다.
