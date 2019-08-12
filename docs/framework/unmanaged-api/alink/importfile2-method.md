---
title: "ImportFile2 Method"
ms.date: "03/30/2017"
api_name: 
  - "IALink.ImportFile2"
api_location: 
  - "alink.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "ImportFile2"
helpviewer_keywords: 
  - "ImportFile2 method"
ms.assetid: 9a6be861-c260-4a35-acea-3372ea515a0f
topic_type: 
  - "apiref"
author: "mairaw"
ms.author: "mairaw"
---
# ImportFile2 Method
Imports assemblies and unbound modules. This method is like [ImportFile Method](../../../../docs/framework/unmanaged-api/alink/importfile-method.md), but works even if the file being imported does not exist on disk.  
  
## Syntax  
  
```cpp  
HRESULT ImportFile2(  
    LPCWSTR         pszFilename,  
    LPCWSTR         pszTargetName,  
    IMetaDataAssemblyImport* pAssemblyScopeIn,  
    BOOL            fSmartImport,  
    mdToken*        pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD*          pdwCountOfScopes  
) PURE;  
```  
  
## Parameters  
 `pszFilename`  
 Name of file to be imported.  
  
 `pszTargetName`  
 Optional output file name that can be used to rename the file as it is linked into the assembly.  
  
 `pAssemblyScopeIn`  
 Optional scope [IMetaDataAssemblyImport Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md) interface.  
  
 `fSmartImport`  
 If TRUE, ImportTypes is used, otherwise importing must be performed manually.  
  
 `pImportToken`  
 Receives the ID for the file or assembly.  
  
 `ppAssemblyScope`  
 Receives the [IMetaDataAssemblyImport Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md) interface. NULL if the file is not an assembly.  
  
 `pdwCountOfScopes`  
 Receives the found of files and/or scopes imported.  
  
## Return Value  
 Returns S_OK if the method succeeds.  
  
## Requirements  
 Requires alink.h.  
  
## See also

- [IALink Interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 Interface](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
