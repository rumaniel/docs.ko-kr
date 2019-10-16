---
title: <loadFromRemoteSources> 요소
ms.date: 05/24/2018
helpviewer_keywords:
- loadFromRemoteSources element
- <loadFromRemoteSources> element
ms.assetid: 006d1280-2ac3-4db6-a984-a3d4e275046a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 83980d315c83aa5cc23944dbd271c29e0ed83206
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252475"
---
# <a name="loadfromremotesources-element"></a>\<loadFromRemoteSources > 요소
원격 소스에서 로드 된 어셈블리에 .NET Framework 4 이상에서 완전 신뢰를 부여 해야 하는지 여부를 지정 합니다.
  
> [!NOTE]
> Visual Studio 프로젝트 오류 목록 또는 빌드 오류의 [오류 메시지 때문에이 문서를 전달 하는 경우 방법: Visual Studio](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ee890038(v=vs.100))에서 웹의 어셈블리를 사용 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<loadFromRemoteSources >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<loadFromRemoteSources    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 원격 소스에서 로드 된 어셈블리에 완전 신뢰 권한을 부여 해야 하는지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|원격 원본에서 응용 프로그램에 완전 신뢰를 부여 하지 마십시오. 이 값이 기본값입니다.|  
|`true`|원격 원본에서 응용 프로그램에 완전 신뢰를 부여 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명

.NET Framework 3.5 이전 버전에서 원격 위치에서 어셈블리를 로드 하는 경우 어셈블리의 코드는 로드 되는 영역에 따라 권한 부여 집합을 사용 하 여 부분 신뢰로 실행 됩니다. 예를 들어 웹 사이트에서 어셈블리를 로드 하는 경우 인터넷 영역에 로드 되 고 인터넷 권한 집합이 부여 됩니다. 즉, 인터넷 샌드박스에서 실행 됩니다.

.NET Framework 4부터 CAS (코드 액세스 보안) 정책이 사용 하지 않도록 설정 되 고 어셈블리가 완전 신뢰로 로드 됩니다. 일반적으로이는 이전에 샌드 박싱 된 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드로 로드 된 어셈블리에 완전 신뢰를 부여 합니다. 이를 방지 하기 위해 원격 소스에서 로드 된 어셈블리에서 코드를 실행 하는 기능은 기본적으로 비활성화 되어 있습니다. 기본적으로 원격 어셈블리 <xref:System.IO.FileLoadException> 를 로드 하려고 하면 다음과 같은 예외 메시지가 포함 된이 throw 됩니다.

```text
System.IO.FileNotFoundException: Could not load file or assembly 'file:assem.dll' or one of its dependencies. Operation is not supported. 
(Exception from HRESULT: 0x80131515)
File name: 'file:assem.dll' ---> 
System.NotSupportedException: An attempt was made to load an assembly from a network location which would have caused the assembly 
to be sandboxed in previous versions of the .NET Framework. This release of the .NET Framework does not enable CAS policy by default, 
so this load may be dangerous. If this load is not intended to sandbox the assembly, please enable the loadFromRemoteSources switch. 
```

에 어셈블리를 로드 하 고 해당 코드를 실행 하거나 다음을 수행 해야 합니다.

- 어셈블리에 대 한 샌드박스를 명시적으로 만듭니다 [(방법: 샌드박스에서](../../../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)부분적으로 신뢰할 수 있는 코드를 실행 합니다.

- 완전 신뢰에서 어셈블리의 코드를 실행 합니다. 요소를 `<loadFromRemoteSources>` 구성 하 여이 작업을 수행 합니다. 이를 통해 이전 버전의 .NET Framework에서 부분 신뢰로 실행 되는 어셈블리가 이제 .NET Framework 4 이상 버전에서 완전 신뢰로 실행 되도록 지정할 수 있습니다.

> [!IMPORTANT]
> 어셈블리가 완전 신뢰로 실행 되지 않아야 하는 경우이 구성 요소를 설정 하지 마십시오. 대신 어셈블리를 로드할 샌드박스가 <xref:System.AppDomain> 적용 된을 만듭니다.

요소에 대 한 `enabled` 특성은 CAS (코드 액세스 보안)를 사용 하지 않도록 설정한 경우에만 `<loadFromRemoteSources>` 적용 됩니다. 기본적으로 CAS 정책은 .NET Framework 4 이상 버전에서 사용할 수 없습니다. 를로 `enabled` `true`설정 하면 원격 어셈블리에 완전 신뢰가 부여 됩니다.

가 `enabled` 로 `true` 설정되지않은경우다음조건중하나에서<xref:System.IO.FileLoadException> 이 throw 됩니다.

- 현재 도메인의 샌드 박싱 동작은 .NET Framework 3.5의 동작과 다릅니다. 이렇게 하려면 CAS 정책을 사용 하지 않도록 설정 해야 하 고 현재 도메인을 샌드 박싱 하지 않아야 합니다.

- 로드 되는 어셈블리가 영역에 `MyComputer` 속하지 않습니다.

요소를로 `true` 설정 하면이 예외가 throw 되지 않습니다. `<loadFromRemoteSources>` 이를 통해 보안을 위해 로드 된 어셈블리를 sandbox 하는 데 공용 언어 런타임에 의존 하지 않도록 지정 하 고 완전 신뢰로 실행 되도록 허용할 수 있습니다.

## <a name="notes"></a>노트

- .NET Framework 4.5 이상 버전에서 로컬 네트워크 공유의 어셈블리는 기본적으로 완전 신뢰로 실행 됩니다. `<loadFromRemoteSources>` 요소를 사용 하도록 설정할 필요는 없습니다.

- 응용 프로그램을 웹에서 복사한 경우, Windows에서는 해당 프로그램이 로컬 컴퓨터에 있더라도 웹 응용 프로그램이라는 플래그가 지정됩니다. 해당 파일 속성을 변경 하 여 해당 지정을 변경 하거나, `<loadFromRemoteSources>` 요소를 사용 하 여 어셈블리에 완전 신뢰를 부여할 수 있습니다. 또는 <xref:System.Reflection.Assembly.UnsafeLoadFrom%2A> 메서드를 사용하여 운영 체제가 웹에서 로드되었음을 표시하는 로컬 어셈블리를 로드할 수 있습니다.

- Windows 가상 PC 응용 <xref:System.IO.FileLoadException> 프로그램에서 실행 되는 응용 프로그램에서가 발생할 수 있습니다. 호스팅 컴퓨터의 연결 된 폴더에서 파일을 로드 하려고 하면이 문제가 발생할 수 있습니다. [원격 데스크톱 서비스](https://go.microsoft.com/fwlink/?LinkId=182775) (터미널 서비스)를 통해 연결 된 폴더에서 파일을 로드 하려고 할 때에도 발생할 수 있습니다. 예외를 방지 하려면를로 `enabled` `true`설정 합니다.

## <a name="configuration-file"></a>구성 파일

이 요소는 일반적으로 응용 프로그램 구성 파일에서 사용하지만 컨텍스트에 따라 다른 구성 파일에서도 사용할 수 있습니다. 자세한 내용은 .NET 보안 블로그에서 [Ca 정책의 더 암시적인 사용: loadFromRemoteSources](https://go.microsoft.com/fwlink/p/?LinkId=266839) 문서를 참조 하세요.  

## <a name="example"></a>예제

다음 예제에서는 원격 소스에서 로드 된 어셈블리에 완전 신뢰를 부여 하는 방법을 보여 줍니다.

```xml
<configuration>  
   <runtime>  
      <loadFromRemoteSources enabled="true"/>  
   </runtime>  
</configuration>  
```

## <a name="see-also"></a>참고 항목

- [CAS 정책의 보다 암시적 사용: loadFromRemoteSources](https://go.microsoft.com/fwlink/p/?LinkId=266839)
- [방법: 샌드박스에서 부분적으로 신뢰할 수 있는 코드 실행](../../../misc/how-to-run-partially-trusted-code-in-a-sandbox.md)
- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>
