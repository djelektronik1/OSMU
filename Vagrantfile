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

  config.vm.define "ub1" do |uvm| # ������ ������
      uvm.vm.box = "ubuntu/trusty64" # ����� �� ������ �������� ����� ��������� ������

      uvm.vm.network "private_network", ip: "192.168.2.20" # ������ ���������� ���� � 
	                                                       # ���������� ������ �����
      uvm.vm.hostname = "ub1" # ������������� ��� ������
      uvm.vm.provider :virtualbox do |vb| # ������� ������������ � virtual box
          vb.name = "ubuntu1" # ����� ��� ������
          vb.gui = true # ������� virtual box ��� ����� ������� ��������� ���
          vb.cpus = 1 # �������� ���������� ����������� �� ������
          vb.memory = "1024" # ������������� ����� ���
      end
	    uvm.vm.synced_folder "folder/", "/home/vagrant/.ssh/"
	    uvm.vm.provision "shell", inline: $script # ��������� ������ ���������� ����     
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