Vagrant.configure("2") do |config|

  ###################################################################################
  # define number of nodes
  W = 2

  # provision W VMs as nodes
  (1..W).each do |i|

    # name the VMs
    config.vm.define "prometheus-node#{i}" do |node|

      # which image to use
      node.vm.box = "opensuse/Leap-15.6.x86_64"

      # disable synced folders
      node.vm.synced_folder ".", "/vagrant", disabled: true

      # sizing of the VMs
      node.vm.provider "libvirt" do |lv|
        lv.random_hostname = true
        lv.memory = 1024
        lv.cpus = 2
      end

      # set the hostname
      node.vm.hostname = "prometheus-node#{i}"

    end # config.vm.define nodes

  end # each-loop nodes

  ###############################################

  # name the VMs
  config.vm.define "prometheus-server" do |node|

    # which image to use
    node.vm.box = "opensuse/Leap-15.6.x86_64"

    # disable synced folders
    node.vm.synced_folder ".", "/vagrant", disabled: true

    # sizing of the VMs
    node.vm.provider "libvirt" do |lv|
      lv.random_hostname = true
      lv.memory = 2048
      lv.cpus = 2
    end

    # set the hostname
    node.vm.hostname = "prometheus-server"

    #################################################
    # only target one node to not run ansible twice
    # but do not limit this to this node (set ansible.limit to all)
    node.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.limit = "all"
      ansible.groups = {
        "prometheus_server"  => [ "prometheus-server" ],
        "prometheus_nodes"   => [ "prometheus-node1", "prometheus-node2" ]
      }
      ansible.playbook = "ansible/playbook-vagrant.yml"
    end # node.vm.provision

  end # config.vm.define server

end # Vagrant.configure
