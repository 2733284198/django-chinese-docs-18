<!--
  ���ߣ�WrongWay [www.wrongway.me]
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

ÿ����ɸѡһ����������õ��Ķ���ȫ�µ���һ�������������֮ǰ�Ľ����֮��û���κΰ󶨹�ϵ��ÿ��ɸѡ���ᴴ��һ�������Ľ���������Ա��洢������ʹ�á�

���磺

```
>>> q1 = Entry.objects.filter(headline__startswith="What")
>>> q2 = q1.exclude(pub_date__gte=datetime.date.today())
>>> q3 = q1.filter(pub_date__gte=datetime.date.today())
```

������ QuerySets �ǲ�ͬ�ġ� ��һ�� QuerySet �����������"What"��ͷ�����м�¼���ڶ������ǵ�һ�����Ӽ�����һ�����ӵ������ų��˳������� pub_date �ǽ���ļ�¼�� ������Ҳ�ǵ�һ�����Ӽ�����ֻ������������ pub_date �ǽ���ļ�¼�� ����� QuerySet (q1) û���ܵ�ɸѡ��Ӱ�졣

## ��ѯ�����ӳٵ� ##

QuerySets �Ƕ��Ե� -- ���� QuerySet �Ķ������漰�κ����ݿ�����������һֱ��ӹ�����������������У�Django ����ִ���κ����ݿ��ѯ������ QuerySet ��ִ��. ���������������:

```
>>> q = Entry.objects.filter(headline__startswith="What")
>>> q = q.filter(pub_date__lte=datetime.now())
>>> q = q.exclude(body_text__icontains="food")
>>> print q
```

��Ȼ����Ĵ��뿴��ȥ�����������ݿ��������ʵ����ֻ�����һ�� (print q) ִ����һ�����ݿ��������һ������£� QuerySet ���ܴ����ݿ��������ػ�����ݣ��ñ��������������󡣶� QuerySet ��ֵ����ζ�� Django ��������ݿ⡣���˽�Բ�ѯ����ʱ��ֵ����鿴 ��ʱ�Բ�ѯ����ֵ (When QuerySets are evaluated).

## ������ѯ������  ##

��������ʹ�� all(), filter() �� exclude() ���㹻�ˡ� ��Ҳ��һЩ�����õģ���鿴 ��ѯAPI�ο� (QuerySet API Reference) �������� QuerySet �����б�

## ���Ʋ�ѯ����Χ ##

������ python ��������Ƭ�﷨��������� QuerySet �Եõ�һ���ֽ�������ȼ���SQL�е� LIMIT �� OFFSET ��

���磬�����������ӷ���ǰ������� (LIMIT 5):

```
>>> Entry.objects.all()[:5]
```

������ӷ��ص�������ʮ֮��Ķ��� (OFFSET 5 LIMIT 5):

```
>>> Entry.objects.all()[5:10]
```

Django ��֧�ֶԲ�ѯ������������ (���� Entry.objects.all()[-1]) ��

һ����˵���� QuerySet ��Ƭ�᷵���µ� QuerySet -- ��������в�������в�ѯ������Ҳ�����⣬���������Ƭʱʹ���� "step" ��������ѯ���ͻᱻ��ֵ���������ݿ������в�ѯ���ٸ����ӣ�ʹ��������������ѯ������ǰʮ�������е�ż���ζ��󣬾ͻ��������ݿ��ѯ:

```
>>> Entry.objects.all()[:10:2]
```

Ҫ���������Ķ��󣬶����б� (���� SELECT foo FROM bar LIMIT 1)������ֱ��ʹ��������������Ƭ���ٸ����ӣ�������δ��뽫���ش���������ĵ�һ����¼ Entry:

```
>>> Entry.objects.order_by('headline')[0]
```

��Լ�ȼ��ڣ�

```
>>> Entry.objects.order_by('headline')[0:1].get()
```
Ҫע����ǣ�����Ҳ������������Ķ��󣬵�һ�ַ������׳� IndexError �����ڶ��ַ������׳� DoesNotExist�� �꿴 get() ��

## �ֶ�ɸѡ����  ##

�ֶ�ɸѡ�������� SQL ����е� WHERE �Ӿ䡣���� Django �е� QuerySet �� filter(), exclude() �� get() �����еĹؼ��ֲ�����

ɸѡ��������ʽ�� field__lookuptype=value �� (ע�⣺������˫�»���)�����磺

```
>>> Entry.objects.filter(pub_date__lte='2006-01-01')
```

������Է���Ϊ���µ� SQL ���:

```
SELECT * FROM blog_entry WHERE pub_date <= '2006-01-01';
```

������ô�쵽�ģ�

Python ����ʽ��������� name-value ��ʽ�Ĳ�������������ʱ��ȷ��name��value��ֵ����������Ĺٷ�Python�̳��е� �ؼ��ֲ���(Keyword Arguments)��

����㴫����һ����Ч�Ĺؼ��ֲ��������׳� TypeError ������

���ݿ� API ֧��24�ֲ�ѯ���ͣ������� �ֶ�ɸѡ�ο�(field lookup reference) �鿴��ϸ���б�Ϊ�˸���һ��ֱ�۵���ʶ�����������г�һЩ���õĲ�ѯ���ͣ�

**exact**

"exact" ƥ�䡣���磺

```
>>> Entry.objects.get(headline__exact="Man bites dog")
```

���������µ� SQL ��䣺

```
SELECT ... WHERE headline = 'Man bites dog';
```

�����û���ṩ��ѯ���� -- Ҳ����˵�ؼ��ֲ�����û��˫�»��ߣ���ô��ѯ���;ͻᱻָ��Ϊ exact��

�ٸ����ӣ��������������ȵģ�

```
>>> Blog.objects.get(id__exact=14)  # Explicit form
>>> Blog.objects.get(id=14)         # __exact is implied
```

�������ܷ��㣬��Ϊ exact ����õġ�

**iexact**

���Դ�Сд��ƥ�䡣��������������ѯ:

```
>>> Blog.objects.get(name__iexact="beatles blog")
```

��ƥ������� "Beatles Blog", "beatles blog", ���� "BeAtlES blOG" �� Blog

**contains**

��Сд���е�ģ��ƥ�䡣 ���磺

```
Entry.objects.get(headline__contains='Lennon')
```

������Է���Ϊ���µ� SQL��

```
SELECT ... WHERE headline LIKE '%Lennon%';
```

Ҫע����δ���ƥ������ 'Today Lennon honored' ��������ƥ�� 'today lennon honored'��

��Ҳ��һ�����Դ�Сд�İ汾������ icontains��

**startswith, endswith**

�ֱ�ƥ�俪ͷ�ͽ�β��ͬ��Ҳ�к��Դ�Сд�İ汾 istartswith �� iendswith��
��ǿ��һ�Σ�������Ǽ�̽��ܡ������Ĳο���μ� �ֶ�ɸѡ�����ο�(field lookup reference)��

## ���ϵ��ѯ ##

Django �ṩ��һ��ֱ�۶���Ч�ķ�ʽ�ڲ�ѯ(lookups)�б�ʾ������ϵ�������Զ�ȷ�� SQL JOIN ��ϵ��Ҫ�����ϵ��ѯ����ʹ�������»���������ģ��(model)������ֶε����ƣ�ֱ���������ӵ�����Ҫ�� model Ϊֹ��

������Ӽ������й��� Blog �� name ֵΪ 'Beatles Blog' ������ Entry ����

```
>>> Entry.objects.filter(blog__name__exact='Beatles Blog')
```

���ϵ��ɸѡ��������һֱ��չ��

��ϵҲ�ǿ���ġ�������Ŀ�� model ��ʹ��Դ model ���Ƶ�Сд��ʽ�õ����������

����������Ӽ������ٹ���һ�� Entry �Ҵ���� headline ���� 'Lennon' ������ Blog ����

```
>>> Blog.objects.filter(entry__headline__contains='Lennon')
```

�����ĳ������ model ���Ҳ������Ϲ��������Ķ���Django ������Ϊһ���յ� (���е�ֵ���� NULL), ���ǿ��õĶ�������ζ�Ų������쳣�׳�������������У�

```
Blog.objects.filter(entry__author__name='Lennon')
```

(��������� Author ��), ���û���ĸ� author �� entry �������Django ����Ϊ��û�� name ���ԣ���������Ϊ������ author �׳��쳣��ͨ����˵������������ϣ���Ļ��ơ�Ψһ��������ʹ�� isnull �����������:

```
Blog.objects.filter(entry__author__name__isnull=True)
```

��δ����õ� author �� name Ϊ�յ� Blog �� entry �� authorΪ�յ� Blog�� ��������鷳����������д��

```
Blog.objects.filter (entry__author__isnull=False,
        entry__author__name__isnull=True)
```

��һ�Զ࣯��Զ��ϵ(Spanning multi-valued relationships)

�ⲿ����Django 1.0�������ģ� ��鿴�汾��¼
�����Ĺ����ǻ��� ManyToManyField �������� ForeignKeyField �ģ�����ܻ�������������������Ȥ���ع� Blog/Entry �Ĺ�ϵ(Blog �� Entry ��һ�Զ��ϵ)�����Ҫ���������� blog��������һ����������"Lennon"������2008������ entry ������Ҫ���������� blogs��������һ����������"Lennon"�� entry ��ͬʱ���ֹ�������һ����2008������ entry ����Ϊһ�� Blog ����������Entry���������������������ʵӦ�����Ǻ��п��ܳ��ֵġ�

ͬ��������Ҳ������ ManyToManyField �ϡ����磬��� Entry ��һ�� ManyToManyField �ֶΣ������� tags��������õ� tags ��"music"��"bands"�� entries������������õ�������Ϊ"music" �ı�ǩ��״̬��"public"�� entry��

��������������Django ��һ�ֺܷ���ķ�ʽ��ʹ�� filter() �� exclude()�����ڰ�����ͬһ�� filter() �е�ɸѡ��������ѯ��Ҫͬʱ��������ɸѡ������������������ filter() ����ѯ���ķ�Χ�������޶��ġ������ڿ�һ�Զ࣯��Զ��ϵ��ѯ��˵���ڵڶ�������£�ɸѡ������Ե����� model ���еĹ������󣬶����Ǳ�ǰ��� filter() ���˺�Ĺ�������

���������������Ժ����ٸ����ӻὲ�ø������Ҫ���������� blog����Ҫ��ϵһ��������к��� "Lennon" ������2008������ entry (��� entry ͬʱ��������������)����������д��

```
Blog.objects.filter(entry__headline__contains='Lennon',
        entry__pub_date__year=2008)
```

Ҫ��������һ�� blog��������һ������⺬��"Lennon"�� entry ���ֹ���һ����2008������ entry ��һ�� entry �Ĵ���⺬�� Lennon��ͬһ������һ�� entry ����2008�����ģ�����������д��

```
Blog.objects.filter(entry__headline__contains='Lennon').filter(
        entry__pub_date__year=2008)
```

�ڵڶ��������У���һ��������(filter)�ȼ�������������� entry ������������� blogs���ڶ����������ڴ˻����ϴ���Щ blogs �м�����ڶ��� entry Ҳ������� blog���ڶ���������ѡ��� entry �������һ����������ѡ�����ȫ��ͬ��Ҳ���ܲ�ͬ�� ��Ϊ��������˵��� Blog�������� Entry��

����ԭ��ͬ�������� exclude()��һ������ exclude() �е�����ɸѡ��������������ͬһ��ʵ�� (�����Щ�����������ͬһ��һ�Զ࣯��Զ�Ĺ�ϵ)�������� filter() �� exclude() ȴ����ͬ����ɸѡ�����������ڲ�ͬ�Ĺ�������

�ڹ����������� model �е��ֶ�(Filters can reference fields on the model)

�ⲿ���� Django 1.1 ������: ��鿴�汾��¼
���������е������У����ǹ���Ĺ�������ֻ�ǽ��ֶ�ֵ��ĳ���������Ƚϡ��������Ҫ�������ֶε�ֵ���Ƚϣ��Ǹ���ô���أ�

Django �ṩ F() ���������ıȽϡ�F() ��ʵ�������ڲ�ѯ�������ֶΣ����Ƚ�ͬһ�� model ʵ����������ͬ�ֶε�ֵ��

���磺Ҫ��ѯ�ظ���(comments)���ڹ㲥��(pingbacks)�Ĳ���(blog entries)�����Թ���һ�� F() �����ڲ�ѯ����������������

```
>>> from django.db.models import F
>>> Entry.objects.filter(n_pingbacks__lt=F('n_comments'))
```

Django ֧�� F() ����֮���Լ� F() ����ͳ���֮��ļӼ��˳���ȡģ�Ĳ��������磬Ҫ�ҵ��㲥�����������������Ĳ��ģ����������޸Ĳ�ѯ��䣺

```
>>> Entry.objects.filter(n_pingbacks__lt=F('n_comments') * 2)
```

Ҫ�����Ķ�����С����������㲥��֮�͵Ĳ��ģ���ѯ����:

```
>>> Entry.objects.filter(rating__lt=F('n_comments') + F('n_pingbacks'))
```

��Ҳ������ F() ������ʹ�������»��������ϵ��ѯ��F() ����ʹ�������»��������Ҫ�Ĺ����������磬Ҫ��ѯ����(blog)����������(author)������ͬ�Ĳ���(entry)����ѯ�Ϳ�������д��

```
>>> Entry.objects.filter(author__name=F('blog__name'))
```

## ������ѯ�ļ�ݷ�ʽ  ##

Ϊʹ�÷��㿼�ǣ�Django �� pk ��������"primary key"��

�� Blog Ϊ��, ������ id �ֶΣ���������������䶼�ǵȼ۵ģ�

```
>>> Blog.objects.get(id__exact=14) # Explicit form
>>> Blog.objects.get(id=14) # __exact is implied
>>> Blog.objects.get(pk=14) # pk implies id__exact
```

pk �� __exact ��ѯͬ����Ч���κβ�ѯ������� pk ��������������Ĳ�ѯ��

```
# Get blogs entries with id 1, 4 and 7
>>> Blog.objects.filter(pk__in=[1,4,7])

# Get all blog entries with id > 14
>>> Blog.objects.filter(pk__gt=14)
```

pk ��ѯҲ���Կ��ϵ��������������ǵȼ۵ģ�

```
>>> Entry.objects.filter(blog__id__exact=3) # Explicit form
>>> Entry.objects.filter(blog__id=3)        # __exact is implied
>>> Entry.objects.filter(blog__pk=3)        # __pk implies __id__exact
```

## ��LIKE�����ת��ٷֺ�%���»���_ ##

�ֶ�ɸѡ�����൱�� LIKE SQL ��� (iexact, contains, icontains, startswith, istartswith, endswith �� iendswith) �������Զ�ת������������� -- �ٷֺ�%���»���_��(�� LIKE ����У��ٷֺ�%��ʾ���ַ�ƥ�䣬���»���_��ʾ���ַ�ƥ�䡣)

�����ζ�����ǿ���ֱ��ʹ���������ַ��������ÿ������ǵ� SQL ���塣���磬Ҫ��ѯ������к���һ���ٷֺ�%�� entry��

```
>>> Entry.objects.filter(headline__contains='%')
```

Django �ᴦ��ת�壻���յ� SQL ����������������

```
SELECT ... WHERE headline LIKE '%\%%';
```

�»���_�Ͱٷֺ�%�Ĵ���ʽ��ͬ��Django �����Զ�ת�塣

## ����Ͳ�ѯ ##

ÿ�� QuerySet ������һ�����棬�Լ��ٶ����ݿ�ķ��ʡ�Ҫ��д��Ч���룬��Ҫ��⻺������ι����ġ�

һ�� QuerySet ʱ�ոմ�����ʱ�򣬻����ǿյġ� QuerySet ��һ������ʱ����ִ�����ݿ��ѯ�������� Django ���� QuerySet �Ļ����б����ѯ�Ľ�������������󷵻���Щ���(���磬�����ٴε������ QuerySet ��ʱ��)���ٴ����� QuerySet ʱ�ͻ�������Щ��������

Ҫ��ס������˵�Ļ�����Ϊ��������ʹ�� QuerySet ʱ���ܻ������ɲ�С���鷳�����磬������������ QuerySet ������������ֵ��Ȼ���ͷţ�

```
>>> print [e.headline for e in Entry.objects.all()]
>>> print [e.pub_date for e in Entry.objects.all()]
```

�����ζ����ͬ�����ݿ��ѯ��ִ�����Σ���ʵ�϶�ȡ���������ݿ⡣���ң������ζ��������б���ܲ�����ȫ��ͬ����Ϊ�������ֿ��ܣ������ζ�ȡ֮�䣬ĳ�� Entry ����ӵ����ݿ��У����Ǳ�ɾ���ˡ�

Ҫ����������⣬ֻҪ�򵥵ر��� QuerySet Ȼ�����ü��ɣ�

```
>>> queryset = Poll.objects.all()
>>> print [p.headline for p in queryset] # Evaluate the query set.
>>> print [p.pub_date for p in queryset] # Re-use the cache from the evaluation.
```

�� Q ����ʵ�ָ��Ӳ��� (Complex lookups with Q objects)

�� filter() �Ⱥ�ʽ�йؼ��ֲ����˴�֮�䶼�� "AND" ��ϵ�������Ҫִ�и����ӵĲ�ѯ(���磬ʵ��ɸѡ������ OR ��ϵ)������ʹ�� Q ����

Q ����(django.db.models.Q)��������װһ���ѯ�ؼ��ֵĶ��������ᵽ�Ĳ�ѯ�ؼ�����鿴����� "Field lookups"��

���磬������� Q �����װ��һ�������� LIKE ��ѯ��

```
Q(question__startswith='What')
```

Q ��������� & �� | ������������ӡ���ĳ�������������� Q ����ʱ���ͻ����һ���µĵȼ۵� Q ����

���磬����������Ͳ�����һ�� Q �������� "OR" ��ϵ���ӵ����� "question__startswith" ��ѯ��

```
Q(question__startswith='Who') | Q(question__startswith='What')
```

��������ӵȼ�������� SQL WHERE �Ӿ䣺

```
WHERE question LIKE 'Who%' OR question LIKE 'What%'
```

������� & �� | ���������� Q ���󣬶��ҿ��������ŷ��顣Q ����Ҳ������ ~ ����ȡ����������ͨ��ѯ��ȡ����ѯ(NOT)����������һ��ʹ�ã�

```
Q(question__startswith='Who') | ~Q(pub_date__year=2005)
```

ÿ�ֲ�ѯ��ʽ(���� filter(), exclude(), get()) �����ܽ��չؼ��ֲ������⣬Ҳ����λ�ò�������ʽ����һ������ Q ������������ѯ��ʽ�����˶�� Q ������ô���Ǳ˴˼䶼�� "AND" ��ϵ�����磺

```
Poll.objects.get(
    Q(question__startswith='Who'),
    Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6))
)
```

... ������Է���Ϊ����� SQL��

```
SELECT * from polls WHERE question LIKE 'Who%'
    AND (pub_date = '2005-05-02' OR pub_date = '2005-05-06')
```

���Һ�ʽ���Ի��� Q ����͹ؼ��ֲ�������ѯ��ʽ�����в���(Q ��ϵ�͹ؼ��ֲ���) ���� "AND" ��ϵ�����ǣ������������ Q �����������������еĹؼ��ֲ���֮ǰ�����磺

```
Poll.objects.get(
    Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6)),
    question__startswith='Who')
```

... ��һ����Ч�Ĳ�ѯ�������������ѯ��Ȼ����ȥ��ǰ�ߵȼۣ�

```
# INVALID QUERY
Poll.objects.get(
    question__startswith='Who',
    Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6)))
```

... �������ѯȴ����Ч�ġ�

> �μ�
> 
> �� Django �ĵ�Ԫ���� OR��ѯʵ��(OR lookups examples) ��չʾ�� Q ��������

## ����Ƚ� ##

Ҫ�Ƚ��������󣬾ͺ� Python һ����ʹ��˫�Ⱥ��������==��ʵ���ϱȽϵ������� model ������ֵ��

������� Entry Ϊ����������������ǵȼ۵ģ�

```
>>> some_entry == other_entry
>>> some_entry.id == other_entry.id
```

��� model ���������Ʋ��� id��Ҳû��ϵ��Django ���Զ��Ƚ�������ֵ�����������ǵ�������ʲô�����磬���һ�� model �������ֶ������� name����ô������������ǵȼ۵ģ�

```
>>> some_obj == other_obj
>>> some_obj.name == other_obj.name
```

## ����ɾ�� ##

ɾ���������� delete()��������ʱ����ɾ��������������κ�ֵ�����磺

```
e.delete()
```

��Ҳ����һ����ɾ���������ÿ�� QuerySet ����һ�� delete() ��������һ����ɾ�� QuerySet �����еĶ���

���磬����Ĵ��뽫ɾ�� pub_date ��2005��� Entry ����

```
Entry.objects.filter(pub_date__year=2005).delete()
```

Ҫ�μ���һ�㣺������ʲô����£�QuerySet �е� delete() ������ֻʹ��һ�� SQL ���һ����ɾ�����ж��󣬶������Ƿֱ�ɾ��ÿ�������������ʹ���� model ���Զ���� delete() ��������Ҫ���е���ÿ�������delete ������(���磬���� QuerySet����ÿ�������ϵ��� delete()����)��������ʹ�� QuerySet �е� delete()������

�� Django ɾ������ʱ����ģ�� SQL Լ�� ON DELETE CASCADE ����Ϊ�����仰˵��ɾ��һ������ʱҲ��ɾ�����������������������磺

```
b = Blog.objects.get(pk=1)
# This will delete the Blog and all of its Entry objects.
b.delete()
```

Ҫע����ǣ� delete() ������ QuerySet �ϵķ����������������� Manager ��������һ�ֱ������ƣ���Ϊ�˱�������ص��� Entry.objects.delete() �������� ���е� ��¼����ɾ���������ȷ��Ҫɾ�����еĶ�����ô�������ʽ�ص��ã�

```
Entry.objects.all().delete()
```

һ�θ��¶������ (Updating multiple objects at once)

�ⲿ���� Django 1.0 �������ģ� ��鿴�汾�ĵ�
��ʱ����� QuerySet �е����ж���һ�θ���ĳ���ֶε�ֵ�����Ҫ������� update() ������ɡ����磺

```
# Update all the headlines with pub_date in 2007.
Entry.objects.filter(pub_date__year=2007).update(headline='Everything is the same')
```

���ַ����������ڷǹ�ϵ�ֶκ� ForeignKey ����ֶΡ����·ǹ�ϵ�ֶ�ʱ�������ֵӦ����һ������������ ForeignKey �ֶ�ʱ�������ֵӦ��������������Ǹ����ĳ��ʵ�������磺

```
>>> b = Blog.objects.get(pk=1)

# Change every Entry so that it belongs to this Blog.
>>> Entry.objects.all().update(blog=b)
```

update() ����Ҳ�Ǽ�ʱ��Ч���������κ�ֵ��(�� delete() ����)�� �� QuerySet ���и���ʱ��Ψһ�����ƾ���һ��ֻ�ܸ���һ�����ݱ����ǵ�ǰ model ���������Բ�Ҫ���Ը��¹������������ƵĲ�������Ϊ���ǲ��������еġ�

ҪС�ĵ��ǣ� update() ������ֱ�ӷ����һ�� SQL ���ġ��������ֱ�ӵ�һ��������и��¡������������� model �е� save() ������Ҳ���ᷢ�� pre_save �� post_save �ź�(��Щ�ź��ڵ��� save() ����ʱ����)��������뱣�� QuerySet �е�ÿ�����󣬲��ҵ���ÿ��������Ե� save() ��������ô�㲻�������дһ����ʽ��ֻҪ������Щ�������ε��� save() �������ɣ�

```
for item in my_queryset:
    item.save()
```

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
�ڵ��� update ʱ����ʹ�� F() ���� ����ĳ���ֶε�ֵ����Ϊ��һ���ֶε�ֵ������������������Ƿǳ����õġ����磬�����еĲ��� (entry) �Ĺ㲥�� (pingback) ��һ��

```
>>> Entry.objects.all().update(n_pingbacks=F('n_pingbacks') + 1)
```

���ǣ��� F() �����ڲ�ѯʱ����ͬ���ǣ���filter �� exclude�Ӿ��У��㲻���� F() ���������������ϵ(NO-Join)����ֻ�����õ�ǰ model ��Ҫ���µ��ֶΡ�������� F() ����������Join ��ϵobject���ͻ��׳� FieldError �쳣��

```
# THIS WILL RAISE A FieldError
>>> Entry.objects.update(headline=F('blog__name'))
```

## ������� ##

���㶨���� model �����ϵʱ (���磬 ForeignKey, OneToOneField, �� ManyToManyField)��model ��ʵ���Դ�һ�׺ܷ����API�Ի�ȡ�����Ķ���

��������� models Ϊ����һ�� Entry ���� e ��ͨ�� blog ���Ի��������� Blog ���� e.blog��

(�ڳ������������������ Python �� descriptors ʵ�ֵġ������Դ˸���Ȥ�������˽�һ�¡�)

Django Ҳ�ṩ�����ȡ��������� API�������ɴӱ������Ķ���õ��䶨���ϵ�����������磬һ�� Blog ���ʵ�� b ����ͨ�� entry_set ���Եõ������������ Entry �����б�: b.entry_set.all()��

��һ�����е����Ӷ�ʹ�ñ�ҳ�������г��� Blog, Author �� Entry model��

## һ�Զ��ϵ ##

### ���� ###

���һ�� model ��һ�� ForeignKey�ֶΣ�����ֻҪͨ��ʹ�ù��� model �����ƾͿ��Եõ���������������

���磺

```
>>> e = Entry.objects.get(id=2)
>>> e.blog # Returns the related Blog object.
```

��������úͻ��������ԡ��������������ģ��ı��������Ϊ�����������ݿ������ֱ������� save()����ʱ���Żᱣ�浽���ݿ⡣���磺

```
>>> e = Entry.objects.get(id=2)
>>> e.blog = some_blog
>>> e.save()
```

�������ֶ� ForeignKey ��һ�� null=True ������(������������ܿ�ֵ NULL)������Ը�������ֵ None �����磺

```
>>> e = Entry.objects.get(id=2)
>>> e.blog = None
>>> e.save() # "UPDATE blog_entry SET blog_id = NULL ...;"
```

��һ�Զ��ϵ�У���һ�������ȡ��������ʱ����������ᱻ���档�������������ʱ���ʵ�����ͻ�ӻ����л���������磺

```
>>> e = Entry.objects.get(id=2)
>>> print e.blog  # Hits the database to retrieve the associated Blog.
>>> print e.blog  # Doesn't hit the database; uses cached version.
```

Ҫע����ǣ�QuerySet �� select_related() ������ǰ�����е�һ�Զ��ϵ���뻺���С����磺

```
>>> e = Entry.objects.select_related().get(id=2)
>>> print e.blog  # Doesn't hit the database; uses cached version.
>>> print e.blog  # Doesn't hit the database; uses cached version.
```

### ������� ###

��� model ��һ�� ForeignKey����ֶΣ���ô���� model ��ʵ������ͨ������ Manager ���õ������������Դ model ��ʵ����Ĭ������£���� Manager ������Ϊ FOO_set, ������� FOO ����Դ model ��Сд���ơ���� Manager ���� QuerySets�����ǿɹ��˺Ϳɲ����ģ������� "�����ȡ(Retrieving objects)" ���ἰ��

���磺

```
>>> b = Blog.objects.get(id=1)
>>> b.entry_set.all() # Returns all Entry objects related to Blog.

# b.entry_set is a Manager that returns QuerySets.
>>> b.entry_set.filter(headline__contains='Lennon')
>>> b.entry_set.count()
```

�����ͨ���� ForeignKey() �Ķ��������� related_name ��ֵ����д FOO_set �����ơ����磬��� Entry model ����һ�¸��ģ� blog = ForeignKey(Blog, related_name='entries')����ô�������ͻ������ǿ�����㣺

```
>>> b = Blog.objects.get(id=1)
>>> b.entries.all() # Returns all Entry objects related to Blog.

# b.entries is a Manager that returns QuerySets.
>>> b.entries.filter(headline__contains='Lennon')
>>> b.entries.count()
```

�㲻����һ���൱�з��� ForeignKey Manager ��������ͨ�����ʵ�������ʣ�

```
>>> Blog.entry_set
Traceback:
    ...
AttributeError: "Manager must be accessed via instance".
```

���������� "�����ȡRetrieving objects" һ�����ᵽ�� QuerySet ����֮�⣬ForeignKey Manager ��������һЩ���������������������һ����̽��ܣ�������鿴 related objects reference��

`add(obj1, obj2, ...)`

��ĳ���ض��� model ������ӵ����������󼯺��С�

`create(**kwargs)`

����������һ���¶���Ȼ���������ӱ���������ļ����У�Ȼ�󷵻�����¶���

`remove(obj1, obj2, ...)`

��ĳ���ض��Ķ���ӱ��������󼯺���ȥ����

`clear()`

��ձ��������󼯺ϡ�
��һ��ָ���������ϵĳ�Ա����ôֻҪ���������Ϸ���һ���ɵ����Ķ��󼴿ɡ������԰��������ʵ����Ҳ����ֻ����������ֵ�����磺

```
b = Blog.objects.get(id=1)
b.entry_set = [e1, e2]
```

����������У�e1 �� e2 ������������ Entry ʵ����Ҳ���������͵�����ֵ��

��� clear() �����ǿ��õģ��ڵ�����(�����о���һ���б�)�еĶ�����뵽 entry_set ֮ǰ���Ѵ����ڹ��������е����ж��󽫱���ա���� clear() ���� �����ã�ԭ�еĹ��������еĶ���Ͳ���Ӱ�죬�������ڡ�

��һ���ᵽ��ÿһ�� "reverse" ��������ʵʱ�������ݿ�ģ�ÿһ����ӣ�������ɾ���������ἰʱ���潫������浽���ݿ��С�

## ��Զ��ϵ ##

�ڶ�Զ��ϵ���κ�һ��������ʹ�� API �������������һ������Զ�� API �������������ᵽ�� "����" һ�Զ��ϵ��ϵ�ǳ�����

Ψһ�Ĳ�����������Ե������� ManyToManyField ���ڵ� model (Ϊ�˷��㣬�ҳ�֮ΪԴmodel A) ʹ���ֶα�������������ʹ������󣻶�����������һ����ʹ�� A ��Сд���Ƽ��� '_set' ��׺(���������һ�Զ��ϵ�ǳ�����)��

����������ӻ����˸�������⣺

```
e = Entry.objects.get(id=3)
e.authors.all() # Returns all Author objects for this Entry.
e.authors.count()
e.authors.filter(name__contains='John')

a = Author.objects.get(id=5)
a.entry_set.all() # Returns all Entry objects for this Author.
```

�� ForeignKey һ��, ManyToManyField Ҳ����ָ�� related_name��������������У���� Entry �е� ManyToManyField ָ�� related_name='entries'����ô������ÿ�� Author ʵ���� entry_set ���Զ��� entries �����档

### һ��һ��ϵ ###

����ڶ��һ��ϵ���ԣ�һ��һ��ϵ���Ƿǳ��򵥵ġ�������� model �ж�����һ�� OneToOneField ��ϵ����ô��Ϳ���������ֶε�������Ϊ�������������������Ķ���

���磺

```
class EntryDetail(models.Model):
    entry = models.OneToOneField(Entry)
    details = models.TextField()

ed = EntryDetail.objects.get(id=2)
ed.entry # Returns the related Entry object.
```

�� "reverse" ��ѯ��ͬ���ǣ�һ��һ��ϵ�Ĺ�������Ҳ���Է��� Manager ���󣬵������ Manager ����һ�������Ķ��󣬶�����һ���б�

```
e = Entry.objects.get(id=2)
e.entrydetail # returns the related EntryDetail object
```

���һ���ն��󱻸��������ϵ��Django �ͻ��׳�һ�� DoesNotExist �쳣��

���㶨������������õķ�ʽһ�������ʵ��Ҳ���Ը������������ϵ��

```
e.entrydetail = ed
```

## ��ϵ�еķ�����������������ģ� ##

���������ϵ��ӳ��(ORM)��Ҫ���ڹ���˫���������ϵ���� Django �Ŀ���������Ϊ��Υ���� DRY ԭ�� (Don't Repeat Yourself)������ Django ֻ��Ҫ����һ�������ϵ���ɡ�

������һ�� model �ಢ����֪������ model ����������������ģ����������� model Ҳ�����룬��ô������ΰ쵽�ģ�

�𰸾����� INSTALLED_APPS �����С��κ�һ�� model �ڵ�һ�ε���ʱ��Django �ͻ�������е� INSTALLED_APPS ������ models���������ڴ��д����б�Ҫ�ķ������ӡ���������˵��INSTALLED_APPS ������֮һ����ȷ�� Django ������ model ��Χ��

## �ڹ��������ϵĲ�ѯ ##

������������Ĳ�ѯ�������ͨ�ֶ�ֵ�Ĳ�ѯ����ѭ��ͬ�Ĺ���Ϊĳ����ѯָ��ĳ��ֵ��ʱ�������ʹ��һ����ʵ����Ҳ����ʹ�ö��������ֵ��

���磬�������һ�� Blog ���� b ������ id=5, ����������ѯ��һ���ģ�

```
Entry.objects.filter(blog=b) # Query using object instance
Entry.objects.filter(blog=b.id) # Query using id from instance
Entry.objects.filter(blog=5) # Query using id directly
```

## ֱ��ʹ��SQL ##

����㷢��ĳ�� SQL ��ѯ�� Django �����ݿ�ӳ���������ǳ����ӵĻ��������ʹ��ֱ��д SQL ����ɡ�

����ķ�ʽ������� model �Զ��巽�������Զ��� model �� manager ���������в�ѯ����Ȼ Django ��Ҫ�����ݲ��������� model ����ִ�С����ǰ������ҵ�߼��������һ���ط����Ӵ�����֯�ĽǶ�������Ҳ��ʮ�����ǵġ�������鿴 ִ��ԭ��SQL��ѯ(Performing raw SQL queries).

���Ҫע����ǣ�Django�����ݲ���������Ƿ������ݿ��һ���ӿڡ�������������Ĺ��ߣ�������ԣ����ݿ������������ݿ⡣��������ݿ���ԣ�ûʲô�Ƿ��� Django ���ɵġ�