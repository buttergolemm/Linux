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

#run docker
docker compose up -d
````
## gophish [+ docker]
```
login: https://localhost:333
password: read from the command "docker-compose up"
````
````
#create gophish folder (/usr/local/bin/gophish/)
cd /usr/local/bin/
sudo mkdir gophish
cd gophish

#docker compose download -> /usr/local/bin/gophish/docker-compose.yml
sudo wget https://gist.githubusercontent.com/buttergolemm/6267ee15e8cde525daf20489bee578ae/raw/a506fc24202cf67a1d1aeb9462fa12909e6e733b/docker-compose.yml


#create folder -> (/usr/local/bin/gophish/src/secrets | docker-compose.yml)
sudo mkdir src
cd src
sudo mkdir secrets
cd secrets


#Download Configs (quelle:https://github.com/cisagov/gophish-docker)
sudo wget https://raw.githubusercontent.com/cisagov/gophish-docker/develop/src/secrets/admin_fullchain.pem
sudo wget https://raw.githubusercontent.com/cisagov/gophish-docker/develop/src/secrets/admin_privkey.pem
sudo wget https://raw.githubusercontent.com/cisagov/gophish-docker/develop/src/secrets/config.json
sudo wget https://raw.githubusercontent.com/cisagov/gophish-docker/develop/src/secrets/phish_fullchain.pem
sudo wget https://raw.githubusercontent.com/cisagov/gophish-docker/develop/src/secrets/phish_privkey.pem

cd /usr/local/bin/gophish

#run docker
docker-compose up
````
