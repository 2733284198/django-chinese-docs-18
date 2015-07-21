<!--
  ���ߣ�Github@wizardforcel
-->

# ִ�в�ѯ #

һ���㽨����*����ģ��*֮��django���Զ�����һ�����ݿ�����API����������ִ����ɾ�Ĳ�Ĳ�������ƪ�ĵ����������ʹ����ЩAPI����������ģ�ͼ���ѡ�����ϸ���ݣ����*[����ģ�Ͳο�](https://docs.djangoproject.com/en/1.8/ref/models/)*��

�������ĵ����Լ��ο����У����ǻ����ʹ�������ģ�ͣ���������һ������Ӧ�á�

```
from django.db import models

class Blog(models.Model):
    name = models.CharField(max_length=100)
    tagline = models.TextField()

    def __str__(self):              # __unicode__ on Python 2
        return self.name

class Author(models.Model):
    name = models.CharField(max_length=50)
    email = models.EmailField()

    def __str__(self):              # __unicode__ on Python 2
        return self.name

class Entry(models.Model):
    blog = models.ForeignKey(Blog)
    headline = models.CharField(max_length=255)
    body_text = models.TextField()
    pub_date = models.DateField()
    mod_date = models.DateField()
    authors = models.ManyToManyField(Author)
    n_comments = models.IntegerField()
    n_pingbacks = models.IntegerField()
    rating = models.IntegerField()

    def __str__(self):              # __unicode__ on Python 2
        return self.headline
```

## �������� ##

Ϊ�˰����ݿ���е����ݱ�ʾ��python����djangoʹ��һ��ֱ�۵ķ�ʽ��һ��ģ����������ݿ��һ����һ��ģ�͵�ʵ���������ݿ���е�һ���ض��ļ�¼��

ʹ�ùؼ��ʲ���ʵ����һ����������������Ȼ�����**save()**�������浽���ݿ��С�

����ģ�ʹ�����ļ�**mysite/blog/models.py**�У�������һ�����ӣ�

```
>>> from blog.models import Blog
>>> b = Blog(name='Beatles Blog', tagline='All the latest Beatles news.')
>>> b.save()
```

����Ĵ����ڱ���ִ����sql��**INSERT**������������ʽ����**save()**֮ǰ��django����������ݿ⡣

**save()**����û�з���ֵ��

> ��μ�
> 
> **save()**��������һЩ�߼�ѡ�����û�������������������ϸ�����**save()**�ĵ���
> 
> �������ֻ��һ����䴴��������һ������ʹ��**create()**������

## �������ĸĶ� ##

����**save()**�������������Ѿ����������ݿ��еĶ���ĸĶ���

����һ��**Blog**��ʵ��**b5**�Ѿ������������ݿ��У�������Ӹ������������֣����������ݿ��и������ļ�¼��

```
>>> b5.name = 'New name'
>>> b5.save()
```

����Ĵ����ڱ���ִ����sql��**UPDATE**������������ʽ����**save()**֮ǰ��django����������ݿ⡣

### ����**ForeignKey**��**ManyToManyField**�ֶ� ###

����**ForeignKey**�ֶεķ�ʽ�ͱ�����ͨ�ֶ���ͬ--ֻ�Ǽ򵥵ذ�һ��������ȷ�Ķ���ֵ���ֶ��С���������Ӹ�����**Entry**���ʵ��**entry**��**blog**���ԣ�����**Entry**��һ�����ʵ�ʵ���Լ�**Blog**�Ѿ����������ݿ��У����ǿ���������������ȡ���ǣ���

```
>>> from blog.models import Entry
>>> entry = Entry.objects.get(pk=1)
>>> cheese_blog = Blog.objects.get(name="Cheddar Talk")
>>> entry.blog = cheese_blog
>>> entry.save()
```

����**ManyToManyField**�ķ�ʽ��һЩ��ͬ--ʹ���ֶε�**add()**���������ӹ�ϵ�ļ�¼�����������**entry**�������**Author**���ʵ��**joe**��

```
>>> from blog.models import Author
>>> joe = Author.objects.create(name="Joe")
>>> entry.authors.add(joe)
```

Ϊ����һ������У���**ManyToManyField**��Ӷ�����¼�������ڵ���**add()**����ʱ��������������������

```
>>> john = Author.objects.create(name="John")
>>> paul = Author.objects.create(name="Paul")
>>> george = Author.objects.create(name="George")
>>> ringo = Author.objects.create(name="Ringo")
>>> entry.authors.add(john, paul, george, ringo)
```

Django����������Ӵ������͵Ķ���ʱ�׳��쳣��

## ��ȡ���� ##

ͨ��ģ���е�**Manager**����һ��**QuertSet**������������ݿ��л�ȡ����

**QuerySet**��ʾ�����ݿ���ȡ������һ������ļ��ϡ������Ժ��������һ�����߶�������������������������Ĳ������Ʋ�ѯ����ķ�Χ����sql�ĽǶȣ�**QuerySet**��**SELECT**����ȼۣ�����������**WHERE**��**LIMIT**һ���������Ӿ䡣

����Դ�ģ�͵�**Manager**����ȡ��**QuerySet**��ÿ��ģ�Ͷ�������һ��**Manager**����ͨ������Ϊ**objects**��ͨ��ģ����ֱ�ӷ���������������

```
>>> Blog.objects
<django.db.models.manager.Manager object at ...>
>>> b = Blog(name='Foo', tagline='Bar')
>>> b.objects
Traceback:
    ...
AttributeError: "Manager isn't accessible via Blog instances."
```

> **ע��**
> 
> ������ͨ��ֻ����ͨ��ģ���������ʣ�������ͨ��ģ��ʵ�������ʡ�����Ϊ��ǿ�����ֱ���ͼ�¼����Ĳ�����

����һ��ģ����˵��**Manager**��**QuerySet**����Ҫ��Դ�����磬** Blog.objects.all() **�᷵�س������ݿ�������**Blog**�����һ��**QuerySet**��

### ��ȡ���ж��� ###

��ȡһ���������ж������򵥵ķ�ʽ��ȫ����ȡ��ʹ��**Manager**��**all()**������

```
>>> all_entries = Entry.objects.all()
```

**all()**�������ذ������ݿ������ж����**QuerySet**��

### ʹ�ù�������ȡ�ض����� ###

**all()**�������صĽ�����а���ȫ�����󣬵��Ǹ��ձ�����������Ҫ��ȡ�������ϵ�һ���Ӽ���

Ҫ��������һ���Ӽ�����Ҫ��������Ľ����������һЩ��������Ϊ�������������ձ��;���ǣ�

**filter(\*\*kwargs)**
����һ����������ļ��ϣ��������������������������

**exclude(\*\*kwargs)**
����һ����������ļ��ϣ�����***��***���������������������

��ѯ���������溯�������е�**\*\*kwargs**����Ҫ�����ض��ĸ�ʽ��*�ֶμ���*һ���л��ᵽ��

�ٸ����ӣ�Ҫ��ȡ���Ϊ2006���������µĽ��������������ʹ��**filter()**������

```
Entry.objects.filter(pub_date__year=2006)
```

��Ĭ�ϵĹ��������У����൱�ڣ�

```
Entry.objects.all().filter(pub_date__year=2006)
```

#### ��ʽ���� ####

**QuerySet**�ľ����������**QuerySet**����������԰Ѿ����õ������ϵ�һ����������

```
>>> Entry.objects.filter(
...     headline__startswith='What'
... ).exclude(
...     pub_date__gte=datetime.date.today()
... ).filter(
...     pub_date__gte=datetime(2005, 1, 30)
... )
```

�ʼ��**QuerySet**�������ݿ��е����ж���֮������һ��������ȥ��һ���֣���֮����������һ�������������Ľ����һ��**QuerySet**���������б����ԡ�word����ͷ�ļ�¼������������2005��һ�£���Ϊ�����ֵ��

#### ���˺�Ľ�����Ƕ����� ####

ÿ���㾫��һ����������õ��Ķ���ȫ�µ���һ�������������֮ǰ�Ľ����֮��û���κΰ󶨹�ϵ��ÿ�ξ������ᴴ��һ�������Ľ���������Ա��洢������ʹ�á�

���磺

```
>>> q1 = Entry.objects.filter(headline__startswith="What")
>>> q2 = q1.exclude(pub_date__gte=datetime.date.today())
>>> q3 = q1.filter(pub_date__gte=datetime.date.today())
```

