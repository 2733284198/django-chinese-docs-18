<!--
  ��Դ��http://django-chinese-docs.readthedocs.org/
-->

# ��̽ Django #

��Դ��[django-chinese-docs.readthedocs.org](http://django-chinese-docs.readthedocs.org/)

����Django����һ�����������ű༭�һ����¿��������ģ����������Ƴ�����ͨ����վ���������򵥶��� �ݡ����¼򵥽���������� Django ��дһ�����ݿ�������WebӦ�ó���

���ĵ���Ŀ���Ǹ��������㹻�ļ���ϸ�����������Django����ι����ģ�������������ʾ��һ������ָ�ϻ�ο�Ŀ¼ �C ��ʵ��Щ���Ƕ���! ����׼���½�һ����Ŀ������� *������ָ�Ͽ�ʼ* ���� *�����Ķ���ϸ���ĵ�*.

## ������ģ��(model) ##

�������� Django �п��Բ�ʹ�����ݿ⣬�������ṩ��һ�����ƵĿ����� Python ��������������ݿ�ṹ�Ķ������ӳ��(ORM)��

*����ģ���﷨* �ṩ�����ḻ�ķ�����չ�����ģ�� �C ��ĿǰΪֹ�����Ѿ������������������������ݿ�ܹ����⡣�����Ǹ��򵥵����ӣ����ܱ�����Ϊ mysite/news/models.py:

```
class Reporter(models.Model):
    full_name = models.CharField(max_length=70)

    def __unicode__(self):
        return self.full_name

class Article(models.Model):
    pub_date = models.DateField()
    headline = models.CharField(max_length=200)
    content = models.TextField()
    reporter = models.ForeignKey(Reporter)

    def __unicode__(self):
        return self.headline
```

## ��װ�� ##

��һ�������� Django �����й������Զ��������ݿ��

```
manage.py syncdb
```

syncdb �������������п��õ�ģ��(models)Ȼ����������ݿ��д����������ڵ����ݿ��

## ���ñ�ݵ� API ##

���ţ���Ϳ���ʹ��һ������ҹ��ܷḻ�� *Python API* ������������ݡ�API �Ƕ�̬���ɵģ�����Ҫ��������:

```
# ���������� "news "Ӧ���д�����ģ�͡�
>>> from news.models import Reporter, Article

# ��ϵͳ�л�û�� reporters ��
>>> Reporter.objects.all()
[]

# ����һ���µ� Reporter ��
>>> r = Reporter(full_name='John Smith')

# �����󱣴浽���ݿ⡣����Ҫ��ʾ�ĵ��� save() ������
>>> r.save()

# ������ӵ����һ��ID��
>>> r.id
1

# �����µ� reporter �Ѿ��������ݿ����ˡ�
>>> Reporter.objects.all()
[<Reporter: John Smith>]

# �ֶα���ʾΪһ�� Python ��������ԡ�
>>> r.full_name
'John Smith'

# Django �ṩ�˷ḻ�����ݿ��ѯ API��
>>> Reporter.objects.get(id=1)
<Reporter: John Smith>
>>> Reporter.objects.get(full_name__startswith='John')
<Reporter: John Smith>
>>> Reporter.objects.get(full_name__contains='mith')
<Reporter: John Smith>
>>> Reporter.objects.get(id=2)
Traceback (most recent call last):
    ...
DoesNotExist: Reporter matching query does not exist. Lookup parameters were {'id': 2}

# ����һ�� article.
>>> from datetime import date
>>> a = Article(pub_date=date.today(), headline='Django is cool',
...     content='Yeah.', reporter=r)
>>> a.save()

# ���� article �Ѿ��������ݿ����ˡ�
>>> Article.objects.all()
[<Article: Django is cool>]

# Article ������ API ���Է��ʵ������� Reporter ����
>>> r = a.reporter
>>> r.full_name
'John Smith'

# ��֮��Ȼ��Reporter ����Ҳ�з��� Article �����API��
>>> r.article_set.all()
[<Article: Django is cool>]

# API ����Ļ���Ч�Ĺ�������������Ĺ�����ѯ������
# �����������ҳ����ֿ�ͷΪ "John" �� reporter ������ articles ��
>>> Article.objects.filter(reporter__full_name__startswith="John")
[<Article: Django is cool>]

# ͨ������һ�����������ֵ��Ȼ���ٵ��� save() �������ı�����
>>> r.full_name = 'Billy Goat'
>>> r.save()

# ���� delete() ������ɾ��һ������
>>> r.delete()
```

## һ����̬�Ĺ���ӿڣ����������Ǹ����ּ� �C ���Ǹ������ķ��� ##

һ����� models ������ã�Django ���Զ�����һ��רҵ�ģ������������������� *�������* �C һ��������Ȩ�û���ӣ��޸ĺ�ɾ���������վ����ʹ�������ǳ���ֻ������� admin site ��ע�����ģ�ͼ��ɡ�:

```
# In models.py...

from django.db import models

class Article(models.Model):
    pub_date = models.DateField()
    headline = models.CharField(max_length=200)
    content = models.TextField()
    reporter = models.ForeignKey(Reporter)


# In admin.py in the same directory...

import models
from django.contrib import admin

admin.site.register(models.Article)
```

������������������վһ������һ��Ա��,���߿ͻ������߽��������Լ�ȥ�༭ �C ����Ӧ�ò�����Ҫ����Ϊ�˹������ݶ�ȥ������̨���档

��һ������ Django Ӧ�õĵ��͹������У�������Ҫ����ģ�Ͳ������ܿ������������ admin sites�� ������Ա��(���߿ͻ�)�ܹ���ʼ¼�����ݡ�Ȼ��,�ſ���չ�����ݸ����ڵķ�ʽ��

## ������ URLs ##

һ���ɾ��ģ����ŵ� URL ������һ�������� Web Ӧ�ó������Ҫϸ�ڡ� Django ����ʹ��Ư���� URL ��ƣ����Ҳ�������û��Ҫ�Ķ����ŵ� URLs ���棬�� .php �� .asp.

Ϊ�˸�һ�� app ��� URLs������Ҫ����һ�� Python ģ����� [URLconf](/topics/http/urls)������һ����� app ����Ŀ¼�� ������һ���򵥵� URL ƥ��ģʽ�� Python �ص��������ӳ���ϵ���������ڽ��� Python ����� URLs ��

����������� Reporter/Article ���������õ� URLconf �������:

```
from django.conf.urls import patterns

urlpatterns = patterns('',
    (r'^articles/(\d{4})/$', 'news.views.year_archive'),
    (r'^articles/(\d{4})/(\d{2})/$', 'news.views.month_archive'),
    (r'^articles/(\d{4})/(\d{2})/(\d+)/$', 'news.views.article_detail'),
)
```

����Ĵ���ӳ���� URLs ����һ���򵥵�������ʽ���� Python �ص�����(��views��)���ڵ�λ�á� ������ʽͨ��Բ������������ URLs �е�ֵ����һ���û�����һ��ҳ��ʱ�� Django ������˳��ȥƥ��ÿһ��ģʽ����ͣ�ڵ�һ��ƥ������� URL �ϡ�(���û��ƥ�䵽�� Django ����չʾһ��404�Ĵ���ҳ�档) ���������Ǽ���ģ���Ϊ�ڼ���ʱ������ʽ�ͽ����˱��롣

һ����һ��������ʽƥ�����ˣ�Django ������͵��ö�Ӧ����ͼ������ʵ����һ���򵥵� Python ������ÿ����ͼ���õ�һ�� request ���� �C �������� request �� meta ��Ϣ �C ��������ʽ�����񵽵�ֵ��

���磺���һ���û������˸� URL ��/articles/2005/05/39323/��, Django �����������ú��� news.views.article_detail(request, '2005', '05', '39323').

## ��д�����ͼ(views) ##

ÿ����ͼֻ�����������е�һ��������һ����������ҳ�����ݵ� HttpResponse ����; ���׳�һ���쳣�� Http404 �����������Ϳ����ˡ�

ͨ����һ����ͼ����ݲ������������ݣ�����һ��ģ�岢�Ҹ��ݸ�ģ�������ּ������������ݡ� �����Ǹ��������� year_archive ����

```
def year_archive(request, year):
    a_list = Article.objects.filter(pub_date__year=year)
    return render_to_response('news/year_archive.html', {'year': year, 'article_list': a_list})
```

�������ʹ���� Django �� [ģ��ϵͳ](/topics/templates)����ģ��ϵͳ����ǿ���Ҽ����ã������Ǳ����ԱҲ��ʹ�á�

������ģ��(templates)

����������������� news/year_archive.html ģ�塣

Django ��һ��ģ������·���壬�����㾡���ܵļ���������ظ�����ģ�塣����� Django�����У������ָ��һ������ģ���Ŀ¼�б����һ��ģ��û������� �б��У���ô����ȥ���ҵڶ�����Ȼ���Դ����ơ�

�����ҵ���ģ�� news/year_archive.html ������������ŵ�����:

```
{% extends "base.html" %}

{% block title %}Articles for {{ year }}{% endblock %}

{% block content %}
<h1>Articles for {{ year }}</h1>

{% for article in article_list %}
    <p>{{ article.headline }}</p>
    <p>By {{ article.reporter.full_name }}</p>
    <p>Published {{ article.pub_date|date:"F j, Y" }}</p>
{% endfor %}
{% endblock %}
```
����ʹ��˫�����Ű�Χ��``{{ article.headline }}`` ��ʾ ����� article �� headline ���ԡ���������Ų������ڱ�ʾ���Բ��ң����������ֵ�ļ�ֵ���ҡ��������Һͺ������á�

ע�� {{ article.pub_date|date:"F j, Y" }} ʹ���� Unix ���ġ��ܵ���(��|������)���������ν��ģ���������һ��ͨ������������ֵ�ķ�ʽ�������У�Python datetime ���󱻹��˳�ָ���ĸ�ʽ(�� PHP �����ں����п��Լ������ֱ任)��

����������Ƶش���ʹ�ö��������������Ա�д�Զ���Ĺ�����������Զ����� ����ģ���ǣ���Ļ�������Զ���� Python ���롣

���Django ʹ���ˡ�ģ��̳С��ĸ������� {% extends "base.html" %} �������¡�����ζ�� ������������Ϊ ��base�� ��ģ���е����ݵ���ǰģ�壬Ȼ���ٴ���ģ���е��������ݡ�����֮��ģ��̳�������ģ���������������ݣ�ÿһ��ģ��ֻ��Ҫ���������صĲ��ּ��ɡ�

������ʹ���� *��̬�ļ�* �� ��base.html�� ģ��Ĵ������:

```
{% load staticfiles %}
<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>
    <img src="{% static "images/sitelogo.png" %}" alt="Logo" />
    {% block content %}{% endblock %}
</body>
</html>
```

�򵥵�˵������������վ����ۣ�����վ�� logo �����������˸�����������ģ������䡣��ʹվ���������Ʊ�÷ǳ����ף�ֻ��ı�һ���ļ� �C ��base.html�� ģ�塣

��Ҳ�������㴴��һ����վ�Ķ���汾����ͬ�Ļ���ģ�壬��������ģ�塣 Django �Ĵ������Ѿ�������һ������������������ͬ���ֻ��汾����վ �C ֻ�贴��һ���µĻ���ģ�塣

��ע�⣬�����ϲ������ģ��ϵͳ����ô����Բ�ʹ�� Django ��ģ��ϵͳ�� ��Ȼ Django ��ģ��ϵͳ�ر𼯳��� Django ��ģ�Ͳ㣬����û��ǿ����ʹ������ͬ����Ҳ���Բ�ʹ�� Django �����ݿ� API��������ʹ���������ݿ����㣬�����Զ�ȡ XML �ļ�������ԴӴ����ж�ȡ�ļ������κ�����Ҫ�ķ���ȥ�������ݡ� Django ��ÿ����ɲ��֣� ģ�͡���ͼ��ģ�嶼���Խ���Ժ��̸����

## �������һ��Ƥë ##

����ֻ�Ǽ�Ҫ������ Django �Ĺ��ܡ�������һЩ�����õĹ��ܣ�

һ�� *������* ������ memcached ��������˻��漯�ɡ�
һ�� *�ۺϿ��* �����ô��� RSS �� Atom �� feeds ͬдһ��СС�� Python ��һ�����ס�
���Ըе��Զ���������վ�㹦�� �C ���Ľ��������˵�Ƥë��
��Ȼ����һ����Ӧ�� ���� Django���Ķ� [���Ž̳�](/intro/tutorial01) ���Ҽ��� *����*. ��л���Ĺ�ע��