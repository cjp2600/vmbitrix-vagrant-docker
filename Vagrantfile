Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.box_check_update = true
  config.vm.network "private_network", ip: "192.168.56.11"

  config.ssh.username="vagrant"
  config.ssh.password="vagrant"

  config.vm.network :forwarded_port, guest: 80, host: 8888, auto_correct: true
  config.vm.network :forwarded_port, guest: 3306, host: 8889, auto_correct: true
  config.vm.network :forwarded_port, guest: 5432, host: 5433, auto_correct: true

  # Заменить на своё доменное имя
  config.vm.hostname = 'bitrixapp.dev'
        
  config.vm.synced_folder "www", "/var/www", {:mount_options => ['dmode=777','fmode=777']}
  config.vm.provision :shell, :inline => "echo \"Europe/Moscow\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     # vb.gui = true
     vb.memory = "2048"
  end

  config.vm.provider "parallels" do |prl|
     # Display the VirtualBox GUI when booting the machine
     # vb.gui = true
     prl.update_guest_tools = true
     prl.memory = 2048
  end

  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  config.vm.provision :shell,
    :keep_color => true,
    :inline => "export PYTHONUNBUFFERED=1 && export ANSIBLE_FORCE_COLOR=1 && cd /vagrant/provisioning && ./init.sh",
    run: "always"

end
