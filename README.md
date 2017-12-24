# ansible-bind9

Ansible Playbook for installing bind9 + domains

## Main usage

That is primarily my own set of instructions how to install bind9. But feel free to look around ...


## Files and Directories

* _files/named.conf.local.template_: template for _files/named.conf.local_, either use the template or create your own file
* _files/named.conf.options.template_: template for _files/named.conf.options_, either use the template or create your own file
* _files/keys/_: install any key files here, for communication with other nameservers - any file which ends on _.key_ will be copied
* _files/zones/_: install any zone file here - any file which ends on _.zone_ will be copied, and the _zone_serial_ variable will he handled
* _files/zone-data/_: storage area for zone checksums and serials - do not touch

## Serial handling

You can handle the serial number in a zone as you like - if you include a variable {{ zone_serial }}, this variable will he handled by the Playbook.

Every time the zone is changed, the current date (yyyymmdd) and a two-digit counter will be set and increased. Date changes will reset the counter to "01", and after "99" changes a day the Playbook will reject any further changes.
