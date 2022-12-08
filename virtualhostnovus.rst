NovusFactura
======================

* app.qa.novusfactura.com			FRONTEND

* api-qa.novusfactura.com:5001	BACKEND

* db.qa.novusfactura.com			BASE DATOS



En el servidor en donde esta Apache nos vamos al directorio de configuración de los Virtual Host::

  # cd /etc/apache2/sites-available

Creamos el archivo del virtual host::

  # nano app.qa.novusfactura.com.conf
  
Agregar este contenido::

  <VirtualHost *:80>
           ServerAdmin webmaster@novusfactura.com.conf
           DocumentRoot /var/www/html/app.qa.novusfactura.com/
           ServerName app.qa.novusfactura.com
           ServerAlias app.qa.novusfactura.com.
           ErrorLog /var/www/html/app.qa.novusfactura.com/app.qa.novusfactura.com_error.log
           CustomLog /var/www/html/app.qa.novusfactura.com/app.qa.novusfactura.com.log common
  </VirtualHost>

Nos vamos al directorio en donde se habilitan los virtual server::

  # cd /etc/apache2/sites-enabled/

Creamos el enlace simbolico, para activar el virtual server::

  # ln -s ../sites-available/app.qa.novusfactura.com.conf .

Probamos que la sintaxis del virtual host este operativa::

  # apachectl configtest
    Syntax OK

Reiniciamos el Apache::

  # systemctl restart apache2
  
 
Creamos el directorio en donde se va colocar el programa del FRONTEND::

  # mkdir /var/www/html/app.qa.novusfactura.com

Vamos a crear un archivo de prueba, solo para certificar que el Virtual host esta operativo::


  # vi /var/www/html/app.qa.novusfactura.com/index.html

  <html>
    <head>
          <title>app.qa.novusfactura.com</title>
    </head>
    <body>
          <h1>Felicitaciones, se creo el Virtual Host de app.qa.novusfactura.com</h1>
    </body>
  </html>
