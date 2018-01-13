# ansible-bind9

Ansible Playbook for installing bind9 + domains

## Main usage

That is primarily my own set of instructions how to install bind9. But feel free to look around ...


## Files and Directories

* _files/named.conf.local.template_: template for _bind9-data/named.conf.local_, either use the template or create your own file
* _files/named.conf.options.template_: template for _bind9-data/named.conf.options_, either use the template or create your own file
* _bind9-data/keys/_: install any key files here, for communication with other nameservers - any file which ends on _.key_ will be copied
* _bind9-data/zones/_: install any zone file here - any file which ends on _.zone_ will be copied, and the _zone_serial_ variable will he handled
* _bind9-data/zone-data/_: storage area for zone checksums and serials - do not touch


## Preparation

By default, all data for bind9 lives in the _bind9-data_ directory in the root of the Playbook. This can be changed by modifying the _bind9_data_ variable in _vars/main.yml_.

A few directories have to be created before this role can be used:

```
mkdir bind9-data
mkdir bind9-data/keys
mkdir bind9-data/zones
mkdir bind9-data/zone-data
chmod 0700 bind9-data
```


## Serial handling

You can handle the serial number in a zone as you like - if you include a variable {{ zone_serial }}, this variable will he handled by the Playbook.

Every time the zone is changed, the current date (yyyymmdd) and a two-digit counter will be set and increased. Date changes will reset the counter to "01", and after "99" changes a day the Playbook will reject any further changes.
