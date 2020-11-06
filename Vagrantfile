
Vagrant.configure("2") do |config|
  server_configs = [    			
    {"hostname" => "master", "ip" => "192.168.30.2", "port" => 2290, "memory_size" => "1024", "cpus" => 1, "execute_script" => true, "run" => "once"},  
    {"hostname" => "node1", "ip" => "192.168.30.3", "port" => 2291, "memory_size" => "1024", "cpus" => 1, "execute_script" => false, "run" => ""},    
    # {"hostname" => "node2", "ip" => "192.168.30.4", "port" => 2292, "memory_size" => "1024", "cpus" => 1, "execute_script" => false, "run" => ""}  
  ]

  $script  = "
    sudo apt-get -y update
    sudo apt install -y software-properties-common
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    sudo apt-get install -y sshpass
    sudo apt-get install -y ansible
    sudo apt-get install -y dos2unix
    cd ansible-playbook
    cp vagrant/insecure_private_key /home/vagrant/.ssh/id_rsa
    cp vagrant/ssh_config /home/vagrant/.ssh/config
    chmod -R og-rwx /home/vagrant/.ssh
    chown -R vagrant.vagrant /home/vagrant/.ssh
    sudo cp vagrant/ansible.cfg /etc/ansible/ansible.cfg
    cd source
    git config core.filemode false
  "

  server_configs.each do |server_config|
    config.vm.define "#{server_config['hostname']}" do |server|
      server.vm.hostname = server_config['hostname']
      server.vm.box = "bento/ubuntu-16.04"
      server.vm.network :private_network, ip: server_config['ip']
      server.vm.network :forwarded_port, guest: 22, host: server_config['port'], id: "ssh"
      server.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", server_config['memory_size']]
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["setextradata", :id, "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 0]
      end
      server.vm.synced_folder ".", "/home/vagrant/ansible-playbook", owner: "vagrant", group: "vagrant", :create => true, :mount_options => ["fmode=777", "dmode=777"]
      if server_config['execute_script'] then
        server.vm.provision :shell, inline: $script, run: server_config['run'] 
      end
      server.ssh.private_key_path = "./vagrant/insecure_private_key"
      server.ssh.insert_key = false
    end
  end
end
