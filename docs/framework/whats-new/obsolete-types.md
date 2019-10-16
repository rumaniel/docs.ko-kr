---
title: .NET Framework에서 사용되지 않는 형식
ms.date: 03/30/2017
helpviewer_keywords:
- .NET Framework 4.5, obsolete types
- types, obsolete in .NET Framework 4.5
- obsolete types [.NET Framework]
ms.assetid: e636d024-0fac-45eb-b721-25a8c0ceca8f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d8af0f32c676f4438334f7c64b771e237db90dd3
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663850"
---
# <a name="obsolete-types-in-the-net-framework"></a>.NET Framework에서 사용되지 않는 형식

<a name="introduction"></a> 이 문서의 표에는 .NET Framework 4.5 및 .NET Framework 4.6에서 사용되지 않은 형식이 어셈블리별로 나열되어 있습니다. 사용하지 않는 형식과 각 어셈블리에서 권장되는 대체 형식의 목록을 보려면 다음 링크를 사용합니다. 이러한 형식은 사용되지 않으므로 해당 형식의 멤버도 모두 사용되지 않습니다. .NET Framework 클래스 라이브러리의 사용되지 않는 멤버에 대한 추가 목록은 [사용되지 않는 멤버](obsolete-members.md)를 참조하십시오.

- [시스템 어셈블리에서 사용되지 않는 형식](#obsolete_types_in_system_assemblies)

  - [mscorlib.dll](#mscorlib)

  - [System.Core.dll](#Core)

  - [System.Data.dll](#data)

  - [System.Data.OracleClient.dll](#oracleclient)

  - [System.Design.dll](#design)

  - [System.dll](#system)

  - [System.EnterpriseServices.dll](#enterpriseservices)

  - [System.Net.dll](#net)

  - [System.ServiceModel.dll](#servicemodel)

  - [System.Web.dll](#web)

  - [System.Web.Mobile.dll](#mobile)

  - [System.Workflow.Activities.dll](#workflow_activities)

  - [System.Workflow.ComponentModel.dll](#workflow_componentmodel)

  - [System.Workflow.Runtime.dll](#workflow_runtime)

  - [System.WorkflowServices.dll](#workflowservices)

  - [System.Xaml.dll](#xaml)

  - [System.Xml.dll](#xml)

  - [WindowsBase.dll](#WindowsBase)

- [Microsoft 어셈블리에서 사용되지 않는 형식](#obsolete_types_in_microsoft_assemblies)

  - [IEHost.dll 및 IEExec.exe](#IEHost)

  - [Microsoft.Build.Engine.dll](#Engine)

  - [Microsoft.JScript.dll](#jscript)

  - [Microsoft.VisualBasic.Compatibility.dll](#VBCompat)

  - [Microsoft.VisualBasic.Compatibility.Data.dll](#VBCompatData)

  - [Microsoft.VisualC.dll](#visualc)

<a name="obsolete_types_in_system_assemblies"></a>

## <a name="obsolete-types-in-system-assemblies"></a>시스템 어셈블리에서 사용되지 않는 형식

다음 표에서는 시스템 어셈블리에서 사용되지 않는 것으로 선언된 형식을 보여 줍니다. 이러한 어셈블리는 .NET Framework를 대상으로 하는 일반\-용도의 애플리케이션 개발에 사용됩니다.

<a name="mscorlib"></a>

### <a name="assembly-mscorlibdll"></a>어셈블리: mscorlib.dll

|Type|Message|
|----------|-------------|
|<xref:System.ExecutionEngineException?displayProperty=nameWithType>|이 형식은 이전에 런타임에서 지정되지 않은 심각한 오류를 나타냈습니다. 이 예외는 런타임에서 더 이상 발생하지 않으므로 이 형식은 사용되지 않습니다.|
|<xref:System.Collections.CaseInsensitiveHashCodeProvider?displayProperty=nameWithType>|대신 <xref:System.StringComparer?displayProperty=nameWithType>를 사용하십시오.|
|<xref:System.Collections.IHashCodeProvider?displayProperty=nameWithType>|대신 <xref:System.Collections.IEqualityComparer?displayProperty=nameWithType>를 사용하십시오.|
|<xref:System.Configuration.Assemblies.AssemblyHash?displayProperty=nameWithType>|<xref:System.Configuration.Assemblies.AssemblyHash> 클래스는 사용되지 않습니다.|
|<xref:System.Diagnostics.Contracts.Internal.ContractHelper?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음 System.Runtime.CompilerServices 네임스페이스의 <xref:System.Runtime.CompilerServices.ContractHelper?displayProperty=nameWithType> 클래스를 대신 사용합니다.|
|<xref:System.Reflection.Emit.UnmanagedMarshal?displayProperty=nameWithType>|대체 API를 사용할 수 있습니다. 대신 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> 사용자 지정 특성을 내보냅니다.|
|<xref:System.Runtime.InteropServices.BIND_OPTS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.BIND_OPTS?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.BINDPTR?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.BINDPTR?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.CALLCONV?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.CALLCONV?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.CONNECTDATA?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.CONNECTDATA?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.DESCKIND?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.DESCKIND?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.DISPPARAMS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.DISPPARAMS?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.ELEMDESC?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.ELEMDESC?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.EXCEPINFO?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.EXCEPINFO?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.FILETIME?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.FILETIME?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.FUNCDESC?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.FUNCDESC?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.FUNCFLAGS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.FUNCFLAGS?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.FUNCKIND?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.FUNCKIND?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.IDispatchImplAttribute?displayProperty=nameWithType>|이 특성은 사용되지 않으며 이후 버전에서 제거됩니다.|
|<xref:System.Runtime.InteropServices.IDispatchImplType?displayProperty=nameWithType>|<xref:System.Runtime.InteropServices.IDispatchImplAttribute?displayProperty=nameWithType>는 사용되지 않습니다.|
|<xref:System.Runtime.InteropServices.IDLDESC?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IDLDESC?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.IDLFLAG?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IDLFLAG?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.IMPLTYPEFLAGS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IMPLTYPEFLAGS?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.INVOKEKIND?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.INVOKEKIND?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.LIBFLAGS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.LIBFLAGS?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.PARAMDESC?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.PARAMDESC?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.PARAMFLAG?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.PARAMFLAG?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.SetWin32ContextInIDispatchAttribute?displayProperty=nameWithType>|이 특성은 사용되지 않습니다. 애플리케이션 도메인에서는 더 이상 IDispatch 호출의 활성화 컨텍스트 경계를 따르지 않습니다.|
|<xref:System.Runtime.InteropServices.STATSTG?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.STATSTG?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.SYSKIND?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.SYSKIND?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.TYPEATTR?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.TYPEATTR?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.TYPEDESC?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.TYPEDESC?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.TYPEFLAGS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.TYPEFLAGS?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.TYPEKIND?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.TYPEKIND?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.TYPELIBATTR?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.TYPELIBATTR?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIBindCtx?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IBindCtx?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIConnectionPoint?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIConnectionPointContainer?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIEnumConnectionPoints?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IEnumConnectionPoints?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIEnumConnections?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IEnumConnections?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIEnumMoniker?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IEnumMoniker?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIEnumString?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IEnumString?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIEnumVARIANT?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIMoniker?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IMoniker?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIPersistFile?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IPersistFile?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIRunningObjectTable?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IRunningObjectTable?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMIStream?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.IStream?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMITypeComp?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.ITypeComp?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMITypeInfo?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.UCOMITypeLib?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.ITypeLib?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.VARDESC?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.VARDESC?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Runtime.InteropServices.VARFLAGS?displayProperty=nameWithType>|대신 <xref:System.Runtime.InteropServices.ComTypes.VARFLAGS?displayProperty=nameWithType> 를 사용하세요.|
|<xref:System.Security.SecurityCriticalScope?displayProperty=nameWithType>|<xref:System.Security.SecurityCriticalScope>는 .NET 2.0 투명도 호환성을 위한 용도로만 사용됩니다.|
|<xref:System.Security.SecurityTreatAsSafeAttribute?displayProperty=nameWithType>|<xref:System.Security.SecurityTreatAsSafeAttribute>는 .NET 2.0 투명도 호환성을 위한 용도로만 사용됩니다. 대신 <xref:System.Security.SecuritySafeCriticalAttribute?displayProperty=nameWithType>를 사용하십시오.|
|<xref:System.Security.Policy.FirstMatchCodeGroup?displayProperty=nameWithType>|이 형식은 사용되지 않으며 .NET Framework의 이후 릴리스에서 제거됩니다.|
|<xref:System.Security.Policy.PermissionRequestEvidence?displayProperty=nameWithType>|어셈블리 수준의 선언적 보안은 사용되지 않으며 더 이상 기본적으로 CLR에서 적용되지 않습니다.|
|<xref:System.Security.Policy.UnionCodeGroup?displayProperty=nameWithType>|이 형식은 사용되지 않으며 .NET Framework의 이후 릴리스에서 제거됩니다.|

[맨 위로 이동](#introduction)

<a name="Core"></a>

### <a name="assembly-systemcoredll"></a>어셈블리: System.Core.dll

|Type|Message|
|----------|-------------|
|<xref:System.Runtime.CompilerServices.ExecutionScope?displayProperty=nameWithType>|이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 형식은 사용하지 마십시오.|

[맨 위로 이동](#introduction)

<a name="data"></a>

### <a name="assembly-systemdatadll"></a>어셈블리: System.Data.dll

|Type|Message|
|----------|-------------|
|<xref:System.Data.DataSysDescriptionAttribute?displayProperty=nameWithType>|<xref:System.Data.DataSysDescriptionAttribute>는 사용되지 않습니다.|
|<xref:System.Data.PropertyAttributes?displayProperty=nameWithType>|<xref:System.Data.PropertyAttributes>는 사용되지 않습니다.|
|<xref:System.Data.TypedDataSetGenerator?displayProperty=nameWithType>|<xref:System.Data.TypedDataSetGenerator> 클래스는 이후 릴리스에서 제거됩니다. System.Design.dll의 <xref:System.Data.Design.TypedDataSetGenerator?displayProperty=nameWithType>를 사용하십시오.|
|<xref:System.Xml.XmlDataDocument?displayProperty=nameWithType>|<xref:System.Xml.XmlDataDocument> 클래스는 이후 릴리스에서 제거됩니다.|

[맨 위로 이동](#introduction)

<a name="oracleclient"></a>

### <a name="assembly-systemdataoracleclientdll"></a>어셈블리: System.Data.OracleClient.dll

|Type|Message|
|----------|-------------|
|<xref:System.Data.OracleClient.OracleClientFactory?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OracleClientFactory>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OracleCommand?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OracleCommand>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OracleCommandBuilder?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OracleCommandBuilder>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OracleConnection?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OracleConnection>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OracleDataAdapter>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OraclePermission?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OraclePermission>는 사용되지 않습니다.|
|<xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=nameWithType>|<xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=nameWithType>는 사용되지 않습니다.|

[맨 위로 이동](#introduction)

<a name="design"></a>

### <a name="assembly-systemdesigndll"></a>어셈블리: System.Design.dll

|Type|Message|
|----------|-------------|
|<xref:System.ComponentModel.Design.LocalizationExtenderProvider?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다. 대신 <xref:System.ComponentModel.Design.Serialization.CodeDomLocalizationProvider?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Web.UI.Design.DataBindingCollectionConverter?displayProperty=nameWithType>|DataBindings 편집은 속성 표가 아닌 <xref:System.ComponentModel.Design.DesignerActionList?displayProperty=nameWithType>를 통해 시작되므로 이 형식은 사용하지 않는 것이 좋습니다.|
|<xref:System.Web.UI.Design.DataBindingCollectionEditor?displayProperty=nameWithType>|DataBindings 편집은 속성 표가 아닌 <xref:System.ComponentModel.Design.DesignerActionList?displayProperty=nameWithType>를 통해 시작되므로 이 형식은 사용하지 않는 것이 좋습니다.|
|<xref:System.Web.UI.Design.IControlDesignerBehavior?displayProperty=nameWithType>|<xref:System.Web.UI.Design.IControlDesignerTag?displayProperty=nameWithType> 및 <xref:System.Web.UI.Design.IControlDesignerView?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.UI.Design.IHtmlControlDesignerBehavior?displayProperty=nameWithType>|<xref:System.Web.UI.Design.IControlDesignerTag?displayProperty=nameWithType> 및 <xref:System.Web.UI.Design.IControlDesignerView?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.UI.Design.ITemplateEditingFrame?displayProperty=nameWithType>|템플릿 편집은 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType>에서 처리되므로 이 형식은 사용하지 않는 것이 좋습니다. 템플릿 편집을 지원하려면 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=nameWithType> 속성에서 템플릿 데이터를 노출하고 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=nameWithType>를 호출하십시오.|
|<xref:System.Web.UI.Design.IWebFormReferenceManager?displayProperty=nameWithType>|<xref:System.Web.UI.Design.WebFormsReferenceManager?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다. <xref:System.Web.UI.Design.WebFormsReferenceManager>는 기능을 추가로 포함하며 보다 높은 확장성을 허용합니다. <xref:System.Web.UI.Design.WebFormsReferenceManager>를 가져오려면 `RootDesigner.ReferenceManager`의 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType> 속성을 사용하십시오.|
|<xref:System.Web.UI.Design.IWebFormsDocumentService?displayProperty=nameWithType>|<xref:System.Web.UI.Design.WebFormsRootDesigner?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다. <xref:System.Web.UI.Design.WebFormsRootDesigner>는 기능을 추가로 포함하며 보다 높은 확장성을 허용합니다. <xref:System.Web.UI.Design.WebFormsRootDesigner>를 가져오려면 <xref:System.Web.UI.Design.ControlDesigner.RootDesigner%2A>의 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType> 속성을 사용하십시오.|
|<xref:System.Web.UI.Design.ITemplateEditingService?displayProperty=nameWithType>|템플릿 편집은 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType>에서 처리되므로 이 형식은 사용하지 않는 것이 좋습니다. 템플릿 편집을 지원하려면 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=nameWithType> 속성에서 템플릿 데이터를 노출하고 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=nameWithType>를 호출하십시오.|
|<xref:System.Web.UI.Design.ReadWriteControlDesigner?displayProperty=nameWithType>|콘텐츠 편집에 <xref:System.Web.UI.Design.ContainerControlDesigner?displayProperty=nameWithType>을 사용하는 <xref:System.Web.UI.Design.EditableDesignerRegion?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다. 디자이너 영역을 사용하면 편집 중인 콘텐츠를 보다 효율적으로 제어할 수 있습니다.|
|<xref:System.Web.UI.Design.TemplateEditingService?displayProperty=nameWithType>|템플릿 편집은 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType>에서 처리되므로 이 형식은 사용하지 않는 것이 좋습니다. 템플릿 편집을 지원하려면 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=nameWithType> 속성에서 템플릿 데이터를 노출하고 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=nameWithType>를 호출하십시오.|
|<xref:System.Web.UI.Design.TemplateEditingVerb?displayProperty=nameWithType>|템플릿 편집은 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType>에서 처리되므로 이 형식은 사용하지 않는 것이 좋습니다. 템플릿 편집을 지원하려면 <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=nameWithType> 속성에서 템플릿 데이터를 노출하고 <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=nameWithType>를 호출하십시오.|
|<xref:System.Web.UI.Design.WebControls.CalendarAutoFormatDialog?displayProperty=nameWithType>|자동 서식 대화 상자는 디자이너 호스트를 통해 시작되므로 이 형식은 사용하지 않는 것이 좋습니다. 사용 가능한 자동 서식 목록은 <xref:System.Web.UI.Design.ControlDesigner?displayProperty=nameWithType> 속성의 <xref:System.Web.UI.Design.ControlDesigner.AutoFormats%2A?displayProperty=nameWithType>에서 노출됩니다.|
|<xref:System.Web.UI.Design.WebControls.PanelDesigner?displayProperty=nameWithType>|콘텐츠 편집에 <xref:System.Web.UI.Design.WebControls.PanelContainerDesigner?displayProperty=nameWithType>을 사용하는 <xref:System.Web.UI.Design.EditableDesignerRegion?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다. 디자이너 영역을 사용하면 편집 중인 콘텐츠를 보다 효율적으로 제어할 수 있습니다.|

[맨 위로 이동](#introduction)

<a name="system"></a>

### <a name="assembly-systemdll"></a>어셈블리: System.dll

|Type|Message|
|----------|-------------|
|<xref:System.ComponentModel.IComNativeDescriptorHandler?displayProperty=nameWithType>|이 인터페이스는 사용되지 않습니다. <xref:System.ComponentModel.TypeDescriptionProvider?displayProperty=nameWithType> 형식을 처리하려면 대신 <xref:System.ComponentModel.TypeDescriptor.ComObjectType%2A?displayProperty=nameWithType>를 추가합니다.|
|<xref:System.ComponentModel.RecommendedAsConfigurableAttribute?displayProperty=nameWithType>|새 설정 모델을 사용하려면 대신 <xref:System.ComponentModel.SettingsBindableAttribute?displayProperty=nameWithType>를 사용하십시오.|
|<xref:System.ComponentModel.Design.Serialization.RootDesignerSerializerAttribute?displayProperty=nameWithType>|이 특성은 사용되지 않습니다. 대신 <xref:System.ComponentModel.Design.Serialization.DesignerSerializerAttribute?displayProperty=nameWithType>를 사용하세요.|
|<xref:System.Diagnostics.DiagnosticsConfigurationHandler?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다.|
|<xref:System.Diagnostics.PerformanceCounterManager?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다. 대신 <xref:System.Diagnostics.PerformanceCounter?displayProperty=nameWithType> 클래스를 통해 성능 카운터를 사용하십시오.|
|<xref:System.Net.GlobalProxySelection?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다. 전역 기본 프록시를 액세스 및 설정하려면 대신 <xref:System.Net.WebRequest.DefaultWebProxy%2A?displayProperty=nameWithType>를 사용하십시오. <xref:System.Net.GlobalProxySelection.GetEmptyWebProxy%2A?displayProperty=nameWithType> 대신 'null'을 사용하십시오.|
|<xref:System.Net.Sockets.SocketClientAccessPolicyProtocol?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|

[맨 위로 이동](#introduction)

<a name="enterpriseservices"></a>

### <a name="assembly-systementerpriseservicesdll"></a>어셈블리: System.EnterpriseServices.dll

|Type|Message|
|----------|-------------|
|<xref:System.EnterpriseServices.RegistrationHelperTx?displayProperty=nameWithType>|<xref:System.EnterpriseServices.RegistrationHelperTx> 클래스는 사용되지 않습니다.|

[맨 위로 이동](#introduction)

<a name="net"></a>

### <a name="assembly-systemnetdll"></a>어셈블리: System.Net.dll

|Type|Message|
|----------|-------------|
|<xref:System.Net.INetworkProgress?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.IUnsafeWebRequestCreate?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.NetworkProgressChangedEventArgs?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.UiSynchronizationContext?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.Sockets.HttpPolicyDownloaderProtocol?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.Sockets.SecurityCriticalAction?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.Sockets.SocketPolicy?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.Sockets.UdpAnySourceMulticastClient?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Net.Sockets.UdpSingleSourceMulticastClient?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|

[맨 위로 이동](#introduction)

<a name="servicemodel"></a>

### <a name="assembly-systemservicemodeldll"></a>어셈블리: System.ServiceModel.dll

|Type|Message|
|----------|-------------|
|<xref:System.ServiceModel.NetPeerTcpBinding?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|
|<xref:System.ServiceModel.Channels.HttpCookieContainerBindingElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식은 사용되지 않습니다. Http <xref:System.Net.CookieContainer>를 사용하려면 Http 바인딩 또는 `AllowCookies`의 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 속성을 사용합니다.|
|<xref:System.ServiceModel.Channels.PeerCustomResolverBindingElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|
|<xref:System.ServiceModel.Channels.PeerTransportBindingElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|
|<xref:System.ServiceModel.Configuration.NetPeerTcpBindingCollectionElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|
|<xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|
|<xref:System.ServiceModel.Configuration.PeerTransportElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|
|<xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 피어 채널 기능은 사용되지 않으며 향후 제거될 예정입니다.|

[맨 위로 이동](#introduction)

<a name="web"></a>

### <a name="assembly-systemwebdll"></a>어셈블리: System.Web.dll

|Type|Message|
|----------|-------------|
|<xref:System.Web.Configuration.PassportAuthentication?displayProperty=nameWithType>|이 형식은 사용되지 않습니다. Passport 인증 제품은 더 이상 지원되지 않으며 [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=733413)로 대체되었습니다.|
|<xref:System.Web.Mail.MailAttachment?displayProperty=nameWithType>|<xref:System.Net.Mail.Attachment?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.Mail.MailEncoding?displayProperty=nameWithType>|<xref:System.Net.Mime.TransferEncoding?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.Mail.MailFormat?displayProperty=nameWithType>|<xref:System.Net.Mail.MailMessage.IsBodyHtml%2A?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.Mail.MailMessage?displayProperty=nameWithType>|<xref:System.Net.Mail.MailMessage?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.Mail.MailPriority?displayProperty=nameWithType>|<xref:System.Net.Mail.MailPriority?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.Mail.SmtpMail?displayProperty=nameWithType>|<xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|
|<xref:System.Web.Security.PassportAuthenticationEventArgs?displayProperty=nameWithType>|이 형식은 사용되지 않습니다. Passport 인증 제품은 더 이상 지원되지 않으며 [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=733413)로 대체되었습니다.|
|<xref:System.Web.Security.PassportAuthenticationEventHandler?displayProperty=nameWithType>|이 형식은 사용되지 않습니다. Passport 인증 제품은 더 이상 지원되지 않으며 [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=733413)로 대체되었습니다.|
|<xref:System.Web.Security.PassportAuthenticationModule?displayProperty=nameWithType>|이 형식은 사용되지 않습니다. Passport 인증 제품은 더 이상 지원되지 않으며 [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=733413)로 대체되었습니다.|
|<xref:System.Web.Security.PassportIdentity?displayProperty=nameWithType>|이 형식은 사용되지 않습니다. Passport 인증 제품은 더 이상 지원되지 않으며 [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=733413)로 대체되었습니다.|
|<xref:System.Web.Security.PassportPrincipal?displayProperty=nameWithType>|이 형식은 사용되지 않습니다. Passport 인증 제품은 더 이상 지원되지 않으며 [Microsoft Account](https://go.microsoft.com/fwlink/?LinkId=733413)로 대체되었습니다.|
|<xref:System.Web.UI.ObjectConverter?displayProperty=nameWithType>|<xref:System.Convert?displayProperty=nameWithType> 및 <xref:System.String.Format%2A?displayProperty=nameWithType>를 대신 사용하는 것이 좋습니다.|

[맨 위로 이동](#introduction)

<a name="mobile"></a>

### <a name="assembly-systemwebmobiledll"></a>어셈블리: System.Web.Mobile.dll

|Type|Message|
|----------|-------------|
|<xref:System.Web.Mobile.CookielessData?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.DeviceFilterElement?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.DeviceFilterElementCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.DeviceFiltersSection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.ErrorHandlerModule?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.MobileCapabilities?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.MobileDeviceCapabilitiesSectionHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.MobileErrorInfo?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.Mobile.MobileFormsAuthentication?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.Design.MobileControls.IMobileDesigner?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.Design.MobileControls.IMobileWebFormServices?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.Design.MobileControls.MobileResource?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.Design.MobileControls.Converters.DataFieldConverter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.Design.MobileControls.Converters.DataMemberConverter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.AdRotator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Alignment?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ArrayListCollectionBase?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.BaseValidator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.BooleanOption?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Calendar?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Command?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.CommandFormat?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.CompareValidator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Constants?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ControlElement?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ControlElementCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ControlPager?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.CustomValidator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DesignerAdapterAttribute?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceElement?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceElementCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceOverridableAttribute?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecific?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoice?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceTemplateBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceTemplateContainer?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.DeviceSpecificControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ErrorFormatterPage?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.FontInfo?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.FontSize?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Form?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.FormControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.FormMethod?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.IControlAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Image?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.IObjectListFieldCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.IPageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ItemPager?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ITemplateable?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Label?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Link?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.List?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListCommandEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListCommandEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListDataBindEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListDataBindEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListDecoration?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ListSelectType?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.LiteralLink?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.LiteralText?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.LiteralTextContainerControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.LiteralTextControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.LoadItemsEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.LoadItemsEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileControl?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileControlsSection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileControlsSectionHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileListItem?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileListItemCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileListItemType?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobilePage?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileTypeNameConverter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.MobileUserControl?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectList?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListCommand?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListCommandCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListCommandEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListCommandEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListDataBindEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListDataBindEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListField?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListFieldCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListItem?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListItemCollection?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListSelectEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListSelectEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListShowCommandsEventArgs?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListShowCommandsEventHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListTitleAttribute?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ObjectListViewMode?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.PagedControl?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.PagerStyle?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Panel?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.PanelControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.PersistNameAttribute?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.PhoneCall?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.RangeValidator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.RegularExpressionValidator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.RequiredFieldValidator?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.SelectionList?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Style?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.StyleSheet?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.StyleSheetControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.TemplateContainer?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.TextBox?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.TextBoxControlBuilder?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.TextControl?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.TextView?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.TextViewElement?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.ValidationSummary?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Wrapping?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlCalendarAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlCommandAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlFormAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlImageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlLinkAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlMobileTextWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlPageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlPhoneCallAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlSelectionListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlTextBoxAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.ControlAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlCalendarAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlCommandAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlControlAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlFormAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlImageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLabelAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLinkAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLiteralTextAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlMobileTextWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlObjectListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPanelAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPhoneCallAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlSelectionListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlTextBoxAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlTextViewAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlValidationSummaryAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.HtmlValidatorAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.MobileTextWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.MultiPartWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.UpWmlMobileTextWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.UpWmlPageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlCalendarAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlCommandAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlControlAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlFormAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlImageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlLabelAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlLinkAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlLiteralTextAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlMobileTextWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlObjectListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlPageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlPanelAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlPhoneCallAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlPostFieldType?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlSelectionListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlTextBoxAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlTextViewAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlValidationSummaryAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.WmlValidatorAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.Doctype?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.StyleSheetLocation?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCalendarAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCommandAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlControlAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCssHandler?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlFormAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlImageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLabelAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLinkAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLiteralTextAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlMobileTextWriter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlObjectListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPageAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPanelAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPhoneCallAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlSelectionListAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlTextBoxAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlTextViewAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlValidationSummaryAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlValidatorAdapter?displayProperty=nameWithType>|System.Web.Mobile.dll 어셈블리는 사용되지 않으므로 사용하면 안 됩니다. ASP.NET 모바일 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [모바일용 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=157231)을 참조하십시오.|

[맨 위로 이동](#introduction)

<a name="workflow_activities"></a>

### <a name="assembly-systemworkflowactivitiesdll"></a>어셈블리: System.Workflow.Activities.dll

|Type|Message|
|----------|-------------|
|<xref:System.Workflow.Activities?displayProperty=nameWithType> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Activities.Configuration.ActiveDirectoryRoleFactoryConfiguration?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Activities.Rules.RuleActionTrackingEvent?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Activities.Rules.RuleConditionReference?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Activities.Rules.RuleSetReference?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|

[맨 위로 이동](#introduction)

<a name="workflow_componentmodel"></a>

### <a name="assembly-systemworkflowcomponentmodeldll"></a>어셈블리: System.Workflow.ComponentModel.dll

|Type|Message|
|----------|-------------|
|<xref:System.Workflow.ComponentModel> 및 <xref:System.Workflow.ComponentModel.GetValueOverride?displayProperty=nameWithType>를 제외한 <xref:System.Workflow.ComponentModel.SetValueOverride?displayProperty=nameWithType> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Compiler> 및 <xref:System.Workflow.ComponentModel.Compiler.ValidationError?displayProperty=nameWithType>를 제외한 <xref:System.Workflow.ComponentModel.Compiler.ValidationErrorCollection?displayProperty=nameWithType> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Design>를 제외한 <xref:System.Workflow.ComponentModel.Design.ConnectorEventHandler> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.ActivityCodeDomSerializationManager?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.ActivityCodeDomSerializer?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.ActivityMarkupSerializer?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.ActivitySurrogateSelector?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.ActivityTypeCodeDomSerializer?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.CompositeActivityMarkupSerializer?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.ComponentModel.Serialization.DependencyObjectCodeDomSerializer?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|

[맨 위로 이동](#introduction)

<a name="workflow_runtime"></a>

### <a name="assembly-systemworkflowruntimedll"></a>어셈블리: System.Workflow.Runtime.dll

|Type|Message|
|----------|-------------|
|<xref:System.Activities.Statements.Interop?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br />Workflow Foundation 3.0 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 Workflow 4.0 형식을 사용하세요.|
|<xref:System.Activities.Tracking.InteropTrackingRecord?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br />Workflow Foundation 3.0 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 Workflow 4.0 형식을 사용하세요.|
|<xref:System.Workflow.Runtime> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Runtime.Configuration> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Runtime.DebugEngine>를 제외한 <xref:System.Workflow.Runtime.DebugEngine.DebugEngineCallback> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Runtime.Hosting>를 제외한 <xref:System.Workflow.Runtime.Hosting.WorkflowCommitWorkBatchService.CommitWorkBatchCallback> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|
|<xref:System.Workflow.Runtime.Tracking> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> System.Workflow.\* 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 형식을 사용하세요.|

[맨 위로 이동](#introduction)

<a name="workflowservices"></a>

### <a name="assembly-systemworkflowservicesdll"></a>어셈블리: System.WorkflowServices.dll

|Type|Message|
|----------|-------------|
|<xref:System.ServiceModel.WorkflowServiceHost?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Activation.WorkflowServiceHostFactory?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Activities.Description.WorkflowRuntimeEndpoint?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Configuration.ExtendedWorkflowRuntimeServiceElementCollection?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Configuration.PersistenceProviderElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Configuration.WorkflowRuntimeElement?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Description.DurableOperationAttribute?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Description.DurableServiceAttribute?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Description.PersistenceProviderBehavior?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Description.UnknownExceptionAction?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Description.WorkflowRuntimeBehavior?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Dispatcher.DurableOperationContext?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.InstanceLockException?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.InstanceNotFoundException?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.LockingPersistenceProvider?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.PersistenceException?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.PersistenceProvider?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.PersistenceProviderFactory?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.ServiceModel.Persistence.SqlPersistenceProviderFactory?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.Workflow.Activities?displayProperty=nameWithType> 네임스페이스의 모든 형식|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|
|<xref:System.Workflow.Runtime.Hosting.ChannelManagerService?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> WF 3 형식은 사용되지 않습니다. 대신 <xref:System.Activities>.\*의 새 WF 4 형식을 사용하세요.|

[맨 위로 이동](#introduction)

<a name="xaml"></a>

### <a name="assembly-systemxamldll"></a>어셈블리: System.Xaml.dll

|Type|Message|
|----------|-------------|
|<xref:System.Windows.Markup.AcceptedMarkupExtensionExpressionTypeAttribute?displayProperty=nameWithType>|XAML 파서에서 사용되지 않습니다. <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute?displayProperty=nameWithType>를 참조하십시오.|

[맨 위로 이동](#introduction)

<a name="xml"></a>

### <a name="assembly-systemxmldll"></a>어셈블리: System.Xml.dll

|Type|Message|
|----------|-------------|
|<xref:System.Xml.IApplicationResourceStreamResolver?displayProperty=nameWithType>|.NET Framework 4.5에서 처음으로 사용되지 않음<br /><br /> 이 형식을 사용하면 컴파일러 오류가 생성됩니다.<br /><br /> 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Xml.Schema.XmlSchemaCollection?displayProperty=nameWithType>|스키마 컴파일 및 유효성 검사에는 <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=nameWithType>을 사용하십시오.|
|<xref:System.Xml.XmlValidatingReader?displayProperty=nameWithType>|대신 적절한 <xref:System.Xml.XmlReader?displayProperty=nameWithType>를 사용하여 <xref:System.Xml.XmlReader.Create%2A?displayProperty=nameWithType> 메서드에서 만드는 <xref:System.Xml.XmlReaderSettings?displayProperty=nameWithType>를 사용하십시오.|
|<xref:System.Xml.XmlXapResolver?displayProperty=nameWithType>|이 형식을 사용하면 컴파일러 오류가 생성됩니다. 이 API는 .NET Framework 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.|
|<xref:System.Xml.Xsl.XslTransform?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다. 대신 <xref:System.Xml.Xsl.XslCompiledTransform?displayProperty=nameWithType>를 사용하십시오.|

[맨 위로 이동](#introduction)

<a name="WindowsBase"></a>

### <a name="assembly-windowsbasedll"></a>어셈블리: WindowsBase.dll

|Type|Message|
|----------|-------------|
|<xref:System.Windows.Markup.IReceiveMarkupExtension?displayProperty=nameWithType>|<xref:System.Windows.Markup.IReceiveMarkupExtension?displayProperty=nameWithType>는 사용되지 않습니다. 이 인터페이스는 더 이상 사용되지 않습니다.|

[맨 위로 이동](#introduction)

<a name="obsolete_types_in_microsoft_assemblies"></a>

## <a name="obsolete-types-in-microsoft-assemblies"></a>Microsoft 어셈블리에서 사용되지 않는 형식

다음 단원에서는 Microsoft 어셈블리에서 사용되지 않는 형식을 보여 줍니다. 이러한 어셈블리는 Microsoft.JScript.dll, Microsoft.VisualC.dll 등의 개별 언어를 대상으로 하는 어셈블리와 같은 특수 용도의 어셈블리입니다.

<a name="IEHost"></a>

### <a name="assembly-iehostdll-and-ieexecexe"></a>어셈블리: IEHost.dll 및 IEExec.exe

IEHost.dll 및 IEExec.exe 어셈블리는 .NET Framework에서 제거되었습니다. 해당 형식 및 멤버는 모두 사용되지 않으며 .NET Framework 4부터 지원되지 않습니다. 이러한 어셈블리는 Windows Forms 컨트롤을 호스팅하여 Internet Explorer에서 실행 파일을 실행하기 위해 사용되었습니다. ClickOnce, XBAP(XAML 브라우저 애플리케이션) 및 Microsoft Silverlight를 대신 사용하는 것이 좋습니다.

[맨 위로 이동](#introduction)

<a name="Engine"></a>

### <a name="assembly-microsoftbuildenginedll"></a>어셈블리: Microsoft.Build.Engine.dll

|Type|Message|
|----------|-------------|
|<xref:Microsoft.Build.BuildEngine.Engine?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다. 대신 *Microsoft.Build* 어셈블리의 <xref:Microsoft.Build.Evaluation.ProjectCollection?displayProperty=nameWithType>을 사용하세요.|
|<xref:Microsoft.Build.BuildEngine.Project?displayProperty=nameWithType>|이 클래스는 사용되지 않습니다. 대신 *Microsoft.Build* 어셈블리의 <xref:Microsoft.Build.Evaluation.ProjectCollection?displayProperty=nameWithType>을 사용하세요.|

[맨 위로 이동](#introduction)

<a name="jscript"></a>

### <a name="assembly-microsoftjscriptdll"></a>어셈블리: Microsoft.JScript.dll

|Type|Message|
|----------|-------------|
|<xref:Microsoft.JScript.Vsa.BaseVsaEngine?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.BaseVsaSite?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.BaseVsaStartup?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaCodeItem?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaEngine?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaError?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaGlobalItem?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaItem?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaItems?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaPersistSite?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaReferenceItem?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.IJSVsaSite?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.JSVsaError?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.JSVsaException?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.JSVsaItemFlag?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.JSVsaItemType?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.ResInfo?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|
|<xref:Microsoft.JScript.Vsa.VsaEngine?displayProperty=nameWithType>|이 형식은 Visual Studio 2005에서 더 이상 사용되지 않습니다. 이 기능을 대체할 수 없습니다. 추가 도움말은 <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=nameWithType> 문서를 참조하십시오.|

[맨 위로 이동](#introduction)

<a name="VBCompat"></a>

### <a name="assembly-microsoftvisualbasiccompatibilitydll"></a>어셈블리: Microsoft.VisualBasic.Compatibility.dll

Visual Basic 6에서 마이그레이션에 대한 정보는 [Visual Basic 6.0 리소스 센터](https://docs.microsoft.com/previous-versions/visualstudio/visual-basic-6/visual-basic-6.0-documentation)를 참조하세요.

|Type|Message|
|----------|-------------|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseControlArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseOcxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ButtonArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CheckBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CheckedListBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ColorDialogArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ComboBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DirListBox?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DirListBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DriveListBox?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DriveListBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FileListBox?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FileListBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FixedLengthString?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FontDialogArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FormShowConstants?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.GroupBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.HScrollBarArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ImageListArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.LabelArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListBoxItem?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListViewArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.LoadResConstants?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MaskedTextBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MenuItemArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MouseButtonConstants?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.OpenFileDialogArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PanelArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PictureBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PrintDialogArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ProgressBarArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.RadioButtonArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.RichTextBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.SaveFileDialogArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ScaleMode?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ShiftConstants?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.StatusBarArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.StatusStripArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.Support?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TabControlArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TextBoxArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TimerArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolBarArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolStripArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolStripMenuItemArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TreeViewArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.VScrollBarArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebBrowserArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClass?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassContainingClassNotOptional?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassCouldNotFindEvent?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassNextItemCannotBeCurrentWebItem?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassNextItemRespondNotFound?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassUserWebClassNameNotOptional?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassWebClassFileNameNotOptional?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassWebItemNotValid?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItem?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemAssociatedWebClassNotOptional?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemClosingTagNotFound?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemCouldNotLoadEmbeddedResource?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemCouldNotLoadTemplateFile?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemNameNotOptional?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemNoTemplateSpecified?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemTooManyNestedTags?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemUnexpectedErrorReadingTemplateFile?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ZOrderConstants?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|

[맨 위로 이동](#introduction)

<a name="VBCompatData"></a>

### <a name="assembly-microsoftvisualbasiccompatibilitydatadll"></a>어셈블리: Microsoft.VisualBasic.Compatibility.Data.dll

|Type|Message|
|----------|-------------|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.BOFActionEnum?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.EndOfRecordsetDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.EOFActionEnum?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.ErrorDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FetchCompleteDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FetchProgressDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FieldChangeCompleteDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.MoveCompleteDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.OrientationEnum?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.RecordChangeCompleteDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.RecordsetChangeCompleteDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeFieldDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeRecordDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeRecordsetDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillMoveDelegate?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODCArray?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseDataEnvironment?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BindingCollectionEnumerator?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CONNECTDATA?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBBINDING?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBCOLUMNINFO?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBID?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBinding?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBindingCollection?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBKINDENUM?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBPROPIDSET?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IAccessor?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IChapteredRowset?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IColumnsInfo?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IConnectionPoint?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IConnectionPointContainer?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IDataFormat?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IDataFormatDisp?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IEnumConnectionPoints?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IEnumConnections?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowPosition?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowPositionChange?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowset?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetChange?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetIdentity?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetInfo?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetNotify?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MBinding?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MBindingCollection?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.SRDescriptionAttribute?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UGUID?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UNAME?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UpdateMode?displayProperty=nameWithType>|이 멤버는 사용되지 않습니다.|

[맨 위로 이동](#introduction)

<a name="visualc"></a>

### <a name="assembly-microsoftvisualcdll"></a>어셈블리: Microsoft.VisualC.dll

|Type|Message|
|----------|-------------|
|<xref:Microsoft.VisualC.DebugInfoInPDBAttribute?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.DecoratedNameAttribute?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.IsConstModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.IsCXXReferenceModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.IsLongModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.IsSignedModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.IsVolatileModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.MiscellaneousBitsAttribute?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.NeedsCopyConstructorModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|
|<xref:Microsoft.VisualC.NoSignSpecifiedModifier?displayProperty=nameWithType>|Microsoft.VisualC.dll은 사용되지 않는 어셈블리이며 이전 버전과의 호환성을 위해서만 존재합니다.|

## <a name="see-also"></a>참고 항목

- [클래스 라이브러리의 사용되지 않는 기능](whats-obsolete.md)
- [사용되지 않는 멤버](obsolete-members.md)
