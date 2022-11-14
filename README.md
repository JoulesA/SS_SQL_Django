# Django
## Inicialización del proyecto 
Django es un framework para desarrollo web escrito en python, por lo que las instrucciones deben de ser ejecutadas en una terminal de python.
Para crear un nuevo proyecto se usa la instrucción: 

	django-admin startproject Name

En este caso se nombro Tutorial, lo que genera un carpeta con el nombre que se le asigno y las funciones para que inicie el servidor.

Para iniciar el servidor se usa la instrucción:

	manage.py runserver


>[!Note]
> En mi caso para correr este comando en terminal debo llamar a python desde la capeta raiz y despues usar el path para finalmente correr el programa:   
	& C:/Users/loboa/AppData/Local/Programs/Python/Python39/python.exe c:/Users/loboa/OneDrive/Documentos/SS/Tutorial/manage.py runserver

![image](https://user-images.githubusercontent.com/57508332/198139596-7dd3a842-79b4-47ce-a0b6-7f44672ba645.png)

## Iniciar app
Para generar el sitio web y sus demas funciones necesitamos crear una app, esto se realiza con el comando `manage.py startapp Name`, en este caso la app se llamó libreria.
Este comando genera una carpeta dentro de la carpeta principal del proyecto con el nombre que se le haya dado.
>[!Caution] Precaución 
>	Para poder hacer uso de la nueva app hay que declararla en el programa `settings.py` en la seccion Aplication definition que esta en la carpeta con el mismo nombre que el proyecto `\proyecto\proyecto\settings.py`
```Python
	# Application definition
	INSTALLED_APPS = [	
	    'django.contrib.admin',
	    'django.contrib.auth',
	    'django.contrib.contenttypes',
	    'django.contrib.sessions',
	    'django.contrib.messages',
	    'django.contrib.staticfiles',
	    'libreria',
	]
```

## Añadir vistas a la pagina web
El manejo de las vistas se hace mediante funciones que se declaran en `\proyecto\newapp\views.py` en donde se añaden los modulos necesarios como _HttpResponse_, estas vistas contienen las llamadas a los archivos `.html` que contienen las vistas de la pagina.

La gestion de las direcciones web se hace en `\proyecto\newapp\urls.py` donde se añaden las direcciones web y la vista asociada a esa direccion.
>[!Danger]
>Hay dos archivos `urls.py` uno ubicado en `\proyecto\proyecto\` y otro en `\proyecto\newapp\`, el que esta dentro de la app creada no existe por lo que hay que crearlo y añadir el siguiente codigo:
```Python
	from django.urls import path
	from . import views`
	urlpatterns = [
	path('', views.inicio, name = 'inicio'),
	]
```
> En el archivo `\proyecto\proyecto\urls.py` hay que añadir en urlpatterns el nuevo archivo creado en la app
```Python
path('', include('newapp.urls')),
```
> Ademas tambien hay que importar el comando `include`
```Python
from django.urls import include
```

### Carpeta templates
Las archivos `.html` se guardan en una carpeta llamada templates en la app creada, para el ejemplo se realizo un archivo plantilla (`base.html`) que sirve de base para las vistas asi como las vistas.
Se crearon las siguientes vistas:
- Inicio
- Nosotros
- Libros
	- Editar
	- Crear
 ![image](https://user-images.githubusercontent.com/57508332/198154648-8d9f2d6d-b80a-41e6-8ae9-d3e63f4db544.png)
 ![image](https://user-images.githubusercontent.com/57508332/198154666-c2932900-a9c5-4367-9f64-9e6bcf3d493a.png)
 ![image](https://user-images.githubusercontent.com/57508332/198155438-46834027-0572-4d1a-a628-7d03f7f9a211.png)

## Migración 

Para realizar la migración se requiere que la base de datos exista y, tener un modelo creado y guardado en `models.py`
La creación de la base de datos se hace en MySQL Workbench
```MySQL
create database name;
```

En python necesitamos que la libreria `pymysql` este instalada en caso que no lo este se usa
```Terminal
pip install pymysql
```

En el archivo `proyecto/settings.py` hay que modificar el apartado de databases
```Python
DATABASES = {
	'default': {
		'ENGINE': 'django.db.backends.mysql',
		'NAME': 'eeg_db',
		'USER': 'root',
		'PASSWORD': 'qwerty',
		'HOST': '127.0.0.1',
		'PORT': '3306',
	}
}
```

Los modelos (tablas) se declaran en el archivo `models.py` 
>[!Note] 
> Para este ejemplo se uso el siguiente modelo
``` Python
from django.db import models
# Create your models here.
 class Libro(models.Model):
     id = models.IntegerField(primary_key=True)
     titulo = models.CharField(max_length=100, verbose_name='Titulo')
     imagen = models.ImageField(upload_to='imagenes/', null=True, verbose_name='imagen')      descripcion = models.TextField(null=True, verbose_name='descripcion') 
```

En el archivo `__init__.py` hay que añadir
``` Python
import pymysql
pymysql.install_as_MySQLdb()
```

Para realizar las migraciones hay que introducir en una terminal de python 
```
manage.py makemigrations
```

```
manage.py migrate
```

Una vez se crean los modelos, estos se declaran en el programa `admin.py` de la app:
```Python
from django.contrib import admin
from .models import *
# Register your models here.
admin.site.register(Libro)
```

### Usuario y contraseña de la base de datos
Una vez se tiene la estructura se crea el usuario para la base de datos usando una terminal de python
``` Terminal
 & C:/Users/loboa/AppData/Local/Programs/Python/Python39/python.exe c:/Users/loboa/OneDrive/Documentos/SS/Tutorial/manage.py createsuperuser
```
Lo cual nos pedira un usuario, correo y contraseña.

>[!Warning]
>Aqui SQL puede der lata, si no esta bien configurado el puerto de la base de datos, si el servicio esta detenido en la maquina o si hay dos servicios entrando apor el mismo puerto.

Despues de creado el usuario, se puede acceder a la base de datos con la ruta `/admin`



## Prueba de tablas 
![image](https://user-images.githubusercontent.com/57508332/197007152-64979edc-6ca4-4676-b040-6a318606042b.png)

## Migracion de sqlite a My SQL
La migracion se hace desde la ejecuacion del programa manage.py en consola, para ello se necesita que que la base de datos ya exista, por lo que se genera esta desde MySQL Workbench y se prueba que conecte usando manage.py runserver

manage.py makemigrations 
![image](https://user-images.githubusercontent.com/57508332/197304296-3b077495-5b0a-41e0-b4ec-432a346bb367.png)

Eventualmente se hace monta el modelo usando manage.py migrate

![image](https://user-images.githubusercontent.com/57508332/197304881-bddf3ab1-2716-4811-b2e0-e26d1750d089.png)
![image](https://user-images.githubusercontent.com/57508332/197304945-b25e7f14-1b19-43e4-b8c0-7a1ea45060ff.png)
Aqui se puede ver que ya esta hecha la migracion y ya estan las tablas User, EEG_data e info 


# Vistas de la web al 21/10/22
![image](https://user-images.githubusercontent.com/57508332/197305144-e8db3a90-4e3f-4142-a450-237449d95e9f.png)
![image](https://user-images.githubusercontent.com/57508332/197305152-c9278970-b8ed-48cb-afee-48fab4e1dd83.png)
Hay labels temporales en lo que se inserta la info de la base de datos 
![image](https://user-images.githubusercontent.com/57508332/197305192-fb019e78-e0a7-4d90-a6aa-9dee783540da.png)
Falta formato y que el resto se secciones solo puedan ser accesadas si se rellena debidamente el campo de usuario y contraseña
![image](https://user-images.githubusercontent.com/57508332/197305269-22116650-882b-4126-80d7-fa38675a3986.png)
![image](https://user-images.githubusercontent.com/57508332/197305285-c75a149f-e4c7-4896-9b6c-ec6311f73596.png)

![image](https://user-images.githubusercontent.com/57508332/197305911-a7e693c3-a258-422b-9da6-cc6ecaa1550f.png)
![image](https://user-images.githubusercontent.com/57508332/197306108-459c1c10-43f1-492c-ad24-ea1e0c4c6309.png)

# Modelo de tablas 
Codigo que genera los modelos de tablas en el servidor el cual esta montado en CleverCloud

Se plantean 4 tablas las cuales son las principales, proyecto, voluntario, prueba y muestra, ademas de una tabla de usuario que viene por defecto en el framework de DJANGO.
Asociado a los campos que tienen foregin keys en sus modelos se anade el parametro `on_delete` el cual hace referencia a que pasa con todos aquellos elementos que poseen una foregin key si es que esta instancia es eliminada, en este caso cascade elimina los datos en caso de que la foregin key a la que se hace referencia es eliminada, es decir si alguien borra el proyecto al que los datos hacen referencia los datos seran borrados pero no aplica de forma inversa, es decir si un dato es borrado esta accion no afecta al proyecto principal 

``` Python
class Tareas(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=50, )

class Proyecto(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=50, )
    fs = models.FloatField()

    tarea = models.ForeignKey(Tareas, on_delete=models.CASCADE)
    encargado = models.ForeignKey(User, on_delete=models.CASCADE)
    
class Prueba(models.Model):
    id = models.AutoField(primary_key=True)
    descripcion = models.TextField(max_length=400)
    clase = models.IntegerField(verbose_name='clase')
    canales = models.CharField(max_length=50)

    proyecto = models.ForeignKey(Proyecto, null=True, on_delete=models.CASCADE,)

class Voluntario(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=50, )
    edad = models.IntegerField()
    genero = models.CharField(max_length=50)
    salud = models.BooleanField()
    notas = models.TextField(max_length=400, null=True)

    def __str__(self):
        texto = 'Voluntario No.'+self.id+': '+self.genero+' de '+self.edad+' años'
        if self.salud:
            texto += 'Padecimientos: Ninguno'
        else: 
            texto += 'Padecimientos: '+self.notas
        return texto

class Muestra(models.Model):
    id = models.AutoField(primary_key=True)
    duracion = models.FloatField()
    signal_data = models.FileField(upload_to='signal_data/', verbose_name='Datos' )

    prueba = models.ForeignKey(Prueba, on_delete=models.CASCADE,)
    # clase = models.ForeignKey(Prueba.clase,on_delete=models.CASCADE,)
    voluntario = models.ForeignKey(Voluntario, on_delete=models.CASCADE,)

```

Si llega a aparecer el error:
    > You are trying to add a non-nullable field 'new_field' to userprofile without a default;
    > we can't do that (the database needs something to populate existing rows).
El truco esta en eliminar los archivos generados en migrations excepto el scrip de `__init__`

