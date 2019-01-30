# ansible-cockpit

This is to demo Cockpit on RHEL 8 beta. Inventory consists of 3 hosts across 2 groups, `head` and `nodes`.

Hosts must be registered first using `subscription-manager`. `cockpit.yml` installs all Cockpit packages, adds hosts in `nodes` group to `cockpit-dashboard` on the `head` node and writes their ssh pubkeys to a `known_hosts` file for Cockpit. This allows to manage all `nodes` from a single machine.

![Cockpit screenshot](https://raw.githubusercontent.com/cloin/ansible-cockpit/master/cockpit-screenshot.png)
