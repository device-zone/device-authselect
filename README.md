# device-authselect
Provides control over the authselect mechanism used to define where user
accounts are defined.

This appliance does the following:

- All parameters passed to the device commands are syntax checked and canonicalised,
  with bash completion.
- Allows selection of authselect profiles installed on the system.

## before

- Deploy the device-authselect package.

```
[root@server ~]# dnf install device-authselect
```

## set profile

To set the profile on the machine to sssd, run this. Other possible profiles include 'minimal',
'winbind' or 'none'.

```
[root@server ~]# device system auth set profile=sssd
```

# device-authselect-sssd
Extends the authselect appliance with sssd support.

This appliance extension does the following:

- All parameters passed to the device commands are syntax checked and canonicalised,
  with bash completion.
- Allows setting of sssd specific configuration parameters.

## before

- Deploy the device-authselect-sssd package.

```
[root@server ~]# dnf install device-authselect-sssd
```

## set sssd parameters

To set sssd specific parameters, run the following.

```
[root@server ~]# device system auth sssd set with-mkhomedir=yes with-sudo=yes
```

Options include the following:

- with-faillock=[yes|no]
- with-fingerprint=[yes|no]
- with-mkhomedir=[yes|no]
- without-pam-u2f-nouserok=[yes|no]
- with-pam-u2f=[yes|no]
- with-pam-u2f-2fa=[yes|no]
- with-smartcard=[yes|no]
- with-sudo=[yes|no]

## set sssd smartcard parameters

To set sssd smartcard specific parameters, run the following.

```
[root@server ~]# device system auth sssd smartcard set lock-on-removal=yes
```

Options include the following:

- ca-certificate=[cert]
- lock-on-removal=[yes|no]
- required=[yes|no]


# device-authselect-sssd-ldap
Extends the authselect appliance sssd support with ldap.

This appliance extension does the following:

- All parameters passed to the device commands are syntax checked and canonicalised,
  with bash completion.
- Allows setting of ldap specific configuration parameters for sssd.

## note

As of this writing, the authselect appliance is secured using ldap over unix domain
sockets, which has been added to sssd here: https://github.com/SSSD/sssd/pull/6484

RPMs can be found here: https://copr.fedorainfracloud.org/coprs/minfrin/sssd/

## before

- Deploy the device-authselect-sssd-ldap package.

```
[root@server ~]# dnf install device-authselect-sssd-ldap
```

# add a given ldap suffix to sssd directories

To point sssd at a given ldap suffix, run this. 

```
[root@server ~]# device system auth sssd ldap add suffix=seawitch-example sudo-search-base="dc=example,dc=com"
```

# remove a given ldap suffix from sssd directories

To remove the entry above, run this.

```
[root@server ~]# device system auth sssd ldap remove seawitch-example
```

