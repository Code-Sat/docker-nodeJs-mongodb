# Docker Project :

## MongoDB - Redis - NodeJS :

This project use nodejs for the backend part, mongoDB for the database and nginx for the proxy.  
The `docker-compose.yml` file will create the different containers. Each container will be connected through network created by the same file.

## How to use ?
* Clone the repo
* `cd api/` then `yarn install`
* `cd ..` then `docker-compose up`
* Open the brower at [localhost](http://localhost/hello/world)

## What is the goal ?
Actually the application has no purpose but it's fully fonctional to add a nodeJs application.


## Docker-compose file : 
```
version: "2"
services:
  api:
    image: node:boron
    depends_on:
      - mongodb
      - redis
    volumes:
      - ./api:/home/node/api/
    working_dir: /home/node/api
    command: yarn start
    networks:
      - backend
    logging:
      driver: "json-file"
      options:
        max-size: "100MB"
        max-file: "3"

  mongodb:
    image: mongo:3.0
    volumes:
      - mongodb:/data/db/
    networks:
      - backend
    logging:
      driver: "json-file"
      options:
        max-size: "100MB"
        max-file: "3"

  redis:
    image: redis:3.2-alpine
    networks:
      - backend
    volumes:
      - redis:/data/
    logging:
      driver: "json-file"
      options:
        max-size: "100MB"
        max-file: "3"

  nginx:
    image: nginx:stable-alpine
    depends_on:
      - api
    networks:
      - backend
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    ports:
      - "80:80"
      - "443:443"
    logging:
      driver: "json-file"
      options:
        max-size: "100MB"
        max-file: "3"

networks:
  backend:

volumes:
  mongodb:
  redis:
```


