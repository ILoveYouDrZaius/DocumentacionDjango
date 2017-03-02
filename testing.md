# Testing en Django

- Clase y métodos:

```python
from django.test import TestCase

class TestUserClient(TestCase):
    @classmethod
    def setUpTestData(self):
      self.user_test = User(username="000000001", password="123a123b")
      self.user_test.save()

    def test_createC1(self):
      self.assertTrue(FinalClient.objects.get(user__username="000000001"))

    def test_deleteC1(self):
      self.user_test.delete()
      self.assertFalse(FinalClient.objects.filter(user__username="000000001").exists())
```

Con *setUpTestData*, se ejecuta su contenido sólo una vez antes de todas las funciones. Con *setUp* ejecutaríamos su contenido cada vez antes de cada función.

- Ejecutar tests:
```bash
./manage.py test
```

## Probar métodos de *views*
```python
post_data = {
    'username' : '987777777',
    'password' : '123a123b',
}
response = self.client.post(reverse('loginUI'), data=post_data)
self.assertTrue('Hola, ' in str(response))
```
