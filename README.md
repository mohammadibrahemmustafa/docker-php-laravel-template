This project is to provide a template for php projects

It contains: 

- MySQL database
- Mailcatcher: a tool for storing emails sent from the app
- Redis
- phpMyAdmin
- PHP
- Nginx

# How to use:
1. Clone the project (you need to have ssh key)
```
git clone git@github.com:mohammadibrahemmustafa/docker-php-laravel-template.git
```
2. Go to the project
```
cd docker-php-template
```
3. Copy .env file
```
cp .env.example .env
```
4. Copy .env file for the project

```
cp project/.env.example project/.env
```
5. Build the containers
```
docker-compose up --build
```
6. Go to the php container 
```
docker exec -it {container_name} bash
```

7. Run the commands to install the packages and create the database tables
```
composer install
php artisan migrate
```

 Now the website should be accessible via [this link](http://localhost:8000) and the phpmyadmin via [this link](http://localhost:8081/index.php) 

 This project is based on the [blog](https://polcode.com/resources/blog/how-to-run-a-laravel-application-locally-with-docker/)