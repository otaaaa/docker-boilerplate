# docker-boilerplate

## Node.js

### Run Node.js scripts

```bash
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  node:21.7 index.js
```

### Run bash in interactive mode

```bash
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  node:21.7 /bin/bash
```

### Run bash script as stdin

```bash
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

```bash
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

```bash
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  ruby:3.2 ruby script.rb
```

# Python

```bash
docker run -it --rm \
  -e HOME=/usr/src/app \
  -v $(pwd):/usr/src/app \
  -w /usr/src/app \
  python:3.9 python main.py
```

# Terraform

```bash
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

```bash
#!/bin/sh -eu

readonly PYTHON_VERSION=3.9
readonly WORK_DIR=$(git rev-parse --show-toplevel)

docker run -it --rm \
  -e HOME=/usr/src/app \
  -v ${WORK_DIR}:/usr/src/app \
  -w /usr/src/app \
  python:${PYTHON_VERSION} python main.py
```

```bash
chmod +x bin/run
```


# Machine Learning

```bash
docker run -it --rm \
  --entrypoint bash \
  condaforge/miniforge3 -c "conda install -y numpy && \
                            conda install -y pandas && \
                            conda install -y jupyter && \
                            conda install -y matplotlib && \
                            conda install -y scikit-learn && \
                            conda install -y seaborn && \
                            conda install -y graphviz && \
                            conda install -y python-graphviz && \
                            exec /bin/bash"
```
