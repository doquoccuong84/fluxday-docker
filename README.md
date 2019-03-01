
# fluxday on docker
I have forked it from # [foradian/fluxday](https://github.com/foradian/fluxday) and fixed some configuration issues. 

## Installation
There are 2 options for your installation on Docker. Option 1 is the original one. I shared my pre-built docker images to make it more simple.

### Option 1: Original guidelines from Foradian with some tips.
You can clone the source code here: https://github.com/doquoccuong84/fluxday.git , then setup the dockers as the following steps (thanks to the tips shared here: https://github.com/foradian/fluxday/issues/43):

1. cp config/database.yml.example config/database.yml
2. cp app.env.example app.env
3. cp db.env.example db.env (had to do this also)
4. container fluxday-db is created later so you have to edit app.env file and change
DB_HOST=db to DB_HOST=fluxday-db
5. edit docker-compose.yml and change
image: mysql to image: mysql:5.6
(works with 5.6 tag, doesnt work with the latest mysql version)
6. docker-compose up -d --build --remove-orphans
7. docker exec -it fluxday-app /bin/bash (to log in to the container)
8. rake db:create
9. rake db:migrate
10. rake db:seed
11. bundle install
12. rails server &

### Option 2: Use pre-built docker images
1. Clone this source code
``` sh
https://github.com/doquoccuong84/fluxday.git
```
2. Build "fluxday-app" and "fluxday-db" services on docker by runing below command.
``` sh
docker-compose up -d --build --remove-orphans
``` 
3. Get into the "fluxday-app" to setup the database.
``` sh
docker exec -it fluxday-app /bin/bash (to log in to the container)
```
4. Set up the database 
``` sh
    rake db:create
    rake db:migrate
    rake db:seed
```
5. Start the server
``` sh
    rails server &
```
Fluxday can be accessed from the browser by navigating to [http://localhost:3000]().
#### Initial login credentials:
Email: admin@fluxday.io

Password: password