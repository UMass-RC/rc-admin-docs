### Installing SLAPD ###

Install slapd from the Ubuntu package repository

```
apt install slapd
```

During the installation, you will be asked several questions:

1. Specify the admin password for the database
1. Specify DIT, which is your domain organized into "domain components", or "dc": `dc=unity,dc=rc,dc=umass,dc=edu` would correspond to `unity.rc.umass.edu`. This is done by convention, although you can set this to anything arbitrary.
1. Organization name is `Users`.
1. Use `MDB` for database.
1. Select `yes` for "move old database"

### Configuring SLAPD ###

For Unity, we need to activate a number of *schemas*, which are files that you can important into the ldap database that add attributes / classes for ldap objects.

The included schemas are located in `/etc/ldap/schema`.  

To activate a schema, use:
```
ldapadd -Y EXTERNAL -H ldapi:/// -f <LOCATION OF SCHEMA>
```

On Unity, we activate:

* `cosine.ldif`
* `nis.ldif`
* `inetorgperson.ldif`
* `ssh.ldif` this ldif is not included, but ldif files are plain text so you can create it:

```
dn: cn=openssh-lpk,cn=schema,cn=config
objectClass: olcSchemaConfig
cn: openssh-lpk
olcAttributeTypes: ( 1.3.6.1.4.1.24552.500.1.1.1.13 NAME 'sshPublicKey'
    DESC 'MANDATORY: OpenSSH Public key'
    EQUALITY octetStringMatch
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.40 )
olcObjectClasses: ( 1.3.6.1.4.1.24552.500.1.1.2.0 NAME 'ldapPublicKey' SUP top AUXILIARY
    DESC 'MANDATORY: OpenSSH LPK objectclass'
    MAY ( sshPublicKey $ uid )
    )
```