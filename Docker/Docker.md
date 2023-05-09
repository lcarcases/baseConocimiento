#### Instalación de docker en ubuntu: 

 1-) Instalar docker: 
   1.1-) Instrucciones de instalación:
              https://docs.docker.com/engine/install/ubuntu/
              
   1.2-) Para que no tengas que ejecutar los comandos de docker con sudo, añade tu usuario al grupo de docker con el siguiente comando: 
   
               `sudo usermod -aG docker lisandro` 
               
   El comando anterior añade el usuario `lisandro` al grupo `docker`, pero para que tome efecto el cambio, debemos ejecutar el siguiente comando:

              `newgrp docker`

