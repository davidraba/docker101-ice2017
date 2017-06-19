## 1.0 Executant el primer container
Un cop ho tenim tot configurat, és hora d'embrutar-se les mans. En aquesta secció, executarem un container [Alpine Linux](http://www.alpinelinux.org/) (una distribucio especialment lleugera de linux) al nostre sistema i testejar el comandament `docker run`.

Per començar executeu la següent comanda al vostre terminal:

```
$ docker pull alpine
```

> Nota: Depenent de com hagueu fet la instal·lació al vostre sustema, podria ser que us donés un error de `permission denied` després d'executar el l'ordre. Si ets a un Mac ves a [verify your installation](https://docs.docker.com/mac/step_one/). Si ets a un Linux, fes ús del prefixe sobre el comandament `docker` amb `sudo`. Alternativament pots crear un grup específic per docker [create a docker group](http://docs.docker.com/engine/installation/ubuntulinux/#create-a-docker-group) per evitar aquest avís d'error.

El comandament `pull` recupera una imatge d'Alpine **image** des de el **Docker registry** i la guarda al teu sistema. Pots usar el comandament `docker images` per veure la llista d'imatges disponibles al teu sistema.

```
$ docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
alpine                 latest              c51f86c28340        4 weeks ago         1.109 MB
hello-world             latest              690ed74de00f        5 months ago        960 B
```

### 1.1 Docker Run
Ara executarem aquest **container** basat en aquesta imatge. Per fer-ho utilitzarem la comanda `docker run`.

```
$ docker run alpine ls -l
total 52
drwxr-xr-x    2 root     root          4096 May 25 15:18 bin
drwxr-xr-x    5 root     root           340 Jun 18 19:36 dev
drwxr-xr-x    1 root     root          4096 Jun 18 19:36 etc
drwxr-xr-x    2 root     root          4096 May 25 15:18 home
drwxr-xr-x    5 root     root          4096 May 25 15:18 lib
drwxr-xr-x    5 root     root          4096 May 25 15:18 media
drwxr-xr-x    2 root     root          4096 May 25 15:18 mnt
......
......
```
Què ha succeït? Molta cosa ha passat per sota. Quan cridem `run`, el client Docker cerca la imatge (alpine en aquest cas), crea el container i llavors executa la comanda dins aquest container. Quan executem `docker run alpine`, i proveim la comanda (`ls -l`), s'executa i per això veiem aquesta sortida.

Provem amb:

```
$ docker run alpine echo "hello from alpine"
hello from alpine
```
Torna a passar lo mateix. Veiem com de ràpid és el procés. Imagineu com seria arrencar una màquina virtual, executar la comanda i després parar-la. Per això es parla de que els containers son ràpids.

Provem un altra.
```
$ docker run alpine uptime
00:16:48 up  1:48,  0 users,  load average: 0.00, 0.01, 0.04
```

Provem un altra.
```
$ docker run alpine /bin/sh
```

Espera, no ha passat res. No és un error. Aquestes terminals de comandes finalitzen després d'executar-se a menys que s'executin a un terminal interactiu, així, per aquest exemple caldria executar-ho com a `docker run -it alpine /bin/sh`.

You are now inside the container shell and you can try out a few commands like `ls -l`, `uptime` and others. Exit out of the container by giving the `exit` command.

Ara sou a dins el la terminal de comandes del container. Podeu fer un  `docker ps`. La comanda `docker ps` mostra tots els container que s'estàn executant.

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

És buit perque no s'està executant cap container. Si fem un `docker ps -a`

```
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
36171a5da744        alpine              "/bin/sh"                5 minutes ago       Exited (0) 2 minutes ago                        fervent_newton
305297d7a235        alpine             "uptime"                  5 minutes ago       Exited (0) 4 minutes ago                        distracted_goldstine
a6a9d46d0b2f        alpine             "echo 'hello from alp"    6 minutes ago       Exited (0) 6 minutes ago                        lonely_kilby
ff0a5c3750b9        alpine             "ls -l"                   8 minutes ago       Exited (0) 8 minutes ago                        elated_ramanujan
c317d0a9e3d2        hello-world         "/hello"                 34 seconds ago      Exited (0) 12 minutes ago                       stupefied_mcclintock
```

El que podem veure és una llista de containers que has executat. La columna `STATUS` mostra que van sortir fa pocs minuts. Podem executar més d'una comanda a un container? Provem:

```
$ docker run -it alpine /bin/sh
/ # ls
bin      dev      etc      home     lib      linuxrc  media    mnt      proc     root     run      sbin     sys      tmp      usr      var
/ # uptime
 05:45:21 up  5:58,  0 users,  load average: 0.00, 0.01, 0.04
```
Executant `run` amb el flag `-it` entrem a la linea de comandes del container i el podem fer servir com si fos el sistema operatiu host d'on venim. Podeu provar les que us facin gràcia: df, top, echo, etc.

> **Zona de perill**: Si ets aventurer i t'atreveixes a executar `rm -rf /bin` dins el container, assegura't de que ets al container i **no** a la màquina host. Acabem d'eliminar les principals eines del sistema peratiu. Podeu comprovar com si sortiu del terminal fent un `exit`, si torneu a entrar amb la comanda `docker run -it alpine sh` tot està correcte. Docker instancia cada cop la màquina a partir de la images utilitzada, així el container no guarda l'estat.

Va be familiaritzar-se amb la comanda `docker run` ja que serà una de les que més utilitzareu. Per trobar més informació podeu fes servir `docker run --help` per veure la llista de modificadors que suporta.
### 1.2 Terminologia
A la darrera secció, heu pogut veure un seguit de termes associats a docker que al principi poden portar a confusió. Així que, abans de seguir, deixem clars alguns d'aquests termes:

- *Images* - Consta del sistema de fitxers i configuracions de la vostra aplicació que son utilitzats per crear els **containers**. Per tenir més informació de la imatge, executa `docker inspect alpine`. A l'execmple anterior es va utilitzar `docker pull` per descarregar laimatge d' **alpine**. Quan executem la comanda `docker run hello-world`, també s'utilitza `docker pull` sense que es vegi per descarregar la imatge **hello-world**.
- *Containers* - Creats utilitzant imatges docker i executen l'aplicació desitjada. Hem creat un utilitzant `docker run`. La llista de container executant-se la podem veure usant `docker ps`.
- *Docker daemon* - És el servei que s'executa en segón pla al host que gestiona la creació, execució i distribució de containers.
- *Docker client* - És a eina de comandes que permet a l'usuari interactuar amb Doker daemon.
- *Docker Hub* - És un [registre](https://hub.docker.com/explore/) d'imatges Docker. Podem veure el registre com un directori de totes les imatges disponibles.

## Següents passes
Seguidament anirem a [2.0 Webapps amb Docker](./webapps.md)
