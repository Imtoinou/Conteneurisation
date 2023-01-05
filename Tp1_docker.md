# h1Conteneurisation

## TP1

Antoine Zachariades
Roy Sarkis

### Exécuter un serveur web (apache, nginx, ...) dans un conteneur docker

Pull de l'image: `docker pull httpd`
Image apache : ![](https://i.imgur.com/9faP2os.png)

Démarrage du conteneur avec le volume : `docker run -p 8080:80 -v /home/azachariades/Documents/Ecole/Ynov_M1/docker_tp/Conteneurisation:/usr/local/apache2/htdocs/ httpd:latest`

Affichage de l'exemple index.html : ![](https://i.imgur.com/KmiFsci.png)

Execution de l'image httpd avec une copie du fichier index : `sudo docker cp ./Conteneurisation/index.html 168ba01058b6:/usr/local/apache2/htdocs/`

### 6 builder une image

build de l'image :
```
sudo docker build -t httpd:tp1 .
Sending build context to Docker daemon  60.93kB
Step 1/2 : FROM httpd:latest
 ---> 73c10eb9266e
Step 2/2 : COPY index.html /usr/local/apache2/htdocs/
 ---> Using cache
 ---> 0131af15ec69
Successfully built 0131af15ec69
Successfully tagged httpd:tp1
```
Exécution de l'image : `docker run -p 8080:80 -d httpd:tp1`

La différence est qu'ici nous créons une image tout d'un coup avec le dockerfile 
tant dis que la commande docker cp elle va copier un fichier dans un conteneur, ce sont des utilisations différentes.

### 7 Utiliser une base de données dans un conteneur docker

Pull de l'image mysql : `docker pull mysql:5.7`
Pull de l'image Myphpmyadmin : `docker pull phpmyadmin/phpmyadmin`

Exécution des conteneurs 
`docker run --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7`
`docker run --name phpmyadmin --link mysql:db -p 8080:80 -d phpmyadmin/phpmyadmin`

### 8 docker-compose.yml

 Docker Compose rend la gestion de conteneurs multiples très simple, en permettant de définir tous les conteneurs nécessaires dans un fichier de configuration unique. Il permet aussi de définir l'ensemble des variables d'environnement 

Le meilleur moyen de configurer premier utilisateur, première base de
données, mot de passe root au lancement et d'utiliser la variable -e

### 9 Observation de l’isolation réseau entre 3 conteneurs

La commande docker network inspect permet d'afficher des informations détaillées sur un ou plusieurs réseaux Docker. 

avec la commande : `docker network inspect frontend` et `docker network inspect backend`




