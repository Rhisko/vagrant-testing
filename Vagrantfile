
Vagrant.configure("2") do |config|
  # Using Ubuntu 20.04 as the base box
  config.vm.box = "ubuntu/focal64"

  # Defining VMs for the mysqlDB cluster
  (1..3).each do |i|
    config.vm.define "mysql#{i}" do |mysql|
      # Configuring private network, different IP for each VM
      config.ssh.insert_key=false
      mysql.vm.network "private_network", ip: "192.168.56.1#{i}"

      # VM resource specifications
      mysql.vm.provider "virtualbox" do |vb|
        vb.name = "mysql#{i}"
        vb.memory = "1024" # Allocating 1GB memory, adjust as needed
        vb.cpus = 2        # Allocating 2 CPUs, adjust as needed
      end
      config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      apt-get upgrade -y
      apt-get autoremove -y
      apt-get upgrade -y --with-new-pkgs
      apt install net-tools -y
    SHELL
      # Provisioning with shell script or Ansible (optional)
      # mysql.vm.provision "shell", path: "path/to/script.sh"
      # or
      # mysql.vm.provision "ansible" do |ansible|
      #   ansible.playbook = "path/to/playbook.yml"
      # end
    end
  end
end
