---
title: "CustomDumpItem Structure"
ms.date: "03/30/2017"
api_name: 
  - "CustomDumpItem"
api_location: 
  - "mscoree.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "CustomDumpItem"
helpviewer_keywords: 
  - "CustomDumpItem structure [.NET Framework hosting]"
ms.assetid: fd9085ff-7beb-4c38-97f0-037cd8ba4f65
topic_type: 
  - "apiref"
author: "rpetrusha"
ms.author: "ronpet"
---
# CustomDumpItem Structure
Describes an item to be added to a custom dump in error reporting.  
  
## Syntax  
  
```cpp  
struct {  
    ECustomDumpItemKind itemKind;   
    union {  
        UINT_PTR pReserved;  
    }  
} CustomDumpItem;  
```  
  
## Members  
  
|Member|Description|  
|------------|-----------------|  
|`itemKind`|An [ECustomDumpItemKind](../../../../docs/framework/unmanaged-api/hosting/ecustomdumpitemkind-enumeration.md) value that indicates the kind of item to be added.|  
|`pReserved`|Not currently used. Any items added to the union must be no larger than pointer size. If a `struct` is required, you must allocate it separately and point to it.|  
  
## Remarks  
 [ICLRErrorReportingManager::BeginCustomDump](../../../../docs/framework/unmanaged-api/hosting/iclrerrorreportingmanager-begincustomdump-method.md) takes a parameter of type `CustomDumpItem`.  
  
## Requirements  
 **Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MSCorEE.idl  
  
 **Library:** Included as a resource in MSCorEE.dll  
  
 **.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## See also

- [Hosting Structures](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)
