# MongoDB-Docker
Descripción paso por paso
CREANDO UN CONTENEDOR
--usando linux en un entorno virtual--

Paso 1. Crear documento de docker-compose.
touch name-archivo.yml
cat > name-archivo.yml (opcional)
--  touch sirve para crear el archivo, y el .yml que vienen del YAML crea un formato de serializacion legible para humanos--
-- cat > ,tambien sirve para crear archivos pero ademas tambien se puden unir archivos y visualizarlos--

Paso 2.

version: '2.2' -- version del docker compose--

services: --el servico que queremos configurar en este caso mongo--

  mongo:                       --nombre del servicio--
    image: mongo:4.0.4         --indica que estamos utilizando la imagen oficial de MongoDB versión 4.0.4.--
    restart: always            --asegura que el contenedor se reinicie automáticamente si se detiene.--
    container_name: monguito    --nombre del cointainer--
    environment:               --entorno, se configura el nombre y contraseña para el usuario raiz --
      - MONGODB_USER="user"
      - MONGODB_PASS="pass"	
      
    volumes:                -- me permite mapear el almacenamiento del contenedor en este caso los dos que contiene--
      - ./monguitodata:/data/db
      - ./monguitodata/log:/var/log/mongodb/
    ports:
      - "27017:27017"       -- puerto que permite acceder a la base de datos MongoDB desde fuera del contenedor.--

----------------------------------------------------------------------------------------------------------------------
paso 3. Crear archivos para correr comando en la la terminal
touch mongo.sh 
--ya sabemos que hace el touch y ahora el .sh, contiene un programa de computadora para ser ejecutado por el shell de Unix

----------------------------------------------------------------------------------------------------------------------
Paso 4. Cargar comandos al archivo creado:

#Crear carpeta para volumen de mongo:
mkdir monguitodata && cd monguitodata; cd monguitodata || mkdir log

mkdir monguitodata: Intenta crear un directorio llamado monguitodata.
&&: Si la creación del directorio anterior tiene éxito, continúa con la siguiente acción.
cd monguitodata: Cambia al directorio recién creado llamado monguitodata.
;  Ejecuta la siguiente acción independientemente del resultado de la acción anterior.
cd monguitodata || mkdir log: Intenta cambiar al directorio monguitodata. Si no existe, crea un directorio llamado log

/*ubuntu@servidor_ubuntu:~/monguitodata$ cd:
Cambia al directorio de inicio del usuario (~ representa el directorio de inicio).
ubuntu@servidor_ubuntu:~$ sudo docker-compose up -d:
Este comando ejecuta los servicios definidos en el archivo docker-compose.yml utilizando Docker Compose.
sudo se utiliza para ejecutar el comando con privilegios de superusuario.
-d inicia los contenedores en segundo plano (modo desatachado).
El resultado muestra que se está creando una red llamada “ubuntu_default” y se está descargando la imagen de MongoDB versión 4.0.4.*/

