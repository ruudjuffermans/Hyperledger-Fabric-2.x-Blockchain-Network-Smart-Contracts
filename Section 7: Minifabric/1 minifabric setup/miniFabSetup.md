# Get minifab
mkdir -p ~/mywork && cd ~/mywork && curl -o minifab -sL https://tinyurl.com/twrt8zv && chmod +x minifab

# Download docker 19.04
sudo snap install docker

# Change docker.sock owner
sudo chown vagrant /var/run/docker.sock
