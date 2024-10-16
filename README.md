# Tarea 2 SXE

## 1.Descarga la imagen "alpine" SIN ARRANCARLA y comprueba que está en tu equipo

Para descargar la imagen de alpine sin descargarla utilicé:
```bash
docker pull alpine
```
y para comprobar que estaba en mi equipo: 
```bash
docker images
```
## 2.Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre

Para crear un contenedor sin especificar nombre se uliliza:
```bash
docker run alpine
```
y para comprobar que está arrancado y además su nombre se ejecuta: 
```bash
docker ps -a
```
Esto lista todos los contenedores, su estado y su nombre entre otras cosas.
En mi caso el contenedor que acabo de crear de alpine está "exited" y su nombre es blissful_brattain.

## 3.Crea un contenedor con el nombre 'dam_alp1'. ¿Como puedes acceder a él?

Para crear un contenedor con el nombre especificado por mi se utiliza:
```bashnewgrp docker
docker run --name dam_alp1 alpine sleep 1000
```
El comando sleep 1000 lo utilizo para mantener el contenedor activo y poder acceder a él.

Para acceder a este contenedor recién creado se utiliza:
```bash
docker exec -it dam_alp1 /bin/sh
```
Con esto accedo a la terminal de ese contenedor.

## 4.Comprueba que ip tiene y si puedes hacer un ping a google.com

Para comprobar primero la ID o el nombre del contenedor recién creado se usa:
```bash
docker ps -l
```
Después se utiliza el nombre o la ID para comprobar la IP de la siguiente manera:
```bash
docker inspect dam_alp1 | grep IPA
```
En lugar del nombre se puede usar la ID.
En mi caso la IP del contenedor es 172.17.0.2.

Para hacer un ping a google.com:
1. Se accede al contenedor con:
```bash
docker exec -it dam_alp1 sh
```
2. Se instala la apk para poder hacer el ping con:
```bash
apk add iputils
```
3. Por último se hace el ping a google.com con:
```bash
ping google.com
```
## 5.Crea un contenedor con el nombre 'dam_alp2'. ¿Puedes hacer ping entre los contenedores?

Para crear el contenedor nuevo utilizo:
```bash
docker run -it --name dam_alp2 alpine /bin/sh
```
Con esto aparte de crearlo, lo empieza y entra en ese contenedor. Por lo tanto para hacer ping al otro lo único que tenemos que hacer es:
```bash
ping -c 2 172.17.0.2 
```
Usando la IP de dam_alp1 dentro del contenedor dam_alp2 se puede hacer ping entre contenedores

## 6.Sal del terminal, ¿que ocurrió con el contenedor?

Al salir de la terminal y luego volver a abrirla ambos contenedores siguen funcionando.

## 7.¿Cuanta memoria en el disco duro ocupaste?

Para ver la memoria en disco duro que se ocupó se utiliza el comando:
```bash
docker system df
```
El resultado que da es este:

|TYPE        |TOTAL        |     ACTIVE 1 |  SIZE    |    RECLAIMABLE|
| --------- | ----------- | ------------- | --------- | ------------ |
|Images     |       4     |    2          |  277.6MB  | 269.8MB (97%) |
|Containers  |      5      |   0          | 7.096MB  | 7.096MB (100%) |
|Local Volumes  |   0       |  0          |   0B     |   0B           |
|Build Cache   |    0        | 0           |  0B     |   0B           |

Aquí podemos ver cuanto ocupan nuestras imágenes y contenedores en el disco duro.

## 8. ¿Cuanta RAM ocupan los contenedores? ¿Hay algún comando docker para saber esto?.

Con el comando
```bash
docker stats
```
Se puede ver en tiempo real el uso de memoria, CPU y red para cada contenedor que esté activo.
Lo que sale por terminal al poner el comando es algo como esto:

|CONTAINER ID |  NAME    |   CPU % |   MEM USAGE / LIMIT |  MEM %   |   NET I/O    |   BLOCK I/O  |   PIDS |
|------------ | -------- | ------- | -------------------- | -------- | ----------- | ------------ | ----- |
|e1ced643f032  |  dam_alp2  | 0.00%   |  504KiB / 7.883GiB |  0.01%  |   7.66kB / 0B  | 1.32MB / 0B  | 1   |
