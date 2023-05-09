1-) Descargamos la llave pública

    wget -O - https://dbeaver.io/debs/dbeaver.gpg.key | sudo apt-key add -

2-) Agregamos la llave a nuestro repositorio

    echo "deb https://dbeaver.io/debs/dbeaver-ce /" | sudo tee /etc/apt/sources.list.d/dbeaver.list

3-) Actualizamos nuestros paquetes

    sudo apt update

4-) Instalamos DBeaver:

    sudo apt install dbeaver-ce

**Referencia**
[Guía de instalación de DBeaver en Ubuntu 20.04 LTS](https://blonder413.wordpress.com/2021/05/20/instalar-dbeaver-ce-en-ubuntu-20-04/)



