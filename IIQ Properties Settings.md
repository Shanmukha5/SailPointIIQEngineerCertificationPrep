**🗓️ Date:** `2025-04-23` | **🕒 Time:** `12:30:57` | **📅 Day:** `Wednesday`

---

# IIQ Properties file

* iiq.properties file is located in \[IIQFolder]\WEB-INF\classes directory.
* Most commonly used setting in iiq.properties provide parameters for connecting to the data source (database).
* Settings required for iiq.properties to manage database connectivity and connection pooling:
	* dataSource.username - username for database login.
	* dataSource.password - password for database login. (can be encrypted with iiq console)
	* dataSource.url - JDBC url path to the database. 
	* dataSource.maxWait - Max milliseconds to wait when there are no available connections.

# Task and Request Scheduler Hosts

iiq.properties configuration is not recommended for current IIQ installations. It remains for backward compatibility. New installations should use ServiceDefinition option. 

IIQ designate some hosts as task and request servers, and reserve others for processing only user interface activity. 
* Task servers run reports and non-partitioned tasks while request servers send emails, run partitioned tasks, and generate certifications.
* environment.taskSchedulerHosts - comma-separated list of task scheduler application instances. (tasks, reports)
* environment.requestSchedulerHosts - comma-separated list of request scheduler application instances. (email sending, scheduled sunrise/sunset activities)

SailPoint doesn't recommend to have more than one instance in one server.

From 6.2+, use "hosts" parameters int he Task and Request Service Definition.
* Default "hosts" are set to global -> tasks and requests can run on any server.
* "global" is separated with comma-separated list of host names, tasks or requests will only execute on the specified servers.
* If "hosts" values are set to null (empty), tasks or request will not run at all.

If host parameters are set in both iiq.properties and in the ServiceDefinition objects, they are additively applied with the ServiceDefinition; this can result in confusion if the host lists are different in the two locations, so this practice is discouraged.


# KeyStore Settings

By default, keystore file is "iiq.dat" and its accompanying config file is "iiq.cfg"; stored in WEB-INF/classes folder (non-human-readable form)
Some customers who are running multiple servers prefer to locate these files in a single shared directory instead of including them in the war file deployed to each server; the file and passwordFile attributes in iiq.properties.
* keyStore.type - type of keystore, defaults to JCEKS if not specified.
* keyStore.file - override the default keystore filename: WEB-INF/classes/iiq.dat
* keyStore.passwordFile - specifies a filename to override of the default master password file for the keystore; default is WEB-INF/classes/iiq.cfg
* keyStore.password - can be used instead of the keyStore.passwordFile to store a string version of the key store master password rather than reading it from a file (takes precedence over passwordFile is specified)


# SQL Debugging

Two diferent options are available for debugging: **Hiberate** and **P6Spy**.

## Hibernate Settings
Hibernate manages the object/relational mapping between the IIQ database and Java object model.
* show_sql parameter can be set to true, to send all the SQL queries to stdout.	
```
#sessionFactory.hibernateProperties.hibernate.show_sql=true
```
* show_sql logs the SQL statements but doesn't include parameter substitutions; p6spy logs the queries and includes all Hibernate SQL parameters values just as they are passed to the database.
* Create / Edit spy.properties file in the same directory as iiq.properties


# RuleRunner Pool Settings

BeanShell Framework (BSF) is used for running rules in IIQ. 
