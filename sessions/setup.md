## Setup

### Prerequisits
No hi ha cap requisit previ a banda de una certa experiència amb l'ús de la inteficie de comandes i l'editor de textes. Farem us de [Docker Hub](https://hub.docker.com/) al llarg de les sessions.

### Configurant el teu PC
La conofiguració de l'entorn és molt fàcil avuí dia i es disposa de instruccions i scripts adaptats per la majoria de distribucions i versiona de sistema operatiu.

La guia d'introducció (*getting started* guide a Docker) conté instruccions detallades per la configuració de Docker a [Mac](http://docs.docker.com/mac/step_one/), [Linux](http://docs.docker.com/linux/step_one/) i [Windows](http://docs.docker.com/windows/step_one/).

Un cop finalitzada la instal·lació pots testejar que funciona correctament:

```
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
03f4658f8b78: Pull complete
a3ed95caeb02: Pull complete
Digest: sha256:8be990ef2aeb16dbcb9271ddfe2610fa6658d13f6dfb8bc72074cc1ca36966a7
Status: Downloaded newer image for hello-world:latest

Hello from Docker.
This message shows that your installation appears to be working correctly.
...
```

Sovint un pas previ contempla configurar docker per no haver de necesitar permisos de root per poder operar [Docker without root privileges](https://docs.docker.com/engine/installation/linux/linux-postinstall/)

## Següents passes

Per continuar les sessions podeu clcak cap a [1.0 Executant el primer container ](alpine.md)
