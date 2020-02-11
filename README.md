# MongoDB Replica Set

En aquest workshop farem servir la imatge Docker de bitname per instanciar tres contenidors MongoDB amb autenticació que conformen un Replica Set de forma automàtica.

## Getting Started

### Prerequisites

 1. Quants nodes hi ha en el Replica Set segons docker-compose.yml?
 2. Quina imatge Docker fan servir aquests contenidors? És la mateixa en tots ells?
 3. Quins tipus de nodes hi ha?

### Installing
Descarrega el projecte i inicia docker-compose
```
docker-compose up -d
```

 4. Comprova que s'ha instanciat tots els contenidors
	 ``` 
	 docker network ls
	 docker inspect ls 
    ```
    
 5. Comprova que s'ha creat la xarxa que conté els contenidors. Inspecciona-la i anota les ips de cada contenidor dins ella.
	 ```
	 docker inspect network mongodbreplicaset_default
	 ```
 6. Esbrina les ips de cada contenidor fent una inspecció a cada contenidor per separat
  ```
 docker inspect mongodbreplicaset_mongodb-secondary_1 | grep IPAddress
  ```
 7. Entra al programa mongo del contenidor que fa de primari al Replicat Set. I mostra per pantalla les bases de dades existents. Per defecte haurien de sortir-ne algunes.
 8. Entra al programa mongo del contenidor que fa de primari amb autenticació. Pots trobar les dades al *docker-compose*.
 ```
docker exec -it mongodbreplicaset_mongodb-primary_1 mongo -u root -p password123
```
 9. Connecta't al Replica Set mitjançant el client de línia de comanda mongoDB. Si per consola mostra errors fixa't i pensa de quina mena pots solucionar-los:

 ```
 mongo -u root -p password123 mongodb://172.19.0.3:27017,172.19.0.2:27017,172.19.0.4/admin?replicaSet=replicaset
  ```

 10. Quin volum s'ha creat amb *docker-compose*? Indica el nom i la ruta del punt de muntatge
```
docker volume ls
docker inspect volume mongodbreplicaset_mongodb_master_data
```
11. Abans has executat de manera autenticada mongo dins del contenidor primari. Fes el mateix amb el secundari i amb l'àrbitre. Hi ha alguna diferencia?
``` No es pot connectar a l'àrbitre
```
12. Connecta't al bash del contenidor àrbitre i des d'allà obre el client mongo.
```
docker exec -it mongocomposer_mongodb-arbiter_1 bash
```
13. Pots obtenir una vista dels recursos en disc dur que ocupa docker amb la comanda:
```docker system df
```
14. Copia el fitxer zips.json del repositori al contenedor node primari del Replica Set. Fes servir la comanda *docker cp*. 
```docker cp zips.json mongodbreplicaset_mongodb-primary_1:/usr/share/
```
15. Executa des del host la comanda que llegeix el contingut del directori /tmp del primari, per demostrar que hi és.
```docker exec -it mongodbreplicaset_mongodb-primary_1 ls /usr/share/
```
16. Entra en el node primari. Crea la base de dades test. crea un usuari de nom test, de password test. Assigna-li el rol adequat perquè pugui crear col·leccions, registres, etc.
```
docker exec -it mongocomposer_mongodb-primary_1 mongo -u root -p password123
use test
db.createUser({user: "test", pwd: "test", roles: ["readWrite","dbAdmin"]})
```
Per saber en quin usuari ets:
```db.runCommand({connectionStatus : 1})
```
17. Comprova amb la comanda que permet obtenir els usuaris de la base de dades que l'usuari test s'ha creat correctament
``` 
db.getUsers()
```
18. Com que sovint hi ha problemes de *too many authorized users* si vols entrar com test, el millor és sortir i entrar directament  com: 
```
docker exec -it mongocomposer_mongodb-primary_1 mongo --authenticationDatabase "test" -u test -p test
```
19. A continuació fes servir:
```docker exec -it mongodbreplicaset_mongodb-primary_1 mongoimport -u test -p test --db test --collection zips --file /usr/share/zips.json```

per importar la col·lecció zips.
20. Entra dins el primari. Comprova que la col·lecció s'ha creat dins la base de dades test i mostra el nombre de registres.
```docker exec -it mongodbreplicaset_mongodb-primary_1 mongoimport -u test -p test --db test --collection zips --file /usr/share/zips.json```
21. Imprimeix les col·leccions de test i el nombre de registres de zips

```use test
show collections
db.zips.find().count()
```

22. És possible obtenir els documents directament des del node primari? Connecta-t'hi i comprova-ho. Comprova si és possible obtenir informació sobre l'status del replicaset.
No és possible, però sí obtenir informació del cluster amb 
``` rs.status()
```
23. Connecta't al replicaset a la base de dades test i amb l'usuari test
```
 docker exec -it mongocomposer_mongodb-secondary_1 mongo --authentication
 ```
 

24. Atura el contenidor del node primari i comprova que ha estat així.
```
 docker stop mongocomposer_mongodb-primary_1
 docker ps
 ```
25. Connecta't al contenidor de nom secondary amb l'usuari test. Pots dur a terme les operacions que abans no podies dur a terme sobre la base de dades test? Indica què passa quan vols comprovar l'status del replicaset.
26.  Tornar a entrar al contenidor secondary però 

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [StackEdit]([https://stackedit.io/](https://stackedit.io/)) - Editor online de Markdown

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
