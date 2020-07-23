## Task

Initialize Vagrant in a specific directory to create Vagrantfile:

`mkdir myvagrant && cd myvagrant`{{execute}}

`vagrant init`{{execute}}

`ls`{{execute}}

Modify Vagrantfile to create docker container and provision: 

`echo 'Vagrant.configure("2") do |config|
  ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'
  config.ssh.username = "root"
  config.ssh.password = "root"
  config.ssh.shell = "sh"
  config.vm.provider "docker" do |d|
    d.name = "vagrant_container"
    d.image = "suriyanath/alpine_ssh"
    d.has_ssh = true
  end
  config.vm.provision "shell", inline: "echo 'vagrant likes docker' > truth.txt", privileged: false
end' > Vagrantfile`{{execute}}

Run vagrant:

`vagrant up`{{execute}}

Wait for the terminal log to end
