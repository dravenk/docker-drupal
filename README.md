# docker-drupal
Docker compose for Drupal.

## Easy to use.
Just need copy the sample file and customize some of the content, sush as changing the database password in the environment variable.
```
cp example.env .env  
cp example.docker-compose.yml docker-compose.yml  
cp nginx/conf.d/app.conf.example nginx/conf.d/app.conf  
docker-compose up -d  
 
```
In this example, the files and directory structure are as follows.
```
nginx/
  conf.d/
    ssl.conf.example  // If you need setup SSL, you can copy and customize this file.
```
