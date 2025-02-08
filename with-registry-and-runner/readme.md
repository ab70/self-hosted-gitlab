### Run the docker compose
```
docker compose up --build --force-recreate
```

Now you can visit your GitLab dashboard at http://localhost:8000
Setup a new Repository

Once you are logged in with your defined user and password from the docker-compose.yml file, Go ahead and create a new repository/project

### Sample ci-cd to push code in gitlab container registry
```
build:
    stage: build
    image: docker:latest
    tags:
        - docker
    script:
        - echo "$CI_REGISTRY_PASSWORD" | docker login $CI_REGISTRY -u $CI_REGISTRY_USER --password-stdin
        - docker build -t "$CI_REGISTRY_IMAGE:${CI_COMMIT_SHA:0:8}" .
        - docker push "$CI_REGISTRY_IMAGE:${CI_COMMIT_SHA:0:8}"
```

and then run that copied docker pull command on our local terminal
```
docker pull localhost:5001/root/build-with-lal:96e63838
```
Docker Image from the registry is private and need authentication (Default).

#### login to our container registry using docker login
```
docker login --username abrar@gmail.com --password abrar12345678 localhost:5001
```