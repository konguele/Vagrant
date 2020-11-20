# Vagrant
Movidas con Vagrant

Paso1: Instalación VirtualBox:

https://download.virtualbox.org/virtualbox/6.1.12/VirtualBox-6.1.12-139181-Win.exe

Paso2: Instalación de Vagrant:

https://releases.hashicorp.com/vagrant/2.2.9/vagrant_2.2.9_x86_64.msi

Nota: Observe la ruta de instalación

Paso3: Entramos nuestro command Prompt y Creamos nuestro directorio para Vagrant:

Ventanita --> cmd

mkdir vagrant_juanjo

cd vagrant_juanjo

Paso4: Verificamos si tenemos algún Boxes:

C:\HashiCorp\Vagrant\bin\vagrant.exe box list

Paso5: Vamos agregar un Box:

C:\HashiCorp\Vagrant\bin\vagrant.exe box add 'bento/centos-8' 

Nota: Leed bien si solicitar seleccionar tu virtualizado:

  1) parallels
  2) virtualbox
  3) vmware_desktop
  
Paso6: Vamos Listar Los box disponibles:

C:\HashiCorp\Vagrant\bin\vagrant.exe box list

Paso7: Vamos crear nuestro Vagrantfile de una de las distro descargada:

C:\HashiCorp\Vagrant\bin\vagrant.exe init bento/centos-8 

dir

Paso8: Iniciamos el despliegue de nuestra distro:

C:\HashiCorp\Vagrant\bin\vagrant.exe up 

Nota: Revisa tu virtualbox que ahora ya debe tener una maquina virtual :)

Paso9: Eliminamos esa maquina virtual:

C:\HashiCorp\Vagrant\bin\vagrant.exe destroy -f 

Paso10: Vamos ha personalizar nuestro vagrantfile:

Nota: Reemplace el contenido por este:

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
  
Paso11: Despleguemos:

C:\HashiCorp\Vagrant\bin\vagrant.exe up 

Nota: Note que luego de la creación de la primera maquina descargara una nueva :) CentOS-7.6

Nota: Revisa tu VirtualBox :P
