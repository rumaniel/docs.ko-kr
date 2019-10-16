---
title: ICorDebugProcess6::EnableVirtualModuleSplitting 메서드
ms.date: 03/30/2017
ms.assetid: e7733bd3-68da-47f9-82ef-477db5f2e32d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8bd06dd3f58a1f74fbdb5ec61c4896f5c1696856
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931066"
---
# <a name="icordebugprocess6enablevirtualmodulesplitting-method"></a>ICorDebugProcess6::EnableVirtualModuleSplitting 메서드
가상 모듈 분할을 사용하거나 사용하지 않도록 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnableVirtualModuleSplitting(  
   BOOL enableSplitting  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `enableSplitting`  
 가상 모듈 분할을 사용하려면 `true`로 설정하고, 사용하지 않으려면 `false`로 설정합니다.  
  
## <a name="remarks"></a>설명  
 가상 모듈 분할을 통해 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 는 빌드 프로세스 중에 병합 된 모듈을 인식 하 고 단일 단일 모듈이 아니라 개별 모듈의 그룹으로 제공 합니다. 이렇게 하면 아래에 설명 된 다양 한 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 메서드의 동작이 변경 됩니다.  
  
> [!NOTE]
> 이 메서드는 .NET 네이티브에서만 사용할 수 있습니다.  
  
 언제든지 이 메서드를 호출하여 `enableSplitting`의 값을 변경할 수 있습니다. [가상 모듈 분할 및 관리 되지 않는 디버깅 api](#APIs) 섹션에 나열 된 메서드를 호출할 때의 동작을 변경 하는 것 외에도 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 개체의 상태 저장 기능 변경은 발생 하지 않습니다. 가상 모듈을 사용하는 경우 해당 메서드를 호출할 때 성능이 저하됩니다. 또한 [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) api를 올바르게 구현 하기 위해 가상화 된 메타 데이터의 메모리 내 캐싱 기능이 필요할 수 있으며, 이러한 캐시는 가상 모듈 분할이 해제 된 후에도 유지 될 수 있습니다.  
  
## <a name="terminology"></a>용어  
 아래에는 가상 모듈 분할을 설명하는 데 사용되는 용어가 나와 있습니다.  
  
 컨테이너 모듈/컨테이너  
 집계 모듈입니다.  
  
 하위 모듈/가상 모듈  
 컨테이너에 있는 모듈입니다.  
  
 일반 모듈  
 빌드 시에 병합되지 않은 모듈로, 컨테이너 모듈도 아니고 하위 모듈도 아닌 모듈입니다.  
  
 컨테이너 모듈과 하위 모듈은 모두 ICorDebugModule interface 개체로 표현 됩니다. 그러나 인터페이스의 동작은 각 사례 \<에서 약간 다릅니다 .이 섹션 > 섹션에서는에 대해 설명 합니다.  
  
## <a name="modules-and-assemblies"></a>모듈 및 어셈블리  
 다중 모듈 어셈블리는 어셈블리 병합 시나리오에서 지원되지 않으므로 모듈과 어셈블리 간에는 일 대 일 관계가 적용됩니다. 컨테이너 모듈이 나 하위 모듈을 나타내는지 여부와 관계 없이 각 ICorDebugModule 개체에는 해당 ICorDebugAssembly 개체가 있습니다. [ICorDebugModule:: GetAssembly](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md) 메서드는 모듈에서 어셈블리로 변환 합니다. 다른 방향으로 매핑하기 위해 [ICorDebugAssembly:: EnumerateModules](../../../../docs/framework/unmanaged-api/debugging/icordebugassembly-enumeratemodules-method.md) 메서드는 1 개의 모듈만 열거 합니다. 이 경우 어셈블리와 모듈은 긴밀하게 결합된 쌍을 형성하므로 '어셈블리'와 '모듈'이라는 용어는 거의 동일한 의미로 사용됩니다.  
  
## <a name="behavioral-differences"></a>동작 차이점  
 컨테이너 모듈의 동작 및 특성은 다음과 같습니다.  
  
- 컨테이너 모듈을 구성하는 모든 하위 모듈의 메타데이터는 병합됩니다.  
  
- 형식 이름이 변환될 수 있습니다.  
  
- [ICorDebugModule:: GetName](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md) 메서드는 디스크에 있는 모듈에 대 한 경로를 반환 합니다.  
  
- [ICorDebugModule:: GetSize](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md) 메서드는 해당 이미지의 크기를 반환 합니다.  
  
- ICorDebugAssembly3.EnumerateContainedAssemblies 메서드는 하위 모듈을 나열합니다.  
  
- ICorDebugAssembly3.GetContainerAssembly 메서드는 `S_FALSE`를 반환합니다.  
  
 하위 모듈의 동작 및 특성은 다음과 같습니다.  
  
- 병합된 원래 어셈블리에 해당하는 축소된 메타데이터 집합을 포함합니다.  
  
- 메타데이터 이름이 변환되지 않습니다.  
  
- 메타데이터 토큰이 빌드 프로세스에서 병합되기 전의 원래 어셈블리에 포함되어 있던 토큰과 일치할 가능성은 거의 없습니다.  
  
- [ICorDebugModule:: GetName](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md) 메서드는 파일 경로가 아니라 어셈블리 이름을 반환 합니다.  
  
- [ICorDebugModule:: GetSize](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md) 메서드는 병합 되지 않은 원래 이미지 크기를 반환 합니다.  
  
- ICorDebugModule3.EnumerateContainedAssemblies 메서드는 `S_FALSE`를 반환합니다.  
  
- ICorDebugAssembly3.GetContainerAssembly 메서드는 포함하는 모듈을 반환합니다.  
  
## <a name="interfaces-retrieved-from-modules"></a>모듈에서 검색되는 인터페이스  
 다양한 인터페이스를 만들거나 모듈에서 검색할 수 있습니다. 여기에는 다음과 같은 항목이 포함됩니다.  
  
- [ICorDebugModule:: GetClassFromToken](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getclassfromtoken-method.md) 메서드에서 반환 되는 ICorDebugClass 개체입니다.  
  
- [ICorDebugModule:: GetAssembly](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md) 메서드에서 반환 되는 ICorDebugAssembly 개체입니다.  
  
 이러한 개체는 항상 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)에 의해 캐시 되며 컨테이너 모듈이 나 하위 모듈에서 만들어지거나 쿼리 되었는지 여부에 관계 없이 동일한 포인터 id를 가집니다. 하위 모듈은 이와 같은 캐시된 개체의 필터링된 보기를 제공하며 자체 복사본이 포함된 별도의 캐시를 제공하지는 않습니다.  
  
<a name="APIs"></a>   
## <a name="virtual-module-splitting-and-the-unmanaged-debugging-apis"></a>가상 모듈 분할 및 관리되지 않는 디버깅 API  
 다음 표에서는 가상 모듈 분할이 관리되지 않는 디버깅 API의 다른 메서드 동작에 주는 영향을 설명합니다.  
  
|메서드|`enableSplitting` = `true`|`enableSplitting` = `false`|  
|------------|---------------------------------|----------------------------------|  
|[ICorDebugFunction::GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction-getmodule-method.md)|이 함수가 원래 정의된 하위 모듈을 반환합니다.|이 함수가 병합된 컨테이너 모듈을 반환합니다.|  
|[ICorDebugClass::GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-getmodule-method.md)|이 클래스가 원래 정의된 하위 모듈을 반환합니다.|이 클래스가 병합된 컨테이너 모듈을 반환합니다.|  
|ICorDebugModuleDebugEvent::GetModule|로드된 컨테이너 모듈을 반환합니다. 이 설정에 관계없이 하위 모듈에는 로드 이벤트가 제공되지 않습니다.|로드된 컨테이너 모듈을 반환합니다.|  
|[ICorDebugAppDomain::EnumerateAssemblies](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-enumerateassemblies-method.md)|하위 어셈블리와 일반 어셈블리 목록을 반환합니다. 컨테이너 어셈블리는 포함되지 않습니다. **참고:**  컨테이너 어셈블리에 기호가 없으면 해당 하위 어셈블리가 열거되지 않습니다. 일반 어셈블리의 경우 기호가 없으면 열거될 수도 있고 열거되지 않을 수도 있습니다.|컨테이너 어셈블리와 일반 어셈블리 목록을 반환합니다. 하위 어셈블리는 포함되지 않습니다. **참고:**  일반 어셈블리의 경우 기호가 없으면 열거될 수도 있고 열거되지 않을 수도 있습니다.|  
|[ICorDebugCode:: GetCode](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getcode-method.md) (IL 코드를 참조 하는 경우에만)|병합 전 어셈블리 이미지에서 유효했던 IL을 반환합니다. 즉, 참조하는 형식이 IL을 포함하는 가상 모듈에 정의되어 있지 않으면 모든 인라인 메타데이터 토큰은 TypeRef 또는 MemberRef 토큰이 됩니다. 이러한 TypeRef 또는 MemberRef 토큰은 해당 가상 ICorDebugModule 개체에 대 한 [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) 개체에서 조회할 수 있습니다.|병합 후 어셈블리 이미지의 IL을 반환합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugProcess6 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess6-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
