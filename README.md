# Spring LDAP

## Development

### Using Docker to simplify development (optional)

You can use Docker to improve your JHipster development experience. Images [pbertera/ldapserver](https://hub.docker.com/r/pbertera/ldapserver) By pbertera `OpenLDAP + NGINX + PhpLdapAdmin` container 

For example, to start a postgresql database in a docker container, run:

    docker run -v /data/ldap:/var/lib/ldap -p 80:80 -p 389:389 -e LDAP_DOMAIN=springframework.org -e LDAP_ORGANISATION="My Mega Corporation" -e LDAP_ROOTPASS=s3cr3tpassw0rd -d pbertera/ldapserver

### Set up user data

LDAP servers can use LDIF (LDAP Data Interchange Format) files to exchange user data. The `spring.ldap.embedded.ldif` property inside `application.properties` allow to Spring Boot pulls in an LDIF data file. This makes it easy to pre-load demonstration data.

`PhpLdapAdmin`

    Login DN: cn=admin,dc=springframework,dc=org
    Password: s3cr3tpassw0rd

`src/main/resources/test-server.ldif`
    
    dn: ou=groups,dc=springframework,dc=org
    objectclass: top
    objectclass: organizationalUnit
    ou: groups

    dn: ou=subgroups,ou=groups,dc=springframework,dc=org
    objectclass: top
    objectclass: organizationalUnit
    ou: subgroups

    dn: ou=people,dc=springframework,dc=org
    objectclass: top
    objectclass: organizationalUnit
    ou: people

    dn: ou=space cadets,dc=springframework,dc=org
    objectclass: top
    objectclass: organizationalUnit
    ou: space cadets

    dn: ou=quoted people,dc=springframework,dc=org
    objectclass: top
    objectclass: organizationalUnit
    ou: quoted people

    dn: ou=otherpeople,dc=springframework,dc=org
    objectclass: top
    objectclass: organizationalUnit
    ou: otherpeople

    dn: uid=ben,ou=people,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: Ben Alex
    sn: Alex
    uid: ben
    userPassword: {SHA}nFCebWjxfaLbHHG1Qk5UU4trbvQ=

    dn: uid=bob,ou=people,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: Bob Hamilton
    sn: Hamilton
    uid: bob
    userPassword: bobspassword

    dn: uid=joe,ou=otherpeople,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: Joe Smeth
    sn: Smeth
    uid: joe
    userPassword: joespassword

    dn: cn=mouse\, jerry,ou=people,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: Mouse, Jerry
    sn: Mouse
    uid: jerry
    userPassword: jerryspassword

    dn: cn=slash/guy,ou=people,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: slash/guy
    sn: Slash
    uid: slashguy
    userPassword: slashguyspassword

    dn: cn=quote guy,ou=quoted people,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: quote\"guy
    sn: Quote
    uid: quoteguy
    userPassword: quoteguyspassword

    dn: uid=space cadet,ou=space cadets,dc=springframework,dc=org
    objectclass: top
    objectclass: person
    objectclass: organizationalPerson
    objectclass: inetOrgPerson
    cn: Space Cadet
    sn: Cadet
    uid: space cadet
    userPassword: spacecadetspassword

    dn: cn=developers,ou=groups,dc=springframework,dc=org
    objectclass: top
    objectclass: groupOfUniqueNames
    cn: developers
    ou: developer
    uniqueMember: uid=ben,ou=people,dc=springframework,dc=org
    uniqueMember: uid=bob,ou=people,dc=springframework,dc=org

    dn: cn=managers,ou=groups,dc=springframework,dc=org
    objectclass: top
    objectclass: groupOfUniqueNames
    cn: managers
    ou: manager
    uniqueMember: uid=ben,ou=people,dc=springframework,dc=org
    uniqueMember: cn=mouse\, jerry,ou=people,dc=springframework,dc=org

    dn: cn=submanagers,ou=subgroups,ou=groups,dc=springframework,dc=org
    objectclass: top
    objectclass: groupOfUniqueNames
    cn: submanagers
    ou: submanager
    uniqueMember: uid=ben,ou=people,dc=springframework,dc=org
    
If you visit the site at http://localhost:8080, you should be redirected to a login page provided by Spring Security.

Enter username ben and password benspassword. You should see this message in your browser:

    Welcome to the home page!
    
### Summary
Congratulations! You have just written a web application and secured it with Spring Security. In this case, you used an LDAP-based user store.
