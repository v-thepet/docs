---
title: "ICorDebugDebugEvent::GetEventKind Method"
ms.date: "03/30/2017"
ms.assetid: c37aaceb-c948-46bd-a943-08be4cbb76f4
author: "rpetrusha"
ms.author: "ronpet"
---
# ICorDebugDebugEvent::GetEventKind Method
Indicates what kind of event this `ICorDebugDebugEvent` object represents.  
  
## Syntax  
  
```cpp  
HRESULT GetEventKind(  
    [out]CorDebugDebugEventKind *pDebugEventKind  
);  
```  
  
## Parameters  
 pDebugEventKind  
 A pointer to a [CorDebugDebugEventKind](../../../../docs/framework/unmanaged-api/debugging/cordebugdebugeventkind-enumeration.md) enumeration member that indicates the type of event.  
  
## Remarks  
 Based on the value of `pDebugEventKind`, you can call `QueryInterface` to get a more precise debug event interface that has additional data.  
  
> [!NOTE]
>  This method is available with .NET Native only.  
  
## Requirements  
 **Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Library:** CorGuids.lib  
  
 **.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## See also

- [ICorDebugDebugEvent Interface](../../../../docs/framework/unmanaged-api/debugging/icordebugdebugevent-interface.md)
- [Debugging Interfaces](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
