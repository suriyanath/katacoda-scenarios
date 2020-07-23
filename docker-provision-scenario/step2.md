## Task

Initialize Vagrant in a specific directory:

`mkdir myvagrant && cd myvagrant`{{execute}}

Create Vagrantfile which contains container image details and credentials for ssh: 

`echo 'Vagrant.configure("2") do |config|
  ENV["VAGRANT_DEFAULT_PROVIDER"] = "docker"
  config.ssh.username = "root"
  config.ssh.password = "root"
  config.ssh.shell = "sh"
  config.vm.provider "docker" do |d|
    d.name = "vagrant_container"
    d.image = "suriyanath/alpine_ssh"
    d.has_ssh = true
  end
  config.vm.provision "shell", inline: "echo vagrant_likes_docker > truth.txt", privileged: false
end' > Vagrantfile`{{execute}}

The above configuration uses alpine image with ssh server running.

VAGRANT_DEFAULT_PROVIDER is an important environment variable that decides type of provider for vagrant. Note: vagrant can create VM in clouds or local machine and not just limited to creating containers.

The provision type is shell and the inline command will create file named truth.txt with content vagrant_likes_docker

Run vagrant command to bring up the container and provision to create file truth.txt:

`vagrant up`{{execute}}

Wait for the terminal log to end
