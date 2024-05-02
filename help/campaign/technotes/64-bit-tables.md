---
title: Adobe Campaign Web User interface
description: 64-bit tables
badge: label="LIMITED AVAILABILITY" type="Informative" url="../campaign-standard-migration-home.md" tooltip="Restricted to Campaign Standard migrated users"
---

# 64-bit tables {#64-bit-tables}

In order to facilite the transition from Campaign Standard to Campaign v8, several tables have been changed from 32 to 64 bits. Indeed, Campaign Standard supports 64-bit PK in several out-of-the-box schemas, whereas Campaign v8 supports 32-bit PK in most schemas. 

## Limitations

* This technical implementation only applies to customers migrating from Campaign Standard. 
* Schema and broadlog extentions are not supported. They will remain in 32 bits. 
* Be aware that logs related to deliveries sent to technical users will not be available in Campaign v8. 
* Only PostgreSQL is suppored.

## Modified schemas

Here is the list of schemas changed to 64 bits and their modified attributes. 

| Schema name | Atribute name |
|--- |--- |
| nms:broadLogRcp | id | 
| nms:trackingLogRcp | id | 
| nms:excludeLogRcp | id | 
| nms:broadLogVisitor | id | 
| nms:trackingLogVisitor | id | 
| nms:propositionRcp | interactionId | 
| nms:propositionVisitor | interactionId | 
| nms:webTrackingLog | id | 
| nms:tmpBroadcast | message-id | 
| nms:tmpMarketingPressure | message-id | 
| nms:tmpBroadcastExclusion | message-id | 
| nms:tmpBroadcastPaper | message-id | 
| nms:broadLogAppSubRcp | id | 
| nms:trackingLogAppSubRcp | id | 
| nms:excludeLogAppSubRcp | id | 
| nms:webEvent | broadLogSrc-id, broadLogRemkt-id | 
| nms:broadLogMid | mktBroadLogId | 
| nms:mirrorPageSearch | remoteMessageId | 


