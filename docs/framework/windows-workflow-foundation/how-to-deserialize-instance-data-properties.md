---
title: '방법: 인스턴스 데이터 속성 Deserialize'
ms.date: 03/30/2017
ms.assetid: b13a3508-1b97-4359-b336-03d85fa23bc4
ms.openlocfilehash: e037d5f8d0b221aa0eb8fdc6eceabf6efb2dc387
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989630"
---
# <a name="how-to-deserialize-instance-data-properties"></a>방법: 인스턴스 데이터 속성 Deserialize
경우에 따라서는 유지되고 있는 워크플로 인스턴스의 상태를 사용자나 워크플로 관리자가 수동으로 조사하고 싶을 수 있습니다. <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>에서는 다음과 같은 네 개의 열이 포함된 인스턴스 테이블에 대한 뷰를 제공합니다.  
  
- ReadWritePrimitiveDataProperties  
  
- WriteOnlyPrimitiveDataProperties  
  
- ReadWriteComplexDataProperties  
  
- WriteOnlyComplexDataProperties  
  
 기본 데이터 속성은 .NET Framework 형식이 "common" (예: Int32 및 String)로 간주 되는 반면, 복합 데이터 속성은 다른 모든 형식을 참조 하는 속성을 나타냅니다. 기본 형식의 정확한 열거형은 이 코드 샘플의 뒷부분에 나와 있습니다.  
  
 읽기/쓰기 속성은 인스턴스를 로드했을 때 워크플로 런타임으로 다시 반환되는 속성을 가리킵니다. WriteOnly 속성은 데이터베이스에 쓴 다음 다시 읽지 않는 속성입니다.  
  
 이 샘플에서는 기본 데이터 속성을 deserialize하는 데 사용할 수 있는 코드를 제공합니다. ReadWritePrimitiveDataProperties 또는 WriteOnlyPrimitiveDataProperties 열에서 읽은 바이트 배열을 지정 하는 경우이 코드는 BLOB (binary large object) <xref:System.Collections.Generic.Dictionary%602> 를 각 키 값이 있는 > 명령의 xname 형식의 \<로 변환 합니다. pair는 속성 이름 및 해당 값을 나타냅니다.  
  
 복합 데이터 속성을 deserialize하는 방법은 이 샘플에서 보여 주지 않습니다. 이와 같은 작업은 아직 지원되지 않습니다.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.IO.Compression;  
using System.Xml.Linq;  
using System.Xml;  
using System.Globalization;  
using System.Data.SqlClient;  
  
namespace PropertyReader  
{  
    class Program  
    {  
        const string ConnectionString = @"Data Source=localhost;Initial Catalog=Persistence;Integrated Security=True;Asynchronous Processing=True";  
        static void Main(string[] args)  
        {  
            string queryString = "SELECT TOP 10 * FROM [System.Activities.DurableInstancing].[Instances]";  
  
            using (SqlConnection connection =  
                       new SqlConnection(ConnectionString))  
            {  
                SqlCommand command =  
                    new SqlCommand(queryString, connection);  
                connection.Open();  
  
                SqlDataReader reader = command.ExecuteReader();  
  
                byte encodingOption;  
  
                while (reader.Read())  
                {  
                    if (reader["ReadWritePrimitiveDataProperties"] != DBNull.Value)  
                    {  
                        encodingOption = (byte)reader["EncodingOption"];  
                        Console.WriteLine("Printing the ReadWritePrimitiveDataProperties of the instance with Id:" + reader["InstanceId"]);  
                        foreach (KeyValuePair<XName, object> pair in (Dictionary<XName, object>)ReadDataProperties((byte[])reader["ReadWritePrimitiveDataProperties"], encodingOption))  
                        {  
                            Console.WriteLine("{0}, {1}" , pair.Key, pair.Value);  
                        }  
                        Console.WriteLine();  
                    }  
                    if (reader["WriteOnlyPrimitiveDataProperties"] != DBNull.Value)  
                    {  
                        encodingOption = (byte)reader["EncodingOption"];  
                        Console.WriteLine("Printing the WriteOnlyPrimitiveDataProperties of the instance with Id:" + reader["InstanceId"]);  
                        foreach (KeyValuePair<XName, object> pair in (Dictionary<XName, object>)ReadDataProperties((byte[])reader["WriteOnlyPrimitiveDataProperties"], encodingOption))  
                        {  
                            Console.WriteLine("{0}, {1}", pair.Key, pair.Value);  
                        }  
                        Console.WriteLine();  
                    }  
                }  
  
                // Call Close when done reading.  
                reader.Close();  
            }  
  
            Console.ReadLine();  
  
        }  
  
        static Dictionary<XName, object> ReadDataProperties(byte[] serializedDataProperties, byte encodingOption)  
        {  
            if (serializedDataProperties != null)  
            {  
                Dictionary<XName, object> propertyBag = new Dictionary<XName, object>();  
                bool isCompressed = (encodingOption == 1);  
  
                using (MemoryStream memoryStream = new MemoryStream(serializedDataProperties))  
                {  
                    // if the instance state is compressed using GZip algorithm  
                    if (isCompressed)  
                    {  
                        // decompress the data using the GZip   
                        using (GZipStream stream = new GZipStream(memoryStream, CompressionMode.Decompress))  
                        {  
                            // create an XmlReader object and pass it on to the helper method ReadPrimitiveDataProperties  
                            using (XmlReader reader = XmlDictionaryReader.CreateBinaryReader(stream, XmlDictionaryReaderQuotas.Max))  
                            {  
                                // invoke the helper method  
                                ReadPrimitiveDataProperties(reader, propertyBag);  
                            }  
                        }  
                    }  
                    else  
                    {  
                        // if the instance data is not compressed   
                        // create an XmlReader object and pass it on to the helper method ReadPrimitiveDataProperties  
                        using (XmlReader reader = XmlDictionaryReader.CreateBinaryReader(memoryStream, XmlDictionaryReaderQuotas.Max))  
                        {  
                            // invoke the helper method  
                            ReadPrimitiveDataProperties(reader, propertyBag);  
                        }  
                    }  
                    return propertyBag;  
                }  
            }  
  
            return null;  
        }  
  
        // reads the primitive data properties from the XML stream  
        // invoked by the ReadDataProperties method  
        static void ReadPrimitiveDataProperties(XmlReader reader, Dictionary<XName, object> propertyBag)  
        {  
            const string xmlElementName = "Property";  
  
            if (reader.ReadToDescendant(xmlElementName))  
            {  
                do  
                {  
                    // get the name of the property  
                    reader.MoveToFirstAttribute();  
                    string propertyName = reader.Value;  
  
                    // get the type of the property  
                    reader.MoveToNextAttribute();  
                    PrimitiveType type = (PrimitiveType)Int32.Parse(reader.Value, CultureInfo.InvariantCulture);  
  
                    // get the value of the property  
                    reader.MoveToNextAttribute();  
                    object propertyValue = ConvertStringToNativeType(reader.Value, type);  
  
                    // add the name and value of the property to the property bag  
                    propertyBag.Add(propertyName, propertyValue);  
                }  
  
                while (reader.ReadToNextSibling(xmlElementName));  
            }  
        }  
  
        // invoked by the ReadPrimitiveDataProperties method  
        // Given a property value as parsed from an XML attribute, and the .NET Type of the Property, recreates the actual property value  
        // (e.g. Given a property value of "1" and a PrimitiveType of Int32, this method will return an object of type Int32 with value 1)  
        static object ConvertStringToNativeType(string value, PrimitiveType type)  
        {  
            switch (type)  
            {  
                case PrimitiveType.Bool:  
                    return XmlConvert.ToBoolean(value);  
                case PrimitiveType.Byte:  
                    return XmlConvert.ToByte(value);  
                case PrimitiveType.Char:  
                    return XmlConvert.ToChar(value);  
                case PrimitiveType.DateTime:  
                    return XmlConvert.ToDateTime(value, XmlDateTimeSerializationMode.RoundtripKind);  
                case PrimitiveType.DateTimeOffset:  
                    return XmlConvert.ToDateTimeOffset(value);  
                case PrimitiveType.Decimal:  
                    return XmlConvert.ToDecimal(value);  
                case PrimitiveType.Double:  
                    return XmlConvert.ToDouble(value);  
                case PrimitiveType.Float:  
                    return float.Parse(value, CultureInfo.InvariantCulture);  
                case PrimitiveType.Guid:  
                    return XmlConvert.ToGuid(value);  
                case PrimitiveType.Int:  
                    return XmlConvert.ToInt32(value);  
                case PrimitiveType.Long:  
                    return XmlConvert.ToInt64(value);  
                case PrimitiveType.SByte:  
                    return XmlConvert.ToSByte(value);  
                case PrimitiveType.Short:  
                    return XmlConvert.ToInt16(value);  
                case PrimitiveType.String:  
                    return value;  
                case PrimitiveType.TimeSpan:  
                    return XmlConvert.ToTimeSpan(value);  
                case PrimitiveType.Type:  
                    return Type.GetType(value);  
                case PrimitiveType.UInt:  
                    return XmlConvert.ToUInt32(value);  
                case PrimitiveType.ULong:  
                    return XmlConvert.ToUInt64(value);  
                case PrimitiveType.Uri:  
                    return new Uri(value);  
                case PrimitiveType.UShort:  
                    return XmlConvert.ToUInt16(value);  
                case PrimitiveType.XmlQualifiedName:  
                    return new XmlQualifiedName(value);  
                case PrimitiveType.Null:  
                case PrimitiveType.Unavailable:  
                default:  
                    return null;  
            }  
        }  
        // .NET Types which SQL Workflow Instance Store considers to be Primitive. Any other .NET type not listed in this enumeration is a "Complex" property.  
        enum PrimitiveType  
        {  
            Bool = 0,  
            Byte,  
            Char,  
            DateTime,  
            DateTimeOffset,  
            Decimal,  
            Double,  
            Float,  
            Guid,  
            Int,  
            Null,  
            Long,  
            SByte,  
            Short,  
            String,  
            TimeSpan,  
            Type,  
            UInt,  
            ULong,  
            Uri,  
            UShort,  
            XmlQualifiedName,  
            Unavailable = 99  
        }  
    }  
}  
```
