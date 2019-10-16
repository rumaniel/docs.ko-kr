---
title: 이진 Serialization
ms.date: 01/02/2018
helpviewer_keywords:
- binary serialization
- serialization, about serialization
- deserialization
- binary serialization, about serialization
- binary serialization, .net core serialization
- serialization, cross-framework
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
author: ViktorHofer
ms.author: mairaw
ms.openlocfilehash: 4a061b3128f8d0952f800be7173203b62f89c672
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65639103"
---
# <a name="binary-serialization"></a>이진 Serialization

serialization은 개체의 상태를 스토리지 매체에 스토리지하는 프로세스로 정의됩니다. 이 프로세스 도중 클래스가 포함된 어셈블리를 포함하여 개체의 public 및 private 필드와 클래스의 이름을 바이트의 스트림으로 변환한 다음 데이터 스트림에 씁니다. 그런 다음 개체가 deserialize되면 원본 개체의 정확한 복제본이 만들어집니다.

개체 지향적 환경에서 serialization 메커니즘을 구현할 때는 사용 편의성과 유연성 사이에서 균형을 조정해야 합니다. 프로세스를 충분히 제어할 수 있으면 프로세스의 많은 부분을 자동화할 수 있습니다. 예를 들어 단순한 이진 serialization로 충분하지 않거나 클래스의 필드를 serialize해야 하는 것으로 결정할 특별한 이유가 있는 상황이 발생할 수 있습니다. 다음 섹션에서는 .NET에서 제공하는 강력한 serialization 메커니즘을 살펴보고 프로세스를 필요에 따라 사용자 지정할 수 있는 몇 가지 중요한 기능을 강조합니다.

> [!NOTE]
> UTF-8 또는 UTF-7로 인코딩된 개체가 서로 다른 .NET Framework 버전을 사용하여 serialize되고 deserialize될 경우 해당 개체의 상태는 유지되지 않습니다.

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

이진 serialization은 기본적으로 개체 내에서 전용 멤버의 수정과 상태 변경을 허용하므로 공용 API 화면에서 작동하는 JSON.NET 등의 다른 serialization 프레임워크를 사용하는 것이 좋습니다.

## <a name="binary-serialization-in-net-core"></a>.NET Core의 이진 serialization

.NET Core는 형식의 하위 집합에서 이진 serialization을 지원합니다. 지원되는 형식 목록은 [직렬화 가능 형식 섹션](#serializable-types)에서 확인할 수 있습니다. 정의된 형식 집합은 .NET Framework 4.5.1 이상 버전 및 .NET Core 2.0 이상 버전 간에 직렬화 가능 형식으로 보장됩니다. Mono 등의 다른 .NET 구현은 공식적으로 지원되지 않지만 작동합니다.

### <a name="serializable-types"></a>직렬화 가능 형식

- <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderInternalCompilerException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.AccessViolationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.AggregateException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.AppDomainUnloadedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ApplicationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ArgumentException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ArgumentNullException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ArgumentOutOfRangeException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ArithmeticException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Array?displayProperty=nameWithType>
- <xref:System.ArraySegment%601?displayProperty=nameWithType>
- <xref:System.ArrayTypeMismatchException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.BadImageFormatException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Boolean?displayProperty=nameWithType>
- <xref:System.Byte?displayProperty=nameWithType>
- <xref:System.CannotUnloadAppDomainException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Char?displayProperty=nameWithType>
- <xref:System.Collections.ArrayList?displayProperty=nameWithType>
- <xref:System.Collections.BitArray?displayProperty=nameWithType>
- <xref:System.Collections.Comparer?displayProperty=nameWithType>
- <xref:System.Collections.DictionaryEntry?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Comparer%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.EqualityComparer%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.HashSet%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Collections.Generic.KeyValuePair%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.LinkedList%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.SortedList%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Stack%601?displayProperty=nameWithType>
- <xref:System.Collections.Hashtable?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType>
- <xref:System.Collections.Queue?displayProperty=nameWithType>
- <xref:System.Collections.SortedList?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.HybridDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.ListDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.StringCollection?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.StringDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Stack?displayProperty=nameWithType>
- `System.Collections.Generic.NonRandomizedStringEqualityComparer` (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ComponentModel.BindingList%601?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ComponentModel.Design.CheckoutException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ComponentModel.InvalidAsynchronousStateException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ComponentModel.LicenseException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용할 수 있는.NET Core로.NET Framework에서 직렬화는 지원 되지 않음)
- <xref:System.ComponentModel.WarningException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ComponentModel.Win32Exception?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Configuration.ConfigurationErrorsException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Configuration.ConfigurationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Configuration.Provider.ProviderException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Configuration.SettingsPropertyIsReadOnlyException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Configuration.SettingsPropertyNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Configuration.SettingsPropertyWrongTypeException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ContextMarshalException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DBNull?displayProperty=nameWithType> (.NET Core 2.0.2 이상 버전에서 사용 가능)
- <xref:System.Data.Common.DbException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.ConstraintException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.DBConcurrencyException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.DataException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.DataSet?displayProperty=nameWithType>
- <xref:System.Data.DataTable?displayProperty=nameWithType> (RemotingFormat SerializationFormat.Binary를 설정 하지 않은 경우에서 것만을 대체할 수.NET Core 2.1 이상.)
- <xref:System.Data.DeletedRowInaccessibleException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.DuplicateNameException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.EvaluateException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.InRowChangingEventException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.InvalidConstraintException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.InvalidExpressionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.MissingPrimaryKeyException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.NoNullAllowedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.Odbc.OdbcException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.OperationAbortedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.PropertyCollection?displayProperty=nameWithType>
- <xref:System.Data.ReadOnlyException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.RowNotInTableException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.SqlClient.SqlException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용할 수 있는.NET Core로.NET Framework에서 직렬화는 지원 되지 않음)
- <xref:System.Data.SqlTypes.SqlAlreadyFilledException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.SqlTypes.SqlBoolean?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlByte?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlDateTime?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlDouble?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlGuid?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlInt16?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlInt32?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlInt64?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlNotFilledException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.SqlTypes.SqlNullValueException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.SqlTypes.SqlString?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlTruncateException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.SqlTypes.SqlTypeException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.StrongTypingException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.SyntaxErrorException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Data.VersionNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DataMisalignedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DateTime?displayProperty=nameWithType>
- <xref:System.DateTimeOffset?displayProperty=nameWithType>
- <xref:System.Decimal?displayProperty=nameWithType>
- `System.Diagnostics.Contracts.ContractException` (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Diagnostics.Tracing.EventSourceException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.MultipleMatchesException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.NoMatchingPrincipalException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.PasswordException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.PrincipalException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.PrincipalExistsException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.PrincipalOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.AccountManagement.PrincipalServerDownException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectExistsException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryServerDownException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.ActiveDirectory.ForestTrustCollisionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.ActiveDirectory.SyncFromAllServersOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.DirectoryServicesCOMException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.Protocols.BerConversionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.Protocols.DirectoryException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.Protocols.DirectoryOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.Protocols.LdapException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DirectoryServices.Protocols.TlsOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DivideByZeroException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.DllNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Double?displayProperty=nameWithType>
- <xref:System.Drawing.Color?displayProperty=nameWithType>
- <xref:System.Drawing.Point?displayProperty=nameWithType>
- <xref:System.Drawing.PointF?displayProperty=nameWithType>
- <xref:System.Drawing.Rectangle?displayProperty=nameWithType>
- <xref:System.Drawing.RectangleF?displayProperty=nameWithType>
- <xref:System.Drawing.Size?displayProperty=nameWithType>
- <xref:System.Drawing.SizeF?displayProperty=nameWithType>
- <xref:System.DuplicateWaitObjectException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.EntryPointNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Enum?displayProperty=nameWithType>
- <xref:System.EventArgs?displayProperty=nameWithType> (.NET Core 2.0.6 이상 버전에서 사용 가능)
- <xref:System.Exception?displayProperty=nameWithType>
- <xref:System.ExecutionEngineException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.FieldAccessException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.FormatException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Globalization.CompareInfo?displayProperty=nameWithType>
- <xref:System.Globalization.CultureNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Globalization.SortVersion?displayProperty=nameWithType>
- <xref:System.Guid?displayProperty=nameWithType>
- `System.IO.Compression.ZLibException` (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.DriveNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.EndOfStreamException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.FileFormatException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.FileLoadException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.FileNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.IOException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.InternalBufferOverflowException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.InvalidDataException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.IsolatedStorage.IsolatedStorageException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IO.PathTooLongException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.IndexOutOfRangeException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.InsufficientExecutionStackException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.InsufficientMemoryException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Int16?displayProperty=nameWithType>
- <xref:System.Int32?displayProperty=nameWithType>
- <xref:System.Int64?displayProperty=nameWithType>
- <xref:System.IntPtr?displayProperty=nameWithType>
- <xref:System.InvalidCastException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.InvalidOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.InvalidProgramException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.InvalidTimeZoneException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.MemberAccessException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.MethodAccessException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.MissingFieldException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.MissingMemberException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.MissingMethodException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.MulticastNotSupportedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.Cookie?displayProperty=nameWithType>
- <xref:System.Net.CookieCollection?displayProperty=nameWithType>
- <xref:System.Net.CookieContainer?displayProperty=nameWithType>
- <xref:System.Net.CookieException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.HttpListenerException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.Mail.SmtpException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.Mail.SmtpFailedRecipientException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.Mail.SmtpFailedRecipientsException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.NetworkInformation.NetworkInformationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.NetworkInformation.PingException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.ProtocolViolationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.Sockets.SocketException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.WebException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Net.WebSockets.WebSocketException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.NotFiniteNumberException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.NotImplementedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.NotSupportedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.NullReferenceException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Numerics.BigInteger?displayProperty=nameWithType>
- <xref:System.Numerics.Complex?displayProperty=nameWithType>
- <xref:System.Object?displayProperty=nameWithType>
- <xref:System.ObjectDisposedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.OperationCanceledException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.OutOfMemoryException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.OverflowException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.PlatformNotSupportedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.RankException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Reflection.AmbiguousMatchException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Reflection.CustomAttributeFormatException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Reflection.InvalidFilterCriteriaException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Reflection.ReflectionTypeLoadException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용할 수 있는.NET Core로.NET Framework에서 직렬화는 지원 되지 않음)
- <xref:System.Reflection.TargetException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Reflection.TargetInvocationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Reflection.TargetParameterCountException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Resources.MissingManifestResourceException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Resources.MissingSatelliteAssemblyException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.CompilerServices.RuntimeWrappedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.COMException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.ExternalException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.InvalidComObjectException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.InvalidOleVariantTypeException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.MarshalDirectiveException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.SEHException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.Serialization.InvalidDataContractException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Runtime.Serialization.SerializationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.SByte?displayProperty=nameWithType>
- <xref:System.Security.AccessControl.PrivilegeNotHeldException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.Authentication.AuthenticationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.Authentication.InvalidCredentialException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.Cryptography.CryptographicException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.Cryptography.CryptographicUnexpectedOperationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- `System.Security.Cryptography.Xml.CryptoSignedXmlRecursionException` (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.HostProtectionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.Policy.PolicyException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.Principal.IdentityNotMappedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.SecurityException?displayProperty=nameWithType> (.NET Core 2.0.4 및 이상 버전에서는 제한 된 serialization 데이터에서 사용 가능)
- <xref:System.Security.VerificationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Security.XmlSyntaxException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ServiceProcess.TimeoutException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Single?displayProperty=nameWithType>
- <xref:System.StackOverflowException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.StringComparer?displayProperty=nameWithType>
- <xref:System.SystemException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Text.DecoderFallbackException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Text.EncoderFallbackException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Text.RegularExpressions.RegexMatchTimeoutException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Text.StringBuilder?displayProperty=nameWithType>
- <xref:System.Threading.AbandonedMutexException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.BarrierPostPhaseException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.LockRecursionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.SemaphoreFullException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.SynchronizationLockException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.Tasks.TaskCanceledException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.Tasks.TaskSchedulerException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.ThreadInterruptedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.ThreadStartException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.ThreadStateException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Threading.WaitHandleCannotBeOpenedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.TimeSpan?displayProperty=nameWithType>
- <xref:System.TimeZoneInfo.AdjustmentRule?displayProperty=nameWithType>
- <xref:System.TimeZoneInfo?displayProperty=nameWithType>
- <xref:System.TimeZoneNotFoundException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.TimeoutException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Transactions.TransactionAbortedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Transactions.TransactionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Transactions.TransactionInDoubtException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Transactions.TransactionManagerCommunicationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Transactions.TransactionPromotionException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Tuple?displayProperty=nameWithType>
- <xref:System.TypeAccessException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.TypeInitializationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.TypeLoadException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.TypeUnloadedException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.UInt16?displayProperty=nameWithType>
- <xref:System.UInt32?displayProperty=nameWithType>
- <xref:System.UInt64?displayProperty=nameWithType>
- <xref:System.UIntPtr?displayProperty=nameWithType>
- <xref:System.UnauthorizedAccessException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Uri?displayProperty=nameWithType>
- <xref:System.UriFormatException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.ValueTuple?displayProperty=nameWithType> (.NET Framework 4.7 및 이전 버전에서 직렬화 가능 하지)
- <xref:System.ValueType?displayProperty=nameWithType>
- <xref:System.Version?displayProperty=nameWithType>
- <xref:System.WeakReference%601?displayProperty=nameWithType>
- <xref:System.WeakReference?displayProperty=nameWithType>
- <xref:System.Xml.Schema.XmlSchemaException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Xml.Schema.XmlSchemaInferenceException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Xml.Schema.XmlSchemaValidationException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Xml.XPath.XPathException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Xml.XmlException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Xml.Xsl.XsltCompileException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)
- <xref:System.Xml.Xsl.XsltException?displayProperty=nameWithType> (.NET Core 2.0.4 이상 버전에서 사용 가능)

## <a name="in-this-section"></a>단원 내용

- [Serialization 개념](../../../docs/standard/serialization/serialization-concepts.md)\
serialization이 유용하게 사용되는 두 가지 경우, 즉 스토리지에 데이터를 유지할 경우와 애플리케이션 도메인에 개체를 전달할 경우에 대해 설명합니다.

- [기본 serialization](../../../docs/standard/serialization/basic-serialization.md)\
이진 및 SOAP 포맷터를 사용하여 개체를 serialize하는 방법을 설명합니다.

- [선택적 Serialization](../../../docs/standard/serialization/selective-serialization.md)\
클래스의 일부 멤버가 serialize되는 것을 방지하는 방법을 설명합니다.

- [사용자 지정 Serialization](../../../docs/standard/serialization/custom-serialization.md)\
<xref:System.Runtime.Serialization.ISerializable> 인터페이스를 사용하여 클래스에 대한 serialization을 사용자 지정하는 방법을 설명합니다.

- [Serialization 프로세스의 단계](../../../docs/standard/serialization/steps-in-the-serialization-process.md)\
포맷터에서 <xref:System.Runtime.Serialization.Formatter.Serialize%2A> 메서드가 호출될 때 serialization이 수행하는 작업을 설명합니다.

- [버전 독립적 Serialization](../../../docs/standard/serialization/version-tolerant-serialization.md)\
애플리케이션에서 예외가 throw되는 것을 방지하면서 시간 경과에 따라 수정할 수 있는 serialize 가능 형식을 만드는 방법을 설명합니다.

- [Serialization 지침](../../../docs/standard/serialization/serialization-guidelines.md)\
개체를 serialize하는 시점을 결정하기 위한 일반 지침을 제공합니다.

## <a name="reference"></a>참조

- <xref:System.Runtime.Serialization>\
개체를 serialize하거나 deserialize하는 데 사용할 수 있는 클래스를 포함합니다.

## <a name="related-sections"></a>관련 단원

- [XML 및 SOAP Serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md)\
공용 언어 런타임에 포함된 XML serialization 메커니즘을 설명합니다.

- [보안 및 Serialization](../../../docs/framework/misc/security-and-serialization.md)\
serialization을 수행하는 코드를 쓸 때 따를 보안 코딩 지침을 설명합니다.

- [.NET remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))\
.NET Framework에서 원격 통신에 사용할 수 있는 다양한 통신 방법에 대해 설명합니다.

- [ASP.NET 및 XML 웹 서비스 클라이언트를 사용 하 여 만든 XML Web Services](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))\
ASP.NET을 사용하여 만든 XML Web services를 프로그래밍하는 방법을 설명하는 항목을 제공합니다.
