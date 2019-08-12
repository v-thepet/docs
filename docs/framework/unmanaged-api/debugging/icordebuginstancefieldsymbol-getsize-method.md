---
title: "ICorDebugInstanceFieldSymbol::GetSize Method"
ms.date: "03/30/2017"
ms.assetid: a4af1e3b-6a9f-4855-95ba-5317565c8e2b
author: "rpetrusha"
ms.author: "ronpet"
---
# ICorDebugInstanceFieldSymbol::GetSize Method
Gets the size in bytes of the instance field.  
  
## Syntax  
  
```cpp  
HRESULT GetSize(  
   [out] ULONG32 *pcbSize  
);  
```  
  
## Parameters  
 `pcbSize`  
 [out] A pointer to length of the field.  
  
## Remarks  
  
> [!NOTE]
>  This method is available with .NET Native only.  
  
## Requirements  
 **Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Library:** CorGuids.lib  
  
 **.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## See also

- [ICorDebugInstanceFieldSymbol Interface](../../../../docs/framework/unmanaged-api/debugging/icordebuginstancefieldsymbol-interface.md)
- [Debugging Interfaces](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
