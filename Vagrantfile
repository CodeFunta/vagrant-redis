VAGRANTFILE_API_VERSION = "2"
#ENV['VAGRANT_DEFAULT_PROVIDER'] = 'hyperv'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "generic/ubuntu1710"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.network "forwarded_port", guest: 6379, host: 6379, auto_correct: true

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provider "hyperv" do |hv|
    # Customize the amount of memory on the VM:
    hv.memory = "1024"
    hv.maxmemory  = "4096"
    hv.cpus = 4
    config.vm.network "public_network", bridge: "external.net"
    hv.differencing_disk= true
  end

  config.vm.provision "shell", path: "init.sh"
end
