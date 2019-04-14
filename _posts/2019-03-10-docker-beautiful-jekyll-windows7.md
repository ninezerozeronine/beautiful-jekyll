---
layout: post
title: Docker and Beautiful Jekyll on Windows 7
tags: [docker, beautiful-jekyll, development, windows7, virtualbox]
---

* Windows 7 doesn't support the Hypervisor so instead of Docker desktop That normally runs on Windows 10, docker toolbox needs to be used instead (https://docs.docker.com/toolbox/toolbox_install_windows/)
* Install docker toolbox
* VirtualBox gets installed
* Make sure that VMs/virtualisation is enabled in the computers BIOS
* Download kitematic
* Docker quickstart terminal (from the shortcut docker toolbox creates) warns about virtualisation if it isn't enabled.
* `docker build -t beautiful-jekyll "$PWD"` needs to be run in the directory containing the `Dockerfile` file
* "$PWD" can be replaced with the absolute path to the current directory
* As per https://stackoverflow.com/questions/50540721/docker-toolbox-error-response-from-daemon-invalid-mode-root-docker and https://stackoverflow.com/questions/47091139/docker-mount-project-error-response-from-daemon-on-windows-10 windows 7 directories cannot be mounted directly to docker containers. They must first be mounted in the virtual machine that Docker runs in.
* ![Virtual Machine](img/2019-03-10/mount-folder-vm.jpg)
* In this case, `C:\dev\groundtruths\docs` has been mounted to `/groundtruths` in the VM.
* The original docker un command is `docker run -d -p 4000:4000 --name beautiful-jekyll -v "$PWD":/srv/jekyll beautiful-jekyll`
* The -v describes how volumes (on the machine runnign Docker - The VM in this case) are mounted onto the Docker container.
* The command is changed to: `docker run -d -p 4000:4000 --name beautiful-jekyll -v "/groundtruths:/srv/jekyll beautiful-jekyll`
* Run that and the website is available at the normal http://localhost:4000/
