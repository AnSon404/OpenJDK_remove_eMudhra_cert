# OpenJDK_remove_eMudhra_cert
Reference: https://openjdk.org/emudhra

## For JDK 8:
### Step 1: Check
Hint: the CheckCerts.java is not checking comodoaaaca, it is checking AAA Certificate Services!
```
keytool -list -v -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit | grep -E "^(Alias name|Owner):" | grep -B5 -iE "emSign|AAA Certificate Services|eMudhra"
```
### Step 2: Delete eMudhra intermediate CA certificates which were compromised
Read the Step 1 output of "Alias name", then change below command and execute: 
```
$ keytool -delete -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -alias "<step1_alias_name>"
```

Restart any live instances of the runtime.

If you have more than one standalone OpenJDK Java runtime installed, repeat these steps for each installation.
