##################################
#                                #
#    PREREQUISITES               #
#                                #
##################################


# go to your folder that contains the vagrant file

# bring up the virtualmachine
vagrant up

# ssh into the virtualmachine
vagrant ssh


# install git
sudo apt install  git -y

# install curl
sudo apt install curl -y

# install docker
sudo apt install build-essential -y
sudo apt install apt-transport-https ca-certificates gnupg-agent software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose -y
sudo usermod -aG docker $USER
newgrp docker

# install go

    # go1.14.linux-amd64.tar.gz

curl -o "go.tar.gz" https://storage.googleapis.com/golang/...
sudo tar -C /usr/local -xzf "go.tar.gz"

export PATH=$PATH:/usr/local/go/bin
source ~/.bashrc

# install node
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt install nodejs -y

# install ohmyzsh
sudo apt install zsh -y
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"



