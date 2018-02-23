# jenkins-ad-ldap-plugin

## Using Jenkins LDAP plugin to connect to AD for Project based Matrix Authorization

Currently there are at least two plugins available for connecting to a LDAP provider from Jenkins: active directory plugin and LDAP plugin. Earlier we were using Active Directory plugin for connecting Active Directory. Howev due to internal re-organization of the Active Directory,  we encountered an issue while connecting to AD from Jenkins to use Project based Matrix Authorization.

This posting attempts to document the steps required that helped us implement Jenkins-Active Directory Project based matrix authorization using LDAP plugin:

Jenkins version: 2.73.1
LDAP plugin: v 1.15

### LDAP DN hierarchy:

TLD: DC=mydomain,DC=example,DC=com
Users: OU=Users,OU=My Org,DC=mydomain,DC=example,DC=com
Groups: OU=Users,OU=My Org,DC=mydomain,DC=example,DC=com

Here is the LDAP plugin configuration settings that worked for us:

Server: ldap://myldap.mydomain.example.com:3268  (3268 for AD global catalog)

root DN: DC=mydomain,DC=example,DC=com

User search filter: sAMAccountName={0}

Group membership: Parse user attribute for list of groups, select attribute: memberOf

Manager DN: CN=admin,OU=Users,OU=My Org,DC=mydomain,DC=example,DC=com
