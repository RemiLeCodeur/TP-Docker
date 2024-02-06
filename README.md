DATABASE

Créer image : docker build -t database_tp1 .

Créer container BD : docker run --name databaseTP1 -e POSTGRES_DB=db -e POSTGRES_USER=usr -e POSTGRES_PASSWORD=pwd -p 5432:5432 --network app-network -v volume_database_tp1:/var/lib/postgresql/data -d database_tp1

Exécuter BD: docker exec -it databaseTP1 psql -U usr db

Créer volume : docker volume create volume_database_tp1

Image:
	FROM postgres:14.1-alpine

	# ENV POSTGRES_DB=db \
	#   POSTGRES_USER=usr \
	#   POSTGRES_PASSWORD=pwd

	COPY script.sql /docker-entrypoint-initdb.d/



BACKEND API

Image: docker build -t java_tp1 .

Dockerfile :

# TODO: Choose a java JRE
FROM openjdk:latest

# Créez un répertoire de travail dans l'image
WORKDIR /app

# TODO:  Add the compiled java (aka bytecode, aka .class)
COPY Main.class /app/

# TODO: Run the Java with: “java Main” command.
CMD ["java", "Main"]

HTTP SERVEUR



Docker login : aller sur https://hub.docker.com/settings/security pour générer un token

Publish image : 
	docker tag tp1-database remilecodeur/tp1-database:1.0
	docker push remilecodeur/tp1-database:1.0

