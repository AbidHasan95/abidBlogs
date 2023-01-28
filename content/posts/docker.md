---
title: "Docker Guide"
date: 2023-01-25T00:25:03+05:30
tags: ['Docker', 'Linux']
showToc: true
draft: false
---
Install Docker on Raspberry Pi to turn the pi into a personal linux server which will keeps tabs on your favourite RSS feeds. View the feeds across your laptops, mobile devies, tabs etc. The feeds gets auto updated in the background.

## Installation
Docker can be installed using the official script.
```
curl -sSL https://get.docker.com | sh
```

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

**References**  
https://docs.docker.com/engine/install/linux-postinstall/  
https://web.yueh.dev/learning/init-vs-systemd-what-is-an-init-daemon
https://www.tecmint.com/systemd-replaces-init-in-linux/


## Usage
## Manipulation

Log in into the linux container, the image is based on
At first find the container ID through the following command
```
docker ps -a
```

Sample Output:
```
CONTAINER ID   IMAGE                                     COMMAND                  CREATED        STATUS                    PORTS                                              NAMES
aa410b4218cf   lscr.io/linuxserver/freshrss:latest       "/init"                  2 months ago   Up 11 minutes             443/tcp, 0.0.0.0:49999->80/tcp, :::49999->80/tcp   freshrss
0e69dcc8f603   heussd/fivefilters-full-text-rss:latest   "docker-php-entrypoi…"   2 months ago   Up 11 minutes             0.0.0.0:50000->80/tcp, :::50000->80/tcp            full-text-rss
d02a13dab696   hello-world                               "/hello"                 2 months ago   Exited (0) 2 months ago                                                      vigilant_feistel
```

For our use case, the container id is `aa410b4218cf`
Run the following command to log into the linux container with the container ID ```aa410b4218cf```
```
docker exec -u 0 -it aa410b4218cf /bin/bash
```
**References**
https://docs.docker.com/engine/reference/commandline/exec/

### List containers/images

`**docker ps**`

Usage:  docker ps [OPTIONS]

List containers

Options:
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -l, --latest          Show the latest created container (includes all states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display container IDs
  -s, --size            Display total file sizes

eg. `docker ps -a`
Lists all running containers

Output
```text
CONTAINER ID   IMAGE                                     COMMAND                  CREATED      STATUS                  PORTS                                              NAMES
8bbe30bc6e4e   heussd/fivefilters-full-text-rss:latest   "docker-php-entrypoi…"   3 days ago   Up 54 minutes           0.0.0.0:50000->80/tcp, :::50000->80/tcp            full-text-rss
dee018f60ede   lscr.io/linuxserver/freshrss:latest       "/init"                  3 days ago   Up 54 minutes           443/tcp, 0.0.0.0:49999->80/tcp, :::49999->80/tcp   freshrss
b610b5c7ca1b   hello-world                               "/hello"                 3 days ago   Exited (0) 3 days ago                                                      objective_germain
```

`docker image ls`

Usage:  docker image ls [OPTIONS] [REPOSITORY[:TAG]]

List images

Aliases:
  ls, list

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs

eg. docker image ls
Lists all images

Output
```text
REPOSITORY                         TAG       IMAGE ID       CREATED         SIZE
lscr.io/linuxserver/freshrss       latest    7dd0e9c24228   4 days ago      95.2MB
heussd/fivefilters-full-text-rss   latest    3d53fa431c51   5 days ago      332MB
hello-world                        latest    46331d942d63   10 months ago   9.14kB
```