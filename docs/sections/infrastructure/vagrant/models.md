# Models
<hr>
<br>

#### Vagrantfile with shell provision
```ruby
VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
    sudo apt-get update
    sudo apt-get install -y curl
    curl -fsSL get.docker.com -o get-docker.sh
    sh get-docker.sh
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "m2" do |m2|
    m2.vm.box = "generic/ubuntu1804"
    m2.vm.network "forwarded_port", guest: 80, host: 8080
    m2.vm.network "forwarded_port", guest: 443, host: 8443
  end
  config.vm.provision "shell", inline: $script
  config.ssh.username = "vagrant"
end
```
