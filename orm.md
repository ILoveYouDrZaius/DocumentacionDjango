# ORM

### Django shell
```bash
python manage.py shell
```

IMPORTANTE: Debemos importar el modelo el cuál vamos a Utilizar

```bash
from aplicacion.models import NombreModelo
```

### Ver campos modelo
```bash
MyModel._meta.get_fields()
```

### Extraer ciertos campos de un modelo
```bash
MyModel.objects.values_list('column_name').filter(condition)
```

### Ejemplos consultas
```bash
NombreModelo.objects.all() // devuelve todos los objetos NombreModelo
NombreModelo.objects.get(username='Manolo') // devuelve el NombreModelo Manolo
NombreModelo.objects.filter(author=me) // filtra por autor
NombreModelo.objects.filter(title__contains='noticia') // los title que contengan noticia
```

### Multievaluadas
```python
from django.db.models import Q

Call.objects.filter(Q(sender=clientnumber) | Q(receiver=clientnumber))
```

### Ordenar resultados
```bash
NombreModelo.objects.order_by('created_date')
NombreModelo.objects.order_by('-created_date') // orden inverso
```

### Contar resultados (count)
```bash
NombreModelo.objects.all().count()
```

### Crear objetos
```bash
NombreModelo.objects.create(author=me, title='Sample title', text='Test')
```
