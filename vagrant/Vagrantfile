VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["C:/Users/somma/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "C:/Users/somma/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "file", source: "C:/Users/somma/.ssh/id_rsa", destination: "~/.ssh/id_rsa"
  config.vm.provision "file", source: "C:/Users/somma/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo service ssh restart
  EOC
# Script

	$jenkins_script = <<-SCRIPT
      wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
      sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
      sudo apt-get update
      sudo apt-get install default-jre -y
      sudo apt-get install jenkins -y
    SCRIPT

    $docker_script = <<-SCRIPT
      sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo apt-key fingerprint 0EBFCD88
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      sudo apt-get update
      sudo apt-get install docker-ce -y
      sudo groupadd docker
      sudo usermod -aG docker vagrant
      sudo systemctl enable docker
      sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose --silent
      sudo chmod +x /usr/local/bin/docker-compose
    SCRIPT

    $jenkins_node_script = <<-SCRIPT
      sudo apt-get update
      sudo apt-get install default-jre -y
    SCRIPT

    $mongodb_script = <<-SCRIPT
      sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
      echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
      sudo apt-get update
      sudo apt-get install -y mongodb-org
      sudo service mongod start
    SCRIPT

  ## Config
  
end