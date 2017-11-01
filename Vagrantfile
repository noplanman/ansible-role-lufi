role = File.basename(File.expand_path(File.dirname(__FILE__)))

boxes = [
  {
    :name => "ubuntu-1404",
    :box => "bento/ubuntu-14.04",
  },
  {
    :name => "ubuntu-1604",
    :box => "bento/ubuntu-16.04",
  },
  {
    :name => "debian-89",
    :box => "bento/debian-8.9",
  },
  {
    :name => "debian-92",
    :box => "bento/debian-9.2",
  },
]

Vagrant.configure("2") do |config|
  boxes.each do |box|
    config.vm.define box[:name] do |vms|
      vms.vm.box = box[:box]
      vms.vm.hostname = "ansible-#{role}-#{box[:name]}"

      vms.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
        v.customize ["modifyvm", :id, "--memory", "256"]
      end

      vms.vm.provision :ansible do |ansible|
        ansible.playbook = "tests/vagrant.yml"
        ansible.verbose = "vv"
      end
    end
  end
end
