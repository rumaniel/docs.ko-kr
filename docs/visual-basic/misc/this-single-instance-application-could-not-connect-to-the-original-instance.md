---
title: 이 단일 인스턴스 애플리케이션을 원본 인스턴스에 연결할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrAppModel_SingleInstanceCantConnect
ms.assetid: 7c2c0cee-02a1-4157-be03-39d18e18408f
ms.openlocfilehash: 5585da7f2ccf7d5d3ec8db281ab9534249020a63
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619841"
---
# <a name="this-single-instance-application-could-not-connect-to-the-original-instance"></a>이 단일 인스턴스 애플리케이션을 원본 인스턴스에 연결할 수 없습니다.
이 단일 인스턴스 애플리케이션을 원본 인스턴스에 연결할 수 없습니다. 이 문제가 발생할 수 있는 몇 가지 원인은 다음과 같습니다.  
  
- 원래 인스턴스의 응답이 중지되었습니다.  
  
- 커널 개체를 만들 수 있는 권한이 애플리케이션에 없습니다. 커널 개체에 대 한 자세한 내용은 참조 하십시오 [뮤텍스](../../standard/threading/mutexes.md)합니다.  
  
     커널 개체의 기본 이름은 어셈블리의 GUID, 주 버전 번호 및 부 버전 번호를 연결하여 만들어집니다. 예를 들어 기본 이름은 `3639f15d-9547-43da-8145-60da347829915.1`일 수 있습니다.  
  
## <a name="to-correct-this-error-when-developing-the-application"></a>애플리케이션을 개발할 때 이 오류를 해결하려면  
  
1. 애플리케이션이 응답하지 않는 상태로 전환되지 않는지 확인합니다.  
  
2. 애플리케이션에 커널 개체를 만들 수 있는 권한이 있는지 확인합니다.  
  
3. 애플리케이션의 원래 인스턴스를 다시 시작합니다.  
  
4. 컴퓨터를 다시 시작하여 원래 인스턴스 애플리케이션에 연결하는 데 필요한 리소스를 사용 중일 수 있는 프로세스를 지웁니다.  
  
5. 오류가 발생한 상황을 파악하여 Microsoft 기술 지원 서비스에 전화로 문의합니다.  
  
## <a name="see-also"></a>참고자료

- [디버거 기본 사항](/visualstudio/debugger/debugger-basics)
