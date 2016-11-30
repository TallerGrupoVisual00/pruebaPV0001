# README VOTO WEB #

Implementación en DJango del Sistema Automático de Voto Electrónico para permitir que los profesores que están en el extranjero puedan votar también.

### Preparar las elecciones ###

* Conocer el identificador de la(s) elección(es) que se desea iniciar, este número se lo obtiene del sistema SaveAdmin al momento de crear las elecciones.
* Copiar los archivos de seguridad de la junta web correspondiente a cada elección en la ruta:
**security/<idEleccion>/**
```
#!python

booth.xml.encr
booth.xml.encr.sign
SAVESymmKey
eJRVSignPrivateKey
SAVESignPublicKey
```

* Copiar las fotos de los candidatos de todas las elecciones en el directorio:
**media/photos/**
* Copiar los archivos **snusb.xml.encr** y **snusb.xml.encr.sign** de cada junta web en el directorio:
**DATOS/<idEleccion>/** El mismo que deberá tener permisos de escritura 777
### ¿Cómo iniciar una nueva elección? ###

* Ejecutar el siguiente comando desde la ruta donde está instalado este sistema de voto web en el servidor (Ej: /opt/votoweb):
```
#!python

./manage.py start_elections <idEleccion1>,<idEleccion2>,<idEleccion3>...
```

* Después ejecutar el siguiente comando para permitir a los profesores obtener los tokens generados para votar en la respectiva junta web:

```
#!python

./manage.py replicate_codecards
```

* Finalmente, ejecutar el siguiente comando para cada usuario empadronado en la junta web para habilitarlo y que pueda obtener el token luego de autenticarse con su usuario de ESPOL:
```
#!python

./manage.py init_user <Username> <idEleccion>
```


### ¿Cómo cerrar las juntas web? ###

* Ejecutar el siguiente comando desde la ruta donde está instalado este sistema de voto web en el servidor (Ej: /opt/votoweb/):

```
#!python

./manage.py close_elections
```

### Generar los pendrives con los resultados ###
* Copiar el contenido del directorio **DATOS/<idEleccion>/** en un pendrive por cada junta web


### Dependencias del sistema ###
* Django 1.6.5
* Python 2.x
* pycrypto
* SOAPpy
