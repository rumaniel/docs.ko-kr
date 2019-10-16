---
title: XAML 보안 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- security [XAML Services], .NET XAML services
- XAML security [XAML Services]
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
ms.openlocfilehash: 76dce711e46d267c85b0fc9426be452d90b4d07c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622841"
---
# <a name="xaml-security-considerations"></a>XAML 보안 고려 사항
이 항목에서는 XAML 및.NET Framework XAML 서비스 API를 사용 하는 경우 응용 프로그램의 보안을 위한 모범 사례를 설명 합니다.  
  
## <a name="untrusted-xaml-in-applications"></a>응용 프로그램에서 신뢰할 수 없는 XAML  
 가장 일반적인 의미에서 신뢰할 수 없는 XAML는 응용 프로그램을 포함 또는 내보낼 되지 않은 모든 XAML 원본입니다.  
  
 컴파일 또는로 저장 하는 XAML을 `resx`-서명된 된 신뢰할 수 있는 어셈블리 내에서 형식 리소스를 기본적으로 신뢰할 수 없습니다. 전체 어셈블리를 신뢰 하는 만큼의 XAML을 신뢰할 수 있습니다. 대부분의 경우에서만 우려되는 스트림 또는 기타 I/O에서 로드 하는 XAML 소스는 느슨한 XAML의 트러스트 측면입니다. 느슨한 XAML이 특정 구성 요소 또는 응용 프로그램 배포 및 패키징 인프라를 사용 하 여 모델의 기능을 않습니다. 그러나 어셈블리에는 느슨한 XAML 로드를 포함 하는 동작을 구현할 수 있습니다.  
  
 신뢰할 수 없는 XAML에 대 한 처리 해야 일반적으로 동일한 신뢰할 수 없는 코드 처럼 합니다. 신뢰할 수 없는 XAML 신뢰할 수 있는 코드를 액세스 하지 못하도록 샌드 박싱 또는 다른 기능을 사용 합니다.  
  
 XAML 개체를 생성 하 고 해당 속성을 설정할 수 있는 권한을 제공 하는 XAML 기능 특성 합니다. 이러한 기능에도 형식 변환기, 매핑 및 태그 확장을 사용 하 여 응용 프로그램 도메인에서 어셈블리를 액세스 하거나 액세스는 `x:Code` 블록 및 등입니다.  
  
 해당 언어 수준 기능 외에도 XAML은 대부분의 기술에서 UI 정의에 사용 됩니다. 신뢰할 수 없는 XAML 로드를 악의적인 스푸핑 UI가 로드 될 수도 있습니다.  
  
## <a name="sharing-context-between-readers-and-writers"></a>판독기와 기록기 간에 컨텍스트를 공유합니다.  
 XAML 판독기 및 XAML 작성기에 대 한.NET Framework XAML 서비스 아키텍처를 자주 공유 해야 하는 XAML 판독기는 XAML 작성기 또는 XAML 스키마 컨텍스트를 공유 합니다. XAML 노드 루프 논리를 작성 하는 또는 경로 저장 하는 사용자 지정을 제공 하는 경우 개체 또는 컨텍스트를 공유 해야 할 수 있습니다. XAML 판독기 인스턴스, 기본이 아닌 XAML 스키마 컨텍스트 또는 신뢰할 수 있는 항목과 신뢰할 수 없는 코드 간에 XAML 판독기/기록기 클래스에 대 한 설정을 공유 하지 해야 합니다.  
  
 대부분의 시나리오 및 XAML 개체를 백업 하는 CLR 기반 형식에 대 한 쓰기와 관련 된 작업 기본 XAML 스키마 컨텍스트를 사용 수 있습니다. 기본 XAML 스키마 컨텍스트를 완전 신뢰를 손상 시킬 수 있는 설정을 명시적으로 포함 되지 않습니다. 따라서 신뢰할 수 있는 항목과 신뢰할 수 없는 XAML 판독기/기록기 구성 요소 간에 컨텍스트를 공유 하려면 안전 합니다. 그러나이 작업을 수행 하는 경우이 여전히 가장 좋은 방법은 별개의 이러한 판독기 및 작성기를 유지 하려면 <xref:System.AppDomain> 특히 의도 한/샌드박스가 적용 된 부분 신뢰에 대 한 중 하나를 사용 하 여 범위입니다.  
  
## <a name="xaml-namespaces-and-assembly-trust"></a>XAML 네임 스페이스 및 어셈블리 트러스트  
 응용 프로그램 도메인에 로드 된 신뢰할 수 있는 항목과 신뢰할 수 없는 어셈블리 정규화 되지 않은 기본 구문 및 XAML에서 어셈블리에 대 한 사용자 지정 XAML 네임 스페이스 매핑을 해석 하는 방법에 대 한 정의 구분 하지 않습니다. 따라서 것을 신뢰할 수 있는 어셈블리의 의도 한 XAML 네임 스페이스 매핑 스푸핑하여 XAML 소스의 선언 된 개체 및 속성 정보를 캡처하는 신뢰할 수 없는 어셈블리에 대 한 기술적으로 가능 합니다. 이 상황을 방지 하려면 보안 요구 사항이 있는 경우 다음 방법 중 하나를 사용 하 여 의도 한 XAML 네임 스페이스 매핑을 수행 해야:  
  
- 응용 프로그램의 XAML을 수행한 모든 XAML 네임 스페이스 매핑에 대 한 강력한 이름으로 정규화 된 어셈블리 이름을 사용 합니다.  
  
- 특정 구성 하 여 참조 어셈블리의 고정된 된 집합을 매핑할 어셈블리 제한 <xref:System.Xaml.XamlSchemaContext> 에 XAML 판독기 및 XAML 개체 작성기입니다. <xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29>을 참조하세요.  
  
## <a name="xaml-type-mapping-and-type-system-access"></a>XAML 형식 매핑 및 형식 시스템 액세스  
 XAML에는 여러 가지 방법으로 CLR 기본 CLR 형식 시스템을 구현 하는 방법에 피어 자체 형식 시스템을 지원 합니다. 그러나 해당 형식 정보를 기반으로 하는 형식에 대 한 신뢰 결정 한다면 형식 인식의 특정 측면에 대 한 지원 형식을 CLR 형식 정보를 연기 해야 있습니다. XAML 형식 시스템의 특정 보고 기능의 일부 가상 메서드로 열려 되며 따라서 없습니다 완벽 하 게 원래.NET Framework XAML 서비스 구현에 의해 제어 때문입니다. 이러한 확장 지점을 XAML 형식 시스템은 자체 XAML의 확장성 및 기본 CLR 기반 구현 및 기본 XAML 스키마 컨텍스트 및 대체 가능한 형식 매핑 전략에 맞게 확장 가능 하기 때문에 존재 합니다. 자세한 내용은 다양 한 속성에서 특정 정보를 참조 하세요 <xref:System.Xaml.XamlType> 고 <xref:System.Xaml.XamlMember>입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xaml.Permissions.XamlAccessLevel>
