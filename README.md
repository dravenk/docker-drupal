## docker-app
This is an example of creating a [Drupal](drupal.org) project using [docker-compose](https://docs.docker.com/compose/). In this project, common development and management tools such as Composer/Drush/Drupal-Console are used through the drupal integration. You can copy a few lines of command to easily set up a project, including the nginx/drupal/mariadb/adminer.

### Create Drupal project
In order to avoid the loss of resources such as images in the website, it is highly recommended to mount all the contents of the website to the hard disk. Create projects using [Composer](https://getcomposer.org/)
```
mkdir web && composer create-project drupal/recommended-project web/dp "^9.0" -vvv
```
Or copy a project from the Docker container
```
docker run --name dp -d dravenk/dp:web && 
mkdir web && docker cp dp:/var/www/html web/dp &&
docker rm -f dp
```
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
docker exec -it dp drush si --db-url=mysql://root:example@mariadb/dp -vy
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
