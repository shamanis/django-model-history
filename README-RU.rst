=====
Dajngo Model Hisotry
=====

����� ������������ ��� ������������ ��������� �������� �������. ����� ����������� ������ ����� ��������� ������� � ������� ������������ ������, ���� �� ��� ������.
���� ��������� ������� ���� ��������� �������� ��� �� �������, �� ���� user ����� ������.

=====
������� �����
=====
0. ������������� �����::

    pip install django-model-history2

1. ��������� ��� � INSTALLED_APPS::

    INSTALLED_APPS = (
        ...
        'model_history'
    )

3. ��������� ��������::

    python manage.py migrate model_history

4. ��������� ��������� model_hisotry � ������ ����� ������:

.. code-block:: python

    from model_history.decorators import model_history

    @model_history()
    class SomeModel(models.Model):
        field_one = models.CharField()
        last_modified = models.DateTimeField()


=====
��������� ���������� model_history
=====
1. ``exclude`` - �������� ������ �������� �����, ������� �� ����� �����������. ��-�������� []::

    @model_hisotry(exclude=['last_modified'])

2. ``related`` - ����������� ��� ������, ������ ��������� �� �������. ��-��������� False::

    @model_history(exclude=['last_modified'], related=True)

3. ``related_exclude`` - ������, ��������� �������, ������� ���� ��������� �� ������������. ��-��������� []::

    @model_history(exclude=['last_modified'], related=True, related_exclude=['myapp.models.Model2'])

=====
��������� � settings.py
=====
1. ��������� ������������ � ������� � ������ ``MODEL_HISTORY_SETTINGS``::

    MODEL_HISTORY_SETTINGS = {
        'connect': [
            {'model': 'django.contrib.auth.models.User', 'exclude': ['last_login'], 'related': True, 'related_exclude': ['django.contrib.admin.models.LogEntry']}
        ]
    }
2. ������, ������������� � ��������� ``connect`` ����� ���������� �� ������������, � ���������� �����������
3. ``delete_action`` - ������ �� � ������� ���� ������� "������� ��������� �������". ��-��������� False::

    MODEL_HISTORY_SETTINGS = {
        'delete_action': True
        'connect': [
            {'model': 'django.contrib.auth.models.User', 'exclude': ['last_login'], 'related': True, 'related_exclude': ['django.contrib.admin.models.LogEntry']}
        ]
    }
4. ``delete_permission`` - ����� �������� � ������������ ��������� �� ������������ ������� ���� �� �������� ������� �� �������::

    MODEL_HISTORY_SETTINGS = {
        'delete_action': True,
        'delete_permission': 'is_superuser',
        'connect': [
            {'model': 'django.contrib.auth.models.User', 'exclude': ['last_login'], 'related': True, 'related_exclude': ['django.contrib.admin.models.LogEntry']}
        ]
    }
5. ``revert_action`` - ������ �� ���� � ������� ������� "������������ ������". ��� ������� �������� ������� ������ ��������� ���� ������������ ��������� ������ �� �����. ��-��������� True::

    MODEL_HISTORY_SETTINGS = {
        'delete_action': True,
        'delete_permission': 'is_superuser',
        'revert_action': True,
        'connect': [
            {'model': 'django.contrib.auth.models.User', 'exclude': ['last_login'], 'related': True, 'related_exclude': ['django.contrib.admin.models.LogEntry']}
        ]
    }
6. ``revert_permission`` - ����� �������� � ������������ ��������� �� ������������ ������� ���� �� �������������� �������::

    MODEL_HISTORY_SETTINGS = {
        'delete_action': True,
        'delete_permission': 'is_superuser',
        'revert_action': True,
        'revert_permission': 'is_superuser',
        'connect': [
            {'model': 'django.contrib.auth.models.User', 'exclude': ['last_login'], 'related': True, 'related_exclude': ['django.contrib.admin.models.LogEntry']}
        ]
    }