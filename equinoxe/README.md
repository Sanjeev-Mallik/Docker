>First ask for access on Equinoxe GitHub : https://github.com/equinoxevc

>You can refer to this documentation to have more details about docker installation and tip http://confluence.solutionsmetrix.com:8090/display/METKB/Docker+on+Ubuntu+18.04

In your project folder

- Create a folder my cbt or myime

- Clone both repositories

- Create a symbolic link to the laravel app

```
mkdir mycbt
cd mycbt
git clone git@github.com:equinoxevc/CBTSugar.git
mv CBTSugar sugarcrm
git clone git@github.com:equinoxevc/CBTPortal.git
mv CBTPortal laravel
ln -s laravel/public/ portal
```

>On Windows use `mklink portal laravel/portal` to create a symbolic link

Go on dockerized project in equinoxe folder

`docker build .`

Copy the docker image id returned (last thing written by the execution of the command line)

>You could have issues on Linux to build the container. Follow the error messages and split the install lines


Run the docker container

`docker run --name "<clientname>" -d -e VIRTUAL_HOST=<clientname.docker> --add-host="<clientname.docker>:127.0.0.1" -v </var/log/apache2>:/var/log/apache2 -v </var/www/clientname>:/var/www/html --net sugar_nw <IMAGEID>`

Example
`docker run --name "mycbt" -d -e VIRTUAL_HOST=mycbt.docker --add-host="mycbt.docker:127.0.0.1" -v /var/log/apache2:/var/log/apache2 -v /var/www/mycbt:/var/www/html --net sugar_nw 134a3db3976c`

>Do not forget to add your hostname on local. Edit the /etc/hosts file to add mycbt.docker for example.

Edit config.php and do all the installation verfication as specified in http://confluence.solutionsmetrix.com:8090/display/METKB/Docker+on+Ubuntu+18.04

Copy the .htacess of metrixdev

`scp username@metrixdev:/var/www/cbt/sugarcrm/.htaccess sugarcrm/`

Try to run mycbt.docker/admin to see if sugar works.

Copy the .env file from metrixdev'

`scp username@metrixdev:/var/www/cbt/laravel/.env laravel/`

Inside laravel folder do a composer install

Try to access to to the url.
