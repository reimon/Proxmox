# Proxmox

Working install of Docker-CE in LXC unprivileged container in Proxmox

apt-get update -y  & apt-get upgrade -y & curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

echo "deb [arch=amd64] https://download.docker.com/linux/debian buster stable" > /etc/apt/sources.list

apt update -y & apt upgrade -y & apt install docker-ce
