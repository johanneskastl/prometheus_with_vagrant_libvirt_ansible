# prometheus_with_vagrant_libvirt_ansible

This Vagrant setup creates a prometheus-server VM and two VMs as "nodes".

It installs and starts the
[node-exporter](https://github.com/prometheus/node_exporter) on all nodes, then
installs and configures the [Prometheus
server](https://github.com/prometheus/prometheus) to scrape metrics from all of
the nodes.

It also installs Grafana on the Prometheus server VM.

Default OS is openSUSE Leap 15.6, but that can be changed in the Vagrantfile.
Please beware, this might break the ansible provisioning which was only tested
with openSUSE Leap 15.6.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
1. Fetch the box, per default this is `opensuse/Leap-15.6.x86_64`, using
   `vagrant box add opensuse/Leap-15.6.x86_64`.
1. Make sure the git submodules are fully working by issuing `git submodule init
   && git submodule update`
1. Run `vagrant up`
1. Ansible prints out the URLs for the Prometheus Node-Exporter, the Prometheus
   UI and the Grafana UI.
1. Open the Prometheus UI URL. You should find all nodes in `Status` =>
   `Targets`.
1. If you wish you can open the Grafana URL and add a datasource for Prometheus,
   according to [the
   documentation](https://grafana.com/docs/grafana/latest/datasources/prometheus/configure-prometheus-data-source/).
1. Party!

## Cleaning up

The VMs can be torn down after playing around using `vagrant destroy`.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via git@johannes-kastl.de
