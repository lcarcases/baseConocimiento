#### Tener instalado docker (ubuntu): 

 1-) Instalar docker: 
   1.1-) Instrucciones de instalación:
              https://docs.docker.com/engine/install/ubuntu/
              
   1.2-) Para que no tengas que ejecutar los comandos de docker con sudo, añade tu usuario al grupo de docker con el siguiente comando: 
   
               `sudo usermod -aG docker lisandro` 
               
   El comando anterior añade el usuario `lisandro` al grupo `docker`, pero para que tome efecto el cambio, debemos ejecutar el siguiente comando:

              `newgrp docker`

**Nota:** Tener habilitado tu usuario en el grupo de docker es importante, me pasó que una vez instalado minikube trataba de habilitar el plugin del ingress y me daba unos errores de permisos y me sugería que añadiera mi usuario al grupo de docker porque al paracer minikube no podía interactúar con el deamon de docker y aún cuando ya había puesto mi usuario en el grupo de docker como que no agarraba esta configuración, reinicié la máquina (no lo había hecho cuando añadí mi usuario al grupo de docker) y volví a ejecutar el comando y ya pude habilitar el ingress. Inclusive el error me daba para varios comandos de minikube. ^16e928

#### Tener instalado Minikube

  Instrucciones de instalación:
  
  https://minikube.sigs.k8s.io/docs/start/



#### Iniciar Minikube:
   
       minikube start

#### Inicia el dashboard de minikube:

       minikube dahsboard

El dashboard nos permite ir viendo el estado de salud de nuestro cluster y sus objetos.


#### Tener instalado kubectl para insteractuar con  minikube

  1-) Descargamos kubectl:

        curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

  2-)  Hacemos que el binario descargado sea ejecutable:

       chmod +x kubectl

  3-) Movemos el ejecutable hacía /bin:

        sudo mv kubectl /usr/local/bin/

  4-) Ahora ya podemos interactúar con nuestro cluster mediante:

       kubectl <command> <resource>

  Ejemp: 

       kubectl get -n kube-system pods


#### Habilitar el ingress controller de minikube

1-) Primero verificamos que ya no esté habilitado:

      minikube addons list

  El comando anterior nos lista los plugin de minikube,así como, su estado

2-) En caso de que no estén habilitados ejecutamos el siguiente comando:

     
     minikube addons enable ingress


**Nota**: Si se presenta algún error de permisos que te impide habilitar el plugin del ingress checar este link: [[Pre-requisistos#^16e928]]

#### Tener configurado el metrics server para poder obtener métricas de rendimiento de nuestro cluster

El comando a continuación nos instala el metrics server

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.0/components.yaml 

**Nota:** Una vez que apliques el comando de arriba, el pod te va a dar error como el siguiente: *Readiness probe failed: HTTP probe failed with statuscode: 500* porque intenta hacer pruebas mediante https y hay que inhabilitar esas pruebas, para ello tenemos que editar el deployment con el siguiente comando:

     kubectl edit deploy metrics-server -n kube-system 

Con este comando de arriba te abre el editor y añadimos la siguiente línea en los argumentos del contenedor: 

       - --kubelet-insecure-tls 

Una vez edito (presionamos la tecla `i`), salvo los cambios (presionamos tecla ESC, luego :wq!), para salir sin guardar ningún cambio (presionamos la tecla ESC, luego :qa!) , en automático el pod se actualiza y ya no debe dar error. 

![[kubeletInsecureTls.png]]

Al final del imagen anterior vemos la opción ya añadida.

**Nota**: Es un poco especial el archivito, como único pude modificarlo fue parándome al inicio de la linea, escribir el comando de arriba y presionar enter. 

Una vez instalado con el comando de arriba, verificar que exista con el siguiente comando: kubectl get deployment metrics-server -n kube-system

Con esto ya vamos a poder  ver métricas de uso de CPU y Mm en el dashboard de minikube 

![[metricServerMetrics.png]]

**Referencia:** https://github.com/kubernetes-sigs/metrics-server/issues/812 

