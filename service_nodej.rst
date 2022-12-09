Script para detener y/o iniciar nodej
=========================================

Este script se debe crear primero y se debe probar en reiteradas veces para garantizar que haga el stop y start de la app en Nodej.

Debe crear el script, en esta ruta::

  /usr/local/bin


Este es el script::

  # cat nodejs.sh

  #!/bin/bash
  function start {
          cd /opt/middlenaiguata
          (/usr/bin/npm start >> /var/log/node.log &)
          $(netstat -tulpn | grep 3000 | awk '{ print $7}' | awk -F"/" '{print $1}') > nodejs.pid
  }
  function stop {
          kill -9 $(netstat -tulpn | grep 3000 | awk '{ print $7}' | awk -F"/" '{print $1}' )
  }
  case "$1" in
      start|stop|restart)
          $1
          ;;
      status)
          echo "..."
          ;;
      *)
          echo "Debe usar: $0 {start|stop|status|restart}"
          exit 2
          ;;
  esac

Este es el script de services que utilizara el script anterior para que sea como un servicio o demonio::

  # cat /usr/lib/systemd/system/node.service

  [Unit]
  Description=Nodejs
  After=syslog.target network.target

  [Service]
  Type=forking

  User=root
  Group=root

WorkingDirectory=/opt/middlenaiguata
Environment="NODE_PID=/opt/middlenaiguata/nodejs.pid"

ExecStart=/usr/local/bin/nodejs.sh start
ExecStop=/usr/local/bin/nodejs.sh stop

RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
