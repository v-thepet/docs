---
title: "ImportTypes Method"
ms.date: "03/30/2017"
api_name: 
  - "IALink.ImportTypes"
api_location: 
  - "alink.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "ImportTypes"
helpviewer_keywords: 
  - "ImportTypes method"
ms.assetid: 351d4b4c-c939-486d-9471-51914a55f471
topic_type: 
  - "apiref"
author: "mairaw"
ms.author: "mairaw"
---
# ImportTypes Method
Initiates the importing of types from each scope imported via [ImportFile Method](../../../../docs/framework/unmanaged-api/alink/importfile-method.md).  
  
## Syntax  
  
```cpp  
HRESULT ImportTypes(  
    mdAssembly AssemblyID,  
    mdToken FileToken,  
    DWORD dwScope,  
    HALINKENUM* phEnum,  
    IMetaDataImport** ppImportScope,  
    DWORD* pdwCountOfTypes  
) PURE;  
```  
  
## Parameters  
 `AssemblyID`  
 ID of the assembly to import to.  
  
 `FileToken`  
 ID of the file to import from.  
  
 `dwScope`  
 Zero-based scope to import.  
  
 `phEnum`  
 Receives enumerator handle for the types in this scope.  
  
 `ppImportScope`  
 Optionally receives [IMetaDataImport Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) interface.  
  
 `pdwCountOfTypes`  
 Optionally receives count of types in the indicated scope.  
  
## Return Value  
 Returns S_OK if the method succeeds.  
  
## Requirements  
 Requires alink.h  
  
## See also

- [IALink Interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 Interface](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
