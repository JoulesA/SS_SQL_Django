# SQL-Django
Pruebas y tutoriales de SQL y Django

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


