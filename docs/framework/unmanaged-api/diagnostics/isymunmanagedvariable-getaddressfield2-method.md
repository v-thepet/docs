---
title: "ISymUnmanagedVariable::GetAddressField2 Method"
ms.date: "03/30/2017"
api_name: 
  - "ISymUnmanagedVariable.GetAddressField2"
api_location: 
  - "diasymreader.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "ISymUnmanagedVariable::GetAddressField2"
helpviewer_keywords: 
  - "GetAddressField2 method [.NET Framework debugging]"
  - "ISymUnmanagedVariable::GetAddressField2 method [.NET Framework debugging]"
ms.assetid: 1f25b294-72b6-4882-a49b-6c9d364b6008
topic_type: 
  - "apiref"
author: "mairaw"
ms.author: "mairaw"
---
# ISymUnmanagedVariable::GetAddressField2 Method
Gets the second address field for this variable. Its meaning depends on the kind of address.  
  
## Syntax  
  
```cpp  
HRESULT GetAddressField2(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## Parameters  
 `pRetVal`  
 [out] A pointer to a `ULONG32` that receives the second address field.  
  
## Return Value  
 S_OK if the method succeeds; otherwise, E_FAIL or some other error code.  
  
## Requirements  
 **Header:** CorSym.idl, CorSym.h  
  
## See also

- [ISymUnmanagedVariable Interface](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-interface.md)
- [GetAddressField1 Method](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddressfield1-method.md)
- [GetAddressField3 Method](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddressfield3-method.md)
- [GetAddressKind Method](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddresskind-method.md)
