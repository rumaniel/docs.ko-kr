---
title: 인스턴스 인코딩 옵션
ms.date: 03/30/2017
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
ms.openlocfilehash: c4de7c45d899f45a7b5b71d563257d9accb8fdbb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61928718"
---
# <a name="instance-encoding-option"></a>인스턴스 인코딩 옵션
합니다 **Instance Encoding Option** SQL 워크플로 인스턴스 저장소의 속성을 사용 하면 SQL 지 속성 공급자를 저장 하기 전에 GZip 알고리즘을 사용 하 여 워크플로 인스턴스 상태 정보를 압축 해야 하는지 여부를 지정할 수는 지 속성 데이터베이스에 대 한 정보입니다. 이 속성에 대 한 허용 되는 값은 다음과 같습니다. GZip 및 None입니다. 기본값은 None입니다. 다음 목록에서는 이러한 옵션에 대해 설명합니다.  
  
1. **GZip**합니다. 지속성 공급자가 지속성 데이터베이스에 상태 정보를 유지하기 전에 GZip 알고리즘을 사용하여 상태 정보를 인코딩합니다.  
  
2. **없음**. 지속성 공급자가 지속성 데이터베이스에 정보를 저장하기 전에 상태 정보를 인코딩하지 않습니다.  
  
 GZip을 사용하여 워크플로 인스턴스 상태 정보를 인코딩하면 SQL 데이터베이스에서 메모리 사용을 줄일 수 있으며 데이터베이스가 네트워크에서 워크플로 서비스 호스트를 실행하는 컴퓨터와 다른 컴퓨터에 상주할 경우 네트워크 사용도 줄일 수 있습니다. 일반 지침을 설정 하는 것은 **Instance Encoding Option** 속성을 **None** 워크플로 인스턴스 상태가 작은 경우.
