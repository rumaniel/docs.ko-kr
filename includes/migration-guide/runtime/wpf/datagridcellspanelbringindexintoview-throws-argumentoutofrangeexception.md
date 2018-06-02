### <a name="datagridcellspanelbringindexintoview-throws-argumentoutofrangeexception"></a><span data-ttu-id="9b0b2-101">DataGridCellsPanel.BringIndexIntoView가 ArgumentOutOfRangeException을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0b2-101">DataGridCellsPanel.BringIndexIntoView throws ArgumentOutOfRangeException</span></span>

|   |   |
|---|---|
|<span data-ttu-id="9b0b2-102">설명</span><span class="sxs-lookup"><span data-stu-id="9b0b2-102">Details</span></span>|<span data-ttu-id="9b0b2-103"><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)>는 열 가상화가 활성화되었지만 열 너비가 아직 결정되지 않았을 때 비동기적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0b2-103"><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)> will work asynchronously when column virtualization is enabled but the column widths have not yet been determined.</span></span>  <span data-ttu-id="9b0b2-104">비동기 작업이 실행되기 전에 열이 제거되면 <xref:System.ArgumentOutOfRangeException?displayProperty=name>이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0b2-104">If columns are removed before the asynchronous work happens, an <xref:System.ArgumentOutOfRangeException?displayProperty=name> can occur.</span></span>|
|<span data-ttu-id="9b0b2-105">제안 해결 방법</span><span class="sxs-lookup"><span data-stu-id="9b0b2-105">Suggestion</span></span>|<span data-ttu-id="9b0b2-106">다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="9b0b2-106">Any one of the following:</span></span><ol><li><span data-ttu-id="9b0b2-107">NET Framework 4.7로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0b2-107">Upgrade to .NET Framework 4.7.</span></span></li><li><span data-ttu-id="9b0b2-108">.NET Framework 4.6.2에 대한 최신 서비스 패치를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0b2-108">Install the latest servicing patch for .NET Framework 4.6.2.</span></span></li><li><span data-ttu-id="9b0b2-109"><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)>에 대한 비동기 응답이 완료될 때까지 열이 제거되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0b2-109">Avoid removing columns until the asynchronous response to <xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)> has completed.</span></span></li></ol>|
|<span data-ttu-id="9b0b2-110">범위</span><span class="sxs-lookup"><span data-stu-id="9b0b2-110">Scope</span></span>|<span data-ttu-id="9b0b2-111">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="9b0b2-111">Edge</span></span>|
|<span data-ttu-id="9b0b2-112">버전</span><span class="sxs-lookup"><span data-stu-id="9b0b2-112">Version</span></span>|<span data-ttu-id="9b0b2-113">4.6.2</span><span class="sxs-lookup"><span data-stu-id="9b0b2-113">4.6.2</span></span>|
|<span data-ttu-id="9b0b2-114">형식</span><span class="sxs-lookup"><span data-stu-id="9b0b2-114">Type</span></span>|<span data-ttu-id="9b0b2-115">런타임</span><span class="sxs-lookup"><span data-stu-id="9b0b2-115">Runtime</span></span>|
|<span data-ttu-id="9b0b2-116">영향을 받는 API</span><span class="sxs-lookup"><span data-stu-id="9b0b2-116">Affected APIs</span></span>|<ul><li><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object,System.Windows.Controls.DataGridColumn)?displayProperty=nameWithType></li></ul>|
