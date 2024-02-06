# Utiliser l'image de base httpd
FROM httpd

# Copier le fichier reverse-proxy.conf dans le conteneur
COPY reverse-proxy.conf /usr/local/apache2/conf/extra/

# Activer les modules de proxy dans la configuration principale d'Apache
RUN echo "Include conf/extra/reverse-proxy.conf" >> /usr/local/apache2/conf/httpd.conf
