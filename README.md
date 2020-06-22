## docker-app
In this project, common development and management tools such as Composer/Drush/Drupal-Console are used through the Drupal integration. You can copy a few lines of command to easily set up a project, including the nginx/drupal/mariadb/adminer.

### Easy to use.
Just need copy the sample file and customize some of the content, sush as changing the database password in the environment variable.
```
cp example.env .env  
cp example.docker-compose.yml docker-compose.yml  
cp nginx/conf.d/app.conf.example nginx/conf.d/app.conf  
docker-compose up -d  
```

### Quick install
You can use drush command to install drupal quickly after you run docker container.
Replace `example` with the `MARIADB_PASS` password you set in the `.env` file.
```
docker exec -it dp drush --db-url=mysql://root:example@mariadb/dp -vy
```

### Directory structure
In this example, the files and directory structure are as follows.
```
.env                  // Environment variable files that hold content such as database passwords.
docker-compose.yml    // 
nginx/
  conf.d/
    app.conf          // The nginx configuration file is responsible for representing the entire project
    ssl.conf          // The nginx configuration file is responsible for representing the entire project
    app.conf.example  // Configuration file, proxy to each specific application, if you don't need setup SSL, you can use this file.
    ssl.conf.example  // Recommended. If you need setup SSL, you can copy and customize this file.
storage
  mariadb
    data              // Database content for your site
```
