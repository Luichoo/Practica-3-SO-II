# Practica-3-SO-II  
## I. Crear y levantar respaldo de nuestra maquina virtual  
Generaremos el respaldo de esta maquina virtual.  
Para hacer el respaldo de nuestra maquina virtual en Vmware se deben de seguir los siguientes pasos:  
  
![image](https://user-images.githubusercontent.com/75387331/166168015-0c05dfa0-4d24-4615-adb0-cf7e467dc6f9.png)  

### 1. Ubicar la carpeta en donde tenemos la maquina virtual que deseamos hacer un respaldo  
Aqui lo tenemos en la carpeta de documentos, creamos de igual manera la carpeta a la que se desea mandar el contenido de la que ya teniamos.  
  
![image](https://user-images.githubusercontent.com/75387331/166167657-e05f5cf8-0cc4-4fbf-881d-b484f620b111.png)  
  
### 2. Copiar los datos de la carpeta contenedora a la otra  
Dentro de la carpeta de nuestra maquina original todos sus datos los seleccionamos.  
  
![image](https://user-images.githubusercontent.com/75387331/166167719-1a6490b7-9d54-434b-a638-7ee7e2c6b9a4.png)  
  
Los datos copiados los meteremos en la carpeta de "Ubuntu respaldo" y esperamos a que se pasen todos los datos.  
  
![image](https://user-images.githubusercontent.com/75387331/166167723-de8b4db4-43a5-4516-ab0b-61a3ed2ad451.png)  
  
### 3. Levantar respaldo  
Le vamos a dar en Open a Virtual Machine y vamos a nuestra carpeta que acabamos de hacer el duplicado y vamos a abrir el archivo .vmx para que nos detecte a la maquina.  
![image](https://user-images.githubusercontent.com/75387331/166167802-14f003e3-dd2f-4d02-9ed3-0ba532880f85.png)  
  
Una vez hecho eso, le cambiamos el nombre a la nueva maquina para diferenciarla y ya andara detectada por vmware.  
  
![image](https://user-images.githubusercontent.com/75387331/166167900-984b89f6-c5c0-45d0-8a9d-25ba653d9c4d.png)  
### 4. Finalizando
Ahora vamos a iniciar la maquina, nos marcará un mensaje que nos indicara si la movimos de lugar o copiamos esta maquina, le diremos que la copiamos e iniciamos y con eso tendremos ya listo el respaldo en donde trabajaremos a continuación.  
  
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
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
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

![image](https://user-images.githubusercontent.com/75387331/166170952-44c9501c-9966-4807-ae88-cf1a4ebd4a93.png)  

  
## IV. Descargar versión de kernel desde terminal  
  
Para este paso vamos a ver que versión de kernel queremos en la pagina de [kernel.org](kernel.org).  
  
 ![image](https://user-images.githubusercontent.com/75387331/166169318-becb3e5d-62dd-4821-bda0-56bdcd226c28.png)
Aqui vemos que la ultima versión de kernel es la 5.17.5, vemos de igual manera la versión de nuestro kernel de nuestra maquina con el siguiente comando:  
  
```
uname -r
```
  
![image](https://user-images.githubusercontent.com/75387331/166169505-4bb6ac5f-b2b7-4bb3-94cf-afce52996426.png)
  
Vemos que tenemos la versión 5.13.0 por lo que vamos a subirla a la siguiente versión.  
En nuestro caso que vamos a subir a la 5.17.5, pondremos esto en la linea de código para descargar nuestra versión en terminal, si deseas descargar otra versión, cambia el 5.17.5 por tu versión deseada. 
  
```
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.17.5.tar.xz
```
  
Vamos a Guardarlo en la carpeta de Documents y de aqui nos moveremos a los siguientes pasos.  
  
![image](https://user-images.githubusercontent.com/75387331/166171648-07c876a2-bfe4-4b49-a775-95bdc3ae7ace.png)  

## V. Extraer el codigo del kernel  
1. Vamos a correr en la carpeta en donde descargamos el kernel el siguiente comando:  
  
``` 
tar xvf linux-5.17.5.tar.xz
```
Una vez que se haya descomprimido el kernel se deberá de ver así el directorio con la carpeta de nuestro kernel.  
  
![image](https://user-images.githubusercontent.com/75387331/166171905-755987ff-3771-41e5-968b-0cb8778b0dfd.png)

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
  
3. Para hacer los cambios al archivo de la configuracion vamos a correr el comando **make**:  
``` 
make menuconfig
```
4. Cuando corramos este comando nos abrirá una interfaz donde vamos a darle a guardar dejando todo en sus opciones por defecto y salimos.  
  
![image](https://user-images.githubusercontent.com/75387331/166172675-5cd478de-fbf7-4b1e-9f52-cb22028551f9.png)  
  
## VII. Compilar el kernel  
  
  Para la compílación del kernel vamos a correr el **make**:
  ```
  make
  ```
  Esto llega a tardarse dependiendo de la potencia de tu computadora.  
  ![image](https://user-images.githubusercontent.com/75387331/166173030-54b5846e-aa1d-45c8-9131-6bfbffeb9431.png)  
  
 


