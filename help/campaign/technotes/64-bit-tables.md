---
title: Adobe Campaign Web User interface
description: Discover Adobe Campaign Web User interface
badge: label="LIMITED AVAILABILITY" type="Informative" url="campaign-standard-migration-home.md" tooltip="Restricted to Campaign Standard migrated users"
---

# 64-bit tables {#64-bit tables}

In order to facilite the transition from Campaign Standard to Campaign v8, several tables have been changed from 32 to 64 bits. Indeed, Campaign Standard supports 64-bit PK in several out-of-the-box schemas, whereas Campaign v8 supports 32-bit PK in most schemas. 

## Limitations

* This technical implementation only applies to customers migrating from Campaign Standard. 
* Schema and broadlog extentions are not supported. They will remain in 32 bits. 
* Be aware that logs related to deliveries send to technical users will not be available in Campaign v8. 
* Only PostgreSQL is suppored.

## Migrated schemas

Here is the list of extended schemas and their modified attributes. 

| Header | Another header |
|--- |--- |--- |
| row 1 | row 1 column 2 | 
| row 2 | row 2 column 2 | 


