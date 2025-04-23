**🗓️ Date:** `2025-04-23` | **🕒 Time:** `14:11:11` | **📅 Day:** `Wednesday`

---

# Introduction

Extended attributes are used for storing implementation-specific data about an object.
1. Identity
2. Link
3. Bundle
4. ManagedAttribute
5. Application
6. CertificationItem

Number of extended attributes that can be defined is virtually unlimited (constrained only by database limits).

Extended attributes can be designed as searchable; in that case, the attribute is stored in its own separate column in the database instead of in a CLOB (Character Large Object).

By default, IIQ is pre-configured with a small number of placeholder extended attributes (extended1, extended2, etc.)
* These generic placeholder attributes are limited to a max of 20 per object type.
* IIQ also supports defining named extended attributes which created names columns in the database.
* Attributes marked as searchable can be used in reporting, filtering operations, in querying for objects in scripts and rules.

# Defining Searchable Attributes

Process for defining searchable extended attributes:
1. Decide how many searchable extended attributes are needed and whether they will be indexed, and define them in the appropriate Hibernate mapping file (\*Extended.hbm.xml.file).
2. Run the iiq schema command to generate a table-creation DDL script that includes the defined extended columns.
3. Define the object attribute mappings for the extended searchable attributes, marking the attributes as Searchable.

Default:

| Object Type                                               | Number of Preconfigured<br>Searchable Extended Attributes | Number of Indexed<br>Extended Attributes |
| --------------------------------------------------------- | --------------------------------------------------------- | ---------------------------------------- |
| Identity                                                  | 10                                                        | 5                                        |
| Link (account)                                            | 5                                                         | 1                                        |
| Bundle (role)                                             | 4                                                         | 1                                        |
| ManagedAttribute (managed entitlement and account groups) | 3                                                         | 3                                        |
| Application                                               | 4                                                         | 1                                        |
| CertificationItem                                         | 5                                                         | 1                                        |
| Alert                                                     | 1                                                         | 1                                        |
| Server                                                    | 1                                                         | 1                                        |
| Target                                                    | 1                                                         | 1                                        |
Note: Not all preconfigured extended attributes are indexed.


Hibernate will not create an index if one is not request. 
To add an index for a named extended attribute, specify the index as a part of property:
```
<property name="costCenter" type="string" length="450" access="sailpoint.persistence.ExtendedPropertyAccessor" index="spt_identity_cost_center_ci"/>
```
The extended1, extended2, extended3, etc. attributes get specified without this, but the system needs this to address any custom-named columns/properties. 

import init.xml -> to set up the initial system configurations. 

## Object Attribute Mappings

* Identity Mappings for Identity attributes.
* Account Mappings for Link attirbutes.
* Application Attributes for extended application attributes
* Role Configuration for Bundle attributes
* Entitlement Catalog Attributes for Managed Attribute extended attributes. 
