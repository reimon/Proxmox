# Proxmox

Working install of Docker-CE in LXC unprivileged container in Proxmox

apt update -y  && apt upgrade -y && apt install curl gnupg -y && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

echo "deb [arch=amd64] https://download.docker.com/linux/debian buster stable" >> /etc/apt/sources.list

apt update -y && apt upgrade -y && apt install docker-ce -y
