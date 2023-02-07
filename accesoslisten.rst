Adding Client Authentication record in pg_hba.conf file

	vi /etc/postgresql/15/main/pg_hba.conf

	local   all             postgres                                trust

	local   all             all                                     trust


Adding Client Authentication in pg_hba.conf file from multiples host authentication

	host    all             all             0.0.0.0/0               trust

	host    all             all             127.0.0.1/32            scram-sha-256


Cambiar la clave

	su - postgres 

	psql

	# \password postgres

	Enter new password: 
	
Probar la conexion local

	psql -h localhost -p 5432 -d postgres -U postgres
	
Probar la conexion local y consultar las tablas

	$ psql -h 172.30.150.58 -p 5432 -d impredigital -U postgres
	impredigital=# \dt
                List of relations
	 Schema |         Name         | Type  |  Owner
	--------+----------------------+-------+----------
	 public | t_bitacoras          | table | postgres
	 public | t_eventos            | table | postgres
	 public | t_registro_detalles  | table | postgres
	 public | t_registros          | table | postgres
	 public | t_roles              | table | postgres
	 public | t_serviciosdoc       | table | postgres
	 public | t_serviciosmasivos   | table | postgres
	 public | t_serviciostipodoc   | table | postgres
	 public | t_tipocedulacliente  | table | postgres
	 public | t_tipodocumentos     | table | postgres
	 public | t_tranzascorrelativo | table | postgres
	 public | t_usuarios           | table | postgres
	(12 rows)


	
Postgresql listen_addresses

	vi /etc/postgresql/15/main/postgresql.conf

agregar esta linea para que escuche por todos los adaptadores

	listen_addresses = '*'
		
agregar esta linea para que escuche solo por las IP autorizadas


	listen_addresses = '127.0.0.1, 192.168.1.10, 192.168.1.100'

Conectar remoto

	psql -U postgres -h 192.168.1.10 -p 5432
	
Realizar el import de la BD

	psql -U postgres -W -h 172.30.150.58 impredigital < /tmp/bd_novus.sql
