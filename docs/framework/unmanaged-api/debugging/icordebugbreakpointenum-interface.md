---
title: "ICorDebugBreakpointEnum Interface"
ms.date: "03/30/2017"
api_name: 
  - "ICorDebugBreakpointEnum"
api_location: 
  - "mscordbi.dll"
api_type: 
  - "COM"
f1_keywords: 
  - "ICorDebugBreakpointEnum"
helpviewer_keywords: 
  - "ICorDebugBreakpointEnum interface [.NET Framework debugging]"
ms.assetid: 4c6f4f6e-52cc-402e-881b-7b8526544c90
topic_type: 
  - "apiref"
author: "rpetrusha"
ms.author: "ronpet"
---
# ICorDebugBreakpointEnum Interface

Implements ICorDebugEnum methods, and enumerates ICorDebugBreakpoint arrays.  
  
## Methods  
  
|Method|Description|  
|------------|-----------------|  
|[Next Method](../../../../docs/framework/unmanaged-api/debugging/icordebugbreakpointenum-next-method.md)|Gets the specified number of `ICorDebugBreakpoint` instances from the enumeration, starting at the current position.|  
  
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
