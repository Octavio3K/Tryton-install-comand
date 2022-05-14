# Tryton-install-comand

Paso 1 – Instalación de Docker

sudo apt update && sudo apt upgrade

sudo apt install curl python3-pip apt-transport-https ca-certificates software-properties-common

sudo apt install docker.io

sudo usermod -aG docker tuusuario

sudo systemctl enable --now docker

sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

Reiniciamos el servidor con sudo reboot


Paso 2 – Creación de instancia de Tryton

Iniciar instancia de la base de datos a utilizar, en este caso postgreSQL:

docker run --name tryton-postgres -e POSTGRES_PASSWORD=mysecretpassword -e POSTGRES_DB=tryton -d postgres

Configurar la base de datos:

docker run --link tryton-postgres:postgres -e DB_PASSWORD=mysecretpassword -it tryton/tryton trytond-admin -d tryton --all

Inciar instancia web de tryton:

docker run --name tryton -p 8000:8000 --link tryton-postgres:postgres -e DB_PASSWORD=mysecretpassword -d tryton/tryton

Probar http://localhost:8000/


