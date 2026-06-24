Vagrant.configure("2") do |config|
  config.vm.box = "cloudicio/ubuntu-server"
  config.vm.box_version = "24.04.1"

  config.vm.network "forwarded_port", guest: 8000, host: 8000

  config.vm.synced_folder ".", "/vagrant",
    type: "rsync",
    rsync__exclude: [".git/", ".vagrant/", ".venv/"]

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y python3-venv zip unzip rsync

    if ! grep -q "alias python='python3'" /home/vagrant/.bash_aliases 2>/dev/null; then
      echo "alias python='python3'" >> /home/vagrant/.bash_aliases
    fi

    chown vagrant:vagrant /home/vagrant/.bash_aliases
  SHELL
end
