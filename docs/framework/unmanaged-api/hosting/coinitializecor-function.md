---
title: "CoInitializeCor Function"
ms.date: "03/30/2017"
api_name: 
  - "CoInitializeCor"
api_location: 
  - "mscoree.dll"
  - "mscorsvr.dll"
api_type: 
  - "DLLExport"
f1_keywords: 
  - "CoInitializeCor"
helpviewer_keywords: 
  - "CoInitializeCor function [.NET Framework hosting]"
ms.assetid: 9b9079fb-579e-4141-b3f0-791072dd40dc
topic_type: 
  - "apiref"
author: "rpetrusha"
ms.author: "ronpet"
---
# CoInitializeCor Function
`CoInitializeCor` is obsolete.  
  
## Syntax  
  
```cpp  
STDAPI CoInitializeCor (  
    DWORD fFlags  
);  
```  
  
## Remarks  
 To initialize the common language runtime, use either [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) or [CorBindToCurrentRuntime](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md).  
  
## Requirements  
 **Header:** Cor.h  
  
## See also

- [Metadata Global Static Functions](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
