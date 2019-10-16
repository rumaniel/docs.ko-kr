---
title: '방법: 외부 파일로 개체 모델 생성'
ms.date: 03/30/2017
ms.assetid: 2496fa06-3df4-4ecb-86c4-70a49ea08565
ms.openlocfilehash: 915c02de55211efa24a4aa9f21ddc2c7e60fa41a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002744"
---
# <a name="how-to-generate-the-object-model-as-an-external-file"></a>방법: 외부 파일로 개체 모델 생성
특성 기반 매핑을 사용하는 대신 SQLMetal 명령줄 도구를 사용하여 개체 모델을 외부 XML 파일로 생성할 수 있습니다. 자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요. 외부 XML 매핑 파일을 사용하면 코드를 간단하게 표시할 수 있습니다. 또한 애플리케이션의 이진 파일을 다시 컴파일할 필요 없이 외부 파일을 수정하여 동작을 변경할 수 있습니다. 자세한 내용은 [외부 매핑](external-mapping.md)을 참조 하세요.  
  
> [!NOTE]
> 개체 관계형 디자이너는 외부 매핑 파일의 생성을 지원 하지 않습니다.  
  
## <a name="example"></a>예제  
 다음 명령에서는 Northwind 샘플 데이터베이스에서 외부 매핑 파일을 생성합니다.  
  
```console  
sqlmetal /server:myserver /database:northwind /map:externalfile.xml  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 외부 매핑 파일의 일부로, Northwind 샘플 데이터베이스의 Customers 테이블에 대한 매핑을 보여 줍니다. 이 발췌는 **/map** 옵션과 함께 SQLMetal을 실행 하 여 생성 되었습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Database xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Name="northwnd">  
  <Table Name="Customers">  
    <Type Name=".Customer">  
      <Column Name="CustomerID" Member="CustomerID" Storage="_CustomerID" DbType="NChar(5) NOT NULL" CanBeNull="False" IsPrimaryKey="True" />  
      <Column Name="CompanyName" Member="CompanyName" Storage="_CompanyName" DbType="NVarChar(40) NOT NULL" CanBeNull="False" />  
      <Column Name="ContactName" Member="ContactName" Storage="_ContactName" DbType="NVarChar(30)" />  
      <Column Name="ContactTitle" Member="ContactTitle" Storage="_ContactTitle" DbType="NVarChar(30)" />  
      <Column Name="Address" Member="Address" Storage="_Address" DbType="NVarChar(60)" />  
      <Column Name="City" Member="City" Storage="_City" DbType="NVarChar(15)" />  
      <Column Name="Region" Member="Region" Storage="_Region" DbType="NVarChar(15)" />  
      <Column Name="PostalCode" Member="PostalCode" Storage="_PostalCode" DbType="NVarChar(10)" />  
      <Column Name="Country" Member="Country" Storage="_Country" DbType="NVarChar(15)" />  
      <Column Name="Phone" Member="Phone" Storage="_Phone" DbType="NVarChar(24)" />  
      <Column Name="Fax" Member="Fax" Storage="_Fax" DbType="NVarChar(24)" />  
      <Association Name="FK_CustomerCustomerDemo_Customers" Member="CustomerCustomerDemos" Storage="_CustomerCustomerDemos" ThisKey="CustomerID" OtherTable="CustomerCustomerDemo" OtherKey="CustomerID" DeleteRule="NO ACTION" />  
      <Association Name="FK_Orders_Customers" Member="Orders" Storage="_Orders" ThisKey="CustomerID" OtherTable="Orders" OtherKey="CustomerID" DeleteRule="NO ACTION" />  
    </Type>  
  </Table>  
</Database>  
```  
  
## <a name="see-also"></a>참조

- [개체 모델 만들기](creating-the-object-model.md)
- [외부 매핑](external-mapping.md)
- [방법: Visual Basic 또는 C#에서 개체 모델 생성](how-to-generate-the-object-model-in-visual-basic-or-csharp.md)
