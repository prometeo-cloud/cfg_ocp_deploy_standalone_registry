# cfg_ocp_install_standalone_registry

Deploys an openshift standalone Docker [registry](https://docs.openshift.com/container-platform/3.6/install_config/install/stand_alone_registry.html).


## Requirements

- [ocp_configure_node](https://github.com/prometeo-cloud/ocp_configure_node)

## Usage

### With HTPasswd authentication


| Variable  | Description  | Example | Mandatory |
|---|---|---|---|
|**master_default_subdomain**| the master node default subdomain. | myhost.com | yes |

```bash
# install an OCR with httpasswd authentication
$ ansible-playbook -i inv_htpasswd -key-file='/path/to/private/key' -e '{ "master_default_subdomain":"localhost" }'
```

### With LDAP authentication


| Variable  | Description  | Example | Mandatory |
|---|---|---|---|
|**master_default_subdomain**| the master node default subdomain. | myhost.com | yes |
| **ldap_hostnames** | The hostname(s) of the LDAP host to be used by the registry | www.ldaphost.com | yes |
| **ldap_url** | The URL of the LDAP server. |  ldap://www.example.com/ ou=users,dc=acme, dc=com?uid | yes |
| **ldap_certificate_file** | Certificate bundle to use to validate server certificates for the configured URL. If empty, system trusted roots are used. Only applies if insecure: false. | ldap-ca-bundle.crt (defaults to an empty string)| no |
| **ldap_insecure** | When true, no TLS connection is made to the server. When false, ldaps:// URLs connect using TLS, and ldap:// URLs are upgraded to TLS. | false (defaults to true) | no |

```bash
# install an OCR with ldap authentication
$ ansible-playbook -i inv_ldap -key-file='/path/to/private/key' -e '{ "master_default_subdomain":"localhost", "ldap_certificate_file":"", "ldap_insecure":"no", "ldap_url":"ldap://www.example.com/ou=users,dc=acme,dc=com?uid" }'
```
