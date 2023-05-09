#### Instrucciones de instalación de Minikube

  https://minikube.sigs.k8s.io/docs/start/


#### Iniciando minikube:

   -- Iniciar Minikube:
   
       minikube start

  -- Abrir el dashboard de minikube:

       minikube dahsboard

#### Logs

  -- Ver los logs de minikube:

        minikube logs --file=logs.txt

 -- Ver los logs de un pod:

	  kubectl logs -n <namespace> <pod-name>

  Ejemp:
 
       kubectl logs -n kube-system <ingress-nginx-pod-name>


#### Instalar kubectl para insteractuar con  minikube

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


#### Comandos generales

-- Conocer la versión de minikube que tenemos instalada:

     minikube version

-- Listar los plugins que tenemos para ver cuales están habilitados y cuales no:

     minikube addons list

 Si queremos habilitar uno ejecutamos el siguiente comando:

    minikube addons enable <nombre_plugin>
   
   Ejemp:
     
       minikube addons enable ingress


