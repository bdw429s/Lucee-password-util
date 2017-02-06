I am a utility for managing Lucee or Railo passwords for the administrator and data sources.  Normally, you won't need me, but sometimes you need to edit the config files directly.
	
# hashAdministrator
When passing a salt, use this to mimic the same SHA-256 hashing that the Lucee administrator uses for server and web context passwords. You can't duplicate this with the CFML hash() function.  

Values created by this method would go in one of the following XML files:

**lucee-server.xml**
* In the root `<lucee-configuration>` tag as the `hspw` attribute.  Applies to the web administrator for the entire server
* In the root `<lucee-configuration>` tag as the `default-hspw` attribute.  Set's the default password for any new web contexts
* In the root `<lucee-configuration>` tag as the `salt` attribute.  Set's the salt to use for all passwords

**lucee-web.xml.cfm**
* In the root `<lucee-configuration>` tag as the `hspw` attribute.  Applies to the web administrator for that context.
* In the root `<lucee-configuration>` tag as the `salt` attribute.  Set's the salt to use for all passwords
							
# hashAdministrator

> DEPRECATED. use hash with salt instead

Use this to mimic the same SHA-256 hashing that the Lucee or Railo administrator uses for server and web context passwords. You can't duplicate this with the CFML hash() function.  

Values created by this method would go in one of the following XML files:

**lucee-server.xml**
* In the root <lucee-configuration> tag as the "pw" attribute.  Applies to the web administrator for the entire server
* In the root <lucee-configuration> tag as the "default-pw" attribute.  Set's the default password for any new web contexts

**lucee-web.xml.cfm**
* In the root <lucee-configuration> tag as the "pw" attribute.  Applies to the web administrator for that context.
							
# encryptAdministrator

> DEPRECATED, use hash with salt instead

Used to encrypt a string using the BlowFish algorithm with the same salt used for the Lucee or Railo administrator.  

# decryptAdministrator

> DEPRECATED, use hash with salt instead

Used to decrypt a string using the BlowFish algorithm with the same salt used for the Lucee or Railo administrator.  

**lucee-server.xml**
* In the root `<lucee-configuration>` tag as the `password` attribute.  Applies to the web administrator for the entire server
* In the root `<lucee-configuration>` tag as the `default-password` attribute.  Set's the default password for any new web contexts

**lucee-web.xml.cfm**
* In the root `<lucee-configuration>` tag as the `password` attribute.  Applies to the web administrator for that context.
	
# encryptDataSource

Used to encrypt a string using the BlowFish algorithm with the same salt used for data source passwords in the Lucee or Railo administrator.

# decryptDataSource

Used to decrypt a string using the BlowFish algorithm with the same salt used for data source passwords in the Lucee or Railo administrator.

Values created by this method would go in one of the following files:

**lucee-server.xml**
* In a `<data-source>` tag's password attribute, preceded by the string `encrypted:`

```xml	 
<data-source 
 	username="root"
 	name="myDS" 
 	dsn="jdbc:mysql://localhost:3306/myDB" 
 	class="org.gjt.mm.mysql.Driver"
  	password="encrypted:3448cf390fa78e1cbb7745607a68ff6e282d60c044ad09ed" />
```
	
**lucee-web.xml.cfm**
* In a `<data-source>` tag same as above

**Application.cfc**
* In the datasources struct like so:
	
```js
this.datasources.myDS={
    class:"org.gjt.mm.mysql.Driver",
	connectionString:"jdbc:mysql://localhost:3306/myDB",
	username:"root",
	password:"encrypted:3448cf390fa78e1cbb7745607a68ff6e282d60c044ad09ed"
```
