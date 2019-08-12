---
title: "<defaultPorts>"
ms.date: "03/30/2017"
ms.assetid: 725d4ee5-bd46-4f0e-9c20-30ba75d6eb2c
---
# \<defaultPorts>
A collection of default ports listing the default communications endpoints that the client application listens to.  
  
\<system.ServiceModel>  
\<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<useRequestHeadersForMetadataAddress>  
\<defaultPorts>  
  
## Syntax  
  
```xml  
<useRequestHeadersForMetadataAddress>
  <defaultPorts>
    <add scheme="http"
         port="integer" />
  </defaultPorts>
</useRequestHeadersForMetadataAddress>
```  
  
## Attributes and Elements  
 The following sections describe attributes, child elements, and parent elements.  
  
### Attributes  
 None.  
  
### Child Elements  
  
|Element|Description|  
|-------------|-----------------|  
|[\<add> of \<defaultPorts>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-defaultports.md)|A default communications endpoint that the client application listens to.|  
  
### Parent Elements  
  
|Element|Description|  
|-------------|-----------------|  
|[\<useRequestHeadersForMetadataAddress>](../../../../../docs/framework/configure-apps/file-schema/wcf/userequestheadersformetadataaddress.md)|A list of default ports.|  
  
## See also

- <xref:System.ServiceModel.Configuration.DefaultPortElementCollection>
