#build frontend container:

cd frontend
docker build -t test/php-nginx .

docker tag test/php-nginx gcr.io/extended-cable-248113
docker push gcr.io/extended-cable-248113/php-nginx

#postgres

docker pull postgres
docker run --name pg-docker -e POSTGRES_PASSWORD=docker -d -p 5432:5432 -v $HOME/weather/backend2/database:/var/lib/postgresql/data postgres

#run tests
docker rm $(docker ps -a -q)
docker run -p 8080:80 test/php-nginx
docker exec -it 0a6c bash

minikube docker-env | Invoke-Expression

gcloud container clusters get-credentials weather-cluster-1 --zone us-central1-a

kubectl apply -f ./frontend.yaml
kubectl apply -f ./backend.yaml

 kubectl get pods
 kubectl get service
 kubectl get services --watch

kubectl describe deployment hello





TESTS:

front:
sudo apt install apt-transport-https lsb-release ca-certificates
sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt update
apt install php7.2 php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-pgsql php7.2-zip php7.2-fpm php7.2-mbstring


RUN sed -e 's/127.0.0.1:9000/9000/' 
        -e '/allowed_clients/d' 
        -e '/catch_workers_output/s/^;//' 
        -e '/error_log/d' 
        -i /etc/php-fpm.d/www.conf

sudo /etc/init.d/nginx restart
sudo /etc/init.d/php7.2-fpm restart


sudo nano /etc/nginx/sites-available/default
    #enable index.php
    #adjust tsock file


backend:

sudo nano /etc/postgresql/9.6/main/pg_hba.conf
    #host  all  all 0.0.0.0/0 md5
sudo nano /etc/postgresql/9.6/main/postgresql.conf
    #localhost = "*"
sudo /etc/init.d/postgresql restart





sudo -u postgres psql -f create_tables.sql

CREATE TABLE weather (
        location varchar(200) PRIMARY KEY,
        temperature integer NOT NULL
)

INSERT INTO weather values('New York City', 40.73);

INSERT INTO weather values('New York City', 40.73)
ON CONFLICT (location) DO UPDATE
SET temperature = 100;

select * from weather


sudo apt-get install python-pip libpq-dev
pip install psycopg2


create user test;
ALTER ROLE test
WITH PASSWORD 'test';
grant all privileges on database postgres to test;
 GRANT ALL PRIVILEGES ON TABLE weather TO test;

tests:
 psql -d postgres -U test -W -h localhost
 sudo -u postgres psql



