# ansible-cockpit

Roles to setup Cockpit on RHEL 8 beta. Inventory consists of [3 hosts across 2 groups](https://github.com/cloin/ansible-cockpit/blob/master/inventory), `master` and `nodes`.

Hosts must be registered first using [`subscription-manager`](https://docs.ansible.com/ansible/latest/modules/redhat_subscription_module.html). [`cockpit.yml`](https://github.com/cloin/ansible-cockpit/blob/master/cockpit.yml) calls roles for common tasks and master which [adds hosts](https://github.com/cloin/ansible-cockpit/blob/dea4e6612bad6b635ffc57c796d851f2622fda00/roles/cockpit-master/tasks/main.yml#L7) in `nodes` group to `cockpit-dashboard` on the `master` node using a [template](https://github.com/cloin/ansible-cockpit/blob/master/roles/cockpit-master/templates/cockpit-machine.json.j2) and writes their ssh pubkeys to a `known_hosts` file for Cockpit. 

**This allows for management of all hosts from a single Cockpit instance!**

The firewall rule for tcp/9090 only needs to be added on the master where `cockpit-dashboard` is installed. Metrics and management of the other nodes are done through `ssh` so `cockpit.socket` doesn't need to be enabled/started on the nodes group.

![Cockpit screenshot](https://github.com/cloin/ansible-cockpit/blob/dev/cockpit-dashboard.png?raw=true)

