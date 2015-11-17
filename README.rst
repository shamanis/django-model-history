#Dajngo Model Hisotry
����� ������������ ��� ������������ ��������� �������� �������.

## ������� �����
0. ������������� �����:
```
pip install django-model-history
```
1. ��������� ��� � INSTALLED_APPS:
```
INSTALLED_APPS = (
    ...
    'model_history'
)
```
3. ��������� ��������:
```
python manage.py migrate model_history
```
4. ��������� ��������� model_hisotry � ������ ����� ������:

```python
#..some import
from model_history.decorators import model_history


@model_history()
class SomeModel(models.Model):
    field_one = models.CharField()
    last_modified = models.DateTimeField()
```
