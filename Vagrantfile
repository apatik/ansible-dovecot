$script = <<SCRIPT
sudo apt-get install software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get install -y ansible
sudo apt-get install -y python-pip
sudo pip install passlib
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.define "dovecot" do |dovecot|
  end

  config.vm.provider "virtualbox" do |v|
    v.linked_clone = true
  end

  config.vm.provision "shell", :inline => $script


  config.vm.provision "shell",
    :path => "vagrant_specs.sh",
    :upload_path => "/home/ubuntu/specs",
    # change role name below
    :args => "--install ansible-dovecot"
end
