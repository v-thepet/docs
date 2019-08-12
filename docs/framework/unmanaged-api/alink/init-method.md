---
title: "Init Method"
ms.date: "03/30/2017"
api_name: 
  - "IALink.Init"
api_location: 
  - "alink.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "Init"
helpviewer_keywords: 
  - "Init method"
ms.assetid: e48b5c64-049f-4f93-ad87-d07ae9cd5845
topic_type: 
  - "apiref"
author: "mairaw"
ms.author: "mairaw"
---
# Init Method
Prepares objects implementing the [IALink Interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md) for use.  
  
## Syntax  
  
```cpp  
HRESULT Init(  
    IMetaDataDispenserEx* pDispenser,  
    IMetaDataError* pErrorHandler  
) PURE;  
```  
  
## Parameters  
 `pDispenser`  
 [IMetaDataDispenserEx Interface](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-interface.md) pointer to the metadata dispenser.  
  
 `pErrorHandler`  
 [IMetaDataError Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataerror-interface.md) pointer to an optional error handling interface.  
  
## Return Value  
 Returns S_OK if the method succeeds.  
  
## Requirements  
 Requires alink.h  
  
## See also

- [IALink Interface](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 Interface](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
