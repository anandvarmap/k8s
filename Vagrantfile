# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'
Vagrant.configure(2) do |config|
  config.vm.provision "shell", path: "bootstrap.sh"
  # Kubernetes Master Server set up
  config.vm.define "k8s-master" do |k8s-master|
    k8s-master.vm.box = "bento/ubuntu-18.04"
    k8s-master.vm.hostname = "k8s-master.domain.com"
    k8s-master.vm.network "private_network", ip: "192.168.50.100"
    k8s-master.vm.provider "virtualbox" do |v|
      v.name = "k8s-master"
      v.memory = 2048
      v.cpus = 2
    end
    k8s-master.vm.provision "shell", path: "bootstrap_k8s-master.sh"
  end

#Change the value to have number of nodes for your k8s cluster.
  NodeCount = 2
  (1..NodeCount).each do |i|
    config.vm.define "k8s-worker#{i}" do |workernode|
      workernode.vm.box = "bento/ubuntu-18.04"
      workernode.vm.hostname = "k8s-worker#{i}.domain.com"
      workernode.vm.network "private_network", ip: "192.168.50.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "k8s-worker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      workernode.vm.provision "shell", path: "bootstrap_k8s-worker.sh"
    end
  end

end
