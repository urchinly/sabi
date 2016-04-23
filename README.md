# [WABI-SABI](https://github.com/urchinly/wabi-sabi) - Digital Asset Management

Wabi and sabi are two of the key Japanese aesthetic concepts. Their definitions are not exact, but one can get a sense of them from a short discussion of them. Over time, the two have been combined to form a new word, wabi-sabi, meaning an aesthetic sensibility which includes these two related ideas. 

Open source Digital Asset Management platform of great simplicity and beauty.

## [Wabi](https://github.com/urchinly/wabi) [![Build Status](https://travis-ci.org/urchinly/wabi.svg?branch=master)](https://travis-ci.org/urchinly/wabi)

Wabi means things that are fresh and simple. It denotes simplicity and quietude, and also incorporates rustic beauty. It includes both that which is made by nature, and that which is made by man. It also can mean an accidental or happenstance element (or perhaps even a small flaw) which gives elegance and uniqueness to the whole, such as the pattern made by a flowing glaze on a ceramic object.

Wabi modules form the core components of our digital asset management solution.

## Sabi [![Build Status](https://travis-ci.org/urchinly/sabi.svg?branch=master)](https://travis-ci.org/urchinly/sabi)

Sabi means things whose beauty stems from age. It refers to the patina of age, and the concept that changes due to use may make an object more beautiful and valuable. This also incorporates an appreciation of the cycles of life, as well as careful, artful mending of damage.

Sabi modules form the custom components of our digital asset management solution.

### Build and Run

The Sabi modules require a running Wabi application, please the Wabi project for detailed instructions on how to start the Docker stack. Every Sabi module can be build and run with Maven `mvn clean spring-boot:run`, further every module has a _build.sh_ script for creating and running the module in a Docker container.

- Maven 3.2
- Java 8
- Docker 1.10
- Docker Compose 1.7.0

```
./haproxy/build.sh
./sabi-portal/build.sh

mvn clean install -P prod

docker-compose up

http://localhost:8888/

docker-compose scale portal=2
docker-compose restart haproxy
http://localhost:8888/stats

```

## Apache HTTP server benchmarking tool

We would love to hear from you, create your own [benchmark](http://httpd.apache.org/docs/2.2/programs/ab.html) and share the results.

```
sudo apt-get install -y apache2-utils
./ab-benchmark.sh
```

### Run wabi images in the Docker Cloud

[![Deploy to Docker Cloud](https://files.cloud.docker.com/images/deploy-to-dockercloud.svg)](https://cloud.docker.com/stack/deploy/)

### Maven Tips

Build a module

* `mvn clean install`

Run a module

* `mvn spring-boot:run`

* `mvn spring-boot:run -DskipTests`

* `mvn clean install && java -jar ./target/*.jar`

Check and format licence headers across the project

* `mvn license:check` 

* `mvn license:format` 

Check for latest versions

* `mvn versions:display-dependency-updates` 

* `mvn versions:display-plugin-updates`

* `mvn versions:display-property-updates`

### Docker Tips

Run one module

* `docker run -d -e "SPRING_PROFILES_ACTIVE=prod" -p 7088:7088 --rm --net=wabi_sabi-tier --name sabi-x -h sabi-x urchinly/sabi-x`
* `docker exec -it sabi-x /bin/sh`

Run all modules

* `docker-compose up` and `docker-compose down`

Remove all containers

* `docker rm $(docker ps -q -a)`

Remove all images

* `docker rmi $(docker images -q -a)`

Remove all volumes

* `docker volume rm $(docker volume ls -q -f dangling=true)`

