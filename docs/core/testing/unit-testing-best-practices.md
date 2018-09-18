---
title: 단위 테스트 작성에 대한 모범 사례
description: 코드 품질 및 탄력성을 구동하는 단위 테스트 작성에 대한 모범 사례를 알아봅니다.
author: jpreese
ms.author: wiwagn
ms.date: 07/28/2018
ms.openlocfilehash: 69fe0cae141d1ed1e1281eecd78bf03e6e8be961
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43527753"
---
# <a name="unit-testing-best-practices"></a><span data-ttu-id="f4879-103">단위 테스트 모범 사례</span><span class="sxs-lookup"><span data-stu-id="f4879-103">Unit testing best practices</span></span>

<span data-ttu-id="f4879-104">[John Reese](http://reesespieces.io), [Roy Osherove](http://osherove.com/)에 대한 특별한 감사</span><span class="sxs-lookup"><span data-stu-id="f4879-104">By [John Reese](http://reesespieces.io) with special thanks to [Roy Osherove](http://osherove.com/)</span></span>

<span data-ttu-id="f4879-105">단위 테스트 작성에는 회귀를 돕고, 문서를 제공하고, 좋은 디자인을 용이하게 하는 등에 다양한 혜택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-105">There are numerous benefits to writing unit tests; they help with regression, provide documentation, and facilitate good design.</span></span> <span data-ttu-id="f4879-106">그러나 읽기 어렵고 불안정한 단위 테스트는 코드 기반을 파괴할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-106">However, hard to read and brittle unit tests can wreak havoc on your code base.</span></span>

<span data-ttu-id="f4879-107">이 가이드에서는 단위 테스트를 작성할 때 테스트를 탄력적이고 이해하기 쉽게 유지하기 위한 몇 가지 모범 사례를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-107">In this guide, you'll learn some best practices when writing unit tests to keep your tests resilient and easy to understand.</span></span>

## <a name="why-unit-test"></a><span data-ttu-id="f4879-108">단위 테스트하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="f4879-108">Why unit test?</span></span>

### <a name="less-time-performing-functional-tests"></a><span data-ttu-id="f4879-109">기능 테스트 수행 시간 단축</span><span class="sxs-lookup"><span data-stu-id="f4879-109">Less time performing functional tests</span></span>
<span data-ttu-id="f4879-110">기능 테스트는 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-110">Functional tests are expensive.</span></span> <span data-ttu-id="f4879-111">일반적으로 응용 프로그램을 열고 사용자(또는 다른 사용자)가 예상되는 동작의 유효성을 검사하기 위해 따라야 하는 일련의 단계 수행이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-111">They typically involve opening up the application and performing a series of steps that you (or someone else), must follow in order to validate the expected behavior.</span></span> <span data-ttu-id="f4879-112">이러한 단계는 항상 테스터에게 알려진 것은 아니며, 이는 테스트를 수행하기 위해 해당 영역에 더 많은 지식을 갖추어야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-112">These steps may not always be known to the tester, which means they will have to reach out to someone more knowledgeable in the area in order to carry out the test.</span></span> <span data-ttu-id="f4879-113">테스트 자체는 사소한 변경인 경우에는 몇 초가 걸리거나 큰 변경의 경우에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-113">Testing itself could take seconds for trivial changes, or minutes for larger changes.</span></span> <span data-ttu-id="f4879-114">마지막으로, 이 프로세스는 시스템에서 수행하는 모든 변경 사항에 대해 반복되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-114">Lastly, this process must be repeated for every change that you make in the system.</span></span>

<span data-ttu-id="f4879-115">반면에 단위 테스트는 밀리초가 소요되며, 단추를 눌러 실행할 수 있으며 시스템 전체에 대한 지식이 반드시 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-115">Unit tests, on the other hand, take milliseconds, can be run at the press of a button and do not necessarily require any knowledge of the system at large.</span></span> <span data-ttu-id="f4879-116">테스트 통과 또는 실패 여부는 개인이 아닌 test runner의 몫입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-116">Whether or not the test passes or fails is up to the test runner, not the individual.</span></span>

### <a name="protection-against-regression"></a><span data-ttu-id="f4879-117">회귀에 대한 보호</span><span class="sxs-lookup"><span data-stu-id="f4879-117">Protection against regression</span></span>
<span data-ttu-id="f4879-118">회귀 오류는 응용 프로그램이 변경될 때 도입된 결함입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-118">Regression defects are defects that are introduced when a change is made to the application.</span></span> <span data-ttu-id="f4879-119">테스터는 새 기능을 테스트할 뿐만 아니라 이전에 구현된 기능이 여전히 예상대로 작동하는지 확인하기 위해 이전에 존재했던 기능도 테스트하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-119">It is common for testers to not only test their new feature but also features that existed beforehand in order to verify that previously implemented features still function as expected.</span></span>

<span data-ttu-id="f4879-120">단위 테스트를 사용하면 모든 빌드 후에 또는 코드 줄을 변경한 후에도 전체 테스트 도구 모음을 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-120">With unit testing, it's possible to rerun your entire suite of tests after every build or even after you change a line of code.</span></span> <span data-ttu-id="f4879-121">새 코드가 기존 기능을 중단시키지 않는다는 신뢰를 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-121">Giving you confidence that your new code does not break existing functionality.</span></span>

### <a name="executable-documentation"></a><span data-ttu-id="f4879-122">실행 가능한 설명서</span><span class="sxs-lookup"><span data-stu-id="f4879-122">Executable documentation</span></span>
<span data-ttu-id="f4879-123">특정 메서드가 무엇을 하는지 또는 특정 입력이 지정된 동작이 어떻게 수행되는지 항상 명확하지는 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-123">It may not always be obvious what a particular method does or how it behaves given a certain input.</span></span> <span data-ttu-id="f4879-124">빈 문자열을 전달하면 이 메서드는 어떻게 작동하는가를 직접 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-124">You may ask yourself: How does this method behave if I pass it a blank string?</span></span> <span data-ttu-id="f4879-125">Null?</span><span class="sxs-lookup"><span data-stu-id="f4879-125">Null?</span></span>

<span data-ttu-id="f4879-126">이름이 잘 지정된 단위 테스트의 도구 모음이 있는 경우 각 테스트는 지정된 입력에 대해 예상되는 출력을 명확하게 설명할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-126">When you have a suite of well-named unit tests, each test should be able to clearly explain the expected output for a given input.</span></span> <span data-ttu-id="f4879-127">또한 실제로 작동하는지 확인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-127">In addition, it should be able to verify that it actually works.</span></span>

### <a name="less-coupled-code"></a><span data-ttu-id="f4879-128">적은 결합 코드</span><span class="sxs-lookup"><span data-stu-id="f4879-128">Less coupled code</span></span>
<span data-ttu-id="f4879-129">코드가 밀접하게 결합되면 단위 테스트하기가 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-129">When code is tightly coupled, it can be difficult to unit test.</span></span> <span data-ttu-id="f4879-130">작성 중인 코드에 대한 단위 테스트를 만들지 않으면 결합이 덜 분명해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-130">Without creating unit tests for the code that you're writing, coupling may be less apparent.</span></span>

<span data-ttu-id="f4879-131">코드 테스트를 작성하면 자연스럽게 분리됩니다. 그렇지 않으면 테스트하기가 더 어려워지기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-131">Writing tests for your code will naturally decouple your code, because it would be more difficult to test otherwise.</span></span>

## <a name="characteristics-of-a-good-unit-test"></a><span data-ttu-id="f4879-132">좋은 단위 테스트의 특징</span><span class="sxs-lookup"><span data-stu-id="f4879-132">Characteristics of a good unit test</span></span>
- <span data-ttu-id="f4879-133">**Fast**.</span><span class="sxs-lookup"><span data-stu-id="f4879-133">**Fast**.</span></span> <span data-ttu-id="f4879-134">완성도 높은 프로젝트에서 수천 개의 단위 테스트를 수행하는 것은 드문 일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-134">It is not uncommon for mature projects to have thousands of unit tests.</span></span> <span data-ttu-id="f4879-135">단위 테스트는 실행하는 데 시간이 거의 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-135">Unit tests should take very little time to run.</span></span> <span data-ttu-id="f4879-136">밀리초.</span><span class="sxs-lookup"><span data-stu-id="f4879-136">Milliseconds.</span></span>
- <span data-ttu-id="f4879-137">**Isolated**.</span><span class="sxs-lookup"><span data-stu-id="f4879-137">**Isolated**.</span></span> <span data-ttu-id="f4879-138">독립형 단위 테스트는 독립적으로 실행될 수 있으며, 파일 시스템 또는 데이터베이스와 같은 외부 요인에 종속되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-138">Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.</span></span>
- <span data-ttu-id="f4879-139">**반복 가능**.</span><span class="sxs-lookup"><span data-stu-id="f4879-139">**Repeatable**.</span></span> <span data-ttu-id="f4879-140">단위 테스트를 실행하는 것은 해당 결과와 일치해야 합니다. 즉, 실행 사이에 아무 것도 변경하지 않으면 항상 동일한 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-140">Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.</span></span>
- <span data-ttu-id="f4879-141">**자체 검사**.</span><span class="sxs-lookup"><span data-stu-id="f4879-141">**Self-Checking**.</span></span> <span data-ttu-id="f4879-142">테스트는 사람의 개입 없이 통과했는지 여부를 자동으로 검색할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-142">The test should be able to automatically detect if it passed or failed without any human interaction.</span></span>
- <span data-ttu-id="f4879-143">**Timely**.</span><span class="sxs-lookup"><span data-stu-id="f4879-143">**Timely**.</span></span> <span data-ttu-id="f4879-144">단위 테스트는 테스트 중인 코드에 비해 작성하는 데 불균형적으로 긴 시간이 걸리지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-144">A unit test should not take a disproportionally long time to write compared to the code being tested.</span></span> <span data-ttu-id="f4879-145">코드를 작성하는 데 비해 많은 시간이 걸리는 코드를 테스트하는 경우 더 많은 테스트가 가능한 디자인을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f4879-145">If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.</span></span>

## <a name="lets-speak-the-same-language"></a><span data-ttu-id="f4879-146">동일한 언어 사용</span><span class="sxs-lookup"><span data-stu-id="f4879-146">Let's speak the same language</span></span>
<span data-ttu-id="f4879-147">*mock*이라는 용어는 불행히도 테스트에 대해 이야기할 때 잘못 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-147">The term *mock* is unfortunately very misused when talking about testing.</span></span> <span data-ttu-id="f4879-148">다음은 단위 테스트를 작성할 때 *fakes*의 가장 일반적인 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-148">The following defines the most common types of *fakes* when writing unit tests:</span></span>

<span data-ttu-id="f4879-149">*Fake* - fake는 stub 또는 mock 개체를 설명하는 데 사용할 수 있는 일반적인 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-149">*Fake* - A fake is a generic term which can be used to describe either a stub or a mock object.</span></span> <span data-ttu-id="f4879-150">stub 또는 mock인지 여부는 사용되는 컨텍스트에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-150">Whether it is a stub or a mock depends on the context in which it's used.</span></span> <span data-ttu-id="f4879-151">즉, fake는 stub 또는 mock이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-151">So in other words, a fake can be a stub or a mock.</span></span>

<span data-ttu-id="f4879-152">*Mock* - mock 개체는 단위 테스트가 통과되었는지 여부를 결정하는 시스템에서 fake 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-152">*Mock* - A mock object is a fake object in the system that decides whether or not a unit test has passed or failed.</span></span> <span data-ttu-id="f4879-153">mock은 어설션될 때까지 Fake로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-153">A mock starts out as a Fake until it is asserted against.</span></span>

<span data-ttu-id="f4879-154">*Stub* - stub은 시스템의 기존 종속성(또는 협력자)을 제어할 수 있는 대체품입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-154">*Stub* - A stub is a controllable replacement for an existing dependency (or collaborator) in the system.</span></span> <span data-ttu-id="f4879-155">stub을 사용하여 종속성을 직접 처리하지 않고 코드를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-155">By using a stub, you can test your code without dealing with the dependency directly.</span></span> <span data-ttu-id="f4879-156">기본적으로 fake는 stub으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-156">By default, a fake starts out as a stub.</span></span>

<span data-ttu-id="f4879-157">다음 코드 조각을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-157">Consider the following code snippet:</span></span>

```csharp
var mockOrder = new MockOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="f4879-158">이는 stub이 mock이라고 불리는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-158">This would be an example of stub being referred to as a mock.</span></span> <span data-ttu-id="f4879-159">이 경우 stub입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-159">In this case, it is a stub.</span></span> <span data-ttu-id="f4879-160">`Purchase`(테스트 중인 시스템)를 인스턴스화할 수 있는 수단으로 Order를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-160">You're just passing in the Order as a means to be able to instantiate `Purchase` (the system under test).</span></span> <span data-ttu-id="f4879-161">`MockOrder` 이름도 매우 잘못된 것입니다. 다시 말해서, 순서가 mock이 아니기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-161">The name `MockOrder` is also very misleading because again, the order is not a mock.</span></span>

<span data-ttu-id="f4879-162">더 나은 방법은</span><span class="sxs-lookup"><span data-stu-id="f4879-162">A better approach would be</span></span>

```csharp
var stubOrder = new FakeOrder();
var purchase = new Purchase(stubOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="f4879-163">클래스 이름을 `FakeOrder`로 바꾸면 클래스를 훨씬 더 일반화되게 만들므로 클래스를 mock 또는 stub으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-163">By renaming the class to `FakeOrder`, you've made the class a lot more generic, the class can be used as a mock or a stub.</span></span> <span data-ttu-id="f4879-164">어느 것이든 테스트 사례에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-164">Whichever is better for the test case.</span></span> <span data-ttu-id="f4879-165">위의 예에서는 `FakeOrder`가 stub으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-165">In the above example, `FakeOrder` is used as a stub.</span></span> <span data-ttu-id="f4879-166">assert 중에 `FakeOrder`를 어떤 모양 또는 형태로 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-166">You're not using the `FakeOrder` in any shape or form during the assert.</span></span> <span data-ttu-id="f4879-167">`FakeOrder`는 방금 `Purchase` 클래스에 전달되어 생성자의 요구 사항을 충족했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-167">`FakeOrder` was just passed into the `Purchase` class to satisfy the requirements of the constructor.</span></span>

<span data-ttu-id="f4879-168">Mock으로 사용하려면 다음과 같이 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-168">To use it as a Mock, you could do something like this</span></span>

```csharp
var mockOrder = new FakeOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(mockOrder.Validated);
```

<span data-ttu-id="f4879-169">이 경우 Fake(해당 항목에 대한 어설션)의 속성을 확인 중이므로 위의 코드 조각에서 `mockOrder`는 Mock입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-169">In this case, you are checking a property on the Fake (asserting against it), so in the above code snippet, the `mockOrder` is a Mock.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4879-170">이 용어를 올바르게 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-170">It's important to get this terminology correct.</span></span> <span data-ttu-id="f4879-171">stubs를 "mocks"라고 부른다면 다른 개발자는 의도에 대해 잘못된 가정을 하게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-171">If you call your stubs "mocks", other developers are going to make false assumptions about your intent.</span></span>

<span data-ttu-id="f4879-172">mocks와 stubs에 대해 기억해야 할 주요 사항은 mocks는 stubs와 같지만, mock 개체에 대해 어설션하는 반면 stub에 대해서는 어설션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-172">The main thing to remember about mocks versus stubs is that mocks are just like stubs, but you assert against the mock object, whereas you do not assert against a stub.</span></span>

## <a name="best-practices"></a><span data-ttu-id="f4879-173">최선의 구현 방법</span><span class="sxs-lookup"><span data-stu-id="f4879-173">Best practices</span></span>

### <a name="naming-your-tests"></a><span data-ttu-id="f4879-174">테스트 이름 지정</span><span class="sxs-lookup"><span data-stu-id="f4879-174">Naming your tests</span></span>
<span data-ttu-id="f4879-175">테스트의 이름은 다음 세 부분으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-175">The name of your test should consist of three parts:</span></span>
- <span data-ttu-id="f4879-176">테스트할 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-176">The name of the method being tested.</span></span>
- <span data-ttu-id="f4879-177">테스트 중인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-177">The scenario under which it's being tested.</span></span>
- <span data-ttu-id="f4879-178">시나리오에서 호출될 때 예상되는 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-178">The expected behavior when the scenario is invoked.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-179">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-179">Why?</span></span>
- <span data-ttu-id="f4879-180">이름 지정 표준은 테스트의 의도를 명시적으로 표현하기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-180">Naming standards are important because they explicitly express the intent of the test.</span></span>

<span data-ttu-id="f4879-181">테스트는 단순히 코드가 작동하는지 확인하는 것 이상이며, 문서도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-181">Tests are more than just making sure your code works, they also provide documentation.</span></span> <span data-ttu-id="f4879-182">단위 테스트 도구 모음을 살펴봄으로써 코드 자체를 조회하지 않고도 코드의 동작을 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-182">Just by looking at the suite of unit tests, you should be able to infer the behavior of your code without even looking at the code itself.</span></span> <span data-ttu-id="f4879-183">또한 테스트가 실패하는 경우 기대치를 충족하지 못하는 시나리오를 정확히 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-183">Additionally, when tests fail, you can see exactly which scenarios do not meet your expectations.</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-184">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-184">Bad:</span></span>
[!code-csharp[BeforeNaming](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeNaming)]

#### <a name="better"></a><span data-ttu-id="f4879-185">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-185">Better:</span></span>
[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="arranging-your-tests"></a><span data-ttu-id="f4879-186">테스트 정렬</span><span class="sxs-lookup"><span data-stu-id="f4879-186">Arranging your tests</span></span>
<span data-ttu-id="f4879-187">**정렬, 동작, 어설션**은 단위 테스트 시 일반적인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-187">**Arrange, Act, Assert** is a common pattern when unit testing.</span></span> <span data-ttu-id="f4879-188">이름에서 알 수 있듯이 세 가지 주요 작업으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-188">As the name implies, it consists of three main actions:</span></span>
- <span data-ttu-id="f4879-189">개체를 *정렬*하고 필요에 따라 만들고 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-189">*Arrange* your objects, creating and setting them up as necessary.</span></span>
- <span data-ttu-id="f4879-190">개체의 *동작*입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-190">*Act* on an object.</span></span>
- <span data-ttu-id="f4879-191">특정 항목이 예상대로라고 *assert*합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-191">*Assert* that something is as expected.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-192">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-192">Why?</span></span>
- <span data-ttu-id="f4879-193">테스트할 항목을 *정렬* 및 *assert* 단계에서 명확하게 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-193">Clearly separates what is being tested from the *arrange* and *assert* steps.</span></span>
- <span data-ttu-id="f4879-194">어설션과 "Act" 코드를 혼합할 기회가 적습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-194">Less chance to intermix assertions with "Act" code.</span></span>

<span data-ttu-id="f4879-195">가독성은 테스트를 작성할 때 가장 중요한 측면 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-195">Readability is one of the most important aspects when writing a test.</span></span> <span data-ttu-id="f4879-196">테스트 내에서 이러한 작업을 각각 구분하면 코드를 호출하는 데 필요한 종속성, 코드 호출 방법 및 어설션하려는 대상이 명확하게 강조 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-196">Separating each of these actions within the test clearly highlight the dependencies required to call your code, how your code is being called, and what you are trying to assert.</span></span> <span data-ttu-id="f4879-197">몇 가지 단계를 결합하여 테스트의 크기를 줄일 수 있지만, 기본적인 목표는 가능한 한 테스트를 최대한으로 읽을 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-197">While it may be possible to combine some steps and reduce the size of your test, the primary goal is to make the test as readable as possible.</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-198">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-198">Bad:</span></span>
[!code-csharp[BeforeArranging](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeArranging)]

#### <a name="better"></a><span data-ttu-id="f4879-199">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-199">Better:</span></span>
[!code-csharp[AfterArranging](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterArranging)]

### <a name="write-minimally-passing-tests"></a><span data-ttu-id="f4879-200">최소한의 테스트 통과 작성</span><span class="sxs-lookup"><span data-stu-id="f4879-200">Write minimally passing tests</span></span>
<span data-ttu-id="f4879-201">단위 테스트에 사용할 입력은 현재 테스트 중인 동작을 확인하기 위해 가능한 한 가장 간단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-201">The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-202">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-202">Why?</span></span>
- <span data-ttu-id="f4879-203">테스트는 코드베이스의 향후 변화에 대한 복원력이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-203">Tests become more resilient to future changes in the codebase.</span></span>
- <span data-ttu-id="f4879-204">구현에 대한 테스트 동작에 근접합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-204">Closer to testing behavior over implementation.</span></span>

<span data-ttu-id="f4879-205">테스트를 통과하는 데 필요한 것보다 많은 정보를 포함하는 테스트는 테스트에 오류가 발생할 가능성이 높으며 테스트의 의도를 덜 명확하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-205">Tests that include more information than required to pass the test have a higher chance of introducing errors into the test and can make the intent of the test less clear.</span></span> <span data-ttu-id="f4879-206">테스트를 작성할 때 동작에 집중하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-206">When writing tests you want to focus on the behavior.</span></span> <span data-ttu-id="f4879-207">모델의 추가 속성을 설정하거나 필요하지 않을 때 0이 아닌 값을 사용하면 증명하려고 시도한 것만 손상됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-207">Setting extra properties on models or using non-zero values when not required, only detracts from what you are trying to prove.</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-208">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-208">Bad:</span></span>
[!code-csharp[BeforeMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMinimallyPassing)]

#### <a name="better"></a><span data-ttu-id="f4879-209">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-209">Better:</span></span>
[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="avoid-magic-strings"></a><span data-ttu-id="f4879-210">매직 문자열 방지</span><span class="sxs-lookup"><span data-stu-id="f4879-210">Avoid magic strings</span></span>
<span data-ttu-id="f4879-211">단위 테스트의 이름 지정 변수는(프로덕션 코드의 이름 지정 변수보다 더 중요하지는 않지만) 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-211">Naming variables in unit tests is as important, if not more important, than naming variables in production code.</span></span> <span data-ttu-id="f4879-212">단위 테스트에는 매직 문자열이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-212">Unit tests should not contain magic strings.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-213">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-213">Why?</span></span>
- <span data-ttu-id="f4879-214">값을 특별하게 만드는 요인을 파악하기 위해 테스트의 판독기가 프로덕션 코드를 검사할 필요가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-214">Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special.</span></span>
- <span data-ttu-id="f4879-215">*성취*하려는 것보다는 *증명*하려는 것을 명시적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-215">Explicitly shows what you're trying to *prove* rather than trying to *accomplish*.</span></span>

<span data-ttu-id="f4879-216">매직 문자열은 테스트 판독기에 혼동을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-216">Magic strings can cause confusion to the reader of your tests.</span></span> <span data-ttu-id="f4879-217">문자열이 일반적이지 않은 경우 매개 변수 또는 반환 값에 대해 특정 값이 선택된 이유가 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-217">If a string looks out of the ordinary, they may wonder why a certain value was chosen for a parameter or return value.</span></span> <span data-ttu-id="f4879-218">이를 통해 테스트에 집중하기보다는 구현 세부 사항을 더 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-218">This may lead them to take a closer look at the implementation details, rather than focus on the test.</span></span>

> [!TIP] 
> <span data-ttu-id="f4879-219">테스트를 작성할 때는 가능한 한 많은 의도를 표현하는 것을 목표로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-219">When writing tests, you should aim to express as much intent as possible.</span></span> <span data-ttu-id="f4879-220">매직 문자열의 경우 좋은 방법은 이러한 값을 상수에 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-220">In the case of magic strings, a good approach is to assign these values to constants.</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-221">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-221">Bad:</span></span>
[!code-csharp[BeforeMagicString](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMagicString)]

#### <a name="better"></a><span data-ttu-id="f4879-222">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-222">Better:</span></span>
[!code-csharp[AfterMagicString](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterMagicString)]

### <a name="avoid-logic-in-tests"></a><span data-ttu-id="f4879-223">테스트에서 논리 방지</span><span class="sxs-lookup"><span data-stu-id="f4879-223">Avoid logic in tests</span></span>
<span data-ttu-id="f4879-224">단위 테스트를 작성할 때 수동 문자열 연결 및 `if`, `while`, `for`, `switch` 등의 논리 조건을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-224">When writing your unit tests avoid manual string concatenation and logical conditions such as `if`, `while`, `for`, `switch`, etc.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-225">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-225">Why?</span></span>
- <span data-ttu-id="f4879-226">테스트 중에 버그가 발생할 가능성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-226">Less chance to introduce a bug inside of your tests.</span></span>
- <span data-ttu-id="f4879-227">구현 세부 정보보다는 최종 결과에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-227">Focus on the end result, rather than implementation details.</span></span>

<span data-ttu-id="f4879-228">테스트 도구 모음에 논리를 도입하면 버그가 발생할 가능성이 크게 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-228">When you introduce logic into your test suite, the chance of introducing a bug into it increases dramatically.</span></span> <span data-ttu-id="f4879-229">버그를 찾고자 하는 마지막 위치는 테스트 도구 모음 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-229">The last place that you want to find a bug is within your test suite.</span></span> <span data-ttu-id="f4879-230">테스트 작동에 높은 수준의 확신이 있어야 합니다. 그렇지 않으면 신뢰할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-230">You should have a high level of confidence that your tests work, otherwise, you will not trust them.</span></span> <span data-ttu-id="f4879-231">신뢰할 수 없는 테스트는 어떤 가치도 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-231">Tests that you do not trust, do not provide any value.</span></span> <span data-ttu-id="f4879-232">테스트가 실패하면 코드에 실제로 잘못된 것이 있어서 무시할 수 없다는 것을 느낄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-232">When a test fails, you want to have a sense that something is actually wrong with your code and that it cannot be ignored.</span></span>

> [!TIP]
> <span data-ttu-id="f4879-233">테스트의 논리가 불가피한 경우 테스트를 두 개 이상의 다른 테스트로 분할하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-233">If logic in your test seems unavoidable, consider splitting the test up into two or more different tests.</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-234">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-234">Bad:</span></span>
[!code-csharp[LogicInTests](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#LogicInTests)]

#### <a name="better"></a><span data-ttu-id="f4879-235">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-235">Better:</span></span>
[!code-csharp[AfterTestLogic](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterTestLogic)]

### <a name="prefer-helper-methods-to-setup-and-teardown"></a><span data-ttu-id="f4879-236">설정 및 해제할 도우미 방법 선호</span><span class="sxs-lookup"><span data-stu-id="f4879-236">Prefer helper methods to setup and teardown</span></span>
<span data-ttu-id="f4879-237">테스트에 비슷한 개체나 상태가 필요한 경우 Setup 및 Teardown 특성이 있는 경우보다 도우미 메서드를 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-237">If you require a similar object or state for your tests, prefer a helper method than leveraging Setup and Teardown attributes if they exist.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-238">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-238">Why?</span></span>
- <span data-ttu-id="f4879-239">모든 코트가 각 테스트 내에서 볼 수 있기 때문에 테스트를 읽을 때 혼동이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-239">Less confusion when reading the tests since all of the code is visible from within each test.</span></span>
- <span data-ttu-id="f4879-240">지정된 테스트에 대해 너무 많거나 너무 적게 설정될 가능성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-240">Less chance of setting up too much or too little for the given test.</span></span>
- <span data-ttu-id="f4879-241">테스트 간 원치 않는 종속성을 만드는 테스트 간에 상태를 공유할 가능성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-241">Less chance of sharing state between tests which creates unwanted dependencies between them.</span></span>

<span data-ttu-id="f4879-242">단위 테스트 프레임워크에서 `Setup`은 단위 테스트 도구 모음 내의 각각의 모든 단위 테스트 전에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-242">In unit testing frameworks, `Setup` is called before each and every unit test within your test suite.</span></span> <span data-ttu-id="f4879-243">일부는 이를 유용한 도구로 볼 수 있지만, 일반적으로 테스트를 읽기에는 비대해지고 어렵워집니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-243">While some may see this as a useful tool, it generally ends up leading to bloated and hard to read tests.</span></span> <span data-ttu-id="f4879-244">각 테스트는 일반적으로 테스트를 시작하고 실행하기 위한 요구 사항이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-244">Each test will generally have different requirements in order to get the test up and running.</span></span> <span data-ttu-id="f4879-245">아쉽게도 `Setup`에서는 각 테스트에 대해 정확히 동일한 요구 사항을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-245">Unfortunately, `Setup` forces you to use the exact same requirements for each test.</span></span>

> [!NOTE] 
> <span data-ttu-id="f4879-246">xUnit은 버전 2.x에서 SetUp 및 TearDown을 모두 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-246">xUnit has removed both SetUp and TearDown as of version 2.x</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-247">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-247">Bad:</span></span>
[!code-csharp[BeforeSetup](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeSetup)]

```csharp
// more tests...
```

[!code-csharp[BeforeHelperMethod](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeHelperMethod)]

#### <a name="better"></a><span data-ttu-id="f4879-248">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-248">Better:</span></span>
[!code-csharp[AfterHelperMethod](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterHelperMethod)]

```csharp
// more tests...
```

[!code-csharp[AfterSetup](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterSetup)]

### <a name="avoid-multiple-asserts"></a><span data-ttu-id="f4879-249">다중 어설션 방지</span><span class="sxs-lookup"><span data-stu-id="f4879-249">Avoid multiple asserts</span></span>
<span data-ttu-id="f4879-250">테스트를 작성할 때 테스트당 하나의 Assert만 포함하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-250">When writing your tests, try to only include one Assert per test.</span></span> <span data-ttu-id="f4879-251">하나의 어설션만 사용하는 일반적인 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-251">Common approaches to using only one assert include:</span></span>
- <span data-ttu-id="f4879-252">각 어설션에 대한 별도의 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-252">Create a separate test for each assert.</span></span>
- <span data-ttu-id="f4879-253">매개 변수화된 테스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-253">Use parameterized tests.</span></span>

#### <a name="why"></a><span data-ttu-id="f4879-254">이유</span><span class="sxs-lookup"><span data-stu-id="f4879-254">Why?</span></span>
- <span data-ttu-id="f4879-255">하나의 Assert가 실패하면 후속 Assert는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-255">If one Assert fails, the subsequent Asserts will not be evaluated.</span></span>
- <span data-ttu-id="f4879-256">테스트에 여러 사례를 어설션하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-256">Ensures you are not asserting multiple cases in your tests.</span></span>
- <span data-ttu-id="f4879-257">테스트가 실패한 이유에 대한 전체 그림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-257">Gives you the entire picture as to why your tests are failing.</span></span> 

<span data-ttu-id="f4879-258">테스트 사례에 다중 어설션을 도입할 때 모든 어설션이 실행된다는 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-258">When introducing multiple asserts into a test case, it is not guaranteed that all of the asserts will be executed.</span></span> <span data-ttu-id="f4879-259">대부분의 단위 테스트 프레임워크에서 단위 테스트에 어설션이 실패하면 절차 테스트는 자동으로 실패한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-259">In most unit testing frameworks, once an assertion fails in a unit test, the proceeding tests are automatically considered to be failing.</span></span> <span data-ttu-id="f4879-260">실제로 작동하는 기능이 실패한 것으로 표시되므로 혼란스러울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-260">This can be confusing as functionality that is actually working, will be shown as failing.</span></span>

> [!NOTE]
> <span data-ttu-id="f4879-261">이 규칙에 대한 일반적인 예외는 개체에 대해 어설션할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-261">A common exception to this rule is when asserting against an object.</span></span> <span data-ttu-id="f4879-262">이 경우 일반적으로 각 속성에 대해 다중 어설션을 허용하여 개체가 예상되는 상태에 있는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-262">In this case, it is generally acceptable to have multiple asserts against each property to ensure the object is in the state that you expect it to be in.</span></span>

#### <a name="bad"></a><span data-ttu-id="f4879-263">Bad:</span><span class="sxs-lookup"><span data-stu-id="f4879-263">Bad:</span></span>
[!code-csharp[BeforeMultipleAsserts](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMultipleAsserts)]

#### <a name="better"></a><span data-ttu-id="f4879-264">Better:</span><span class="sxs-lookup"><span data-stu-id="f4879-264">Better:</span></span>
[!code-csharp[AfterMultipleAsserts](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterMultipleAsserts)]

### <a name="validate-private-methods-by-unit-testing-public-methods"></a><span data-ttu-id="f4879-265">공용 메서드를 테스트하여 전용 메서드 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f4879-265">Validate private methods by unit testing public methods</span></span>
<span data-ttu-id="f4879-266">대부분의 경우 전용 메서드를 테스트할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-266">In most cases, there should not be a need to test a private method.</span></span> <span data-ttu-id="f4879-267">전용 메서드는 구현 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-267">Private methods are an implementation detail.</span></span> <span data-ttu-id="f4879-268">전용 메서드는 절대 분리되어 존재하지 않는다고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-268">You can think of it this way: private methods never exist in isolation.</span></span> <span data-ttu-id="f4879-269">특정 시점에서는 구현의 일부로 전용 메서드를 호출하는 공용 연결 메서드가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-269">At some point, there is going to be a public facing method that calls the private method as part of its implementation.</span></span> <span data-ttu-id="f4879-270">주의해야 할 것은 사적인 것을 호출하는 공용 메서드의 최종 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-270">What you should care about is the end result of the public method that calls into the private one.</span></span> 

<span data-ttu-id="f4879-271">다음 경우를 참조</span><span class="sxs-lookup"><span data-stu-id="f4879-271">Consider the following case</span></span>

```csharp
public string ParseLogLine(string input)
{
    var sanitizedInput = trimInput(input);
    return sanitizedInput;
}

private string trimInput(string input)
{
    return input.Trim();
}
```

<span data-ttu-id="f4879-272">첫 번째 반응은 메서드가 예상대로 작동하는지 확인하려고 하기 때문에 `trimInput`에 대한 테스트를 작성하는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-272">Your first reaction may be to start writing a test for `trimInput` because you want to make sure that the method is working as expected.</span></span> <span data-ttu-id="f4879-273">그러나 `ParseLogLine`에서 예상하지 못한 방식으로 `sanitizedInput`을 조작하여 쓸모없는 `trimInput`에 대한 테스트를 렌더링하는 것은 전적으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-273">However, it is entirely possible that `ParseLogLine` manipulates `sanitizedInput` in such a way that you do not expect, rendering a test against `trimInput` useless.</span></span> 

<span data-ttu-id="f4879-274">실제 테스트는 공용 연결 메서드 `ParseLogLine`에 대해 수행되어야 합니다. 이는 최종적으로 주의를 기울여야 하는 것이기 때문이다.</span><span class="sxs-lookup"><span data-stu-id="f4879-274">The real test should be done against the public facing method `ParseLogLine` because that is what you should ultimately care about.</span></span> 

```csharp
public void ParseLogLine_ByDefault_ReturnsTrimmedResult()
{
    var parser = new Parser();

    var result = parser.ParseLogLine(" a ");

    Assert.Equals("a", result);
}
```

<span data-ttu-id="f4879-275">이 관점에서, 전용 메서드를 표시하는 경우 공용 메서드를 찾아 해당 메서드에 대해 테스트를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-275">With this viewpoint, if you see a private method, find the public method and write your tests against that method.</span></span> <span data-ttu-id="f4879-276">단지 전용 메서드가 예상된 결과를 반환한다고 해서 최종적으로 전용 메서드를 호출하는 시스템이 결과를 올바르게 사용하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-276">Just because a private method returns the expected result, does not mean the system that eventually calls the private method uses the result correctly.</span></span>

### <a name="stub-static-references"></a><span data-ttu-id="f4879-277">Stub 정적 참조</span><span class="sxs-lookup"><span data-stu-id="f4879-277">Stub static references</span></span>
<span data-ttu-id="f4879-278">단위 테스트의 원칙 중 하나는 테스트 중인 시스템을 완전히 제어해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-278">One of the principles of a unit test is that it must have full control of the system under test.</span></span> <span data-ttu-id="f4879-279">프로덕션 코드에 정적 참조(예: `DateTime.Now`)에 대한 호출을 포함하는 경우 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-279">This can be problematic when production code includes calls to static references (e.g. `DateTime.Now`).</span></span> <span data-ttu-id="f4879-280">다음 코드 참조</span><span class="sxs-lookup"><span data-stu-id="f4879-280">Consider the following code</span></span>

```csharp
public int GetDiscountedPrice(int price)
{
    if(DateTime.Now == DayOfWeek.Tuesday) 
    {
        return price / 2;
    }
    else 
    {
        return price;
    }
}
```

<span data-ttu-id="f4879-281">이 코드를 어떻게 단위 테스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f4879-281">How can this code possibly be unit tested?</span></span> <span data-ttu-id="f4879-282">다음과 같은 방법을 시도하는 경우</span><span class="sxs-lookup"><span data-stu-id="f4879-282">You may try an approach such as</span></span>

```csharp
public void GetDiscountedPrice_ByDefault_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(2, actual)
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(1, actual);
}
```

<span data-ttu-id="f4879-283">아쉽게도 테스트에 몇 가지 문제점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-283">Unfortunately, you will quickly realize that there are a couple problems with your tests.</span></span> 

- <span data-ttu-id="f4879-284">테스트 도구 모음을 화요일에 실행하면 두 번째 테스트는 통과하지만 첫 번째 테스트는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-284">If the test suite is run on a Tuesday, the second test will pass, but the first test will fail.</span></span>
- <span data-ttu-id="f4879-285">테스트 도구 모음을 다른 날에 실행하면 첫 번째 테스트는 통과하지만 두 번째 테스트는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-285">If the test suite is run on any other day, the first test will pass, but the second test will fail.</span></span>

<span data-ttu-id="f4879-286">이러한 문제를 해결하려면 프로덕션 코드에 *이음새*를 도입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-286">To solve these problems, you'll need to introduce a *seam* into your production code.</span></span> <span data-ttu-id="f4879-287">한 가지 방법은 인터페이스에서 제어해야 하는 코드를 래핑하여 프로덕션 코드가 해당 인터페이스에 종속되도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-287">One approach is to wrap the code that you need to control in an interface and have the production code depend on that interface.</span></span>

```csharp
public interface IDateTimeProvider
{
    DayOfWeek DayOfWeek();
}

public bool GetDiscountedPrice(int price, IDateTimeProvider dateTimeProvider)
{
    if(dateTimeProvider.DayOfWeek() == DayOfWeek.Tuesday) 
    {
        return price / 2;
    }
    else 
    {
        return price;
    }
}
```

<span data-ttu-id="f4879-288">이제 테스트 도구 모음이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-288">Your test suite now becomes</span></span>

```csharp
public void GetDiscountedPrice_ByDefault_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Monday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(2, actual);
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Tuesday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(1, actual);
}
```

<span data-ttu-id="f4879-289">이제 테스트 도구 모음은 `DateTime.Now`에 대한 완전한 제어권을 가지며 메서드를 호출할 때 모든 값을 스텁할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4879-289">Now the test suite has full control over `DateTime.Now` and can stub any value when calling into the method.</span></span>