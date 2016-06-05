# vagant-machines
How to create an "N" virtual machines with a loop in a Vagrant file and libvirt provider. 

### Requirements (based in Fedora 22)
* Install Vagrant and libvirt dependencies

> sudo dnf install @vagrant

* Check libvirt daemon is running and the kvm module is loaded:

> $ sudo systemctl status libvirtd

### Config Vagranfile

```ruby
Vagrant.configure(2) do |config|
    config.vm.box = "dliappis/centos7minlibvirt"
    (1..3).each do |i|
      config.vm.define "edureka_vm#{i}" do |node|
        config.vm.provider "libvirt" do |domain|
          domain.uri = 'qemu+unix:///system'
          domain.driver = 'kvm'
          domain.storage_pool_name = 'USB_VMs'
          domain.host = "test#{i}"
          domain.driver = "kvm"
          domain.memory = 1024
          domain.cpus = 1
        end
      end
    end
  end
```

