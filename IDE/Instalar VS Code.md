1-) Actualizar los repositorios del sistema:

	sudo apt update

2-) Instalar las dependencias de paquetes:

    sudo apt install software-properties-common apt-transport-https wget -y

3-) Añadir la llave GPG:

	wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -

4-) Añadir el repositorio:

	 sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"

5-) Instalar VS Code

	sudo apt install code

6-) Verificar la instalación

	   code --version

**Referencia:**

[Instrucciones de instalación de VS Code en Linux](https://phoenixnap.com/kb/install-vscode-ubuntu)