Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  
  config.vm.provision "shell", inline: "sudo echo TestPassword | passwd root --stdin"
  config.vm.provision "shell", inline: "adduser juanjo"
  config.vm.provision "shell", inline: "sudo echo TestPassword | passwd juanjo --stdin"
  config.vm.provision "shell", inline: "echo LC_CTYPE=en_US.UTF-8 >>  /etc/environment  "
  config.vm.provision "shell", inline: "
  echo '
  #Este es mi server de pruebas 
  #Puedes ver mis movidas en https://github.com/konguele' > /etc/motd"
  
  config.vm.define :acl do |acl|
  acl.vm.box = "bento/centos-8"
  acl.vm.hostname = "Master.fcld.acl"
  acl.vm.network :private_network, ip: "192.168.56.105"
  acl.vm.provider :virtualbox do |vb|
  vb.memory = 2068
  vb.cpus = 1
  vb.name = "Master-CentOS-8"
  end
  end
  
  config.vm.define :fcld do |fcld|
  fcld.vm.hostname = "Slave.fcld.acl"
  fcld.vm.box = "bento/centos-7.6"
  fcld.vm.network :private_network, ip: "192.168.56.106"
  fcld.vm.provider :virtualbox do |vb|
  vb.memory = 2068
  vb.cpus = 1
  vb.name = "Slave-CentOS-7"
  end
  end
  end
