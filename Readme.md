# TAREA 3

*Esteban Miguel Montes Adraz* - *2 DAM* - *SXE*
***

## 1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.

Para descargar la imagen httpd de apache en la versión 2.4 ejecutamos el siguiente comando

```
docker pull httpd:2.4
```

## 2. Crea un contenedor con el nombre 'dam_web1'.

Para crear un contenedor con este nombre hacemos lo siguiente

```
docker run -d --name dam_web1 httpd:2.4
```

## 3. Si quieres poder acceder desde el navegador de tu equipo, ¿que debes hacer?

**Utiliza bind mount para que el directorio del apache2 'htdocs' esté montado un directorio que tu elijas.**

Para poder hacer esto, empezamos creando un directorio para contener nuestro HTML
```
mkdir ~/mi_web
```

Luego entramos en el directorio y creamos el HTML
```bash
cd mi_web

echo "<html><body><h1>Hola Mundo</h1></body></html>" > index.html
```
Eliminaremos el contenedor dam_web1 de antes ya que no lo hicimos con mount y lo volveremos a crear para que conecte con el directorio que creamos anteriormente
```
docker rm -f dam_web1

docker run -d --name dam_web1 -p 8000:80 -v ~/mi-web:/usr/local/apache2/htdocs httpd
```
Este comando monta el directorio ```~/mi-web``` (en tu host) en ```/usr/local/apache2/htdocs``` (en el contenedor), que es donde Apache busca los archivos que debe servir.

## 4. Comprobar que puedes acceder a la página desde el navegador

Para entrar a la página desde el navegador pondremos esto en el buscador
```
http://localhost:8000
```

## 5. Crea otro contenedor 'dam_web2' con el mismo bind mount y a otro puerto, por ejemplo 9080.

Vamos a crear el contenedor dam_web2 con el puerto 9080
```
docker run -d --name dam_web2 -p 9080:80 -v ~/mi-web:/usr/local/apache2/htdocs httpd
```

## 6. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:
* http://localhost:9080
* http://localhost:8000

Para comprobar los servicios pondremos esto en el buscador
```
https://localhost:8000
(para dam_web1)

https://localhost:9080
(para dam_web2)
```

## 7. Realiza modificaciones de la página y comprueba que los dos servidores 'sirven' la misma página

Ambos contenedores están utilizando el mismo bind mount, así que editaremos el HTML y los cambios se reflejarán en ambos contenedores
```bash
echo "<html><body><h1>¡Hola Mundo Modificado!</h1></body></html>" > ~/mi-web/index.html
```

