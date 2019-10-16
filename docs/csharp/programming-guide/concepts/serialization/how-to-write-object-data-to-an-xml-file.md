---
title: '방법: XML 파일에 개체 데이터 쓰기(C#)'
ms.date: 07/20/2015
ms.assetid: 7681eb98-703d-4005-a369-26a7bca0f894
ms.openlocfilehash: 5da79d68bf7e1c955cb6edededb3914bd9c898e5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590691"
---
# <a name="how-to-write-object-data-to-an-xml-file-c"></a>방법: XML 파일에 개체 데이터 쓰기(C#)
이 예제에서는 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 XML 파일에 클래스의 개체를 씁니다.  
  
## <a name="example"></a>예  
  
```csharp  
public class XMLWrite  
{  
  
   static void Main(string[] args)  
    {  
        WriteXML();  
    }  
  
    public class Book  
    {  
        public String title;   
    }  
  
    public static void WriteXML()  
    {  
        Book overview = new Book();  
        overview.title = "Serialization Overview";  
        System.Xml.Serialization.XmlSerializer writer =   
            new System.Xml.Serialization.XmlSerializer(typeof(Book));  
  
        var path = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments) + "//SerializationOverview.xml";  
        System.IO.FileStream file = System.IO.File.Create(path);  
  
        writer.Serialize(file, overview);  
        file.Close();  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 직렬화되는 클래스에는 매개 변수가 없는 공용 생성자가 있어야 합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- serialize되는 클래스에 매개 변수가 없는 public 생성자가 없는 경우  
  
- 파일이 있지만 읽기 전용인 경우(<xref:System.IO.IOException>)  
  
- 경로가 너무 긴 경우(<xref:System.IO.PathTooLongException>)  
  
- 디스크가 꽉 찬 경우(<xref:System.IO.IOException>)  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 이 예제에서는 파일이 아직 없는 경우 새 파일을 만듭니다. 애플리케이션에서 파일을 만들어야 하는 경우 해당 애플리케이션에 폴더에 대한 `Create` 권한이 있어야 합니다. 파일이 이미 있는 경우 애플리케이션에 더 낮은 권한인 `Write` 권한만 있으면 됩니다. 가능한 경우 배포하는 동안 파일을 만들고, 폴더에 대한 `Create` 권한 대신 단일 파일에 대해 `Read` 권한만 부여하는 것이 더 안전합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.StreamWriter>
- [방법: XML 파일에서 개체 데이터 읽기(C#)](./how-to-read-object-data-from-an-xml-file.md)
- [Serialization(C#)](./index.md)
