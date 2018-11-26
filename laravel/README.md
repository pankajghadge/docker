step1: Create project directory

       e.g: mkdir laravel_project

step2: Create mysql data directory under project + database directory

       $ mkdir -p laravel_project/database/mysql-data

step3: Downloading Laravel and Installing Dependencies

       $ cd laravel_project

       $ git clone https://github.com/laravel/laravel.git laravel-app

       $ cd ./laravel-app

       #Use Docker's composer image to mount the directories that you will need for your Laravel project & avoid the overhead of installing Composer globally

       $ docker run --rm -v $(pwd):/app composer install

step4: Copy given Dockerfile under laravel_project/laravel-app

step5: Configuring PHP

       $ mkdir ./laravel-app/php


       Next, open the local.ini file and add below contains (ignore hash "#" while copying)

       
       vim ./laravel-app/php/local.ini
       ###########################################
       ### upload_max_filesize=40M             ###
       ### post_max_size=40M                   ###
       ###########################################


step6: Running the Containers and Modifying Environment Settings

       cp ./laravel-app/.env.example ./laravel-app/.env

       Find the block in .evn file that specifies DB_CONNECTION and update it to reflect the specifics of your setup. You will modify the following fields:
       ############################################
       ### DB_CONNECTION=mysql                  ###
       ### DB_HOST=mysql-db-host                ###
       ### DB_PORT=3306                         ###
       ### DB_DATABASE=laravel_db               ### 
       ### DB_USERNAME=laravel_user             ###
       ### DB_PASSWORD=laravel@1234             ###
       ############################################


      cd ./laravel_project
      With all of the services defined in your docker-compose file, we will need to issue a single command to start all of the containers.
      $ docker-compose up -d

      Once the process is complete, use the following command to list all of the running containers:
      $ docker ps -a

step7: Set the application key for the Laravel application with the php artisan key:generate command
      $ docker-compose exec laravel_app php artisan key:generate
      $ docker-compose exec laravel_app php artisan config:cache

step 8: Final step, visit http://your_server_ip:5580 in the browser

Note: Please modify port you want to expose in docker-compose file
      For web port 80 I'm using 5580
          mysql port 3306 I'm using 5506 

