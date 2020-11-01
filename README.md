# Docker Project :

## MongoDB - Redis - NodeJS :

This project use nodejs for the backend part, mongoDB for the database and nginx for the proxy.  
The `docker-compose.yml` file will create the different containers. Each container will be connected through network created by the same file.

## How to use ?
* Clone the repo
* `cd api/` then `yarn install`
* `cd ..` then `docker-compose up`
* Open the brower at [localhost](http://localhost/hello/world)

## Why ?
Actually the application has no purpose but it's fully fonctional to add a nodeJs application.
