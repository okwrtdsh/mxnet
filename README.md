# mxnet [![](https://img.shields.io/docker/stars/okwrtdsh/mxnet.svg)![](https://img.shields.io/docker/pulls/okwrtdsh/mxnet.svg)![](https://img.shields.io/docker/automated/okwrtdsh/mxnet.svg)![](https://img.shields.io/docker/build/okwrtdsh/mxnet.svg)](https://hub.docker.com/r/okwrtdsh/mxnet/)
## How to Use

### CPU
1. docker-compose.yml (image: `okwrtdsh/mxnet:latest`)

```yml
version: '3'
services:
  jupyter:
    image: okwrtdsh/mxnet:latest
    ports:
      - '8888:8888'
    volumes:
      - ./notebooks:/src/notebooks
```

2. Run with docker-compose

```bash
$ docker-compose up -d
```

3. Open `http://localhost:8888` in web browser

### GPU
1. docker-compose.yml (image: `okwrtdsh/mxnet:gpu`)

```yml
version: '3'
services:
  jupyter:
    image: okwrtdsh/mxnet:gpu
    ports:
      - '8888:8888'
    volumes:
      - ./notebooks:/src/notebooks
```

2. run with nvidia-docker-compose

```bash
$ nvidia-docker-compose up -d
```

3. Open `http://localhost:8888` in web browser
