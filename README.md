# prometheus_with_vagrant_libvirt_ansible

This Vagrant setup creates a prometheus-server VM and two VMs as "nodes".

It installs and starts the [node-exporter](https://github.com/prometheus/node_exporter) on all nodes, then installs and configures the [Prometheus server](https://github.com/prometheus/prometheus) to scrape metrics from all of the nodes.

It also installs Grafana on the Prometheus server VM.

Default OS is openSUSE Leap 15.6, but that can be changed in the Vagrantfile. Please beware, this might break the ansible provisioning which was only tested with openSUSE Leap 15.6.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
2. Fetch the box, per default this is `opensuse/Leap-15.6.x86_64`, using `vagrant box add opensuse/Leap-15.6.x86_64`.
3. Make sure the git submodules are fully working by issuing `git submodule init && git submodule update`
4. Run `vagrant up`
5. Find out the IP address of the prometheus-server, open it in a browser using port 9090 and you should see the Prometheus UI. You should find all nodes in `Status` => `Targets`
6. Party!
