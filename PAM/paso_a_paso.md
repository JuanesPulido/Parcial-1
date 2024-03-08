Principal mente para inicalizacion de la practica debemos verificar
la instalacion de apache y PAM, si aun no estan instalados, utilizamos
estos comandos:

#apt-get update
#apt-get install apache2 libapache2-mod-authnz-pam

Siguiente habilitamos el modulo de autenticacion Apache PAM

#a2enmod authnz_pam

Para poder llevar acabo a autenticacion debemos crear nuestro directorio
que es nuestro caso se llamara Archivos_privados siguiendo los pasos:

# cd /var/www/html
#mkdir Archivos_privados
# chown www-data.www-data /var/www/html/Archivos_privados -R

Para poder configurar el servicio apache para la Autenticacion PAM entonces:

#cd /etc/apache2/sites-available
#vim 000-default.conf

Donde colocaremos las siguientes instrucciones

<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

<Directory "/var/www/html/Archivos_privados">
AuthType Basic
AuthName "private area"
AuthBasicProvider PAM
AuthPAMService apache
Require valid-user
</Directory>
</VirtualHost>

Para poder acceder a una pagina extra al cancelar el programa crearemos
un archivo llamado Error.html en la direccion /var/www/html y 
lo invocaremos dentro de la configuracion apache:

<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
<Directory "/var/www/html/test">
AuthType Basic
AuthName "private area"
AuthBasicProvider PAM
AuthPAMService apache
ErrorDocumento 401 /Error.html
Require valid-user
</Directory>
</VirtualHost>

Para la configuracion PAM para la verificacion de usuarios
debemos crear un archivo de configuracion PAM entonces:

vi /etc/pam.d/apache

Dentro del archivo vim:

#auth required pam_unix.so
#account required pam_unix.so
#auth required pam_lisfile.so onerr=fail item=user sense =deny 
file=/etc/apache2/denegados.txt

Para la configuracion se debe habilitar el servicio apache 
para poder leer un archivo llamado "SHADOW".

#groupadd shadow
#usermod -a -G shadow www-data
#chown root:shadow /etc/shadow
#chmod g+r /etc/shadow

por ultimo debemos reiniciar el servicio apache:

#systemctl restart apache2

De esta manera podemos configurar la autenticacion por medio de PAM.



