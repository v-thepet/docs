---
title: "SetAssemblyFile2 Method"
ms.date: "03/30/2017"
api_name: 
  - "IALink2.SetAssemblyFile2"
api_location: 
  - "alink.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "SetAssemblyFile2"
helpviewer_keywords: 
  - "SetAssemblyFile2 method"
ms.assetid: eedb9125-1ef1-4000-abfc-7de86e5a1f17
topic_type: 
  - "apiref"
author: "mairaw"
ms.author: "mairaw"
---
# SetAssemblyFile2 Method
Sets the name of and options for a new assembly. Do not call this method when you produce unbound modules.  
  
## Syntax  
  
```cpp  
HRESULT SetAssemblyFile2(  
    LPCWSTR pszFilename,  
    IMetaDataEmit2* pEmitter,  
    AssemblyFlags   afFlags,  
    mdAssembly* pAssemblyID  
) PURE;  
```  
  
## Parameters  
 `pszFilename`  
 Name of manifest file.  
  
 `pEmitter`  
 [IMetaDataEmit2 Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md) interface for this file.  
  
 `afFlags`  
 Options represented by [AssemblyFlags Enumeration](../../../../docs/framework/unmanaged-api/metadata/assemblyflags-enumeration.md).  
  
 `pAssemblyID`  
 Receives unique ID for the assembly being constructed.  
  
## Return Value  
 Returns S_OK if the method succeeds.  
  
## Requirements  
 Requires alink.h.  
  
## See also

- [IALink2 Interface](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [IALink Interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
