---
title: <enforceFIPSPolicy> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- enforceFIPSPolicy element
- FIPS
- <enforceFIPSPolicy> element
- Federal Information Processing Standards (FIPS)
ms.assetid: c35509c4-35cf-43c0-bb47-75e4208aa24e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f90abf9f6c2bc0aed2cf01558b2c0cca4e967e81
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252642"
---
# <a name="enforcefipspolicy-element"></a>\<enforceFIPSPolicy > 요소
암호화 알고리즘이 FIPS(Federal Information Processing Standards)를 준수해야 하는 컴퓨터 구성 요구 사항을 적용할지를 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<enforceFIPSPolicy>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<enforceFIPSPolicy enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|사용|필수 특성입니다.<br /><br /> 암호화 알고리즘이 FIPS와 호환 되어야 하는 컴퓨터 구성 요구 사항을 적용 하도록 설정할지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`true`|암호화 알고리즘을 FIPS 규격으로 요구 하도록 컴퓨터를 구성한 경우에는 해당 요구 사항이 적용 됩니다. 클래스가 FIPS와 호환 되지 않는 알고리즘을 구현 하는 경우 해당 클래스에 대 `Create` 한 생성자 또는 메서드는 해당 컴퓨터에서 실행 될 때 예외를 throw 합니다. 이 값이 기본값입니다.|  
|`false`|응용 프로그램에서 사용 하는 암호화 알고리즘은 컴퓨터 구성에 관계 없이 FIPS를 준수 하지 않아도 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 2\.0 .NET Framework부터 암호화 알고리즘을 구현 하는 클래스를 만드는 것은 컴퓨터의 구성에 의해 제어 됩니다. 컴퓨터가 FIPS와 호환 되지 않는 알고리즘을 요구 하도록 구성 되어 있고 클래스가 FIPS와 호환 되지 않는 알고리즘을 구현 하는 경우 해당 클래스의 인스턴스를 만들려고 하면 예외가 throw 됩니다. 생성자는 <xref:System.InvalidOperationException> 예외를 throw 하 `Create` 고 메서드는 <xref:System.Reflection.TargetInvocationException> 내부 <xref:System.InvalidOperationException> 예외를 사용 하 여 예외를 throw 합니다.  
  
 구성에서 FIPS를 준수 해야 하는 컴퓨터에서 응용 프로그램을 실행 하는 경우 응용 프로그램에서 FIPS와 호환 되지 않는 알고리즘을 사용 하는 경우 구성 파일에서이 요소를 사용 하 여 CLR (공용 언어 런타임)이 사용 되지 않도록 할 수 있습니다. FIPS 준수 적용. 이 요소는 .NET Framework 2.0 서비스 팩 1에서 도입 되었습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 CLR에서 FIPS 준수를 적용 하지 않도록 방지 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
    <runtime>  
        <enforceFIPSPolicy enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [암호화 모델](../../../../standard/security/cryptography-model.md)
