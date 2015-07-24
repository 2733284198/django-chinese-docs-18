<!--
  ���ߣ�Github@wizardforcel
-->

# ��д���ݿ�Ǩ�� #

��һ�ڽ���������������ڲ�ͬ�������η����ͱ�д���ݿ�Ǩ��. �й�Ǩ�Ƶ��������ϣ���鿴 the topic guide.

## ����Ǩ�ƺͶ����ݿ� ##

��ʹ�ö�����ݿ�ʱ����Ҫ����Ƿ����ĳ���ض����ݿ�����Ǩ�ơ����磬����� ֻ ����ĳ���ض����ݿ�������Ǩ�ơ�

Ϊ���������RunPython��ͨ���鿴schema_editor.connection.alias ������������ݿ����ӱ�����

```
from django.db import migrations

def forwards(apps, schema_editor):
    if not schema_editor.connection.alias == 'default':
        return
    # Your migration code goes here

class Migration(migrations.Migration):

    dependencies = [
        # Dependencies to other migrations
    ]

    operations = [
        migrations.RunPython(forwards),
    ]
```

```
Django 1.8 ��������
```

��Ҳ�����ṩһ����ʾ��Ϊ **hints�������ݵ����ݿ�·�ɵ�allow_migrate() ������

```
myapp/dbrouters.py
class MyRouter(object):

    def allow_migrate(self, db, app_label, model_name=None, **hints):
        if 'target_db' in hints:
            return db == hints['target_db']
        return True
```

Ȼ��Ҫ�����Ǩ�������ã�ִ�����²�����

```
from django.db import migrations

def forwards(apps, schema_editor):
    # Your migration code goes here

class Migration(migrations.Migration):

    dependencies = [
        # Dependencies to other migrations
    ]

    operations = [
        migrations.RunPython(forwards, hints={'target_db': 'default'}),
    ]
```

������RunPython����RunSQL����ֻ��һ��ģ����Ӱ�죬���ʵ���ǽ�model_name��Ϊ��ʾ���ݣ�ʹ�価���ܶ�·�ɿɼ�����Կɸ��õĺ͵�����Ӧ�ü�����Ҫ��

## ���Ψһ�ֶε�Ǩ�� ##

�����Ӧ����һ�������ء���Ǩ�ƣ������һ���Ѵ��ڵ����������һ��Ψһ�ķǿ��ֶΣ������������Ϊλ���Ѵ������е�ֵֻ������һ�Ρ�������Ҫ�Ƴ�Ψһ�Ե�Լ����

���ԣ�Ӧ��ִ������Ĳ��衣����������У����ǻ���Ĭ��ֵ���һ���ǿյ�UUIDField�ֶΡ�����Ը��������Ҫ�޸ĸ����ֶΡ�

+ ��default=...��unique=True������ӵ���ģ�͵��ֶ��С�����������У�����Ĭ��ʹ��uuid.uuid4��
+ ���� makemigrations ���
+ �༭������Ǩ���ļ���

���ɵ�Ǩ���࿴��ȥ��������

```
class Migration(migrations.Migration):

    dependencies = [
        ('myapp', '0003_auto_20150129_1705'),
    ]

    operations = [
        migrations.AddField(
            model_name='mymodel',
            name='uuid',
            field=models.UUIDField(max_length=32, unique=True, default=uuid.uuid4),
        ),
    ]
```

����Ҫ���������ģ�

+ �������ɵ�Ǩ�����и��ƣ���ӵڶ���AddField����������ΪAlterField��
+ �ڵ�һ��AddField�����У���unique=True��Ϊ null=True����ᴴ��һ���м��null�ֶΡ�
+ ����������֮�䣬���һ��RunPython��RunSQL����Ϊÿ���Ѵ��ڵ�������һ��Ψһֵ������UUID����

���յ�Ǩ����Ӧ�ÿ�������������

```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.db import migrations, models
import uuid

def gen_uuid(apps, schema_editor):
    MyModel = apps.get_model('myapp', 'MyModel')
    for row in MyModel.objects.all():
        row.uuid = uuid.uuid4()
        row.save()

class Migration(migrations.Migration):

    dependencies = [
        ('myapp', '0003_auto_20150129_1705'),
    ]

    operations = [
        migrations.AddField(
            model_name='mymodel',
            name='uuid',
            field=models.UUIDField(default=uuid.uuid4, null=True),
        ),
        # omit reverse_code=... if you don't want the migration to be reversible.
        migrations.RunPython(gen_uuid, reverse_code=migrations.RunPython.noop),
        migrations.AlterField(
            model_name='mymodel',
            name='uuid',
            field=models.UUIDField(default=uuid.uuid4, unique=True),
        ),
    ]
```

�����������ƽ��һ��ʹ��migrate����Ӧ��Ǩ�ơ�

ע������������Ǩ������ʱ�ö��󱻴������ͻ������������(race condition)����AddField֮�� RunPython֮ǰ�����Ķ���Ḳд����ԭʼ��uuid��