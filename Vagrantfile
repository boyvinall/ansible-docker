# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.forward_agent = true
  config.vm.synced_folder Dir.getwd, "/home/vagrant/roles/ansible-docker", nfs: true

  # ubuntu 12.04 that Travis CI is using
  config.vm.define 'travis', primary: true do |c|
    c.vm.network "private_network", ip: "192.168.100.2"
    c.vm.box = "precise-server-cloudimg-amd64-vagrant-disk1"
    c.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-amd64-vagrant-disk1.box"
    c.vm.provision "shell" do |s|
      s.inline = "apt-get update -y; apt-get install python-software-properties; add-apt-repository ppa:rquillo/ansible; apt-get update -y; apt-get install ansible -y; cd /home/vagrant/roles/ansible-docker/tests; ansible-playbook -i inventory playbook.yml"
      s.privileged = true
    end
  end

  # ubuntu 14.04
  config.vm.define 'ubuntu', primary: true do |c|
    c.vm.network "private_network", ip: "192.168.100.3"
    c.vm.box = "trusty-server-cloudimg-amd64-vagrant-disk1"
    c.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
    c.vm.provision "shell" do |s|
      s.inline = "apt-get update -y; apt-get install -y software-properties-common; apt-add-repository ppa:ansible/ansible; apt-get update -y; apt-get install -y ansible; cd /home/vagrant/roles/ansible-docker/tests; ansible-playbook -i inventory playbook.yml"
      s.privileged = true
    end
  end

  # centos 7:
  config.vm.define 'centos7' do |c|
    c.vm.network "private_network", ip: "192.168.100.5"
    c.vm.box = "centos/7"
    c.vm.provision "shell" do |s|
      s.inline = "yum install -y epel-release; yum install -y ansible; cd /home/vagrant/roles/ansible-docker/tests; ansible-playbook -i inventory playbook.yml"
      s.privileged = true
    end
  end

end
