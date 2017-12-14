# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu-16-04-x64"

  config.vm.define "microServiceMachine" do |microServiceMachine|
    microServiceMachine.vm.hostname = 'microServiceMachine'
    microServiceMachine.vm.network "private_network", ip: "192.168.50.100"
    microServiceMachine.vm.network "forwarded_port", guest: 8080, host: 8080, guest_ip: "192.168.50.100", host_ip:"127.0.0.1"

    microServiceMachine.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
      vb.customize ["modifyvm", :id, "--name", "DockerMicroservice_microServiceMachine"]
    end

    microServiceMachine.vm.provision "docker" do |d|
      d.build_image "/vagrant", args: "-t maury/microservice"
      d.run "maury/microservice", args: "-p 8080:8080 -t maury/microservice"
    end
  end

  if Vagrant.has_plugin?("vagrant-cachier")
  config.cache.scope = :box
  end
end