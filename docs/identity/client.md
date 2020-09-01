Our objective is to get our clients (all the nodes on the cluster), to talk to a centralized LDAP server to obtain all user information, so that we don't have to create local users on each node. To accomplish this, we will use NSLCD, which will contact the LDAP server, and NSCD, which will cache that information.

### Installing NSLCD/NSCD ###

Install from Ubuntu package repositories:
```
apt install libpam-ldapd
```

During the installation, you will be asked several questions:

1. LDAP URI is the location of the ldap server. In our case, thats `ldap://identity/`
1. DN (distinguished name) is the base DN, which is usually the domain component of the LDAP server. For Unity, `dc=unity,dc=rc,dc=umass,dc=edu`
1. Now it will ask where to use LDAP info. You should check `passwd`, `group`, and `shadow`.

At this point the system will be able to begin using the centralized users. However, the `ldapsearch` command won't work, because its config file is seperate. In `/etc/ldap/ldap.conf`:

```
BASE dc=unity,dc=rc,dc=umass,dc=edu
URI ldap://identity/
```