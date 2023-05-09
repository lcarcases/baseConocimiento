
**Pre-requisitos:**

- Memoria USB de mínimo 8 GB

**Nota**:  En la Mm Rojita tienes la versión Ubuntu 20.04.6 LTS

- La explicación que veremos a continuación es para Windows que tiene configurado el *BIOS Mode* en UEFI y *Partition Style* en GUID Partition Table (GPT)

BIOS MODE:
![[biosMode.png]]

Partition Style:
![[partitionStyle.png]]

Para llegar a la pantalla anterior, vamos a la ventana *Disk Managment* y damos click derecho sobre la partición donde tenemos instalado Windows (*C* o también *Disk 0*) y en el menú que se despliega seleccionamos *Properties*, nos sale la pantalla anterior y nos movemos a la pestaña de *Volumes*.


1-) En windows, dar un formateo rápido a tu memoria , en  File System selecciona NTFS para que en el nombre del Volumen puedas usar caracteres especiales

2-) Descargar la imagen (.iso) de Ubuntu del sitio oficial:

[Descargar la última versión de Ubuntu](https://ubuntu.com/download/desktop)

[Descargar versiones anteriores de Ubuntu](https://releases.ubuntu.com/?_ga=2.65037742.1421072910.1683393589-1678790841.1683393589)

3-) Descargamos el programita Rufus:

  [Rufus](https://rufus.ie/en/)

   Una vez insertada nuestra memoria:
   
   **Boot selection:** Damos click en el botón SELECT y buscamos el .iso con la imagen de Ubuntu que descargamos en el punto 2.

  **Partition Scheme:**  GPT
     **Nota:** Si nuestro *Partition style* no hubiera sido GPT, en esta opción seleccionariamos la otra
 
  **Target system:** UEFI (non CSM) 

  **Volume Label:** Ponemos un nombre que haga referencia a la versión de Ubuntu, Ejem: Ubuntu 20_04_06 LTS

  **File System:** NTFS

 Una seleccionado los campos damos click en START y comienza el proceso de generación del USB Booteable con la versión. Esto puede tardar varios minutos.
   

![[rufus.png]]

4-) En Windows realizamos las siguientes acciones

   4.1-) Deshabilitamos el BitLocker,  que es una característica de algunas versiones de windows que encripta el contenido del disco duro, para ello, buscamos la opción *Manage BitLocker* y si está habilitada, la inhabilitamos.

![[bitLocker.png]]

  4.2-) Deshabilitamos la opción *Fast Reboot* para que esto no interfiera cuando vayamos a acceder nuestro BIOS, para ellos buscamos la opción *Fast startup*.

   ![[fastStartup.png]]

  Luego damos click en *Additional power settings*

  ![[additionalPowerSettings.png]]

   Luego damos click en la opción *Choose what the power do*

  ![[chooseWhatPowerButtonsDo.png]]

   Verificamos que la opción *Turn on fast startup* esté deshabilitada

![[turnOnFastStartup.png]]

5-) En la Bios realizamos los siguientes cambios:

 **Nota:** En las PC Dell para acceder al Bios, reiniciamos la máquina y cuando nos salga el logo de Dell presionamos continuamente la tecla *F12*.

 5.1-) Verificamos que la opción *Secure Boot* esté desabilitado

  ![[secureBoot.png]]

   Esto según para evitar que el SO verifique los fireware o firma del Ubuntu que vamos a instalar

  Una vez hecho esto nos debe salir en System Information *Secure Boot State* en *false*.
   ![[secureBootState.png]]

5.2-) En Sata Operation que está dentro  de System Configuration por defecto viene en el modo *RAID On* que es con el que trabaja Windows pero Ubuntu trabaja AHCI, por tanto para nuestro proceso de instalación tenemos que seleccionar esa opción. Posteriormente veremos como hacer que Windows trabaje en este modo también.

![[ahciMode.png]]

6-) Habilitamos el espacio en el Disco Duro donde vamos a instalar nuestro Ubuntu.

  6.1-) Vamos a *Disk Managment*, nos colocamos sobre el *Disco C*
           damos click derecho y seleccionamos *Shrink Volume*
           
![[diskManagment.png]]

6.2-) En la opción que dice *Enter the amount of space to shrink in MB* colocamos en MB, la cantidad de espacio que le queremos dar a nuestra partición de Ubuntu, en mi caso la última vez coloqué *614400 MB* para reservar un espacio de *600 GB* para Ubuntu. Una vez colocada  la cantidad, damos click en el botón *Shrink*

![[shrinkC.png]]

Una vez hecho lo anterior podemos ver el espacio en disco ya libre

![[unallocatedDiskSapce.png]]

7-) Ahora sí ya estamos listos para iniciar nuestra instalación de Ubuntu, para ello, con la USB Booteable conectada:

  7.1-) Accedemos al Bios e indicamos que inicie desde la USB

       ![[USB Boot.png]]
      
  7.2-) Una vez nos aparezca la Guía de instalación, seleccionamos instalar Ubuntu:

      ![[installUbuntu.png]]

   7.3-) Seleccionamos el idioma que queremos para nuestro teclado, yo seleccioné English y posteriormente instalé el español para tener acceso a los caracteres del español.

    ![[Pasted image 20230507090132.png]]

7.4-) Nos conectamos a nuestra WI-FI

    ![[Pasted image 20230507090239.png]]

7.5-) En *Installation Type* seleccionamos *Somenthing else* para que nos muestre la pantalla donde podemos configurar el espacio de disco duro que queremos para nuestro sistema operativo y cuanto para la memoria *SWAP*

![[installationType.png]]

7.6-) En la siguiente pantalla vamos a crear dos particiones sobre el espacio libre que creamos en el punto 6.2 y que aquí nos aparece como *free space* , en mi caso el número que aparecía era como *600400MB*, no tiene que ser exactamente el mismo número que pusimos en el punto 6.2, pero si un aproximado. Una partición va ser para la memoria SWAP y lo restante para el SO

![[partitionFreeSpace.png]]

**Nota:** 
     - Pueden aparecer varias particiones con la etiqueta *free space* pero tu vas a seleccionar la que el tamaño se aproxime al que seleccionaste en el punto 6.2
     - El tamaño recomendado el SWAP en la actualidad  para Mm RAM de 16GB en adelante es de la mitad. Por ejemplo si tienes 16GB de RAM dejar para el SWAP 8GB, si tienes 32GB de RAM dejar para el SWAP 16GB, etc. 

7.7-) Creamos la partición para la Mm SWAP, para ello, con la partición *free space* seleccionada de la imagen anterior, damos click sobre el botón *+* y nos sale la siguiente imagen:

![[osSwapPartition.png]]

Aquí en el *Size* dejé los 16384MB, que es el equivalente a 16GB . También dejé el resto de las opciones tal como se ve en la pantalla, *Partition type* como *Primary*, *Location for the new partition* como *Beginning of this space*, la opción *Use as* como *swap area*. Una vez hecho esto ya debemos ver nuestra nueva partición swap (*/dev/nvmeOn1p6 swap*)

![[osSwapPartitionCreated.png]]

 7.8-) Creamos la partición donde va a vivir nuestro SO, para ello, con la partición *free space* seleccionada de la imagen anterior, damos click sobre el botón *+* y nos sale la siguiente imagen:

![[osPartitionConfiguration.png]]  

En mi caso como primero configuré la Mm SWAP, aquí en *Size* dejé los 600000MB restantes para un total aprox. de 600 GB. También dejé el resto de las opciones tal como se ve en la pantalla, *Partition type* como *Primary*, *Location for the new partition* como *Beginning of this space*, la opción *Use as* como *Ext4 journaling file system* y *Mount point* como */* . Una vez hecho esto ya debemos ver nuestra nueva partición para el SO (*/dev/nvmeOn1p5 ext4*)

![[osPartitionCreated.png]]

7.9-) A continuación seleccionamos la opción *Device for boot loader Installation que tiene que con donde se va a colocar el programa de booteo de nuestro SO Ubuntu, aquí vamos a seleccionar la nueva partición que acabamos de crear para nuestro SO Ubuntu (*/dev/nvmeOn1p5 ext4*)

![[deviceForBootLoader.png]]

**Nota:** Aquí muchos recomiendan usar la particion de *Windows Boot Manager* pero esto puede hacer que se sobreescriba la de Windows y darnos error posteriormente, por tal razón yo en esta opción seleccioné la partición donde va a vivir nuestro nuevo SO Ubuntu.

8.0-) Una vez hecho lo anterior ahora sí damos click en el botón *Install Now*

![[installNow.png]]

Y Luego damos click en *Continue*

![[continueInstallation.png]]

9-) Seleccionamos nuestra área geográfica

![[grographicArea.png]]

10-) Configuración de usuario y contraseña

![[userAndPassowrdConfiguration.png]]

Y así vamos siguiendo el asistente hasta que termine y nos pida reiniciar

![[restartAfterInstallation.png]]

11-) Hacer que Windows trabaje en el modo *AHCI* 

 La razón por la que Windows no arranca en modo *AHCI* es por que necesita un Driver, para que quede instalado vamos a realizar los siguientes pasos:

  11.1-) Cuando reiniciemos la máquina accedemos al Bios Setup y reestablecemos el modo  RAID On

  ![[raidOn.png]]

   11.1-) Accedemos a Windows y configuramos el modo seguro, para ello vamos a *System Configuration* y en la pestaña de *Boot* seleccionamos la opción *Safe Boot*, una vez hecho esto reiniciamos nuestra PC

 ![[safeBoot.png]]

11.2-) Accedemos al Bios nuevamente para habilitar la opción de *AHCI* nuevamente

 ![[ahciMode.png]]

11.3-) Inciamos en Windows nuevamente, y como previamente habilitamos el modo seguro no nos va a dar error por estar en *AHCI*. Una vez logueados, vamos *System Configuration* y en la pestaña *General* seleccionamos la opción *Normal startup*.  

![[normalStartup.png]]

Listo, ya con esto reinciamos y ya podemos seleccionar ingresar a Windows o Ubuntu desde el Menú que nos sale al reiniciar la máquina, este menú es concido como *GRUB Menu*

**Referencias:**

[How to Dual Boot Ubuntu 20.04 on Windows 10 | UEFI | GPT | WITHOUT DATA Loss | Detailed 2021 Guide](https://www.youtube.com/watch?v=hT4m71ghD6A)

[Arranque dual Ubuntu y Windows en una laptop Dell | Desactivar RST](https://www.youtube.com/watch?v=wDrCaAdGuMk)