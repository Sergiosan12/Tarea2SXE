# Tarea 2 SXE

## 1.Descarga la imagen "alpine" SIN ARRANCARLA y comprueba que está en tu equipo

Para descargar la imagen de alpine sin descargarla utilicé:
```bash
sudo docker pull alpine
```
y para comprobar que estaba en mi equipo: 
```bash
sudo docker images
```
## 2.Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre

Para crear un contenedor sin especificar nombre se uliliza:
```bash
sudo docker run alpine
```
y para comprobar que está arrancado y además su nombre se ejecuta: 
```bash
sudo docker ps -a
```
Esto lista todos los contenedores, su estado y su nombre entre otras cosas
En mi caso el contenedor que acabo de crear de alpine está "exited" y su nombre es blissful_brattain
