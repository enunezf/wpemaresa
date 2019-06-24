# Ambiente de pruebas Wordpress Emaresa

## Prerequisitos

* Ubuntu 18.04, usuario con privilegios de sudo
* Docker instalado
* Docker compose instalado
* Un dominio de pruebas (http://www.freenom.com/en/index.html)
* DNS Configurado a la IP publica del servidor


## Deply de ambiente
### Creación de certificado
Ejecutar
```
docker-compose up -d
```
La salida debe terminar con:
```
Creating db ... done
Creating wordpress ... done
Creating webserver ... done
Creating certbot   ... done
```
Revisar el estado de los contenedores creados:
```
docker-compose ps
  Name                 Command               State           Ports       
-------------------------------------------------------------------------
certbot     certbot certonly --webroot ...   Exit 0                      
db          docker-entrypoint.sh --def ...   Up       3306/tcp, 33060/tcp
webserver   nginx -g daemon off;             Up       0.0.0.0:80->80/tcp 
wordpress   docker-entrypoint.sh php-fpm     Up       9000/tcp
```
En caso de algún error se puede revisar con:
```
docker-compose logs service_name
```
**para verificar la creación del sertificado**
```
docker-compose exec webserver ls -la /etc/letsencrypt/live
drwx------    3 root     root          4096 May 10 15:45 .
drwxr-xr-x    9 root     root          4096 May 10 15:45 ..
-rw-r--r--    1 root     root           740 May 10 15:45 README
drwxr-xr-x    2 root     root          4096 May 10 15:45 emaresa.unudev.com
```
