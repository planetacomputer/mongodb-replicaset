
# MongoDB Replica Set

En aquest workshop farem servir la imatge Docker de bitname per instanciar tres contenidors MongoDB amb autenticació que conformen un Replica Set de forma automàtica.

## Getting Started

### Prerequisites

 1. Quants nodes hi ha en el Replica Set segons docker-compose.yml?
 2. Quins tipus de nodes hi ha?

### Installing
Descarrega el projecte i inicia docker-compose
```
docker-compose up -d
```

 3. Comprova que s'ha instanciat tots els contenidors
	 ``` 
	 docker network ls
	 docker inspect ls 
    ```
    
 5. Comprova que s'ha creat la xarxa que conté els contenidors. Inspecciona-la i anota les ips de cada contenidor dins ella.
	 ```
	 ```
 6. Esbrina les ips de cada contenidor fent una inspecció a cada contenidor per separat

And repeat

```
until finished
```

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