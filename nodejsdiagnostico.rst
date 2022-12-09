Nodejs demo para diagnostico
===============================

Primero nos aseguramos de tener el node y el npm actualizado::

	npm install -g n
	n latest
	node -v 
	npm -v

Todo lo debemos hacer con el usuario soporte

En el directorio en donde esta la aplicación::

	$ cd /home/soporte/api_imprenta_novus

Creamos un package.json::

	$ cat package.json
	{
	  "scripts": {
		"dev": "NODE_OPTIONS='' /usr/bin/node /home/soporte/api_imprenta_novus/app.js"
	  }
	}


Ahora creamos el app.js::


	$ cat app.js
	// app.js

	const http = require('http');

	// Create an instance of the http server to handle HTTP requests
	let app = http.createServer((req, res) => {
		// Set a response type of plain text for the response
		res.writeHead(200, {'Content-Type': 'text/plain'});

		// Send back a response and end the connection
		res.end('Hello World!\n');
	});

	// Start the server on port 3000
	app.listen(3000, '192.168.1.10');
	console.log('Node server running on port 3000');

Listamos los archivos::

	$ ls
	app.js  package.json  package-lock.json
	
Ponemos a correr la aplicación::

	$ npm run dev

	> dev
	> NODE_OPTIONS='' /usr/bin/node /home/soporte/api_imprenta_novus/app.js

	Node server running on port 5001
	


Instalaciones
------------------
::

	npm cache clean -f
	npm install npm@latest -g
	npm install -g n
	n latest
	node -v 
	npm -v

script::
    - npm config set proxy http://10.132.0.10:8080
    - npm config set strict-ssl false
    - git config --global http.proxy http://10.132.0.10:8080
    - npm install -g npm
    - npm install
