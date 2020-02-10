


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
13. Pots obtenir una vista dels recursos en disc dur que ocupa docker amb la comanda:
```docker system df
```
14. Copia el fitxer zips.json del repositori al contenedor node primari del Replica Set. Fes servir la comanda *docker cp*. 
```docker cp zips.json mongodbreplicaset_mongodb-primary_1:/tmp/
```
15. Executa des del host la comanda que llegeix el contingut del directori /tmp del primari, per demostrar que hi és.
```docker exec -it mongodbreplicaset_mongodb-primary_1 ls /tmp
```
16. Entra en el node primari. Crea la base de dades test. crea un usuari de nom test, de password test. Assigna-li el rol adequat perquè pugui crear col·leccions, registres, etc.
```
use test
**db.createUser({user: "test", pwd: "test", roles: ["readWrite","dbAdmin"]})**
```
17. Comprova amb la comanda que permet obtenir els usuaris de la base de dades que l'usuari test s'ha creat correctament
``` 
db.getUsers()
```

19. A continuació fes servir:
```
docker exec -it mongodbreplicaset_mongodb-primary_1 mongoimport -u test -p test --db test --collection zips --file /tmp/zips.json
```
per importar la col·lecció zip.
20. Entra dins el primari. Comprova que la col·lecció s'ha creat dins la base de dades test i mostra el nombre de registres.

21. 
End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
