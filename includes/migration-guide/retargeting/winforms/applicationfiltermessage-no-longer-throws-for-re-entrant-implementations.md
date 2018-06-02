### <a name="applicationfiltermessage-no-longer-throws-for-re-entrant-implementations-of-imessagefilterprefiltermessage"></a><span data-ttu-id="ffcec-101">Application.FilterMessage는 IMessageFilter.PreFilterMessage의 재진입 구현에 대해 더 이상 throw하지 않음</span><span class="sxs-lookup"><span data-stu-id="ffcec-101">Application.FilterMessage no longer throws for re-entrant implementations of IMessageFilter.PreFilterMessage</span></span>

|   |   |
|---|---|
|<span data-ttu-id="ffcec-102">설명</span><span class="sxs-lookup"><span data-stu-id="ffcec-102">Details</span></span>|<span data-ttu-id="ffcec-103">.NET Framework 4.6.1에 앞서 <xref:System.Windows.Forms.Application.AddMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name> 또는 <xref:System.Windows.Forms.Application.RemoveMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name>라고 하는 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)>를 사용하여 <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)>을 호출하면(<xref:System.Windows.Forms.Application.DoEvents>도 호출하면서) <xref:System.IndexOutOfRangeException?displayProperty=name>을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ffcec-103">Prior to the .NET Framework 4.6.1, calling <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)> with an <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> which called <xref:System.Windows.Forms.Application.AddMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name> or <xref:System.Windows.Forms.Application.RemoveMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name> (while also calling <xref:System.Windows.Forms.Application.DoEvents>) would cause an <xref:System.IndexOutOfRangeException?displayProperty=name>.</span></span><p/><span data-ttu-id="ffcec-104">4.6.1.NET Framework를 대상으로 하는 응용 프로그램부터 이 예외는 더 이상 throw되지 않으며 위에서 설명한 것처럼 재진입 필터가 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcec-104">Beginning with applications targeting the .NET Framework 4.6.1, this exception is no longer thrown, and re-entrant filters as described above may be used.</span></span>|
|<span data-ttu-id="ffcec-105">제안 해결 방법</span><span class="sxs-lookup"><span data-stu-id="ffcec-105">Suggestion</span></span>|<span data-ttu-id="ffcec-106">위에서 설명한 재진입 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> 동작 때문에 <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)>가 더 이상 throw되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcec-106">Be aware that <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)> will no longer throw for the re-entrant <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> behavior described above.</span></span> <span data-ttu-id="ffcec-107">이는 .NET Framework 4.6.1을 대상으로 하는 응용 프로그램에만 영향을 줍니다. .NET Framework 4.6.1을 대상으로 하는 응용 프로그램은 [DontSupportReentrantFilterMessage](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md#mitigation) 호환성 스위치를 사용하여 이 변경을 옵트아웃(또는 이전 프레임워크를 대상으로 하는 응용 프로그램은 옵트인)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcec-107">This only affects applications targeting the .NET Framework 4.6.1.Apps targeting the .NET Framework 4.6.1 can opt out of this change (or apps targeting older Frameworks may opt in) by using the [DontSupportReentrantFilterMessage](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md#mitigation) compatibility switch.</span></span>|
|<span data-ttu-id="ffcec-108">범위</span><span class="sxs-lookup"><span data-stu-id="ffcec-108">Scope</span></span>|<span data-ttu-id="ffcec-109">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="ffcec-109">Edge</span></span>|
|<span data-ttu-id="ffcec-110">버전</span><span class="sxs-lookup"><span data-stu-id="ffcec-110">Version</span></span>|<span data-ttu-id="ffcec-111">4.6.1</span><span class="sxs-lookup"><span data-stu-id="ffcec-111">4.6.1</span></span>|
|<span data-ttu-id="ffcec-112">형식</span><span class="sxs-lookup"><span data-stu-id="ffcec-112">Type</span></span>|<span data-ttu-id="ffcec-113">대상 변경</span><span class="sxs-lookup"><span data-stu-id="ffcec-113">Retargeting</span></span>|
|<span data-ttu-id="ffcec-114">영향을 받는 API</span><span class="sxs-lookup"><span data-stu-id="ffcec-114">Affected APIs</span></span>|<ul><li><xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)?displayProperty=nameWithType></li></ul>|
