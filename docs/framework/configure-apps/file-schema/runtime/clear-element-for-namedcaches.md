---
title: "<clear> Element for <namedCaches>"
ms.date: "03/30/2017"
helpviewer_keywords: 
  - "<clear> element for <namedCaches>"
  - "clear element for <namedCaches>"
ms.assetid: ea01a858-65da-4348-800f-5e3df59d4d79
---
# \<clear> Element for \<namedCaches>
Clears all `namedCache` entries in the `namedCaches` collection for a memory cache.  
  
 \<system.runtime.caching>  
\<memoryCache>  
\<namedCaches>  
\<add>  
  
## Syntax  
  
```xml  
<namedCaches>  
    <clear name="Default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## Type  
 `Type`  
  
## Attributes and Elements  
 The following sections describe attributes, child elements, and parent elements.  
  
### Attributes  
 `None`  
  
### Child Elements  
 `None`  
  
### Parent Elements  
  
|Element|Description|  
|-------------|-----------------|  
|[\<namedCaches>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|Contains a collection of configuration settings for the named <xref:System.Runtime.Caching.MemoryCache> instances.|  
  
## Remarks  
 The `clear` element clears all `namedCache` entries in the named cache collection for a memory cache. You can use the `clear` element before you use the `add` element to add a new named cache entry in order to be certain there are no other named caches in the collection.  
  
## See also

- [\<namedCaches> Element (Cache Settings)](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)
