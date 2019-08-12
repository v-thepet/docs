---
title: "ICorDebugFrameEnum Interface"
ms.date: "03/30/2017"
api_name: 
  - "ICorDebugFrameEnum"
api_location: 
  - "mscordbi.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "ICorDebugFrameEnum"
helpviewer_keywords: 
  - "ICorDebugFrameEnum interface [.NET Framework debugging]"
ms.assetid: ee3f85d3-044e-46b8-945c-93ebfa5d9e91
topic_type: 
  - "apiref"
author: "rpetrusha"
ms.author: "ronpet"
---
# ICorDebugFrameEnum Interface

Implements ICorDebugEnum methods, and enumerates ICorDebugFrame arrays.  
  
## Methods  
  
|Method|Description|  
|------------|-----------------|  
|[Next Method](../../../../docs/framework/unmanaged-api/debugging/icordebugframeenum-next-method.md)|Gets the specified number of `ICorDebugFrame` instances from the enumeration, starting at the current position.|  
  
## Remarks  
  
> [!NOTE]
>  This interface does not support being called remotely, either cross-machine or cross-process.  
  
## Requirements  
 **Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Library:** CorGuids.lib  
  
 **.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## See also

- [Debugging Interfaces](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
