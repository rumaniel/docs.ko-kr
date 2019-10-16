---
title: Mgmtclassgen.exe(강력하게 형식화된 관리 클래스 생성기)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CIM types
- Management Strongly Typed Class Generator
- WMI class
- Mgmtclassgen.exe
- early-bound managed classes
ms.assetid: 02ce6699-49b5-4a0b-b0d5-1003c491232e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b40cb5d5d629ea7a3cb019be42b42a1072572311
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044380"
---
# <a name="mgmtclassgenexe-management-strongly-typed-class-generator"></a>Mgmtclassgen.exe(강력하게 형식화된 관리 클래스 생성기)
강력하게 형식화된 관리 클래스 생성기 도구를 사용하면 지정된 WMI(Windows Management Instrumentation) 클래스에 대해 초기 바인딩 관리되는 클래스를 신속하게 생성할 수 있습니다. 생성된 클래스는 WMI 클래스의 인스턴스에 액세스할 때 작성해야 하는 코드를 단순화합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
mgmtclassgen   
WMIClass [options]   
```  
  
|인수|설명|  
|--------------|-----------------|  
|*WMIClass*|초기 바인딩 관리되는 클래스를 생성할 Windows Management Instrumentation 클래스|  
  
|옵션|설명|  
|------------|-----------------|  
|**/l**  *language*|초기 바인딩 관리되는 클래스를 생성할 때 사용하는 언어를 지정합니다. 언어 인수로 **CS**(C#; default), **VB**(Visual Basic), **MC**(C++) 또는 **JS**(JScript)를 지정할 수 있습니다.|  
|**/m**  *machine*|WMI 클래스가 있는 연결할 컴퓨터를 지정합니다. 기본값은 로컬 컴퓨터입니다.|  
|**/n**  *path*|WMI 클래스가 포함된 WMI 네임스페이스의 경로를 지정합니다. 이 옵션을 지정하지 않으면 도구에서 기본 **Root\cimv2** 네임스페이스에 *WMIClass*의 코드를 생성합니다.|  
|**/o**  *classnamespace*|관리 코드 클래스를 생성할 .NET 네임스페이스를 지정합니다. 이 옵션을 지정하지 않으면 도구에서 WMI 네임스페이스와 스키마 접두사를 사용하여 네임스페이스를 생성합니다. 스키마 접두사는 밑줄 앞에 오는 클래스 이름의 일부분입니다. 예를 들어 **Root\cimv2** 네임스페이스에 있는 **Win32_OperatingSystem** 클래스의 경우 도구에서는 **ROOT.CIMV2.Win32**에 클래스를 생성합니다.|  
|**/p**  *filepath*|생성된 코드를 저장할 파일의 경로를 지정합니다. 이 옵션을 지정하지 않으면 도구에서 현재 디렉터리에 파일을 만듭니다. *WMIClass* 인수를 사용하여 클래스 및 클래스를 생성한 파일의 이름을 지정합니다. 클래스 이름과 파일 이름은 *WMIClass*의 이름과 동일합니다. *WMIClass*에 밑줄이 있는 경우 도구에서는 밑줄 뒤에 나오는 클래스 이름 일부를 사용합니다. 예를 들어 *WMIClass* 이름이 **Win32_LogicalDisk** 형식인 경우 생성된 클래스와 파일의 이름은 "logicaldisk"입니다. 파일이 이미 있는 경우 도구에서는 기존 파일을 덮어씁니다.|  
|**/pw**  *password*|**/m** 옵션으로 지정된 컴퓨터에 로그온할 때 사용할 암호를 지정합니다.|  
|**/u**  *user name*|**/m** 옵션으로 지정된 컴퓨터에 로그온할 때 사용할 사용자 이름을 지정합니다.|  
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
## <a name="remarks"></a>설명  
 Mgmtclassgen.exe는 <xref:System.Management.ManagementClass.GetStronglyTypedClassCode%2A?displayProperty=nameWithType> 메서드를 사용합니다. 따라서 사용자 지정 코드 공급자를 사용하여 C#, Visual Basic 및 JScript 이외의 관리되는 언어로 코드를 생성할 수 있습니다.  
  
 생성된 클래스는 생성 대상인 스키마에 바인딩됩니다. 기본 스키마가 변경되는 경우 스키마의 변경 사항을 클래스에 반영하려면 클래스를 다시 생성해야 합니다.  
  
 다음 표에서는 WMI CIM(Common Information Model) 형식이 생성된 클래스의 데이터 형식에 어떻게 매핑되는지를 보여 줍니다.  
  
|CIM 형식|생성된 클래스의 데이터 형식|  
|--------------|--------------------------------------|  
|CIM_SINT8|**SByte**|  
|CIM_UINT8|**Byte**|  
|CIM_SINT16|**Int16**|  
|CIM_UINT16|**UInt16**|  
|CIM_SINT32|**Int32**|  
|SIM_UINT32|**UInt32**|  
|CIM_SINT64|**Int64**|  
|CIM_UINT64|**UInt64**|  
|CIM_REAL32|**Single**|  
|CIM_REAL64|**double**|  
|CIM_BOOLEAN|**Boolean**|  
|CIM_String|**String**|  
|CIM_DATETIME|**DateTime** 또는 **TimeSpan**|  
|CIM_REFERENCE|**ManagementPath**|  
|CIM_CHAR16|**Char**|  
|CIM_OBJECT|**ManagementBaseObject**|  
|CIM_IUNKNOWN|**개체**|  
|CIM_ARRAY|위에 명시된 개체의 배열|  
  
 WMI 클래스를 생성할 때는 다음 사항에 유의하십시오.  
  
- 표준 공용 속성이나 메서드의 이름이 기존 속성이나 메서드의 이름과 같을 수 있습니다. 이런 경우에는 도구에서 이름 충돌을 방지하기 위해 생성된 클래스에 있는 속성이나 메서드의 이름을 변경합니다.  
  
- 생성된 클래스에 있는 속성이나 메서드의 이름이 대상 프로그래밍 언어의 키워드일 수 있습니다. 이런 경우에는 도구에서 이름 충돌을 방지하기 위해 생성된 클래스에 있는 속성이나 메서드의 이름을 변경합니다.  
  
- WMI에서 한정자에는 클래스, 인스턴스, 속성 또는 메서드를 설명하는 정보가 포함됩니다. WMI에서는 **Read**, **Write**, **Key** 등의 표준 한정자를 사용하여 생성된 클래스의 속성을 설명합니다. 예를 들어 **Read** 한정자로 한정되는 속성은 생성된 클래스에서 속성 **get** 접근자를 통해서만 정의됩니다. **Read** 한정자로 표시된 속성은 읽기 전용이므로 **set** 접근자가 정의되지 않습니다.  
  
- 숫자 속성은 지정된 허용 값으로만 설정될 수 있음을 나타내기 위해 **Values** 및 **ValueMaps** 한정자를 사용하여 한정될 수 있습니다. 열거형이 이러한 **Values** 및 **ValueMaps**와 함께 생성되며 속성은 이 열거형으로 매핑됩니다.  
  
- WMI에서는 singleton이라는 용어를 사용하여 인스턴스를 하나만 갖는 클래스를 설명합니다. 따라서 singleton 클래스의 매개 변수가 없는 생성자는 클래스를 해당 클래스의 유일한 인스턴스로 초기화합니다.  
  
- WMI 클래스에는 개체인 속성이 있을 수 있습니다. 이러한 유형의 WMI 클래스에 대한 강력한 형식의 클래스를 생성하는 경우 포함된 개체 속성의 형식에 대한 강력한 형식의 클래스를 생성할 것을 고려해야 합니다. 이렇게 하면 포함된 개체에 강력한 형식을 사용하여 액세스할 수 있습니다. 생성된 코드는 포함된 개체의 형식을 감지하지 못할 수도 있습니다. 이런 경우 이 문제를 알려 주는 주석이 생성된 코드 안에 작성됩니다. 따라서 생성된 코드를 수정하여 생성된 다른 클래스에 속성을 입력할 수 있습니다.  
  
- WMI에서는 CIM_DATETIME 데이터 형식의 데이터 값을 특정 날짜 및 시간이나 시간 간격으로 나타낼 수 있습니다. 데이터 값이 날짜 및 시간을 나타내는 경우 생성된 클래스의 데이터 형식은 **DateTime**이 되고, 데이터 값이 시간 간격을 나타내는 경우 생성된 클래스의 데이터 형식은 **TimeSpan**이 됩니다.  
  
 또는 Visual Studio .NET의 Server Explorer Management Extension을 사용하여 강력한 형식의 클래스를 생성할 수 있습니다.  
  
 WMI에 대한 자세한 내용은 Platform SDK 설명서의 **WMI(Windows Management Instrumentation)** 항목을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 명령은 C# 코드로 **Root\cimv2** 네임스페이스의 **Win32_LogicalDisk** WMI 클래스에 대한 관리되는 클래스를 생성합니다. 도구에서 관리되는 클래스를 **ROOT.CIMV2.Win32** 네임스페이스의 c:\disk.cs에 소스 파일로 작성합니다.  
  
```console  
mgmtclassgen Win32_LogicalDisk /n root\cimv2 /l CS /p c:\disk.cs  
```  
  
 다음 코드 예제에서는 생성된 클래스를 프로그래밍 방식으로 사용하는 방법을 보여 줍니다. 첫째, 클래스의 인스턴스가 열거되고 경로가 인쇄됩니다. 그런 다음, 초기화할 생성된 클래스의 인스턴스는 WMI의 인스턴스를 사용하여 만들어집니다. `Process`는 **Win32_Process**에 대해 생성된 클래스이고 `LogicalDisk`는 **Root\cimv2** 네임스페이스에서 **Win32_LogicalDisk**에 대해 생성된 클래스입니다.  
  
```vb  
Imports System  
Imports System.Management  
Imports ROOT.CIMV2.Win32  
  
Public Class App     
   Public Shared Sub Main()        
      ' Enumerate instances of the Win32_process.  
      ' Print the Name property of the instance.  
      Dim ps As Process     
      For Each ps In  Process.GetInstances()  
         Console.WriteLine(ps.Name)  
      Next ps  
  
      ' Initialize the instance of LogicalDisk with  
      ' the WMI instance pointing to logical drive d:.  
      Dim dskD As New LogicalDisk(New _  
         ManagementPath("win32_LogicalDisk.DeviceId=""d:"""))  
      Console.WriteLine(dskD.Caption)  
   End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Management;  
using ROOT.CIMV2.Win32;  
  
public class App  
{  
   public static void Main()  
   {  
      // Enumerate instances of the Win32_process.  
      // Print the Name property of the instance.  
      foreach(Process ps in Process.GetInstances())  
      {  
         Console.WriteLine(ps.Name);  
      }  
  
      // Initialize the instance of LogicalDisk with  
      // the WMI instance pointing to logical drive d:.  
      LogicalDisk dskD = new LogicalDisk(new ManagementPath(  
        "win32_LogicalDisk.DeviceId=\"d:\""));  
      Console.WriteLine(dskD.Caption);  
   }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Management>
- <xref:System.Management.ManagementClass.GetStronglyTypedClassCode%2A?displayProperty=nameWithType>
- <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType>
- [도구](index.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
