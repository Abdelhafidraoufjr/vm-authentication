Vagrant.configure("2") do |config|
  # Utilisez une box de votre choix (par exemple Ubuntu)
  config.vm.box = "ubuntu/jammy64" # Ubuntu 22.04 LTS
  
  # Configurez les ressources de la VM
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8081, host: 8081
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048" # Mémoire de la VM
    vb.cpus = 2 # Nombre de cœurs de processeur
  end

  # Installation de JDK 17 et Gradle 8.10.0
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install -y openjdk-17-jdk
    wget https://services.gradle.org/distributions/gradle-8.10.0-bin.zip
    sudo unzip -d /opt/ gradle-8.10.0-bin.zip
    sudo ln -s /opt/gradle-8.10.0/bin/gradle /usr/bin/gradle
    echo "export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64" >> ~/.bashrc
    echo "export PATH=$PATH:/opt/gradle-8.10.0/bin" >> ~/.bashrc
    source ~/.bashrc
  SHELL

  # Montrez votre dossier de projet à l'intérieur de la VM
  config.vm.synced_folder ".", "/home/vagrant/app"
end
