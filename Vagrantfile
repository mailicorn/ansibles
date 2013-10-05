# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "opscode-f19-64"
  config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode-fedora-19_provisionerless.box"
  config.vm.network :forwarded_port, guest: 9300, host: 9300, auto_correct: true

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize ["modifyvm", :id, "--memory", "1500"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
    # This allows symlinks to be created within the /vagrant root directory, 
    # which is something librarian-puppet needs to be able to do. This might
    # be enabled by default depending on what version of VirtualBox is used.
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end
  config.vm.provision :ansible do |ansible|
    ansible.node_name = "ryansb-local"
    ansible.sudo = true
    ansible.verbose = true
    ansible.playbook = "provisioning/all.yml"
  end
end
