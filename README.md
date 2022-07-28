# Linux Bootstrap

## bash
````
# force color prompt
sed -i 's/#force_color_prompt=yes/force_color_prompt=yes/g' ~/.bashrc

# l = ls -la
echo "# quick folder view: list folders + files, human readable!" | tee -a ~/.bashrc
echo "alias l='ls -lh --group-directories-first'" | tee -a ~/.bashrc

source ~/.bashrc

# copy .bashrc to root
sudo cp ~/.bashrc /root/.bashrc

# red prompt for root user
sudo sed -i 's/;32m/;31m/g' /root/.bashrc

# sudo without password
echo "$USER ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
````
## docker
````
# remove old versions
sudo apt-get remove docker docker-engine docker.io containerd runc

# setup docker APT repo
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg lsb-release

# Docker PGP
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# add docker stable Repo
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# install docker
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

# install docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-$(uname -s | awk '{ print tolower($0) }')-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
````
