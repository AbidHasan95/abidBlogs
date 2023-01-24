---
title: "Docker Guide"
date: 2023-01-25T00:25:03+05:30
tags: ['Docker', 'Linux']
draft: false
---
Install Docker on Raspberry Pi to turn the pi into a personal linux server which will keeps tabs on your favourite RSS feeds. View the feeds across your laptops, mobile devies, tabs etc. The feeds gets auto updated in the background.

## Installation
Docker can be installed using the official script.
```curl -sSL https://get.docker.com | sh```

## Post Installation Configuration

Add the current user to the docker group.
```sudo usermod -aG docker $USER```

### Configure Docker to start on boot with systemd

Many modern Linux distributions use systemd to manage which services start when the system boots. On Debian and Ubuntu, the Docker service starts on boot by default. To automatically start Docker and containerd on boot for other Linux distributions using systemd, run the following commands and reboot:

```sh 
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

To disable auto start on boot:
```sh
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```

### Check Installation
To check if the installtion has been successful, run the following command
```docker run hello-world```

### References
https://docs.docker.com/engine/install/linux-postinstall/