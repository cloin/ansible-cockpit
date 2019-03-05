# ansible-cockpit

This is to demo Cockpit on RHEL 8 beta. Inventory consists of [3 hosts across 2 groups](https://github.com/cloin/ansible-cockpit/blob/master/inventory), `head` and `nodes`.

Hosts must be registered first using [`subscription-manager`](https://docs.ansible.com/ansible/latest/modules/redhat_subscription_module.html). [`cockpit.yml`](https://github.com/cloin/ansible-cockpit/blob/master/cockpit.yml) calls roles for common tasks and master which [adds hosts](https://github.com/cloin/ansible-cockpit/blob/master/roles/cockpit-master/templates/cockpit-machine.json.j2) in `nodes` group to `cockpit-dashboard` on the `head` node and writes their ssh pubkeys to a `known_hosts` file for Cockpit. 

**This allows for management of all hosts from a single interface!**

The firewall rule for tcp/9090 only needs to be added on the master where `cockpit-dashboard` is installed. Metrics and management of the other nodes are done through `ssh` so `cockpit.socket` doesn't need to be enabled/started on the nodes group.

![Cockpit screenshot](https://github.com/cloin/ansible-cockpit/blob/dev/cockpit-dashboard.png?raw=true)

