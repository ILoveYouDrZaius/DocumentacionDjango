### Dudas


# General

### Reiniciar apache y ver log de error
```bash
systemctl restart httpd && tail -f /var/log/httpd/error_log
```

### Crear proyecto Django
```bash
django-admin startproject mysite .
```

### Modificar wsgi.py
```python
import os, sys

from django.core.wsgi import get_wsgi_application

sys.path.append('/var/www/django/smartclients/')
sys.path.append('/var/www/django/smartclients/smart/')
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'smart.settings')

application = get_wsgi_application()
```

### Configuración BBDD
*settings.py* :
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'smart_clients',
        'USER': 'smart_clients',
        'PASSWORD': 'smart_clients',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

### Generar aplicación nueva
```python
python manage.py startapp nameapp
```
Y agregar su nombre (namemodel) en la lista *INSTALLED_APPS*, en el archivo *settings.py*

### Propagar cambios de los modelos a la base de datos
Después de cambiar algún modelo tenemos que propagar este cambio a la base de datos. Makemigrations prepara un archivo de migración, migrate lo aplica a BBDD:
```python
python manage.py makemigrations namemodel
python manage.py migrate namemodel
```

### Restaurar base de datos
Limpia toda la BBDD
```bash
python manage.py flush
```

### Generar panel administrador y contraseña
Añadir en *app/admin.py* lo siguiente:

```python
from django.contrib import admin
from .models import Client

admin.site.register(Client)
```
Crear superusuario para entrar al panel:
```bash
python manage.py createsuperuser
```

### Recoger archivos estáticos
Tener configurada la variable *STATIC_ROOT* en *settings.py*:
```python
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

Y ejecutar:
```bash
python manage.py collectstatic
```

# Tipos de datos
### Concatenar Strings
```python
'Mi client number es %s y mi key %d'%(clientnumber, key))
```


# Formularios

### Establecer valores por defecto:
En la vista debemos pasarle esos valores a través del constructor del formulario, a través de initial.
```python
form = UserFeaturesForm(initial={
                'voice_mail'        :   client.voiceMail,
                'call_forwarding'   :   client.callForwarding,
                'night_mode'        :   client.nightMode,
})
```

#### Dudas resueltas
* CSS Admin -> collectstatic
* Ver log Django -> clase logger de Sergio
* ¿Cada modelo es una aplicación aparte? -> No
* ¿Utilizar User de django para usuario telefonía? -> Sí, heredando de ella
* ¿Reiniciar apache para cambios? -> Para cambios en código Python sí
* En la template, ¿para qué sirve block content? -> Genera bloques de contenido que luego al heredar puedes sobrescribir según convenga. Más información en documentación.
* Redirección infinita -> arreglada
* Propagación error desde form hasta template -> añadiendo campo
