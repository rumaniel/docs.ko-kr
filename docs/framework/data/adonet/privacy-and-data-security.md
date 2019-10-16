---
title: 개인 정보 및 데이터 보안
ms.date: 03/30/2017
ms.assetid: 46fa5839-adf7-4c7c-bce3-71e941fa7de9
ms.openlocfilehash: 04e405307d3aa42388c396cd69c465ba7ec70d35
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783233"
---
# <a name="privacy-and-data-security"></a>개인 정보 및 데이터 보안
ADO.NET 애플리케이션의 중요한 정보를 안전하게 보호하고 관리하는 방법은 애플리케이션을 만드는 데 사용된 기본 제품 및 기술에 따라 다릅니다. ADO.NET은 데이터 보안이나 암호화를 위한 서비스를 직접적으로 제공하지 않습니다.  
  
## <a name="cryptography-and-hash-codes"></a>암호화 및 해시 코드  
 ADO.NET 애플리케이션에서 .NET Framework <xref:System.Security.Cryptography> 네임스페이스의 클래스를 사용하면 권한이 없는 제3자가 데이터를 읽거나 수정할 수 없도록 할 수 있습니다. 이 중 일부 클래스는 관리되지 않는 Microsoft CryptoAPI에 대한 래퍼이지만 나머지는 관리되는 구현입니다. [암호화 서비스](../../../standard/security/cryptographic-services.md) 항목에서는 .NET Framework의 암호화에 대해 간략하게 설명 하 고, 고 암호화를 구현 하는 방법과 특정 암호화 작업을 수행할 수 있는 방법을 설명 합니다.  
  
 데이터를 암호화한 다음 해독할 수 있는 암호화와 달리 데이터 해시는 단방향 프로세스입니다. 데이터 해시는 데이터가 변경되지 않았음을 확인하여 훼손되지 않도록 하려는 경우에 유용합니다. 즉, 입력 문자열이 동일하면 해시 알고리즘에서는 항상 손쉽게 비교할 수 있는 동일한 짧은 출력 값을 생성합니다. [해시 코드를 사용 하 여 데이터 무결성을 보장](../../../standard/security/ensuring-data-integrity-with-hash-codes.md) 하 여 해시 값을 생성 하 고 확인 하는 방법을 설명 합니다.  
  
## <a name="encrypting-configuration-files"></a>구성 파일 암호화  
 애플리케이션 보안의 가장 중요한 목표 중 하나는 데이터 소스에 대한 액세스를 보호하는 것입니다. 연결 문자열을 안전하게 보호하지 않으면 이로 인해 보안상 취약한 부분이 생길 수 있습니다. 구성 파일에 저장된 연결 문자열은 .NET Framework에서 공통 요소 집합을 정의한 표준 XML 파일에 저장되어 있습니다. 보호되는 구성을 통해 구성 파일의 중요한 정보를 암호화할 수 있습니다. 보호되는 구성은 원래 ASP.NET 애플리케이션을 위해 디자인된 것이지만 Windows 애플리케이션의 구성 파일 섹션을 암호화하는 데도 사용할 수 있습니다. 자세한 내용은 [연결 정보 보호](protecting-connection-information.md)를 참조하세요.  
  
## <a name="securing-string-values-in-memory"></a>메모리 내 문자열 값 보호  
 애플리케이션은 컴퓨터 메모리에서 데이터를 삭제할 수 없으므로 <xref:System.String> 개체에 암호, 신용 카드 번호, 개인 데이터 등의 중요한 정보가 포함되어 있는 경우 해당 데이터가 사용된 후 외부에 노출될 위험이 있습니다.  
  
 <xref:System.String>은 변경할 수 없습니다. 즉, 한번 만들어진 후에는 수정할 수 없습니다. 이 문자열 값이 수정되어 변경된 것처럼 보일 때도 있습니다. 하지만 실제로는 메모리 내 <xref:System.String> 개체의 새 인스턴스가 만들어지고 데이터가 일반 텍스트로 저장된 것입니다. 뿐만 아니라 이 문자열 인스턴스가 언제 메모리에서 삭제될지 예측할 수도 없습니다. .NET 가비지 수집의 경우 문자열이 포함된 메모리 회수는 명확하게 수행되지 않습니다. 따라서 중요한 데이터에는 <xref:System.String> 및 <xref:System.Text.StringBuilder> 클래스를 사용하지 않아야 합니다.  
  
 <xref:System.Security.SecureString> 클래스는 DPAPI(데이터 보호 API)를 사용하여 메모리 내 텍스트를 암호화하기 위한 메서드를 제공합니다. 이 경우 문자열이 더 이상 필요하지 않으면 메모리에서 삭제됩니다. `ToString`의 내용을 빠르게 읽는 데 사용할 수 있는 <xref:System.Security.SecureString> 메서드는 없습니다. 값을 제공하지 않거나 `SecureString` 개체 배열에 대한 포인터를 전달하여 <xref:System.Char>의 새 인스턴스를 초기화할 수 있습니다. 그런 다음 이 클래스의 다양한 메서드를 사용하여 문자열에 대한 작업을 수행할 수 있습니다. 자세한 내용을 보려면에서 클래스를 `SecureString` 사용 하는 방법을 보여 주는 [SecureString 샘플 응용 프로그램](https://go.microsoft.com/fwlink/?LinkId=120418)을 다운로드 하세요.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](securing-ado-net-applications.md)
- [SQL Server 보안](./sql/sql-server-security.md)
- [ADO.NET 개요](ado-net-overview.md)
