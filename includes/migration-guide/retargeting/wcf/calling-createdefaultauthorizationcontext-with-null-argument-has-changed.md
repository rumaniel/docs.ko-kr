### <a name="calling-createdefaultauthorizationcontext-with-a-null-argument-has-changed"></a><span data-ttu-id="9c80c-101">Null 인수를 사용한 CreateDefaultAuthorizationContext 호출이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c80c-101">Calling CreateDefaultAuthorizationContext with a null argument has changed</span></span>

|   |   |
|---|---|
|<span data-ttu-id="9c80c-102">설명</span><span class="sxs-lookup"><span data-stu-id="9c80c-102">Details</span></span>|<span data-ttu-id="9c80c-103">Null authorizationPolicies를 사용하는 <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=name>에 대한 호출로 반환된 <xref:System.IdentityModel.Policy.AuthorizationContext?displayProperty=name>의 구현이 .NET Framework 4.6에서 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c80c-103">The implementation of the <xref:System.IdentityModel.Policy.AuthorizationContext?displayProperty=name> returned by a call to the <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=name> with a null authorizationPolicies argument has changed its implementation in the .NET Framework 4.6.</span></span>|
|<span data-ttu-id="9c80c-104">제안 해결 방법</span><span class="sxs-lookup"><span data-stu-id="9c80c-104">Suggestion</span></span>|<span data-ttu-id="9c80c-105">드문 경우이지만 사용자 지정 인증을 사용하는 WCF 앱은 다르게 동작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c80c-105">In rare cases, WCF apps that use custom authentication may see behavioral differences.</span></span> <span data-ttu-id="9c80c-106">이러한 경우 두 가지 방법 중 하나로 이전 동작을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c80c-106">In such cases, the previous behavior can be restored in either of two ways:</span></span><ol><li><span data-ttu-id="9c80c-107">4.6 이전 버전의 .NET Framework를 대상으로 사용하도록 앱을 다시 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="9c80c-107">Recompile your app to target an earlier version of the .NET Framework than 4.6.</span></span> <span data-ttu-id="9c80c-108">IIS 호스트 서비스의 경우 .NET Framework의 이전 버전을 대상으로 하려면 &lt;httpRuntime targetFramework =&quot;x.x&quot; /&gt; 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c80c-108">For IIS-hosted services, use the &lt;httpRuntime targetFramework=&quot;x.x&quot; /&gt; element to target an earlier version of the .NET Framework.</span></span></li><li><span data-ttu-id="9c80c-109">다음 줄을 app.config 파일의 <code>&lt;appSettings&gt;</code> 섹션에 추가합니다. <code>&lt;add key=&quot;appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext&quot; value=&quot;true&quot; /&gt;</code></span><span class="sxs-lookup"><span data-stu-id="9c80c-109">Add the following line to the <code>&lt;appSettings&gt;</code> section of your app.config file: <code>&lt;add key=&quot;appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext&quot; value=&quot;true&quot; /&gt;</code></span></span></li></ol>|
|<span data-ttu-id="9c80c-110">범위</span><span class="sxs-lookup"><span data-stu-id="9c80c-110">Scope</span></span>|<span data-ttu-id="9c80c-111">부</span><span class="sxs-lookup"><span data-stu-id="9c80c-111">Minor</span></span>|
|<span data-ttu-id="9c80c-112">버전</span><span class="sxs-lookup"><span data-stu-id="9c80c-112">Version</span></span>|<span data-ttu-id="9c80c-113">4.6</span><span class="sxs-lookup"><span data-stu-id="9c80c-113">4.6</span></span>|
|<span data-ttu-id="9c80c-114">형식</span><span class="sxs-lookup"><span data-stu-id="9c80c-114">Type</span></span>|<span data-ttu-id="9c80c-115">대상 변경</span><span class="sxs-lookup"><span data-stu-id="9c80c-115">Retargeting</span></span>|
|<span data-ttu-id="9c80c-116">영향을 받는 API</span><span class="sxs-lookup"><span data-stu-id="9c80c-116">Affected APIs</span></span>|<ul><li><xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=nameWithType></li></ul>|
