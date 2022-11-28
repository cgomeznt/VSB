Cambiar la ubicación de la carpeta de datos de PostgreSQL
==============================================================

Antes de cambiar la ubicación de los datos de PostgreSQL, primero verificaremos la configuración actual en el servidor PostgreSQL::

  sudo –u postgre psql

  postgres=# SHOW data_directory;
  Output:
     data_directory
  ------------------------------
  /var/lib/postgresql/15/main
  (1 row)
  postgres=#
  
Como podemos ver nuestro data_directory se encuentra configurado en /var/lib/postgresql/15/main. Antes de cambiar la ubicación paramos la base de datos::

  systemctl stop postgresql
  
Copiamos los datos::

  rsync -av /var/lib/postgresql/15 /postgres/
  
renombramos la carpeta::

   mv /var/lib/postgresql/15/main /var/lib/postgresql/15/main.bck
   
Ahora editamos la configuración de postgresq (/etc/postgresql/15/main/postgresql.conf) l y modificamos el atributo data_directory::

  nano etc/postgresql/15/main/postgresql.conf
  
  data_directory = '/postgres/15/main' 
  
Iniciamos la base de datos::

  systemctl start postgresql
  
Comprobamos nuevamente la configuaración::

  sudo –u postgre psql
  postgres=# SHOW data_directory;
        data_directory
  --------------------------
   /psql/postgres/15/main
  (1 fila)

  postgres=#
