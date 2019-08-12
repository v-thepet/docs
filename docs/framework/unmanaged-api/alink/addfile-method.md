---
title: "AddFile Method"
ms.date: "03/30/2017"
api_name: 
  - "IALink.AddFile"
  - "AddFile"
api_location: 
  - "alink.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "AddFile"
helpviewer_keywords: 
  - "AddFile method"
ms.assetid: 9e707abb-f905-4568-9356-12aa21d1b11c
topic_type: 
  - "apiref"
author: "mairaw"
ms.author: "mairaw"
---
# AddFile Method
Adds files to the assembly. Can also be used to create unbound modules.  
  
## Syntax  
  
```cpp  
HRESULT AddFile(  
    mdAssembly      AssemblyID,  
    LPCWSTR         pszFilename,  
    DWORD           dwFlags,  
    IMetaDataEmit*  pEmitter,  
    mdFile*         pFileToken  
) PURE;  
```  
  
## Parameters  
 `AssemblyID`  
 Unique ID of the assembly to be augmented.  
  
 `pszFilename`  
 Fully qualified name of file to be added.  
  
 `dwFlags`  
 COM+ FileDef flags such as `ffContainsNoMetaData` and `ffWriteable`. `dwFlags` is passed to [DefineFile Method](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-definefile-method.md).  
  
 `pEmitter`  
 [IMetaDataEmit Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md) interface to be used to emit metadata, if necessary.  
  
 `pFileToken`  
 Pointer to where the unique ID of the added file will be stored.  
  
## Return Value  
 Returns S_OK if the method succeeds.  
  
## Requirements  
 Requires alink.h.  
  
## See also

- [IALink Interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 Interface](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
