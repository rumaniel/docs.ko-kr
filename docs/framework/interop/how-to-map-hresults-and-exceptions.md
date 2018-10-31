---
title: '방법: HRESULT 및 예외 매핑'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- interoperation with unmanaged code, HRESULTs
- exceptions, HRESULTs
- interoperation with unmanaged code, exceptions
- HRESULTs
- COM interop, HRESULTs
- COM interop, exceptions
ms.assetid: 610b364b-2761-429d-9c4a-afbc3e66f1b9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0d5728de1140df51b9c725db0c8c80d21ace6deb
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49454475"
---
# <a name="how-to-map-hresults-and-exceptions"></a>방법: HRESULT 및 예외 매핑
COM 메서드는 HRESULT를 반환하여 오류를 보고하고, .NET 메서드는 예외를 throw하여 오류를 보고합니다. 런타임은 두 항목 간의 전환을 처리합니다. .NET Framework의 각 예외 클래스는 HRESULT에 매핑됩니다.  
  
 사용자 정의 예외 클래스는 적절한 모든 HRESULT를 지정할 수 있습니다. 이러한 예외 클래스는 예외 개체에서 **HResult** 필드를 설정하여 예외 생성 시 반환될 HRESULT를 동적으로 변경할 수 있습니다. 예외에 대한 추가 정보는 관리되지 않는 프로세스의 .NET 개체에서 구현되는 **IErrorInfo** 인터페이스를 통해 클라이언트에 제공됩니다.  
  
 **System.Exception**을 확장하는 클래스를 만들 경우 생성 중에 HRESULT 필드를 설정해야 합니다. 그러지 않으면 기본 클래스는 HRESULT 값을 할당합니다. 예외 생성자의 값을 제공하여 기존 HRESULT에 새 예외 클래스를 매핑할 수 있습니다.  
  
 스레드에 `IErrorInfo`가 있는 경우 런타임이 `HRESULT`를 무시할 수 있습니다.  `HRESULT` 및 `IErrorInfo`가 동일한 오류를 나타내지 않을 경우 이 동작이 발생할 수 있습니다.  
  
### <a name="to-create-a-new-exception-class-and-map-it-to-an-hresult"></a>새 예외 클래스를 만들고 HRESULT에 매핑하려면  
  
1.  다음 코드를 사용하여 `NoAccessException`이라는 새 예외 클래스를 만들고 HRESULT `E_ACCESSDENIED`에 매핑합니다.  
  
    ```cpp  
    Class NoAccessException : public ApplicationException  
    {  
        NoAccessException () {  
        HResult = E_ACCESSDENIED;   
    }  
    }  
    CMyClass::MethodThatThrows  
    {  
    throw new NoAccessException();  
    }  
    ```  
  
 관리 코드와 비관리 코드를 동시에 사용하는 프로그램(모든 프로그램 언어로 작성)이 나타날 수 있습니다. 예를 들어 다음 코드 예제의 사용자 지정 마샬러는 **Marshal.ThrowExceptionForHR(int HResult)** 메서드를 사용하여 특정 HRESULT 값이 포함된 예외를 throw합니다. 이 메서드는 HRESULT를 조회하고 해당하는 예외 형식을 생성합니다. 예를 들어 다음 코드 조각의 HRESULT는 **ArgumentException**을 생성합니다.  
  
```cpp  
CMyClass::MethodThatThrows  
{  
    Marshal.ThrowExceptionForHR(COR_E_ARGUMENT);  
}  
```  
  
 다음 표에서는 각 HRESULT와 .NET Framework에 있는 해당 예외 클래스 간의 전체 매핑을 제공합니다.  
  
|HRESULT|.NET 예외|  
|-------------|--------------------|  
|**MSEE_E_APPDOMAINUNLOADED**|**AppDomainUnloadedException**|  
|**COR_E_APPLICATION**|**ApplicationException**|  
|**COR_E_ARGUMENT 또는 E_INVALIDARG**|**ArgumentException**|  
|**COR_E_ARGUMENTOUTOFRANGE**|**ArgumentOutOfRangeException**|  
|**COR_E_ARITHMETIC 또는 ERROR_ARITHMETIC_OVERFLOW**|**ArithmeticException**|  
|**COR_E_ARRAYTYPEMISMATCH**|**ArrayTypeMismatchException**|  
|**COR_E_BADIMAGEFORMAT 또는 ERROR_BAD_FORMAT**|**BadImageFormatException**|  
|**COR_E_COMEMULATE_ERROR**|**COMEmulateException**|  
|**COR_E_CONTEXTMARSHAL**|**ContextMarshalException**|  
|**COR_E_CORE**|**CoreException**|  
|**NTE_FAIL**|**CryptographicException**|  
|**COR_E_DIRECTORYNOTFOUND 또는 ERROR_PATH_NOT_FOUND**|**DirectoryNotFoundException**|  
|**COR_E_DIVIDEBYZERO**|**DivideByZeroException**|  
|**COR_E_DUPLICATEWAITOBJECT**|**DuplicateWaitObjectException**|  
|**COR_E_ENDOFSTREAM**|**EndOfStreamException**|  
|**COR_E_TYPELOAD**|**EntryPointNotFoundException**|  
|**COR_E_EXCEPTION**|**Exception**|  
|**COR_E_EXECUTIONENGINE**|**ExecutionEngineException**|  
|**COR_E_FIELDACCESS**|**FieldAccessException**|  
|**COR_E_FILENOTFOUND 또는 ERROR_FILE_NOT_FOUND**|**FileNotFoundException**|  
|**COR_E_FORMAT**|**FormatException**|  
|**COR_E_INDEXOUTOFRANGE**|**IndexOutOfRangeException**|  
|**COR_E_INVALIDCAST 또는 E_NOINTERFACE**|**InvalidCastException**|  
|**COR_E_INVALIDCOMOBJECT**|**InvalidComObjectException**|  
|**COR_E_INVALIDFILTERCRITERIA**|**InvalidFilterCriteriaException**|  
|**COR_E_INVALIDOLEVARIANTTYPE**|**InvalidOleVariantTypeException**|  
|**COR_E_INVALIDOPERATION**|**InvalidOperationException**|  
|**COR_E_IO**|**IOException**|  
|**COR_E_MEMBERACCESS**|**AccessException**|  
|**COR_E_METHODACCESS**|**MethodAccessException**|  
|**COR_E_MISSINGFIELD**|**MissingFieldException**|  
|**COR_E_MISSINGMANIFESTRESOURCE**|**MissingManifestResourceException**|  
|**COR_E_MISSINGMEMBER**|**MissingMemberException**|  
|**COR_E_MISSINGMETHOD**|**MissingMethodException**|  
|**COR_E_MULTICASTNOTSUPPORTED**|**MulticastNotSupportedException**|  
|**COR_E_NOTFINITENUMBER**|**NotFiniteNumberException**|  
|**E_NOTIMPL**|**NotImplementedException**|  
|**COR_E_NOTSUPPORTED**|**NotSupportedException**|  
|**COR_E_NULLREFERENCE 또는 E_POINTER**|**NullReferenceException**|  
|**COR_E_OUTOFMEMORY 또는**<br /><br /> **E_OUTOFMEMORY**|**OutOfMemoryException**|  
|**COR_E_OVERFLOW**|**OverflowException**|  
|**COR_E_PATHTOOLONG 또는 ERROR_FILENAME_EXCED_RANGE**|**PathTooLongException**|  
|**COR_E_RANK**|**RankException**|  
|**COR_E_REFLECTIONTYPELOAD**|**ReflectionTypeLoadException**|  
|**COR_E_REMOTING**|**RemotingException**|  
|**COR_E_SAFEARRAYTYPEMISMATCH**|**SafeArrayTypeMismatchException**|  
|**COR_E_SECURITY**|**SecurityException**|  
|**COR_E_SERIALIZATION**|**SerializationException**|  
|**COR_E_STACKOVERFLOW 또는 ERROR_STACK_OVERFLOW**|**StackOverflowException**|  
|**COR_E_SYNCHRONIZATIONLOCK**|**SynchronizationLockException**|  
|**COR_E_SYSTEM**|**SystemException**|  
|**COR_E_TARGET**|**TargetException**|  
|**COR_E_TARGETINVOCATION**|**TargetInvocationException**|  
|**COR_E_TARGETPARAMCOUNT**|**TargetParameterCountException**|  
|**COR_E_THREADABORTED**|**ThreadAbortException**|  
|**COR_E_THREADINTERRUPTED**|**ThreadInterruptedException**|  
|**COR_E_THREADSTATE**|**ThreadStateException**|  
|**COR_E_THREADSTOP**|**ThreadStopException**|  
|**COR_E_TYPELOAD**|**TypeLoadException**|  
|**COR_E_TYPEINITIALIZATION**|**TypeInitializationException**|  
|**COR_E_VERIFICATION**|**VerificationException**|  
|**COR_E_WEAKREFERENCE**|**WeakReferenceException**|  
|**COR_E_VTABLECALLSNOTSUPPORTED**|**VTableCallsNotSupportedException**|  
|**모든 기타 HRESULT**|**COMException**|  
  
 확장된 오류 정보를 검색하려면 관리되는 클라이언트가 생성된 예외 개체의 필드를 검사해야 합니다. 예외 개체가 오류에 대한 유용한 정보를 제공하려면 COM 개체는 **IErrorInfo** 인터페이스를 구현해야 합니다. 런타임은 **IErrorInfo**에서 제공된 정보를 사용하여 예외 개체를 초기화합니다.  
  
 COM 개체가 **IErrorInfo**를 지원하지 않을 경우 런타임은 기본값으로 예외 개체를 초기화합니다. 다음 표에서는 예외 개체와 연결된 각 필드를 나열하고 COM 개체가 **IErrorInfo**를 지원할 경우 기본 정보의 소스를 식별합니다.  
  
 스레드에 `IErrorInfo`가 있는 경우 런타임이 `HRESULT`를 무시할 수 있습니다.  `HRESULT` 및 `IErrorInfo`가 동일한 오류를 나타내지 않을 경우 이 동작이 발생할 수 있습니다.  
  
|예외 필드|COM의 정보 소스|  
|---------------------|------------------------------------|  
|**ErrorCode**|호출에서 반환된 HRESULT.|  
|**HelpLink**|**IErrorInfo->HelpContext**가 0이 아니면 **IErrorInfo->GetHelpFile**와 “#” 및 **IErrorInfo->GetHelpContext**를 연결하여 문자열을 구성합니다. 이외의 경우에는 **IErrorInfo->GetHelpFile**에서 문자열이 반환됩니다.|  
|**InnerException**|항상 null 참조(Visual Basic의 경우 **Nothing**).|  
|**메시지**|**IErrorInfo->GetDescription**에서 반환된 문자열.|  
|**소스**|**IErrorInfo->GetSource**에서 반환된 문자열.|  
|**StackTrace**|스택 추적입니다.|  
|**TargetSite**|실패한 HRESULT를 반환한 메서드의 이름.|  
  
 **Message**, **Source** 및 **StackTrace**와 같은 예외 필드는 **StackOverflowException**에 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [고급 COM 상호 운용성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))  
 [예외](../../standard/exceptions/index.md)
