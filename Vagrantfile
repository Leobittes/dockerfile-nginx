  # Define Versão do Linux, Habilita placa de rede e porta etc...
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "public_network"
  config.vm.synced_folder "website", "/home/leobittes/app" 
  config.vm.synced_folder "sync", "/home/leobittes"
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.boot_timeout
  
  # Configura Nome, Memória, Cpu etc...
  config.vm.provider "virtualbox" do |vb|
    vb.name = "dockerfile-Nginx"
    vb.memory = "1024"
    end
  
  config.vm.provision "shell", inline: <<-SHELL
   # Instala o Docker  
    apt-get update
    apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    apt-get update
    # instala o Docker-Compose
    apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    mkdir -m 0755 -p /etc/apt/keyrings
    chmod +x /usr/local/bin/docker-compose
    # Adiciona Usuario com ROOT sem senha
    adduser leobittes --disabled-password --gecos ""
    usermod -aG sudo leobittes
    SHELL
end
