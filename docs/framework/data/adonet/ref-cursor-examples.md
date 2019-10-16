---
title: REF CURSOR 예제
ms.date: 03/30/2017
ms.assetid: c257da03-c6c9-4cf8-b591-b7740a962c40
ms.openlocfilehash: 24830452e6d1ab11605ffa88a925fbc55c80b9bf
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794712"
---
# <a name="ref-cursor-examples"></a>REF CURSOR 예제
REF CURSOR 예제는 REF CURSOR를 사용하는 다음 세 개의 Microsoft Visual Basic 예제로 구성됩니다.  
  
|예제|설명|  
|------------|-----------------|  
|[OracleDataReader의 REF CURSOR 매개 변수](ref-cursor-parameters-in-an-oracledatareader.md)|이 예제에서는 REF CURSOR 매개 변수를 반환하는 PL/SQL 저장 프로시저를 실행하고 값을 <xref:System.Data.OracleClient.OracleDataReader>로 읽습니다.|  
|[OracleDataReader를 사용하여 여러 REF CURSOR에서 데이터 검색](retrieving-data-from-multiple-ref-cursors.md)|이 예에서는 두 개의 REF CURSOR 매개 변수를 반환 하는 PL/SQL 저장 프로시저를 실행 하 고 **OracleDataReader**를 사용 하 여 값을 읽습니다.|  
|[하나 이상의 REF CURSOR를 사용하여 데이터 세트 채우기](filling-a-dataset-using-one-or-more-ref-cursors.md)|이 예제에서는 두 개의 REF CURSOR 매개 변수를 반환하는 PL/SQL 저장 프로시저를 실행하고 반환되는 행으로 <xref:System.Data.DataSet>을 채웁니다.|  
  
 이러한 예제를 사용하려면 Oracle 테이블을 만들거나 PL/SQL 패키지 및 패키지 본문을 만들어야 합니다.  
  
## <a name="creating-the-oracle-tables"></a>Oracle 테이블 만들기  
 이 예제에서는 Oracle Scott/Tiger 스키마에 정의된 테이블을 사용합니다. Oracle Scott/Tiger 스키마는 대부분의 Oracle 설치와 함께 제공됩니다. 이 스키마가 없으면 {OracleHome}\rdbms\admin\scott.sql에 있는 SQL 명령 파일을 사용하여 이러한 예제에서 사용되는 테이블과 인덱스를 만들 수 있습니다.  
  
## <a name="creating-the-oracle-package-and-package-body"></a>Oracle 패키지 및 패키지 본문 만들기  
 이러한 예제를 사용하려면 서버에 다음 PL/SQL 패키지 및 패키지 본문이 있어야 합니다. Oracle 서버에 다음과 같은 Oracle 패키지를 만듭니다.  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS   
    TYPE T_CURSOR IS REF CURSOR;   
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,   
                               IO_CURSOR IN OUT T_CURSOR);   
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
                                DEPTCURSOR OUT T_CURSOR);  
END CURSPKG;  
/   
```  
  
 Oracle 서버에 다음 Oracle 패키지 본문을 만듭니다.  
  
```sql
CREATE OR REPLACE PACKAGE BODY CURSPKG AS  
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,  
                               IO_CURSOR IN OUT T_CURSOR)  
    IS   
        V_CURSOR T_CURSOR;   
    BEGIN   
        IF N_EMPNO <> 0   
        THEN  
             OPEN V_CURSOR FOR   
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME   
                  FROM EMP, DEPT   
                  WHERE EMP.DEPTNO = DEPT.DEPTNO   
                  AND EMP.EMPNO = N_EMPNO;  
  
        ELSE   
             OPEN V_CURSOR FOR   
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME   
                  FROM EMP, DEPT   
                  WHERE EMP.DEPTNO = DEPT.DEPTNO;  
  
        END IF;  
        IO_CURSOR := V_CURSOR;   
    END OPEN_ONE_CURSOR;   
  
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,  
                                DEPTCURSOR OUT T_CURSOR)  
    IS   
        V_CURSOR1 T_CURSOR;   
        V_CURSOR2 T_CURSOR;   
    BEGIN   
        OPEN V_CURSOR1 FOR SELECT * FROM EMP;  
        OPEN V_CURSOR2 FOR SELECT * FROM DEPT;  
        EMPCURSOR  := V_CURSOR1;   
        DEPTCURSOR := V_CURSOR2;   
    END OPEN_TWO_CURSORS;   
END CURSPKG;  
/  
```  
  
## <a name="see-also"></a>참고자료

- [Oracle REF CURSOR](oracle-ref-cursors.md)
- [ADO.NET 개요](ado-net-overview.md)
