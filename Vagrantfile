# -*- mode: ruby -*-
# vi: set ft=ruby :

### Realy Nasty Hack to solve this issue:
# https://github.com/mitchellh/vagrant/issues/3083
`VBoxManage dhcpserver remove --netname HostInterfaceNetworking-vboxnet0`

Vagrant.configure("2") do |config|

  #Ubuntu x64 with chef
  config.vm.box = "chef/ubuntu-15.04"

  #---Networking---

  # Port forward 80 to 8080
  config.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true
  config.vm.network :forwarded_port, guest: 443, host: 8443, auto_correct: true
  config.vm.network :forwarded_port, guest: 3306, host: 8006, auto_correct: true

  config.vm.network "private_network", type: :dhcp

  #Uncomment this if you want bridged network functionality
  #config.vm.network :public_network

  config.vm.synced_folder "www/", "/var/www", group: "www-data", create: true

  #SS Shell Script
  config.vm.provision :shell, :path => "ss_provision.sh"

  #Enable SSH forwarding
  #refs
  # http://docs.vagrantup.com/v2/vagrantfile/ssh_settings.html
  # http://stackoverflow.com/questions/11955525/how-to-use-ssh-agent-forwarding-with-vagrant-ssh
  # https://help.github.com/articles/using-ssh-agent-forwarding
  config.ssh.forward_agent = true

end
