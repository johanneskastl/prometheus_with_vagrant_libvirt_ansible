# prometheus_with_vagrant_libvirt_ansible

This Vagrant setup creates a prometheus-server VM and two VMs as "nodes".

It installs and starts the [node-exporter](https://github.com/prometheus/node_exporter) on all nodes, then installs and configures the [Prometheus server](https://github.com/prometheus/prometheus) to scrape metrics from all of the nodes.

It also installs Grafana on the Prometheus server VM.

Default OS is openSUSE Leap 15.4, but that can be changed in the Vagrantfile. Please beware, this might break the ansible provisioning which was only tested with openSUSE Leap 15.4.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
2. Fetch the box, per default this is `opensuse/Leap-15.3.x86_64`, using `vagrant box add opensuse/Leap-15.3.x86_64`.
3. Make sure the git submodules are fully working by issuing `git submodule init && git submodule update`
4. Run `vagrant up`
5. Find out the IP address of the prometheus-server, open it in a browser using port 9090 and you should see the Prometheus UI. You should find all nodes in `Status` => `Targets`
6. Party!

## Disabling the Ansible provisioning

In case you do not want Ansible to install prometheus (because you want to install it yourself), just comment out the following lines in the `Vagrantfile`:
```
    node.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.limit = "all"
      ansible.groups = {
        "prometheus_servers"  => [ "prometheus-server" ],
        "prometheus_nodes"   => [ "prometheus-node1", "prometheus-node2" ]
      }
      ansible.playbook = "ansible/playbook-vagrant.yml"
    end # node.vm.provision
```

## Creating additional agent nodes

You can modify the Vagrantfile to create additional agent nodes by tweaking two lines.

1. Setting the number of agents (in this example to `3`):

```
  ###################################################################################
  # define number of nodes
  W = 3
```

2. Adding the additional nodes to the `ansible_groups` line:
```
      ansible.groups = {
        "prometheus_servers"  => [ "prometheus-server" ],
        "prometheus_nodes"   => [ "prometheus-node1", "prometheus-node2", "prometheus-node3" ]
      }
```
