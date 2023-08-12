This project is to provide a template for php projects

It contains: 

- MySQL database
- Mailcatcher: a tool for storing emails sent from the app
- Redis
- phpMyAdmin
- PHP
- Nginx

# How to use:
1. Clone the project
```
git clone https://github.com/mohammadibrahemmustafa/docker-php-template.git
```
2. Go to the project
```
    cd docker-php-template
```
1. Add a project folder
```
    mkdir project
```
2. Copy .env file
```
    cp .env.example .env
```
3. Build the containers
```
docker-compose up --build
```
4. Add the project to host file
```
172.20.0.7 myapp.test
```
The host name must match with the one set in the file **./etc/nginx/app.conf**, while the IP address is the web container address, which can be found with a 

```
docker inspect <container id>
```

 command. The container ID can be found by running the docker ps command. In our case, the container is named MyApplication_nginx.

5. Go to the php container 
```
docker exec -it MyApplication_php bash
```

6. Run the commands to install the packages and create the database
```
composer install
php artisan migrate
```

 Now the website should be accessible via [this link](http://myapp.test) and the phpmyadmin via [this link](http://localhost:8081/index.php) 

 This project is based on the [blog](https://polcode.com/resources/blog/how-to-run-a-laravel-application-locally-with-docker/) 