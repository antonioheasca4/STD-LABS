# STD - LAB1
## Docker for begginers

### Task 0
- Am descarcat si instalat docker desktop
- Am clonat repository-ul linux_tweet_app

### Task 1
#### Single task container: docker container run alpine hostname
 - alpine:latest nu exitsa local deci se va face pull de pe docker hub
 - apoi, se executa comanda hostname in cadrul containerului

- docker container ls -a SAU docker ps -a
 - cointanerul inca exista in starea EXITED
 - ContainerID este exact outputul comenzii hostname
 - Cointainerele pot fi foarte utile deoarece iti poti construi propria imagine care sa faca ceva(un script de configurare de exemplu), iar oricine poate executa acest ceva(script) doar rulan containerul => nu are nevoie de script sau de alte informatii

#### Interactive Container: docker container run --interactive --tty --rm ubuntu bash
 - rulam un container ubuntu peste Alpine Linux Docker host( asta daca am rula comenzile in Play with Docker)
 - --interactive says you want an interactive session.
 - --tty allocates a pseudo-tty.
 - --rm tells Docker to go ahead and remove the container when it’s done executing.
 - Procesul principal(PID 1) al containerului va fi bash
  - ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  0.3  0.0   4588  3888 pts/0    Ss   22:23   0:00 bash
    root        10  0.0  0.0   7888  3804 pts/0    R+   22:23   0:00 ps aux
 - Cand containerul porneste, apare un prompt de forma root@<container id>:/#
 - CONTAINERELE INTERACTIVE sunt folositoare atunci cand le folosim pentru a ne genera propria imagine. Poti rula containerul si sa observi toti pasii necesari dezvoltarii aplicatiei tale, pe care mai apoi sa ii adaugi in Dockerfile-ul personal

#### Backround Cointainer:  docker container run --detach --name mydb -e MYSQL_ROOT_PASSWORD=my-secret-pw
                            mysql:latest
 -  --detach will run the container in the background.
 -  --name will name it mydb.
 -  -e will use an environment variable to specify the root password (NOTE: This should never be done in production).
 - Containerul va rula in fundal atat timp cat va rula procesul MySQL
 -  docker rename upbeat_borg mydb -> uitasem de optiunea --name
 - docker container ls => Se observa containerul care inca ruleaza
 - docker container logs mydb => putem vizualiza ceea ce sa intampla in containerul mydb
 - docker container top mydb => putem vizualiza procesele care ruleaza in container
 - Cu toate ca MySQL ruleaza, acest serviciu este izolat in container deoarece nu i-am specificat host-ului(laptopului meu) niciun port de retea => traficul de retea nu poate ajunge la container de la host pana cand nu sunt publicate explicit niste porturi
 - docker container exec --> Cand vrem sa rulam o comanda in interiorul  containerului 
 - docker container exec -it mydb mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
    mysql: [Warning] Using a password on the command line interface can be insecure.
    mysql  Ver 9.2.0 for Linux on x86_64 (MySQL Community Server - GPL)
 - docker exec -it mydb sh --> m am conectat la un shell in interiorul containerului ( pot face asta si din interfata docker desktop apasand pe container, sectiunea Exec)
 - sh-5.1#  mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
            mysql: [Warning] Using a password on the command line interface can be insecure.
            mysql  Ver 9.2.0 for Linux on x86_64 (MySQL Community Server - GPL)
            Am dat comanda din interiorul shell ului de data asta -> se observa verisunea 9.2.0 de 2 ori

### Task 2



### Task 3