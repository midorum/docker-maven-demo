# Demo maven application with various variants docker building

### Covered variants

* single layer docker image - demonstrates redownloading dependencies with any project changes 
* layered docker image - demonstrates using docker layer cache to prevent redownloading dependencies
* buildkit chached image - demonstrates using buildkit cache to prevent redownloading dependencies
* multi staged image - demonstrates using docker layer cache in multi stage images


### How to use

#### Build docker image
* single layer docker image
  > docker build -f Dockerfile_single_layer --tag demo-app .
* layered docker image
  > docker build -f Dockerfile_layered_cached --tag demo-app .
* buildkit chached image
  > DOCKER_BUILDKIT=1 docker build -f Dockerfile_buildkit_cached --tag demo-app .
* multi staged image
  - development build
  > docker build -f Dockerfile_multi_stage --target development  --tag demo-app .
  - production build
  > docker build -f Dockerfile_multi_stage --tag demo-app .

#### Run built container

* detached mode
  > docker run --rm -d -p 8080:8080 --name demo-server demo-app
* attached mode 
  > docker run --rm -d -p 8080:8080 --name demo-server demo-app

#### Stop running container
> docker stop demo-server


### References

* [Minimal Spring Web application with Actuator](https://start.spring.io/#!type=maven-project&language=java&platformVersion=3.0.2&packaging=jar&jvmVersion=17&groupId=com.example&artifactId=demo&name=demo&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.demo&dependencies=actuator,web)
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
* [Optimizing builds with cache management](https://docs.docker.com/build/cache/)
* [Multi-stage builds](https://docs.docker.com/build/building/multi-stage/)
* [Maven Docker official image](https://hub.docker.com/_/maven/)
* [Caching Maven Dependencies with Docker](https://www.baeldung.com/ops/docker-cache-maven-dependencies)
* [Can You Mount a Volume While Building Your Docker Image to Cache Dependencies?](https://vsupalov.com/cache-docker-build-dependencies-without-volume-mounting/)
