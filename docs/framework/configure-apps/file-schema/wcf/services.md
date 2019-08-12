---
title: "<services>"
ms.date: "03/30/2017"
ms.assetid: 80d76ba9-2058-48ad-9b91-5e4be7e5c113
---
# \<services>
Services are defined in the `services` section of the configuration file. Each service has its own `service` configuration section.  
  
 \<system.ServiceModel>  
  
## Syntax  
  
```xml  
<system.serviceModel>
  <services>
    <service>
    </service>
  </services>
</system.serviceModel>
```  
  
## Attributes and Elements  
 The following sections describe attributes, child elements, and parent elements.  
  
### Attributes  
 None  
  
### Child Elements  
  
|Element|Description|  
|-------------|-----------------|  
|[\<service>](../../../../../docs/framework/configure-apps/file-schema/wcf/service.md)|Define the service contract, behavior, and endpoints of the particular service.|  
  
### Parent Elements  
  
|Element|Description|  
|-------------|-----------------|  
|[\<system.serviceModel>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)|The root element of all Windows Communication Foundation (WCF) configuration elements.|  
  
## See also

- <xref:System.ServiceModel.Configuration.ServicesSection>
