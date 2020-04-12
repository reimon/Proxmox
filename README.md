# Proxmox

Working install of Docker-CE in LXC unprivileged container in Proxmox

apt update -y  && apt upgrade -y
apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y

curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

echo "deb [arch=amd64] https://download.docker.com/linux/debian buster stable" >> /etc/apt/sources.list
   
 apt update -y && apt upgrade -y && apt install docker-ce -y
 
 
 
should return « Active (running) »
In case not (trick #1), work around the systemd bug by adding an “ExecStartPre=” to containerd service.
This link 79 has a clear explanation of the steps:
a) mkdir -p /etc/systemd/system/containerd.service.d
b) echo -e “[Service]\nExecStartPre=\n” > /etc/systemd/system/containerd.service.d/override.conf
c) systemctl daemon-reload
d) systemctl start docker
e) systemctl enable docker

Now the docker daemon should be OK ; it’s time for the second error:
docker run hello-world returns an error « mounting proc to rootfs…permission denied »

Fix it (trick #2) by inserting manually a line containing the following :

          features:  keyctl=1,nesting=1
in the config file of your LXC as documented in this Proxmox doc 212.
In Proxmox you find the LXC config here: /etc/pve/local/lxc/<container_id>.conf
So you have to do it via an SSH connection directly into your Proxmox host.

stop/start the LXC container
docker run hello-world gives you « Hello from Docker ! » now.
Enjoy!

However I can hardly appreciate whether “keyctl=1,nesting=1” could be regarded as a security concern of not. Maybe Stéphane can provide some light on this question.
