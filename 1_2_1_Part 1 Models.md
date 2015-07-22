<!--
  ��Դ��http://django-chinese-docs.readthedocs.org/
-->

# ��д��ĵ�һ�� Django ���� ��1���� #

������ͨ��������ѧϰ��

�ڱ��̳��У����ǽ�����������һ��������ͶƱӦ�á�

�������������֣�

+ һ��������վ���������ǲ鿴ͶƱ�Ľ���������ǽ���ͶƱ��
+ һ��������վ����������ӡ��޸ĺ�ɾ��ͶƱ��Ŀ��

���Ǽ������Ѿ� ��װ�� Django �����������������������֤�Ƿ��Ѿ���װ�� Django �������ŵİ汾�ţ�

```
python -c "import django; print(django.get_version())"
```

��Ӧ�ÿ����㰲װ�� Django �汾��һ����ʾ�� ��No module named django�� �Ĵ��󡣴��⣬��Ӧ�ü������İ汾�뱾�̵̳İ汾�Ƿ�һ�¡� ����һ�£�����Բο� Django �汾��Ӧ�Ľ̳̻��߸��� Django �����°汾��

��ο� ��ΰ�װ Django �е������ɾ���ɰ汾�� Django �ٰ�װһ���µġ�

> ��������Ի�ð�����
> 
> �������ѧϰ���̳����������⣬���� django-users �Ϸ��������� #django on irc.freenode.net �����������ܻ�������� Django �û�������

## ����һ����Ŀ ##

����������һ��ʹ�� Django ����ô��������һЩ��ʼ���á�Ҳ����ͨ���Զ����ɴ���������һ�� Django ��Ŀ project �C һ�� Django ��Ŀ�����ü������������ݿ����á� Django ��ϸѡ�����ú�Ӧ���������á�

���������У�ʹ�� cd �����������洢�������ڵ�Ŀ¼��Ȼ�������������

```
django-admin.py startproject mysite
```

�⽫�ڵ�ǰĿ¼����һ�� mysite Ŀ¼�����ʧ���ˣ���鿴 Problems running django-admin.py.

> Note
> 
> ����Ҫ����ʹ�� python �����ֻ� Django �������Ϊ��Ŀ�����ơ���������Ӧ�ñ���ʹ�õ������磺 django (�� Django ������ͻ) ���� test (�� Python ���õİ������ͻ).

> ��δ���Ӧ�÷������
> 
> �������һ�� PHP �ı�̱�����δʹ�����еĿ�ܣ������ܻὫ��Ĵ������ Web ���������ĵ���Ŀ¼�£����磺``/var/www``�������� Django �У��㲻����ô�������κ� Python ���������� Web �������ĵ���Ŀ¼������һ�������⣬��Ϊ����ܻ���������ͨ�� Web ��ʽ�鿴����Ĵ���ķ��ա��ⲻ���ڰ�ȫ��

����Ĵ����������ĵ���Ŀ¼ ���� ��ĳЩĿ¼, ���� /home/mycode ��

������������ startproject ��������Щʲô:

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

> ���㿴���Ĳ�һ����
> 
> Ĭ�ϵ���Ŀ��������ոոı��������㿴������һ������ƽ���ṹ��Ŀ¼���֣�û���ڲ� mysite/ Ŀ¼������ܿ�������ʹ��һ���ͱ��̳̰汾��һ�µ� Django �汾������Ҫ�л�����Ӧ�ľɰ�̳̻���ʹ�ý��µ� Django �汾��

��Щ�ļ��ǣ�

+ ��� mysite/ Ŀ¼ֻ������Ŀ��һ������������ Django ��˵��Ŀ¼��������Ҫ; �����������Ϊ��ϲ���ġ�
+ manage.py: һ��ʵ�õ������й��ߣ��������Ը��ַ�ʽ��� Django ��Ŀ���н����� ������� django-admin.py and manage.py �в鿴���� manage.py ���е�ϸ�ڡ�
+ �ڲ� mysite/ Ŀ¼������Ŀ�е�ʵ�� Python ������Ŀ¼������ Python ������ͨ��������Ե�����������κζ����� (e.g. import mysite.settings).
+ mysite/__init__.py: һ�����ļ������� Python ��Ŀ¼��һ�� Python ����(������� Python ���֣���鿴�ٷ��ĵ��˽� ���ڰ��ĸ������� ��)
+ mysite/settings.py: �� Django ��Ŀ������/���á���鿴 Django settings ���������������á�
+ mysite/urls.py: �� Django ��Ŀ�� URL ����; һ���� Django ��������վ��Ŀ¼������鿴 URL dispatcher ���Ի�ȡ�����й� URL ����Ϣ��
+ mysite/wsgi.py: һ�� WSGI ���ݵ� Web ����������ڣ��Ա����������Ŀ����鿴 How to deploy with WSGI ��ȡ����ϸ�ڡ�

## �����÷����� ##

����������֤�Ƿ���������� mysite Ŀ¼�л���ȥ����׼�����˾��������� ``python manage.py runserver``���㽫�ῴ������������������ݣ�

```
Validating models...

0 errors found
December 02, 2013 - 15:50:53
Django version 1.5, using settings 'mysite.settings'
Development server is running at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

���Ѿ������� Django ������������һ��������� Python ��д�������� Web �������������� Django �ڰ����������������������Ϳ���Ѹ�ٿ����ˣ��ڲ�ƷͶ��ʹ��֮ǰ����ȥ����һ̨���������µķ����� �C ���� Apache ��

������һ���ܺõ���ʾʱ����**��Ҫ** ���κ���������������ʹ�ô˷����������������ڿ���������(�����ṩ���� Web ��ܵ�ҵ�񣬶����� Web ��������)

���ڷ��������������У�������� Web ������з��� http://127.0.0.1:8000/ �� ��ῴ��һ���������õģ���͵ĵ���ɫ ��Welcome to Django�� ҳ�档������������

> ���Ķ˿ں�
> 
> Ĭ������£�runserver ���������Ŀ���������ֻ�������� IP �� 8000 �˿ڡ�
> 
> �������ı�������Ķ˿ڣ�������Ϊһ�������в������ݼ��ɡ������������������ķ����������� 8080 �˿ڣ�
> 
```
python manage.py runserver 8080
```
> 
> �������ı������ IP �������Ͷ˿ں�һ�𴫵ݼ��ɡ���ˣ�Ҫ�������й��� IP ��ַ�����������������������ҫ��Ĺ���������ʹ�ã�
> 
```
python manage.py runserver 0.0.0.0:8000
```
> �йؿ����������������ĵ������� runserver �ڲο���

## ���ݿ����� ##

���ڣ��༭ mysite/settings.py �� ����һ����ͨ�� Python ģ�飬�����˴��� Django ���õ�ģ�鼶������ ���� DATABASES �� 'default' �µ����¼���ֵ����ƥ���������ݿ��������á�

+ ENGINE �C �� 'django.db.backends.postgresql_psycopg2', 'django.db.backends.mysql', 'django.db.backends.sqlite3', 'django.db.backends.oracle' ��ѡһ���� ����������鿴 also available.
+ NAME �C ������ݿ����������ʹ�� SQLite�������ݿ⽫���������ϵ�һ���ļ�������������£�NAME ����һ�������ľ���·�������һ��������ļ������ơ�������ļ������ڣ������ڵ�һ��ͬ�����ݿ�ʱ�Զ������������ģ���

��ָ��·��ʱ������ʹ����б�ܣ���ʹ���� Windows ��(���磺``C:/homes/user/mysite/sqlite3.db``) ��

+ USER �C ������ݿ��û��� ( SQLite �²���Ҫ) ��
+ PASSWORD �C ������ݿ����� ( SQLite �²���Ҫ) ��
+ HOST �C ������ݿ�������ַ�������������ݿ��������ͬһ̨����������뽫�˴�����Ϊ�� (��������Ϊ 127.0.0.1) ( SQLite �²���Ҫ) ���鿴 HOST �˽���ϸ��Ϣ��

��������½����ݿ⣬���ǽ���ֻʹ�� SQLite ���� ENGINE ��Ϊ 'django.db.backends.sqlite3' ���ҽ� NAME ����Ϊ���������ݿ�ĵط��� SQLite �������� Python �еģ�����㲻��Ҫ��װ�κζ�����֧��������ݿ⡣

> Note
> 
> �����ʹ�� PostgreSQL ���� MySQL��ȷ�����Ѿ�������һ�����ݿ⡣����ͨ��������ݿ⽻���ӿ��е� ��CREATE DATABASE database_name;�� ����������һ��ġ�
> �����ʹ�� SQLite ���㲻��Ҫ���ȴ����κζ��� - ����Ҫ��ʱ�򣬽����Զ��������ݿ��ļ���
����༭ settings.py ʱ���� TIME_ZONE �޸�Ϊ�����ڵ�ʱ����Ĭ��ֵ����������ʱ����֥�Ӹ磩��

ͬʱ��ע���ļ��ײ��� INSTALLED_APPS ���á��������˵�ǰ Django ʵ���Ѽ�������� Django Ӧ�á�ÿ��Ӧ�ÿ��Ա������Ŀʹ�ã���������Դ���ͷַ��������������ǵ���Ŀ��ʹ�á�

Ĭ������£�INSTALLED_APPS ��������Ӧ�ã���Щ������ Django �ṩ�ģ�

+ django.contrib.auth �C �����֤ϵͳ��
+ django.contrib.contenttypes �C �������Ϳ�ܡ�
+ django.contrib.sessions �C session ��ܡ�
+ django.contrib.sites �C ��վ�����ܡ�
+ django.contrib.messages �C ��Ϣ��ܡ�
+ django.contrib.staticfiles �C ��̬�ļ������ܡ�

��ЩӦ����һ���������Ĭ�ϰ����ġ�

������ЩӦ����ÿ��Ӧ������ʹ��һ�����ݿ��������ʹ������֮ǰ������Ҫ�������ݿ��еı�Ҫ������һ�㣬�������������

```
python manage.py syncdb
```

syncdb ������� INSTALLED_APPS ���ã�������� settings.py �ļ������õ����ݿ��д�����Ҫ�����ݿ��ÿ����һ�����ݿ���㶼�ῴ��һ����Ϣ��������ῴ��һ����ʾѯ�����Ƿ���Ҫ�������֤ϵͳ�ڴ����������û�������ʾ����������

��������Ȥ��������������ݿ������������룺``dt`` (PostgreSQL), SHOW TABLES; (MySQL), �� .schema (SQLite) ���г� Django �������ı�

> ����������
> 
> ��������������˵�ģ�һ�����������Ӧ�ö�Ĭ�ϰ������ڣ�������ÿ���˶���Ҫ���ǡ��������ҪĳЩ��ȫ��Ӧ�ã������� syncdb ����ǰ�ɴ� INSTALLED_APPS ������ע�ͻ�ɾ����Ӧ���С�syncdb ����ֻ��Ϊ INSTALLED_APPS �ڵ�Ӧ�ô�����

## ����ģ�� ##

���������Ŀ���������������ˣ� ����Կ����ˡ�

��ͨ�� Djaong ��д��ÿ��Ӧ�ö����� Python ����ɵģ���Щ���������� Python path �в�����ѭһ���������淶�� Django �ṩ�˸�ʵ�ù��߿����Զ�����һ��Ӧ�õĻ���Ŀ¼�ܹ�����������רע�ڱ�д���������ȥ����Ŀ¼��

> ��Ŀ ( Projects ) vs. Ӧ�� ( apps )
> 
> ��Ŀ��Ӧ��֮����ʲô��֮ͬ����Ӧ����һ���ṩ���ܵ� Web Ӧ�� �C ���磺һ������ϵͳ��һ��������¼�����ݿ����һ���򵥵�ͶƱϵͳ�� ��Ŀ�����һ���ض��� Web ��վ��ص����ú���Ӧ�õ���ϡ�һ����Ŀ���԰������Ӧ�á�һ��Ӧ�ÿ����ڶ����Ŀ��ʹ�á�

���Ӧ�ÿ��Դ���� Python path �е��κ�λ�á��ڱ��̲��У����ǽ�ͨ����� manage.py �ļ��������ǵ�ͶƱӦ�ã��Ա���������Ϊ����ģ�鵼�룬��������Ϊ mysite ����ģ�顣

Ҫ�������Ӧ�ã���ȷ���� manage.py �ļ���ͬһ��Ŀ¼�²������������

```
python manage.py startapp polls
```

�⽫����һ�� polls Ŀ¼����չ��������������ʾ��:

```
polls/
    __init__.py
    models.py
    tests.py
    views.py
```

��Ŀ¼�ṹ����ͶƱӦ�á�

�� Django �б�дһ�������ݿ�֧�ֵ� Web Ӧ�õĵ�һ�����Ƕ������ģ�� �C �ӱ����Ͻ��������ݿ���Ƽ��丽�ӵ�Ԫ���ݡ�

> ����
> 
> ģ�����й������ݵ�Ψһ����ȷ������Դ��������������Ҫ�洢�����ݵĻ����ֶκ���Ϊ�� Django ��ѭ DRY ԭ�� ��Ŀ����Ϊ��ֻ��һ���ط������������ģ�;Ϳɴ����Զ���ȡ���ݡ�

����򵥵�ͶƱӦ���У����ǽ���������ģ�ͣ� Poll �� Choice``��``Poll ������ͷ������������ֶΡ�``Choice`` �������ֶΣ� ѡ�� ( choice ) ���ı����ݺ�ͶƱ����ÿһ�� Choice ����һ�� Poll ������

��Щ����ɼ򵥵� Python �������֡��༭ polls/models.py �ļ���������ʾ��

```
from django.db import models

class Poll(models.Model):
    question = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

class Choice(models.Model):
    poll = models.ForeignKey(Poll)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

����ܼ򵥡�ÿ��ģ�Ͷ��ɼ̳��� django.db.models.Model ��������������� ÿ��ģ�Ͷ���һЩ�������ÿһ���������������һ�����ݿ��ֶΡ�

ÿ���ֶ���һ�� Field ��ʵ�������� �C ���� CharField ��ʾ�ַ����͵��ֶκ� DateTimeField ��ʾ����ʱ���͵��ֶΡ������� Django ÿ���ֶζ�������ʲô���͵����ݡ�

ÿһ�� Field ʵ�������־����ֶε����֣��磺 question ���� pub_date �������ʽ�����׺ͻ���ʽ�ġ������ Python �Ĵ����л�ʹ�����ֵ����������ݿ�Ὣ���ֵ��Ϊ���������

������ڳ�ʼ�� Field ʵ��ʱʹ�õ�һ��λ�õĿ�ѡ������ָ������ɶ������֡�����Django����ʡ�����б�ʹ�õ��ˣ����Ҽ����ĵ���һ��������ǿ����Ŀɶ��ԡ����ֶ�δ�ṩ�ò�����Django ��ʹ�÷��ϻ���ϰ�ߵ����֡��ڱ����У����ǽ�������һ����������ϰ�ߵ��ֶ��� Poll.pub_date ������ģ���е������ֶΣ��������ƾ��Ѿ��㹻������������ˡ�

һЩ Field ʵ������Ҫ�����ġ� ���� CharField ��Ҫ��ָ�� `~django.db.models.CharField.max_length`���ⲻ�����������ݿ�ṹ���Ժ����ǻ��ῴ��Ҳ����������֤�С�

һ�� Field ʵ�������в�ͬ�Ŀ�ѡ������ �ڱ����У����ǽ� votes �� default ��ֵ��Ϊ 0 ��

���ע������ʹ���� ForeignKey ������һ�������������� Django ÿһ��``Choice`` ����һ�� Poll �� Django ֧�ֳ������ݿ�����й��������һ�� many-to-ones ������Զࣨ many-to-manys �� �� һ��һ �� one-to-ones ����

## ����ģ�� ##

�ղ��ǵ�ģ�ʹ����ṩ�� Django ������Ϣ��������Щ Django �Ϳ�������

Ϊ��Ӧ�ô�����Ӧ�����ݿ�ܹ� (CREATE TABLE statements) ��
Ϊ Poll �� Choice ���󴴽� Python �������ݿ�� API ��
�����ȣ�������Ҫ�������ǵ���Ŀ�Ѿ���װ�� polls Ӧ�á�

> ����
> 
> Django Ӧ���ǡ��ɲ�εġ���������ڶ����Ŀʹ��һ��Ӧ�ã��㻹���Էַ�Ӧ�ã���Ϊ����û�б�����һ�������� Django ��װ�����С�

�ٴα༭ settings.py �ļ����� INSTALLED_APPS �����м��� 'polls' �ַ�����˽��������ʾ��

```
INSTALLED_APPS = (
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.sites',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Uncomment the next line to enable the admin:
    # 'django.contrib.admin',
    # Uncomment the next line to enable admin documentation:
    # 'django.contrib.admindocs',
    'polls',
)
```

���� Django �Ѿ�֪�������� polls Ӧ�á������������������

```
python manage.py sql polls
```

�㽫��������������ʾ���� ( �й�ͶƱӦ�õ� CREATE TABLE SQL ��� )��

```
BEGIN;
CREATE TABLE "polls_poll" (
    "id" serial NOT NULL PRIMARY KEY,
    "question" varchar(200) NOT NULL,
    "pub_date" timestamp with time zone NOT NULL
);
CREATE TABLE "polls_choice" (
    "id" serial NOT NULL PRIMARY KEY,
    "poll_id" integer NOT NULL REFERENCES "polls_poll" ("id") DEFERRABLE INITIALLY DEFERRED,
    "choice_text" varchar(200) NOT NULL,
    "votes" integer NOT NULL
);
COMMIT;
```

��ע���������

+ ȷ�е�������ݽ�ȡ������ʹ�õ����ݿ��������ͬ��
+ �������Զ����ɵģ�ͨ�����Ӧ���� (polls) ��Сд��ģ���� �C poll �� choice �� ( �������д����Ϊ��)
+ ���� (IDs) ���Զ���ӵġ�( ��Ҳ������д����Ϊ��)
+ ���չ�����Django ��������ֶ����ϸ��� "_id" �� ( �ǵģ�����Ȼ������д����Ϊ��)
+ �����ϵ�� REFERENCES �����ʾ������
+ ���� SQL ���ʱ�������ʹ�õ����ݿ⣬��Ϊ���Զ������ض������ݿ���ֶΣ����� auto_increment (MySQL), serial (PostgreSQL), �� or integer primary key (SQLite) �� �������ֶ���ʱҲ����� �C ����ʹ��˫���Ż����š� ���̲ĵ�������ʹ�õ��� PostgreSQL������������������ PostgreSQL ���﷨��
+ ��Щ sql ������ʵ��û����������ݿ������й� - ��ֻ������Ļ����ʾ�������Ա������˽� Django ��Ϊʲô���� SQL �Ǳ���ġ� �����Ը�⣬���԰� SQL ���Ʋ�ճ����������ݿ���������ȥִ�С� ���ǣ����Ǻܿ���ܿ����� Django �ṩ��һ�����򵥵ķ�����ִ�д� SQL ��

��������Ȥ�������������������

+ python manage.py validate �C ����ڹ������ģ��ʱ�Ƿ��д���
+ python manage.py sqlcustom polls �C ���ΪӦ�ö�����κ� custom SQL statements ( ������Լ�����޸� ) ��
+ python manage.py sqlclear polls �C ���ݴ�����������ݿ��еı� (����еĻ�) ��ΪӦ�������Ҫ�� DROP TABLE ��
+ python manage.py sqlindexes polls �C ΪӦ����� CREATE INDEX ��䡣
+ python manage.py sqlall polls �C ������� SQL ��䣺sql, sqlcustom, �� sqlindexes ��

������Щ�����������԰���������ܵײ�ʵ���ϴ�����Щʲô��

���ڣ��ٴ����� syncdb ������������ݿ��д�����Щģ�Ͷ�Ӧ�ı�

```
python manage.py syncdb
```

syncdb �������� INSTALLED_APPS ���е����ݿ���û�ж�Ӧ���Ӧ��ִ�� sqlall ������ �ò�����Ϊ����һ��ִ�� syncdb ������������Ŀ����ӵ��κ�Ӧ�ô�����Ӧ�ı���ʼ�����ݺʹ��������� syncdb ����ֻҪ��ϲ���Ϳ���������ã����������ᴴ�������ڵı�

���Ķ� django-admin.py documentation �ĵ��˽� manage.py ���߸���Ĺ��ܡ�

## ��ת API ##

���ڣ����ǽ��� Python �Ľ���ʽ shell ����Ū Django �ṩ����� API ��Ҫ���� Python sell ��ʹ���������

```
python manage.py shell
```

���ǵ�ǰʹ�õĻ�����ͬ�ڼ򵥵����� ��python�� ����� shell ��������Ϊ manage.py ������ DJANGO_SETTINGS_MODULE �����������ñ��������� Django ��Ҫ����� settings.py �ļ�����·����

> ���� manage.py
> 
> ���㲻��ʹ�� manage.py ��Ҳ��û������ġ� ����Ҫ�� DJANGO_SETTINGS_MODULE ��������ֵ��Ϊ mysite.settings ������ manage.py �ļ�����ͬһĿ¼������ python �� ��ȷ��Ŀ¼�� Python path �£��� import mysite �Ϳ����� ����
> 
> ���˽�������Ϣ����ο� django-admin.py �ĵ� ��

һ��������� shell���Ϳ�ͨ�� database API ��������ݣ�:

```
>>> from polls.models import Poll, Choice   # Import the model classes we just wrote.

#  ϵͳ�л�û�� polls ��
>>> Poll.objects.all()
[]

# ����һ���� Poll ��
# ��Ĭ�������ļ���ʱ��֧�����������õģ�
# ��� Django ϣ��Ϊ pub_date �ֶλ�ȡһ�� datetime  with tzinfo ��ʹ���� timezone.now()
# ������ datetime.datetime.now() �Ա��ȡ��ȷ��ֵ��
>>> from django.utils import timezone
>>> p = Poll(question="What's new?", pub_date=timezone.now())

# ����������ݿ��С��������ʾ���� save() ������
>>> p.save()

# ���ڶ���ӵ����һ��ID ����ע������ܻ���ʾ "1L" ������ "1"��ȡ����
# ������ʹ�õ����ݿ⡣ ��ûʲô���˵ģ���ֻ����ζ��������ݿ���
# ϲ�����ص���������Ϊ Python �ĳ����Ͷ�����ѡ�
>>> p.id
1

# ͨ�� Python ���Է������ݿ��е��С�
>>> p.question
"What's new?"
>>> p.pub_date
datetime.datetime(2012, 2, 26, 13, 0, 0, 775217, tzinfo=<UTC>)

# ͨ����Ϊ����ֵ���ı�ֵ��Ȼ����� save() ������
>>> p.question = "What's up?"
>>> p.save()

# objects.all() ������ʾ���ݿ������е� polls ��
>>> Poll.objects.all()
[<Poll: Poll object>]
```

���Եȡ�``<Poll: Poll object>`` ������ʾ���������������ġ� �����Ǳ༭ polls ģ�ͣ� �� polls/models.py �ļ��� �� ���Ҹ� Poll �� Choice �����һ�� __unicode__() �����������˴���

```
class Poll(models.Model):
    # ...
    def __unicode__(self):
        return self.question

class Choice(models.Model):
    # ...
    def __unicode__(self):
        return self.choice_text
```

�����ģ����� __unicode__() �����Ǻ���Ҫ�ģ� ������������������������ȷ��ʾ�������� Django �Զ����ɵĹ��������Ҳ��ʹ�õ�����ĳ��֡�

> Ϊʲô�� __unicode__() ������ __str__()?
> 
> �������Ϥ Python����ô����ܻ�ϰ����������� __str__() ���������� __unicode__() ������ We use ����������ʹ�� __unicode__() ����Ϊ Django ģ��Ĭ�ϴ������ Unicode ��ʽ�������д洢�����ݿ��е����ݷ���ʱ����ת��Ϊ Unicode �ĸ�ʽ��
> 
> Django ģ���и�Ĭ�ϵ� __str__() ���� ��ȥ���� __unicode__() �������ת��Ϊ UTF-8 ������ַ����������ζ�� unicode(p) �᷵��һ�� Unicode �ַ������� str(p) �᷵��һ���� UTF-8 �������ͨ�ַ�����
> 
> ���������о�������ô��ֻҪ��ס��ģ������� __unicode__() ������ �����õĻ�����Щ������������С�

��ע����Щ������ͨ�� Python ����������������Ӹ��Զ��巽����Ϊ����ʾ���ѣ�

```
import datetime
from django.utils import timezone
# ...
class Poll(models.Model):
    # ...
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```

��ע�⣬������ import datetime �� from django.utils import timezone, ��Ϊ�˷ֱ����� Python �ı�׼�� datetime ģ��� Django �� django.utils.timezone �е� time-zone-related ʵ�ù��� ������㲻��Ϥ�� Python �д���ʱ����������� ʱ��֧���ĵ� ѧ�����ࡣ

������Щ���Ĳ����ٴ����� python manage.py shell �Կ���һ���µ� Python shell:

```
>>> from polls.models import Poll, Choice

# ȷ�����Ǹ��ӵ�  __unicode__() �������С�
>>> Poll.objects.all()
[<Poll: What's up?>]

# Django �ṩ��һ���ḻ�����ݿ��ѯ API ��
# ��ȫ�ɹؼ��ֲ�����������
>>> Poll.objects.filter(id=1)
[<Poll: What's up?>]
>>> Poll.objects.filter(question__startswith='What')
[<Poll: What's up?>]

# ��ȡ���귢���ͶƱ��
>>> from django.utils import timezone
>>> current_year = timezone.now().year
>>> Poll.objects.get(pub_date__year=current_year)
<Poll: What's up?>

# ����һ�������ڵ� ID ���⽫����һ���쳣��
>>> Poll.objects.get(id=2)
Traceback (most recent call last):
    ...
DoesNotExist: Poll matching query does not exist. Lookup parameters were {'id': 2}

# ����������ѯ�ǳ������������� Django �ṩ��һ��
# ������ȷ���ҵĿ�ݷ�ʽ��
# ���´����ͬ�� Poll.objects.get(id=1).
>>> Poll.objects.get(pk=1)
<Poll: What's up?>

# ȷ�������Զ��巽���������С�
>>> p = Poll.objects.get(pk=1)
>>> p.was_published_recently()
True

# �� Poll ����һЩ Choices ��ͨ�� create �������ù��췽��ȥ����һ����
# Choice ����ʵ����ִ�� INSERT ������Ӹ� choice ��
# ���õ� choices ���в���������½��� Choice ����ʵ���� Django ������
# һ���������������ϵ�ļ��� ( ���� poll �� choices) �Ա����ͨ�� API
# ȥ���ʡ�
>>> p = Poll.objects.get(pk=1)

# �ӹ�����������ʾ���� choices  -- ��ĿǰΪֹ��û�С�
>>> p.choice_set.all()
[]

# �������� choices ��
>>> p.choice_set.create(choice_text='Not much', votes=0)
<Choice: Not much>
>>> p.choice_set.create(choice_text='The sky', votes=0)
<Choice: The sky>
>>> c = p.choice_set.create(choice_text='Just hacking again', votes=0)

# Choice ����ӵ�з������ǹ����� Poll ����� API ��
>>> c.poll
<Poll: What's up?>

# ��֮��Ȼ�� Poll ����Ҳ�ɷ��� Choice ����
>>> p.choice_set.all()
[<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]
>>> p.choice_set.count()
3

# ֻҪ����Ҫ API ���Զ�����������
# ʹ��˫�»��������������
# ֻҪ����Ҫ��������Ϳ����м��������û�����ơ�
# Ѱ�Һͽ��귢����κ� poll �йص����� Choices
# ( �������������潨���� 'current_year' ���� )��
>>> Choice.objects.filter(poll__pub_date__year=current_year)
[<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]

# ������ʹ�� delete() ɾ�� choices �е�һ����
>>> c = p.choice_set.filter(choice_text__startswith='Just hacking')
>>> c.delete()
```

���˽�����й�ģ�͹�ϵ����Ϣ����鿴 ���ʹ������� �����˽�����й����ʹ��˫�»�����ͨ�� API ִ���ֶβ�ѯ�ģ���鿴 �ֶβ�ѯ �� �������������ݿ� API ��Ϣ����鿴���ǵ� ���ݿ� API �ο� ��

����� API �����˽��, ��鿴 �̳� ��2���� ��ѧϰ Django ���Զ����ɵĹ�����վ����ι����ġ�