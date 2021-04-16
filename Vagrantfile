$script = <<END

       sudo apt-get update 
       apt-get install -y git-all
       sudo apt-get install docker-engine -y
       sudo service docker start
       sudo docker run hello-world
       ALL=(ALL) NOPASSWD:ALL >> /etc/sudoers
       usermod -aG wheel vagrant
     
END
Vagrant.configure("2") do |config|

  config.vm.define "ub1" do |uvm| # создаём машину
      uvm.vm.box = "ubuntu/trusty64" # образ на основе которого будет развёрнута машина

      uvm.vm.network "private_network", ip: "192.168.2.20" # создаём выделенную сеть и 
	                                                       # присвиваем машине адрес
      uvm.vm.hostname = "ub1" # Устанавливаем имя машины
      uvm.vm.provider :virtualbox do |vb| # передаём конфигурайию в virtual box
          vb.name = "ubuntu1" # задаём имя машины
          vb.gui = true # говорим virtual box что хотим увидеть интерфейс его
          vb.cpus = 1 # выделяем количество процеесвров на машину
          vb.memory = "1024" # устанавливаем объём озу
      end
	    uvm.vm.synced_folder "folder/", "/home/vagrant/.ssh/"
	    uvm.vm.provision "shell", inline: $script # выполняем скрипт написанный выше     
  end

  config.vm.define "ub2" do |uvm|
      uvm.vm.box = "ubuntu/trusty64"

      uvm.vm.network "private_network", ip: "192.168.2.10"
      uvm.vm.hostname = "ub2"

      uvm.vm.provider :virtualbox do |vb|
          vb.name = "ub2"
          vb.gui = true
          vb.cpus = 1
          vb.memory = "1024"
      end

      uvm.vm.provision "shell", inline: <<-SHELL
          sudo apt-get update
      SHELL
  end
end