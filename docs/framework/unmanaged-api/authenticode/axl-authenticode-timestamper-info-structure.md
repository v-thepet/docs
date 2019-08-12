---
title: "AXL_AUTHENTICODE_TIMESTAMPER_INFO Structure"
ms.date: "03/30/2017"
ms.assetid: 89e41a81-0f41-45ad-8f20-a120e4ff24fb
author: "rpetrusha"
ms.author: "ronpet"
---
# AXL_AUTHENTICODE_TIMESTAMPER_INFO Structure
Defines the Authenticode time stamper information.  
  
## Syntax  
  
```cpp  
typedef struct _AXL_AUTHENTICODE_SIGNER_INFO {  
    DWORD cbSize;  
    HRESULT dwError;  
    ALG_ID algHash;  
    FILETIME ftTimestamp  
    PCCERT_CHAIN_CONTEXT pChainContext;  
} AXL_AUTHENTICODE_TIMESTAMPER_INFO, * PAXL_AUTHENTICODE_TIMESTAMPER_INFO;  
```  
  
## Members  
  
|Member|Description|  
|------------|-----------------|  
|`cbSize`|The size of this structure.|  
|`dwError`|The error code.|  
|`algHash`|The hash algorithm.|  
|`ftTimestamp`|The time of the time stamp.|  
|`pChainContext`|The time stamper’s chain context.  See the [CERT_CONTEXT](/windows/desktop/api/wincrypt/ns-wincrypt-_cert_context) structure.|  
  
## See also

- [Authenticode](../../../../docs/framework/unmanaged-api/authenticode/index.md)
