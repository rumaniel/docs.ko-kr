---
title: WMI 및 성능 카운터(관리되지 않는 API 참조)
description: WMI 및 성능 카운터 정보에 대한 .NET Framework 관리되지 않는 API를 요약합니다.
author: rpetrusha
ms.author: ronpet
ms.date: 11/06/2017
ms.openlocfilehash: bbf22496098f848cc7c55652198d792c6f631c15
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62049312"
---
# <a name="windows-management-instrumentation-wmi-and-performance-counters-unmanaged-api-reference"></a>WMI(Windows Management Instrumentation) 및 성능 카운터(관리되지 않는 API 참조)

.NET Framework WMI 및 성능 카운터 관리되지 않는 API는 [네이티브 Windows Management Instrumentation API](/windows/desktop/WmiSdk/com-api-for-wmi)에 대한 호출을 래핑하는 함수 집합으로 구성됩니다. 이를 통해 원격 컴퓨터 시스템을 관리하고 모니터링하는 도구와 라이브러리를 개발할 수 있습니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

API에는 다음 함수가 포함됩니다.

| 함수 | 설명 |
|---------|---------|
| [BeginEnumeration 함수](beginenumeration.md) | 열거자를 WMI 개체 속성 열거형의 시작 부분으로 다시 설정합니다. |
| [BeginMethodEnumeration 함수](beginmethodenumeration.md) |  개체에 사용할 수 있는 메서드의 열거형을 시작합니다. |
| [BlessIWbemServices 함수](blessiwbemservices.md) | 사용자 자격 증명이 지정된 IWbemServices 클래스에 대한 액세스를 허용하는지 여부를 나타냅니다. |
| [BlessIWbemServicesObject 함수](blessiwbemservicesobject.md) | 사용자 자격 증명이 지정된 IWbem 서비스 개체에 대한 액세스를 허용하는지 여부를 나타냅니다. |
| [복제 함수](clone.md) | 현재 개체의 전체 복제본인 새 개체를 반환합니다. |
| [CloneEnumWbemClassObject 함수](cloneenumwbemclassobject.md) | 열거형의 현재 위치를 유지하면서 열거자의 논리적 복사본을 만듭니다. |
| [CompareTo 함수](compareto.md) | 개체를 다른 Windows 관리 개체와 비교합니다. |
| [ConnectServerWmi 함수](connectserverwmi.md) | DCOM 통해 지정된 컴퓨터의 WMI 네임스페이스에 대한 연결을 만듭니다. |
| [CreateClassEnumWmi 함수](createclassenumwmi.md) | 지정된 선택 조건을 충족하는 모든 클래스에 대한 열거자를 반환합니다. |
| [CreateInstanceEnumWmi 함수](createinstanceenumwmi.md) | 지정된 선택 조건을 충족하는 지정된 클래스의 인스턴스를 반환하는 열거자를 반환합니다. |
| [Delete 함수](delete.md) | 클래스 정의 및 모든 해당 한정자에서 지정된 속성을 삭제합니다. |
| [DeleteMethod 함수](deletemethod.md) | CIM 클래스 정의에서 지정된 메서드를 삭제합니다. |
| [EndEnumeration 함수](endenumeration.md) | 열거형 시퀀스를 종료합니다. |
| [EndMethodEnumeration 함수](endmethodenumeration.md) | [BeginMethodEnumeration 함수](beginmethodenumeration.md)를 호출하여 시작된 열거형 시퀀스를 종료합니다. |
| [ExecNotificationQueryWmi 함수](execnotificationquerywmi.md) | 쿼리를 실행하여 이벤트를 수신합니다. |
| [ExecQueryWmi 함수](execquerywmi.md) | 쿼리를 실행하여 개체를 검색합니다. |
| [FormatFromRawValue 함수](formatfromrawvalue.md) | 형식 변환이 시간 기반인 경우 하나의 원시 성능 데이터 값을 지정된 형식으로 변화하거나 두 개의 원시 성능 데이터 값으로 변환합니다. |
| [Get 함수](get.md) | 지정된 속성 값이 있으면 검색합니다. |
| [GetCurrentApartmentType 함수](getcurrentapartmenttype.md) | 호출자가 실행 중인 아파트의 유형을 검색합니다. |
| [GetDemultiplexedStub 함수](getdemultiplexedstub.md) | 클라이언트가 Windows 관리에서 비동기 호출을 수신하는 데 도움이 되는 개체 전달자 싱크를 만듭니다. |
| [GetErrorInfo 함수](geterrorinfo.md) | 이전 함수 호출에서 오류 정보를 검색합니다. |
| [GetMethod 함수](getmethod.md) | 지정된 메서드에 대한 정보를 검색합니다. |
| [GetMethodOrigin 함수](getmethodorigin.md) | 메서드가 선언되는 클래스를 결정합니다. |
| [GetMethodQualifierSet 함수](getmethodqualifierset.md) | 특정 메서드에 대한 한정자 집합을 검색합니다. |
| [GetNames 함수](getnames.md) | 개체 속성의 하위 집합 또는 모든 이름을 검색합니다. |
| [GetObjectText 함수](getobjecttext.md) | MOF 구문에서 개체의 텍스트 렌더링을 반환합니다. |
| [GetPropertyHandle 함수](getpropertyhandle.md) | 속성을 식별하는 고유한 핸들을 반환합니다. |
| [GetPropertyOrigin 함수](getpropertyorigin.md) | 속성이 선언되는 클래스를 결정합니다. |
| [GetPropertyQualifierSet 함수](getpropertyqualifierset.md) | 특정 속성에 대한 한정자 집합을 검색합니다.  |
| [GetQualifierSet 함수](getqualifierset.md) | 클래스 인스턴스 또는 클래스 정의에 대한 한정자 집합을 검색합니다. |
| [InheritsFrom 함수](inheritsfrom.md) | 현재 클래스 또는 인스턴스가 지정된 부모 클래스에서 파생되는지 여부를 결정합니다. |
| [Initialize 함수](initialize.md) | WMI 초기화를 수행합니다. |
| [Next 함수](next.md) | 열거형에서 다음 속성을 검색합니다. |
| [NextMethod 함수](nextmethod.md) | 열거형에서 다음 메서드를 검색합니다. |
| [Put 함수](put.md) | 명명된 속성을 새 값으로 설정합니다. |
| [PutClassWmi 함수](putclasswmi.md) | 새 클래스를 만들거나 기존 클래스를 업데이트합니다. |
| [PutInstanceWmi 함수](putinstancewmi.md) | 기존 클래스의 인스턴스를 만들거나 업데이트합니다. 인스턴스가 WMI 리포지토리에 기록됩니다. |
| [PutMethod 함수](putmethod.md) | 메서드를 만듭니다. |
| [QualifierSet_BeginEnumeration 함수](qualifierset-beginenumeration.md) | 개체 한정자의 열거자를 열거형 시작 부분으로 다시 설정합니다. |
| [QualifierSet_Delete 함수](qualifierset-delete.md) | 지정된 한정자를 이름으로 삭제합니다.  |
| [QualifierSet_EndEnumeration 함수](qualifierset-endenumeration.md) | `QualifierSet_BeginEnumeration` 함수에 대한 호출로 시작된 열거형을 종료합니다. |
| [QualifierSet_Get 함수](qualifierset-get.md) | 지정한 명명된 한정자를 가져옵니다.  |
| [QualifierSet_GetNames 함수](qualifierset-getnames.md) | 현재 개체 또는 속성에서 사용할 수 있는 모든 한정자 또는 지정된 한정자의 이름을 검색합니다. |
| [QualifierSet_Next 함수](qualifierset-next.md) | [QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md) 함수를 호출하여 시작된 열거형의 다음 한정자를 검색합니다. |
| [QualifierSet_Put 함수](qualifierset-put.md) | 명명된 한정자 및 값을 씁니다. |
| [ResetSecurity 함수](resetsecurity.md) | 제공된 가장 토큰을 현재 스레드에 할당합니다. |
| [SetSecurity 함수](setsecurity.md) | 현재 스레드와 연결된 가장 토큰을 검색합니다. |
| [SpawnDerivedClass 함수](spawnderivedclass.md) | 지정된 개체에서 새로 파생된 클래스 개체를 만듭니다. |
| [SpawnInstance 함수](spawninstance.md) | 클래스의 새 인스턴스를 만듭니다. |
| [VerifyClient 함수](verifyclientkey.md) | 클라이언트 키가 올바른 보안을 유지하는지 확인합니다. |
| [WritePropertyValue 함수](writepropertyvalue.md) | 지정된 수의 바이트를 속성 핸들로 식별되는 속성에 씁니다. |

## <a name="see-also"></a>참고 항목

- [관리되지 않는 API 참조](../index.md)
