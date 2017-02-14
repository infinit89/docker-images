To update the docker image:

- Modify the Dockerfile with the dependencies or the code you want to add
- Build the image

```
docker build -t php-checker .
```

- Update the tag

```
docker tag php-checker:latest infinit89/php-checker
```

- Push it to dockerhub


```
docker push infinit89/php-checker
```# docker-images
