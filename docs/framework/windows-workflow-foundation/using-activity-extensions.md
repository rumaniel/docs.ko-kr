---
title: 활동 확장 사용
ms.date: 03/30/2017
ms.assetid: 500eb96a-c009-4247-b6b5-b36faffdf715
ms.openlocfilehash: 551ce24db8c0adc8225ac94a1d05f998a26873a9
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988627"
---
# <a name="using-activity-extensions"></a>활동 확장 사용
활동은 호스트에서 워크플로에 명시적으로 모델링되지 않은 추가 기능을 제공할 수 있도록 하는 워크플로 애플리케이션 확장과 상호 작용할 수 있습니다.  이 항목에서는 활동이 실행되는 횟수를 계산하기 위해 확장을 만들고 사용하는 방법을 설명합니다.

### <a name="to-use-an-activity-extension-to-count-executions"></a>활동 확장을 사용하여 실행 횟수를 계산하려면

1. Visual Studio 2010을 엽니다. **새로 만들기**, **프로젝트**를 선택 합니다. **시각적 C#**  노드에서 **워크플로**를 선택 합니다.  템플릿 목록에서 **워크플로 콘솔 응용 프로그램** 을 선택 합니다. 프로젝트 이름을 `Extensions`로 지정합니다. **확인**을 클릭해 프로젝트를 만듭니다.

2. Program.cs 파일에서 **system.xml 네임 스페이스** 에 대 한 문을추가합니다.`using`

    ```csharp
    using System.Collections.Generic;
    ```

3. Program.cs 파일에서 **Executioncountextension**이라는 새 클래스를 만듭니다. 다음 코드는 **Register** 메서드가 호출 될 때 인스턴스 id를 추적 하는 워크플로 확장을 만듭니다.

    ```csharp
    // This extension collects a list of workflow Ids
    public class ExecutionCountExtension
    {
        IList<Guid> instances = new List<Guid>();

        public int ExecutionCount
        {
            get
            {
                return this.instances.Count;
            }
        }

        public IEnumerable<Guid> InstanceIds
        {
            get
            {
                return this.instances;
            }
        }

        public void Register(Guid activityInstanceId)
        {
            if (!this.instances.Contains<Guid>(activityInstanceId))
            {
                instances.Add(activityInstanceId);
            }
        }
    }
    ```

4. **Executioncountextension**을 사용 하는 활동을 만듭니다. 다음 코드는 런타임에서 **Executioncountextension** 개체를 검색 하 고 작업이 실행 될 때 **Register** 메서드를 호출 하는 활동을 정의 합니다.

    ```csharp
    // Activity that consumes an extension provided by the host. If the extension is available
    // in the context, it will invoke (in this case, registers the Id of the executing workflow)
    public class MyActivity: CodeActivity
    {
        protected override void Execute(CodeActivityContext context)
        {
            ExecutionCountExtension ext = context.GetExtension<ExecutionCountExtension>();
            if (ext != null)
            {
                ext.Register(context.WorkflowInstanceId);
            }

        }
    }
    ```

5. Program.cs 파일의 **Main** 메서드에서 작업을 구현 합니다. 다음 코드에는 두 가지 워크플로를 생성하고 각 워크플로를 몇 번 실행하며 확장에 포함된 결과 데이터를 표시하는 메서드가 포함되어 있습니다.

    ```csharp
    class Program
    {
        // Creates a workflow that uses the activity that consumes the extension
        static Activity CreateWorkflow1()
        {
            return new Sequence
            {
                Activities =
                {
                    new MyActivity()
                }
            };
        }

        // Creates a workflow that uses two instances of the activity that consumes the extension
        static Activity CreateWorkflow2()
        {
            return new Sequence
            {
                Activities =
                {
                    new MyActivity(),
                    new MyActivity()
                }
            };
        }

        static void Main(string[] args)
        {
            // create the extension
            ExecutionCountExtension executionCountExt = new ExecutionCountExtension();

            // configure the first invoker and execute 3 times
            WorkflowInvoker invoker = new WorkflowInvoker(CreateWorkflow1());
            invoker.Extensions.Add(executionCountExt);
            invoker.Invoke();
            invoker.Invoke();
            invoker.Invoke();

            // configure the second invoker and execute 2 times
            WorkflowInvoker invoker2 = new WorkflowInvoker(CreateWorkflow2());
            invoker2.Extensions.Add(executionCountExt);
            invoker2.Invoke();
            invoker2.Invoke();

            // show the data in the extension
            Console.WriteLine("Executed {0} times", executionCountExt.ExecutionCount);
            executionCountExt.InstanceIds.ToList().ForEach(i => Console.WriteLine("...{0}", i));
        }
    }
    ```
