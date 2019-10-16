---
title: ODBC 스키마 컬렉션
ms.date: 03/30/2017
ms.assetid: 1bb126a5-ceec-4649-a4bc-8aa19e801046
ms.openlocfilehash: f0240e99d2420b0956d3c144f837b39e094bb78a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794726"
---
# <a name="odbc-schema-collections"></a>ODBC 스키마 컬렉션

이 단원에서는 Microsoft SQL Server, Oracle 및 Microsoft Jet용 ODBC 드라이버에서 지원하는 스키마 컬렉션에 대해 설명합니다.

## <a name="microsoft-sql-server-odbc-driver"></a>Microsoft SQL Server ODBC Driver

Microsoft SQL Server ODBC 드라이버는 공통 스키마 컬렉션 외에도 다음과 같은 특정 스키마 컬렉션을 지원 합니다.

- 테이블

- 인덱스

- 열

- 절차

- ProcedureColumns

- ProcedureParameters

- 뷰

### <a name="tables-and-views"></a>Tables 및 Views

|ColumnName|DataType|
|----------------|--------------|
|TABLE_CAT|문자열|
|TABLE_SCHEM|String|
|TABLE_NAME|문자열|
|TABLE_TYPE|String|
|REMARKS|String|

### <a name="indexes"></a>인덱스

|ColumnName|DataType|
|----------------|--------------|
|TABLE_CAT|String|
|TABLE_SCHEM|문자열|
|TABLE_NAME|String|
|NON_UNIQUE|Int16|
|INDEX_QUALIFIER|문자열|
|INDEX_NAME|문자열|
|TYPE|Int16|
|ORDINAL_POSITION|Int16|
|COLUMN_NAME|문자열|
|ASC_OR_DESC|String|
|CARDINALITY|Int32|
|PAGES|Int32|
|FILTER_CONDITION|문자열|
|SS_TYPE_SCHEMA|String|
|SS_DATA_TYPE|Byte|

### <a name="columns"></a>열

|ColumnName|DataType|
|----------------|--------------|
|TABLE_CAT|String|
|TABLE_SCHEM|String|
|TABLE_NAME|String|
|COLUMN_NAME|String|
|DATA_TYPE|Int16|
|TYPE_NAME|문자열|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|COLUMN_DEF|String|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|문자열|
|SS_TYPE_CATALOG|String|
|SS_TYPE_SCHEMA|문자열|
|SS_DATA_TYPE|Byte|

### <a name="procedures"></a>절차

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_CAT|String|
|PROCEDURE_SCHEM|문자열|
|PROCEDURE_NAME|문자열|
|NUM_INPUT_PARAMS|Int32|
|NUM_OUTPUT_PARAMS|Int32|
|NUM_RESULT_SETS|Int32|
|REMARKS|문자열|
|PROCEDURE_TYPE|Int16|

### <a name="procedurecolumns"></a>ProcedureColumns

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_CAT|String|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|문자열|
|COLUMN_NAME|문자열|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|COLUMN_DEF|String|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|
|SS_TYPE_CATALOG|String|
|SS_TYPE_SCHEMA|문자열|
|SS_DATA_TYPE|Byte|

### <a name="procedureparameters"></a>ProcedureParameters

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_CAT|문자열|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|COLUMN_DEF|문자열|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|
|SS_TYPE_CATALOG|문자열|
|SS_TYPE_SCHEMA|String|
|SS_DATA_TYPE|Byte|

## <a name="microsoft-oracle-odbc-driver"></a>Microsoft Oracle ODBC Driver

Microsoft SQL Server Oracle ODBC 드라이버는 공통 스키마 컬렉션 외에도 다음과 같은 특정 스키마 컬렉션을 지원 합니다.

- 테이블

- 열

- 절차

- ProcedureColumns

- ProcedureParameters

- 뷰

- 인덱스

### <a name="tables-and-views"></a>Tables 및 Views

|ColumnName|DataType|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|문자열|
|TABLE_NAME|String|
|TABLE_TYPE|문자열|
|REMARKS|String|

### <a name="columns"></a>열

|ColumnName|DataType|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|String|
|TABLE_NAME|String|
|COLUMN_NAME|String|
|DATA_TYPE|Int16|
|TYPE_NAME|문자열|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|ORDINAL_POSITION|Int32|

### <a name="procedures"></a>절차

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_QUALIFIER|문자열|
|PROCEDURE_OWNER|문자열|
|PROCEDURE_NAME|String|
|NUM_INPUT_PARAMS|Int16|
|NUM_OUTPUT_PARAMS|Int16|
|NUM_RESULT_SETS|Int16|
|REMARKS|String|
|PROCEDURE_TYPE|Int16|

### <a name="procedurecolumns"></a>ProcedureColumns

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_QUALIFIER|문자열|
|PROCEDURE_OWNER|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|문자열|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|문자열|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|OVERLOAD|Int32|
|ORDINAL_POSITION|Int32|

## <a name="microsoft-jet-odbc-driver"></a>Microsoft Jet ODBC Driver

Microsoft Jet ODBC Driver                                             .

- 테이블

- 인덱스

- 열

- 절차

- ProcedureColumns

- ProcedureParameters

- 뷰

### <a name="tables-and-views"></a>Tables 및 Views

|ColumnName|DataType|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|String|
|TABLE_NAME|문자열|
|TABLE_TYPE|문자열|
|REMARKS|문자열|

### <a name="columns"></a>열

|ColumnName|DataType|
|----------------|--------------|
|TABLE_QUALIFIER|문자열|
|TABLE_OWNER|String|
|TABLE_NAME|String|
|COLUMN_NAME|String|
|DATA_TYPE|Int16|
|TYPE_NAME|문자열|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|ORDINAL_POSITION|Int32|

### <a name="procedures"></a>절차

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_QUALIFIER|문자열|
|PROCEDURE_OWNER|문자열|
|PROCEDURE_NAME|String|
|NUM_INPUT_PARAMS|Int16|
|NUM_OUTPUT_PARAMS|Int16|
|NUM_RESULT_SETS|Int16|
|REMARKS|String|
|PROCEDURE_TYPE|Int16|

### <a name="procedurecolumns"></a>ProcedureColumns

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_QUALIFIER|String|
|PROCEDURE_OWNER|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|OVERLOAD|Int32|
|ORDINAL_POSITION|Int32|

### <a name="procedureparameters"></a>ProcedureParameters

|ColumnName|DataType|
|----------------|--------------|
|PROCEDURE_CAT|문자열|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|문자열|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|REMARKS|String|
|COLUMN_DEF|문자열|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|

## <a name="see-also"></a>참고자료

- [ADO.NET 개요](ado-net-overview.md)
