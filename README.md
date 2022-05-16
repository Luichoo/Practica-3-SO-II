# Practica 3 SOII  
## Kashifugio  
### Integrantes del equipo:  
Luis Antonio Blanco Conde  
Gustavo Contreras Mejía  
Alejandro Octavio Salas Comparán  
Gabriel Salom Fernández  
  
## I. Crear y levantar respaldo de nuestra máquina virtual.  
Generaremos el respaldo de esta máquina virtual.  
Para hacer el respaldo de nuestra máquina virtual en Vmware se deben de seguir los siguientes pasos:  
  
![image](https://user-images.githubusercontent.com/75387331/166168015-0c05dfa0-4d24-4615-adb0-cf7e467dc6f9.png)  

### 1. Ubicar la carpeta en donde tenemos la máquina virtual que deseamos hacer un respaldo  
Aquí lo tenemos en la carpeta de documentos, creamos de igual manera la carpeta a la que se desea mandar el contenido de la que ya teniamos.  
  
![image](https://user-images.githubusercontent.com/75387331/166167657-e05f5cf8-0cc4-4fbf-881d-b484f620b111.png)  
  
### 2. Copiar los datos de la carpeta contenedora a la otra  
Dentro de la carpeta de nuestra máquina original todos sus datos los seleccionamos.  
  
![image](https://user-images.githubusercontent.com/75387331/166167719-1a6490b7-9d54-434b-a638-7ee7e2c6b9a4.png)  
  
Los datos copiados los meteremos en la carpeta de "Ubuntu respaldo" y esperamos a que se pasen todos los datos.  
  
![image](https://user-images.githubusercontent.com/75387331/166167723-de8b4db4-43a5-4516-ab0b-61a3ed2ad451.png)  
  
### 3. Levantar respaldo  
Le vamos a dar en Open a Virtual Machine y vamos a nuestra carpeta que acabamos de hacer el duplicado y vamos a abrir el archivo .vmx para que nos detecte a la máquina.  
![image](https://user-images.githubusercontent.com/75387331/166167802-14f003e3-dd2f-4d02-9ed3-0ba532880f85.png)  
  
Una vez hecho eso, le cambiamos el nombre a la nueva máquina para diferenciarla y ya andara detectada por VMWare.  
  
![image](https://user-images.githubusercontent.com/75387331/166209287-539cc8f3-de57-438c-9335-f7e7cdb4e0d0.png)  
  
### 4. Finalizando
Ahora vamos a iniciar la máquina, nos marcará un mensaje que nos indicara si la movimos de lugar o copiamos esta máquina, le diremos que la copiamos e iniciamos y con eso tendremos ya listo el respaldo en donde trabajaremos a continuación.  
  
![image](https://user-images.githubusercontent.com/75387331/166168006-35e1f3dc-0ef5-4635-940b-766024d76d54.png)  
  
## II. Nomenclatura del Kernel de Linux  
Al ser de codigo abierto, este nos permite acceso a su codigo para poder interacturar directamente con el, por esto se necesita el entendimiento de la nomenclatura de este para poder manejar el kernel directamente.  
La nomenclatura del Kernel de Linux se divide en tres campos separados por un punto: 
- Número de versión. Versión actual del kernel. 
- Número de sub-versión. Si el número es par es una versión estable, de lo contrario es inestable.  
- Nivel de corrección en el que actualmente se encuentra.

## III. Paquetes Requeridos para compilacion de kernel e instalación  
para hacer la compilación necesitamos correr esto en terminal:  
``` 
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison zstd
```
¿Pero qué significa cada uno de estos?  
  
| Paquete | descripción |
| --- | --- |
| git | Permite trabajar con la pagina de github para ahcer cambios o descargas a un codigo. |
| fakeroot | Genera la herramienta necesaria para crear un entorno de superusuario. |
| build-essential | Instala todas las herramientas necesarias de C/C++, gcc y g++. |
| ncurses-dev | Libreria que nos da una API para nuerstra terminal. |
| xz-utils | Mayor velocidad de comprimir y descomprimir archivos. |
| libssl-dev | Encripta la información para hacer una conexión segura a internet. |
| bc | Calculadora desde terminal. |
| flex | Genera analizadores lexicos que convierten caracteres a tokens. |
| libelf-dev | Maneja archivos ELF. |
| bison | GNU parser que convierte una descripción gramática a un programa en C. |  
| zstd | Descomprimir con el Zestandar. |
  
Entendiendo esto ya corremos esto en terminal y podemos continuar con los siguientes pasos.  

![image](https://user-images.githubusercontent.com/75387331/166208513-6eb828ff-0b59-4f6c-bf49-3257568c9170.png)  

  
## IV. Descargar versión de kernel desde terminal  
  
Para este paso vamos a ver que versión de kernel queremos en la pagina de [kernel.org](kernel.org).  
  
![image](https://user-images.githubusercontent.com/75387331/166208790-f22e99b8-1c93-40f9-835c-3c6902cb70a3.png)  
Aqui vemos que la ultima versión de kernel es la 5.17.5, vemos de igual manera la versión de nuestro kernel de nuestra máquina con el siguiente comando:  
  
```
uname -r
```
  
![image](https://user-images.githubusercontent.com/75387331/166208037-611c4034-6294-4ca6-87f0-287094720227.png)  
  
Vemos que tenemos la versión 5.13.0 por lo que vamos a subirla a la siguiente versión.  
En nuestro caso que vamos a subir a la 5.17.5, pondremos esto en la linea de código para descargar nuestra versión en terminal, si deseas descargar otra versión, cambia el 5.17.5 por tu versión deseada. 
  
```
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.17.5.tar.xz
```
  
Vamos a Guardarlo en la carpeta de Documents y de aqui nos moveremos a los siguientes pasos.  
  
![image](https://user-images.githubusercontent.com/75387331/166207941-85a6cd01-5771-4e36-86ac-6ad6a357d983.png)  

## V. Extraer el codigo del kernel  
1. Vamos a correr en la carpeta en donde descargamos el kernel el siguiente comando:  
  
``` 
tar xvf linux-5.17.5.tar.xz
```
Una vez que se haya descomprimido el kernel se deberá de ver así el directorio con la carpeta de nuestro kernel.  
  
![image](https://user-images.githubusercontent.com/75387331/166207723-ea13e848-4240-4ddd-ad5e-3d2e9a8bd6fb.png)  

## VI. Configuración del kernel  

1. Nos iremos a la carpeta de nuestro kernel usando **cd**:
```
cd linux-5.17.5
```
  
2. Copiaremos la configuración actual a nuestro kernel usando **cp**:

``` 
cp -v /boot/config-$(uname -r) .config
```
  
 ### **Nota**:  
Puede que lleguen a encontrarse con el error de en pasos posteriores:   
**"make[1]: *** No rule to make target 'debian/canonical-certs.pem', needed by 'certs/x509_certificate_list'.  Stop. make: *** [Makefile:1831: certs] Error 2"**.  
  
Para resolver eso es necesario ir a nuestro archivo de donde copiamos la configuracion en /boot/config-$(uname -r) y buscar estas lineas y comentarlas todo como superusuario:     
CONFIG_SYSTEM_TRUSTED_KEYS  
CONFIG_MODULE_SIG_KEY  
CONFIG_SYSTEM_REVOCATION_KEYS 
  
![image](https://user-images.githubusercontent.com/75387331/166172343-b4c6a1df-8618-4f1c-90a6-9d7f9347384c.png)  
  
3. Para hacer los cambios al archivo de la configuración, vamos a correr el comando **make**:  
``` 
make menuconfig
```
4. Cuando corramos este comando nos abrirá una interfaz donde vamos a dar enter donde dice Guardar, dejando todo en sus opciones por defecto y salimos.  
  
![image](https://user-images.githubusercontent.com/75387331/166209160-b625b2dc-fbb6-432c-92a3-94fdf943e43a.png)  
  
## VII. Compilar el kernel  
  
  Para la compílación del kernel vamos a correr el **make**:
  ```
  make
  ```
  Esto llega a tardarse dependiendo de la potencia de tu computadora, asegurate de tener buena cantidad de espacio disponible en tu máquina(en mi caso fueron 45GB).  
    
![image](https://user-images.githubusercontent.com/75387331/166208273-524d3b5c-939d-4578-907d-1de4edbb04e6.png)  
  
 ## VIII. Instalar modulos del kernel  
   
 Una vez que termine la instalación del kernel vamos a correr esto en consola: 
 ```
 sudo make modules_install
 ```
Finalizado el proceso podemos continuar.  
  
![image](https://user-images.githubusercontent.com/75387331/166209068-91fde8a8-6512-44dd-8a43-3ed68c43deba.png)  
  
## IX. Instalar el kernel  
   
 Correremos la siguiente linea para finalizar con la instalación de este.  
   
 ```
 sudo make install
 ```
   
![image](https://user-images.githubusercontent.com/75387331/166200144-acacbccd-9961-4d03-8be3-d4f92810fe8d.png)  
  
Después vamos a actualizar los inittramfs a nuestra versión instalada: 
```
sudo update-initramfs -c -k 5.17.5
```
  
Y posteriormente actualizaremos el GRUB: 
  
```
sudo update-grub
```
## X. Elegir kernel para correr la máquina
  
Una vez que reiniciemos nos mandará al GRUB donde nos iremos a Advanced options for Ubuntu. 
  
![image](https://user-images.githubusercontent.com/75387331/166206122-00296ef3-a7a4-44e2-83c8-0681b58ac44d.png)  
  
Y de aqui elegiremos el kernel 5.17.5 que fue el que acabamos de instalar.   
  
![image](https://user-images.githubusercontent.com/75387331/166206287-dd4b944b-f488-41ea-aec1-f8fe90722700.png)  
  
## XI. Verificar que se inició e instaló el kernel en consola  
  
Vamos a correr el siguiente comando para verificar que el kernel que iniciamos es el que queriamos:  
``` 
uname -r
```  
  
![image](https://user-images.githubusercontent.com/75387331/166207533-22c07d7a-8ba9-4064-b25b-3cb3250363cd.png)  

Y listo, asi es como se instala un kernel de Linux.  


