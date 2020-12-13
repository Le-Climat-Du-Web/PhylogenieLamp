# User Guide Apache sur Linux

Les fichiers sont à placer dans /var/www/html/

##########################################################
#            Installation des librairies                 #
##########################################################
Biopython : `pip install biopython`

Mettre à jour Biopython : `pip install biopython --upgrade`

Flask : `pip insatll Flask`

matplotlib : `pip install matplotlib`

##########################################################

1. Installation de apache2

`sudo apt install apache2 php libapache2-mod-php mysql-server php-mysql`

2. Installation du mod_wsgi

`pip install mod_wsgi-standalone`

3. Redémarrage de Apache

`sudo systemctl restart apache2`

4. Modification du virtualhost

s`udo nano /etc/apache2/conf-available/mod-wsgi.conf`

5. Ajouter la ligne suivante

`WSGIScriptAlias /Phylogenie /var/www/html/wsgi_scripts/phylogenie.wsgi`

6. Appliquer la nouvelle configuration

`sudo a2enconf mod-wsgi`

7. Redémarrer Apache

`sudo systemctl restart apache2`

9. Configuration du virtualhost de Flask

`sudo nano /etc/apache2/sites-available/FlaskApp.conf`

10. Taper les lignes suivantes

``<VirtualHost *:80>
	ServerName localhost
	WSGIScriptAlias / /var/www/html/Phylogenie/wsgi_scripts/phylogenie.wsgi
	<Directory /var/www/html/Phylogenie/>
		Order allow,deny
		Allow from all
	</Directory>
	Alias /static /var/www/html/Phylogenie/static
	<Directory /var/www/html/Phylogenie/static/>
		Order allow,deny
		Allow from all
	</Directory>
	ErrorLog ${APACHE_LOG_DIR}/error.log
	LogLevel warn
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>``

Sauver et quitter

11. Appliquer la nouvelle configuration

`sudo a2ensite FlaskApp`

12. Redémarer Apache

`sudo service apache2 restart`

Le site est maintenant accessible à l'adresse http://localhost/Phylogenie

