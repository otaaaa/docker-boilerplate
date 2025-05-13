# docker-boilerplate

## Node.js

### Run Node.js scripts

```
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  node:21.7 index.js
```

### Run bash in interactive mode

```
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  node:21.7 /bin/bash
```

### Run bash script as stdin

```
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  --entrypoint /bin/bash \
  node:21.7 \
    -c "npm install && \
        npm list"
```

# Puppeteer

```
docker run -i --init --cap-add=SYS_ADMIN --rm \
  -e PUPPETEER_EXECUTABLE_PATH=/usr/bin/google-chrome-stable \
  -v $(pwd):/home/pptruser \
  -w /home/pptruser \
  --platform linux/amd64 \
  ghcr.io/puppeteer/puppeteer:22 /bin/bash \
    -c "npm install && \
        npm start"
```

# Ruby

```
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  ruby:3.2 ruby script.rb
```

# Python

```
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  python:3.9 python main.py
```

# Terraform

```
docker run --rm -it \
  -e GOOGLE_APPLICATION_CREDENTIALS=/tmp/secrets/key.json \
  -v $GOOGLE_APPLICATION_CREDENTIALS:/tmp/secrets/key.json:ro \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  --entrypoint /bin/sh \
  hashicorp/terraform:1.8 \
    -c "terraform -version"
```

# bin/run

```
#!/bin/sh -eu

readonly PYTHON_VERSION=3.9
readonly WORK_DIR=$(git rev-parse --show-toplevel)

docker run -it --rm \
  -e HOME=/usr/src/app \
  -v ${WORK_DIR}:/usr/src/app \
  -w /usr/src/app \
  python:${PYTHON_VERSION} python main.py
```

```
chmod +x bin/run
```


# Machine Learning

```
docker run -it --rm \
  --entrypoint bash \
  condaforge/miniforge3 -c "conda install -y numpy && \
                            conda install -y pandas && \
                            conda install -y jupyter && \
                            conda install -y matplotlib && \
                            exec /bin/bash"
```
