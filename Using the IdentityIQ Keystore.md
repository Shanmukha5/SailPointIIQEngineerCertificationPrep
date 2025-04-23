**🗓️ Date:** `2025-04-23` | **🕒 Time:** `14:33:46` | **📅 Day:** `Wednesday`

---

* Default location for keystore file is WEB-INF/classes/iiq.dat with an accompanying configuration file WEB-INF/classes/iiq.cfg. Neither of these files is human readable.
* The iiq.properties file provides two options to specify an alternative location for iiq.dat and iiq.cfg. In the default iiq.properties, these options (keyStore.file and keyStore.passwordFile) are commented out.

## Key Creation

To create or manage the keystore:
```
$ ./iiq keystore (Unix)

C:> iiq.bat keystore (Windows)
```

```
list -> whether a site specific key already exists
addKey -> to generate a new key
```
Restart is required after this change. 
After restarting any newly set password will be encrypted using the new encryption key. 
Without the files iiq.dat and iiq.cfg, passwords cannot be decrypted by IIQ. 
If you run more than one instance of IIQ, these files need to be placed in the WEB-INF/classes folder of each instance, or in the location specified in iiq.properties.


## Re-Encrypt Password

Existing passwords need to be re-encrypted. 
To do so, you need to create a new task of type "Encrypted Data Synchronization Task".

While a password encrypted with the default key is prefixed with "1:", items encrypted with the new encryption key are prefixed with "2:" or another number if multiple encryption keys are stored. 

To lookup administrator password from the console:
```
> search identity password where name spadmin
2:Wpjkafsasfdiabsfda==
```

Encrypt using particular encryption key:
```
iiq encrypt <string> [<key>]
```
