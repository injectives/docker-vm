require "yaml"

_config_path = File.join(File.dirname(__FILE__), "config.yml")
_config = File.exist?(_config_path) ? YAML.load_file(_config_path) : {}
_shared_dir = _config["shared_dir"] || "#{Dir.home}"

Vagrant.configure("2") do |config|
    config.vm.box = "hashicorp/bionic64"
    config.vm.box_version = "1.0.282"
    config.vm.provider "virtualbox" do |vb|
        vb.cpus = _config["cpus"] || 4
        vb.memory = _config["memory"] || 8192
    end
    config.vm.network "private_network", ip: _config["ip"] || "192.168.99.10"
    config.vm.synced_folder _shared_dir, _shared_dir

    config.vm.provision "shell", inline: <<INLINE
        sudo apt-get update && apt-get install -y \
            apt-transport-https \
            ca-certificates \
            curl \
            gnupg-agent \
            software-properties-common
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        sudo add-apt-repository \
            "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
            $(lsb_release -cs) \
            stable"
        sudo apt-get update && apt-get install -y \
            docker-ce \
            docker-ce-cli \
            containerd.io
        sudo usermod -a -G docker vagrant
        sudo mkdir -p /etc/systemd/system/docker.service.d
        sudo cp /vagrant/docker.conf /etc/systemd/system/docker.service.d/docker.conf
        sudo cp /vagrant/daemon.json /etc/docker/daemon.json
        sudo systemctl daemon-reload
        sudo systemctl restart docker
INLINE
end
