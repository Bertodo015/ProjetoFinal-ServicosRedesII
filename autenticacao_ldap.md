## Configuração
```bash
    sudo ldapsearch -Y EXTERNAL -H ldapi:/// -b "cn=config" -LLL
    sudo ldapsearch -Y EXTERNAL -H ldapi:/// -b "olcDatabase={1}mdb,cn=config" -LLL
    sudo ldapsearch -Y EXTERNAL -H ldapi:/// -b "olcDatabase={1}mdb,cn=config" olcSuffix
```
### Arquivo base.ldif
```bash
    dn: dc=technet,dc=local
    objectClass: top
    objectClass: dcObject
    objectClass: organization
    o: TechNet Solutions
    dc: technet

    dn: ou=Usuarios,dc=technet,dc=local
    objectClass: top
    objectClass: organizationalUnit
    ou: Usuarios

    dn: ou=Grupos,dc=technet,dc=local
    objectClass: top
    objectClass: organizationalUnit
    ou: Grupos
```

```bash
    sudo ldapadd -x -D "cn=admin,dc=technet,dc=local" -w admin123 -f base.ldif
```

## Criação dos Usuários
### usuarios.ldif
```bash
    dn: uid=vendedor1,ou=Usuarios,dc=technet,dc=local
    objectClass: top
    objectClass: person
    objectClass: organizationalPerson
    objectClass: inetOrgPerson
    uid: vendedor1
    cn: Vendedor 1
    sn: Vendedor
    userPassword: {SSHA}W9nM5KqL4vL5HbXpQNvJw7RqY8zB2cA=
    mail: vendedor1@technet.local

    dn: uid=vendedor2,ou=Usuarios,dc=technet,dc=local
    objectClass: top
    objectClass: person
    objectClass: organizationalPerson
    objectClass: inetOrgPerson
    uid: vendedor2
    cn: Vendedor 2
    sn: Vendedor
    userPassword: {SSHA}W9nM5KqL4vL5HbXpQNvJw7RqY8zB2cA=
    mail: vendedor2@technet.local

    dn: uid=recursos,ou=Usuarios,dc=technet,dc=local
    objectClass: top
    objectClass: person
    objectClass: organizationalPerson
    objectClass: inetOrgPerson
    uid: recursos
    cn: Recursos Humanos
    sn: RH
    userPassword: {SSHA}W9nM5KqL4vL5HbXpQNvJw7RqY8zB2cA=
    mail: recursos@technet.local

    dn: uid=tecnico,ou=Usuarios,dc=technet,dc=local
    objectClass: top
    objectClass: person
    objectClass: organizationalPerson
    objectClass: inetOrgPerson
    uid: tecnico
    cn: Tecnico TI
    sn: TI
    userPassword: {SSHA}W9nM5KqL4vL5HbXpQNvJw7RqY8zB2cA=
    mail: tecnico@technet.local

    dn: uid=admin,ou=Usuarios,dc=technet,dc=local
    objectClass: top
    objectClass: person
    objectClass: organizationalPerson
    objectClass: inetOrgPerson
    uid: admin
    cn: Admin
    sn: Admin
    userPassword: {SSHA}W9nM5KqL4vL5HbXpQNvJw7RqY8zB2cA=
    mail: admin@technet.local
```

```bash
    sudo ldapadd -x -D "cn=admin,dc=technet,dc=local" -w admin123 -f usuarios.ldif
```

## Testes realizados na pasta /evidencias/autenticacao_ldap/