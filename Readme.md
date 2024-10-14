# TAREA 3


*Esteban Miguel Montes Adraz* - *2 DAM* - *SXE*
***
## 1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.
Para descargar la imagen httpd de apache en la versión 2.4 ejecutamos el siguiente comando
```angular2html
docker pull httpd:2.4
```

## 2. Crea un contenedor con el nombre 'dam_web1'.
Para crear un contenedor con este nombre hacemos lo siguiente
```angular2html
docker run -d --name dam_web1 httpd:2.4
```


