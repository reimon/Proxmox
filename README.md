# Proxmox

Working install of Docker-CE in LXC unprivileged container in Proxmox

apt-get update -y  & apt-get upgrade -y & curl -fsSL https://download.docker.com/linux/<your_distro>/gpg | sudo apt-key add -

echo "deb [arch=amd64] https://download.docker.com/linux/debian <your_distro> stable" > /etc/apt/sources.list

apt update -y & apt upgrade -y & apt install docker-ce
