# -*- mode: ruby -*-

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end
  config.vm.network "forwarded_port", guest: 4000, host: 4050

  # Sync Authorization Files
  config.vm.synced_folder "#{ENV['HOME']}", "/home/vagrant", type: "rsync",
                          rsync__args: ["-r", "--include=.netrc", "--exclude=*"]
  config.vm.synced_folder "#{ENV['HOME']}/.aws", "/home/vagrant/.aws"
  
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
  end

  config.vm.define "blog.mark-roddy.com" do |vm_config|
    vm_config.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
    end
  end

end
