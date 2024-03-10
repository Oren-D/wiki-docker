instruction page simplified : 


open linux : 
git clone the project 
go to project dir
open all the dockers you need -mysql -mediawiki :
docker run --name some-mediawiki -p 8080:80 -d mediawiki
docker run -d --name mysql-container -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 mysql

after dockers are up check with docker ps for ID
type 
sudo apt update.
and 
sudo apt install mysql-client-core-8.0
run the following command to set my_wiki:

mysqladmin -h 127.0.0.1 -u root -pmy-secret-pw create my_wiki
then , restore our wiki with the following commands: 
gunzip < my-wiki.backup.sql.gz | mysql -h 127.0.0.1 -u root -pmy-secret-pw my_wiki
docker cp LocalSettings.php <<CONTAINER ID>>:/var/www/html/LocalSettings.php

after that is complete . restart the wiki server with docker restart (container id)
open browser
go to localhost:8080/index.php/Main_Page
click log in 
username :demoadmin
password:secretpass

and you are done ! 

if you want to add wikis and save it , after youre done type
mysqldump -h 127.0.0.1 -u root -pmy-secret-pw --default-character-set=binary my_wiki
| gzip > my-wiki.backup.sql.gz 

and upload to gitbucket with git add , commit , push 

good luck !
