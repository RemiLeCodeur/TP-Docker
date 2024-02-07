# TP1
## DATABASE

**Créer image**  
	docker build -t database_tp1 .

**Créer container BD**  
	docker run --name databaseTP1 -e POSTGRES_DB=db -e POSTGRES_USER=usr -e POSTGRES_PASSWORD=pwd -p 5432:5432 --network app-network -v volume_database_tp1:/var/lib/postgresql/data -d database_tp1

**Exécuter BD**
	docker exec -it databaseTP1 psql -U usr db

**Créer volume**
	docker volume create volume_database_tp1

**Dockerfile**
```
	FROM postgres:14.1-alpine

	# ENV POSTGRES_DB=db \
	#   POSTGRES_USER=usr \
	#   POSTGRES_PASSWORD=pwd

	COPY script.sql /docker-entrypoint-initdb.d/
```

## BACKEND API

Image: docker build -t java_tp1 .

**Dockerfile**  
```
# TODO: Choose a java JRE
FROM openjdk:latest

# Créez un répertoire de travail dans l'image
WORKDIR /app

# TODO:  Add the compiled java (aka bytecode, aka .class)
COPY Main.class /app/

# TODO: Run the Java with: “java Main” command.
CMD ["java", "Main"]
```
## HTTP SERVEUR
**dockerfile**  
```
# Utiliser l'image de base httpd
FROM httpd

# Copier le fichier reverse-proxy.conf dans le conteneur
COPY reverse-proxy.conf /usr/local/apache2/conf/extra/

# Activer les modules de proxy dans la configuration principale d'Apache
RUN echo "Include conf/extra/reverse-proxy.conf" >> /usr/local/apache2/conf/httpd.conf
```

## DOCKER COMPOSE  
**Docker login**  
	aller sur https://hub.docker.com/settings/security pour générer un token  

**Publish image**  
	docker tag tp1-database remilecodeur/tp1-database:1.0  
	docker push remilecodeur/tp1-database:1.0  


# TP2

**2-1 Qu'est ce que testcontainers ?**

Testcontainers est une bibliothèque Java simplifiant les tests d'intégration en fournissant des instances temporaires et légères de bases de données, de navigateurs web et d'autres services dans des conteneurs Docker, facilitant ainsi les tests d'intégration dans les environnements d'intégration continue.

**2-3 Documentez la configuration de votre quality gate**

Chaque critère doit atteindre au moins une note A.  
La couverture de test doit dépasser 80% et le taux de duplication doit rester sous 3%.  
Si l'une de ces conditions n'est pas remplie, l'étape de contrôle qualité dans la CI échoue.  

# TP3

connect ssh : 
```
ssh -i ~/.ssh/remi.louedec centos@remi.louedec.takima.cloud
```

ping ansible :  
```
ansible all -m ping --private-key=~/.ssh/remi.louedec -u centos
```

mon fichier ansible/inventories/setup.yml :
```
all:
 vars:
   ansible_user: centos
   ansible_ssh_private_key_file: ~/.ssh/remi.louedec
 children:
   prod:
     hosts: remi.louedec.takima.cloud
```

publication image front :
```
	docker build -t front-devops .
	docker tag front-devops remilecodeur/front-devops:1.0  
	docker push remilecodeur/front-devops:1.0  
```
