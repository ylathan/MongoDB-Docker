CREANDO UN CONTENEDOR

Descripción paso por paso

Notas:
  - Vamos a trabajar en Docker-compose y qué es;es una herramienta para ejecutar aplicaciones de múltiples contenedores en Docker definidas mediante el formato de archivo Compose. Un archivo Compose se utiliza para definir cómo se configuran uno o más contenedores que componen su aplicación.

- Se creará un documento llamado docker-compose, otro mongo, carpetas para el volumen llamadas monguitodata y log( esto se aclará porque los nombres los puede elegir el creador a su gusto)

- Uso linux en un entorno virtual(creamos una conexión con virtualbox y ejecutamos los comandos dentro de Putty con la dirección IP proporcionada por el virtualbox).

-----------------------------------------------------------------------------------------------------------------------------------------
Paso 1. Crear documento de docker-compose.

touch docker-compose.yml

cat > docker-compose.yml 

- touch sirve para crear el archivo, y el .yml que vienen del YAML crea un formato de serializacion legible para humanos--
- cat >: sirve para crear archivos pero además, tambien se pueden unir archivos y visualizarlos.
  
-----------------------------------------------------------------------------------------------------------------------------------------
Paso 2. Crear la configuracion documento de docker-compose.yml:

  version: '2.2'
  
  services:
  
    mongo:
      image: mongo:4.0.4
      restart: always
      container_name: monguito
      environment:
        - MONGODB_USER="user"
        - MONGODB_PASS="pass"	
        
      volumes:
        - ./monguitodata:/data/db
        - ./monguitodata/log:/var/log/mongodb/
      ports:
        - "27017:27017"     
      
   Explicación de cada línea   
- version del docker compose
- el servico que queremos configurar en este caso mongo
- nombre del servicio
- indica que estamos utilizando la imagen oficial de MongoDB versión 4.0.4
- asegura que el contenedor se reinicie automáticamente si se detiene
- nombre del cointainer
- entorno, se configura el nombre y contraseña para el usuario raiz
- me permite mapear el almacenamiento del contenedor en este caso los dos que contiene
- puerto que permite acceder a la base de datos MongoDB desde fuera del contenedor.
  
En resumen todo este comando crea el contenedor con usuario y contraseña, monta los volumenes locales para los datos y los registros y expone en puerto 27017 para acceder a la base de datos.

----------------------------------------------------------------------------------------------------------------------
paso 3. Crear archivos para correr comando en la la terminal

touch mongo.sh 

- .sh: contiene un programa de computadora para ser ejecutado por el shell de Unix.

----------------------------------------------------------------------------------------------------------------------
Paso 4. Cargar comandos al archivo creado:

#Crear carpeta para volumen de mongo.

mkdir monguitodata && cd monguitodata; cd monguitodata || mkdir log

- mkdir monguitodata: Intenta crear un directorio llamado monguitodata.
- &&: Si la creación del directorio anterior tiene éxito, continúa con la siguiente acción.
- cd monguitodata: Cambia al directorio recién creado llamado monguitodata.
- ;  Ejecuta la siguiente acción independientemente del resultado de la acción anterior.
- cd monguitodata || mkdir log: Intenta cambiar al directorio monguitodata. Si no existe, crea un directorio llamado log.

cd ~

- Cambia al directorio de inicio del usuario (~ representa el directorio de inicio).

#Iniciar el contenedor.

sudo docker-compose up -d

- Este comando ejecuta los servicios definidos en el archivo docker-compose.yml utilizando Docker Compose.
- sudo: se utiliza para ejecutar el comando con privilegios de superusuario.
- -d: inicia los contenedores en segundo plano (modo desatachado).

El resultado de todo el comando muestra que se está creando una red llamada “ubuntu_default”(en mi caso la red se llama ubuntu) y se está descargando la imagen de MongoDB versión 4.0.4

---------------------------------------------------------------------------------------------------------------------------------------
Paso 5.

Control + d

- Se presiona estando en el prompt de la línea de comandos vacío.

--------------------------------------------------------------------------------------------------------------------------------------
Paso 6. Asignar permisos de ejecución y ejecutar mongo.sh

chmod u+x mongo.sh
./mongo.sh

- chmod: permite la asignación de permisos de acceso a carpetas o directorios​.
u+x: le da el permiso de ejecucion(execution).

- ./: es para ejecutar archivos.En este caso ejecuta el archivo llamaddo mongo.sh
_______
Paso 7. 

¡Usar mongo a placer!
