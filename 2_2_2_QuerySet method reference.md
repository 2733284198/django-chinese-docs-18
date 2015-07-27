<!--
  ���ߣ�WrongWay [www.wrongway.me]
  1.8���£�Github@wizardforcel
-->

# ��ѯ�� API �ο� #

���ĵ���ϸ������ QuerySet �� API��������������ǽ����� model �� database query �ĵ��Ļ����ϣ����Խ������ڿ����ĵ�֮ǰ�ȶ�һ���������ĵ���

�ᴩ���ĵ���������ʹ��database query guide �ĵ��е� example weblog models Ϊ����

## �ڲ�ѯʱ������ʲô ##

���ڲ�����QuerySet ���Ա����죬���ˣ���Ƭ����Ϊ�������ݣ���Щ��Ϊ����������ݿ���в�����ֻҪ���ѯ��ʱ��������Ĳ������ݿ⡣

����� QuerySet ��Ϊ�ᵼ��ִ�в�ѯ�Ĳ�����

+ ѭ��(Iteration)��QuerySet �ǿɵ����ģ������������ʱ�ͻ�ִ�����ݿ���������磬��ӡ�����в��ĵĴ���⣺

```
for e in Entry.objects.all():
    print e.headline
```

+ ��Ƭ(Slicing)���� ��ѯ�޶�(Limiting QuerySets) ���ᵽ, a QuerySet �ǿ����� Python ��������Ƭ�﷨�����Ƭ��һ����˵��һ�� QuerySet ��Ƭ�ͷ�����һ�� QuerySet (�� QuerySet ���ᱻִ��)���������������Ƭʱʹ���� "step" ������Django �Ի�ִ�����ݿ������

+ ���л������滯(Pickling/Caching)�� ������鿴 pickling QuerySets�� ��һ����ǿ����һ���ǲ�ѯ����Ǵ����ݿ��ж�ȡ�ġ�

+ repr(). ���� QuerySet �� repr() ����ʱ����ѯ�ͻᱻ���С������ Python ��������˵�ǳ����㣬�����ʹ�� API ����������ѯ�����

+ len(). ���� QuerySet �� len() ��������ѯ�ͻᱻ���С������������ϣ��᷵�ز�ѯ����б�ĳ��ȡ�

ע�⣺�������õ������м�¼���������Ͳ�Ҫʹ�� QuerySet �� len() ��������Ϊֱ�������ݿ����ʹ�� SQL �� SELECT COUNT(*) ����Ӹ�Ч��Django �ṩ�� count() �����������ԭ�������������� count() ������

+ list(). �� QuerySet Ӧ�� list() �������ͻ����в�ѯ�����磺

```
entry_list = list(Entry.objects.all())
```

Ҫע����ǣ�ʹ�����������ռ�ô����ڴ棬��Ϊ Django ���б����ݶ����뵽�ڴ��С���Ϊ�Աȣ����� QuerySet �Ǵ����ݿ��ȡ���ݣ�����ʹ��ĳ������ʱ�Ž������뵽�����С�

## ���л���ѯ�� ##

�����Ҫ ���л�(pickle) һ�� QuerySet��Django ���ȾͻὫ��ѯ�������뵽�ڴ�����������л���������Ϳ��Ե�һʱ��ʹ�ö���(ֱ�Ӵ����ݿ��ж�ȡ������Ҫһ��ʱ�䣬�����ǻ�����������)�������л��ǻ��滯�����й����������ڻ����ѯʱ�����Ⱦͻ�������л�����������ζ�ŵ��㷴���л� QuerySet ʱ����һʱ��ͻ���ڴ��л�ò�ѯ�Ľ���������Ǵ����ݿ��в��ҡ�

�����ֻ�������л����ֱ�Ҫ����Ϣ�Ա���Щʱ����Դ����ݿ����ؽ� Queryset ����ֻ���л� QuerySet �� query ���Լ��ɡ���������Ϳ���ʹ������Ĵ����ؽ�ԭ���� QuerySet ���⵱��û�����ݿ��ȡ����

```
>>> import pickle
>>> query = pickle.loads(s)     # Assuming 's' is the pickled string.
>>> qs = MyModel.objects.all()
>>> qs.query = query            # Restore the original 'query'.
```

query ������һ����͸���Ķ��������ζ�������ڲ��ṹ�����ǹ����ġ�������ˣ����ڱ����ᵽ�����л��ͷ����л���˵�������ǰ�ȫ�ͱ���ȫ֧�ֵġ�

## ��ѯAPI ##

һ������£����Ƕ���ֱ��ʹ�ö������ֶ�����һ�� Manager ����������������Ҫ����һ�� QuerySet ����ʽ��

`class QuerySet([model=None])`

ͨ�������޸�ĳ�� QuerySet ʱ�����ʹ�� ������(chaining filters)������Ϊ������������������������� QuerySet �����������µĲ�ѯ(querysets)��

## �����²�ѯ�ķ��� ##

Django Ϊ QuerySet �ṩ��һ�����ŵķ����������޸� QuerySet ��ѯ��������ͺ����� SQL ��ѯ�ķ�ʽ��

`filter(**kwargs)`

����һ���µ� QuerySet ������������������ɸѡ������ƥ��Ķ���

��Щɸѡ����(\*\*kwargs)��������ֶ�ɸѡ(Field lookups) ������ϸ���ܡ��������֮���� SQL ������� AND ��ϵ��

`exclude(**kwargs)`

����һ���µ� QuerySet����������Щ������ɸѡ������ƥ��Ķ���

��Щɸѡ����(**kwargs)Ҳ������� �ֶ�ɸѡ(Field lookups) ������ϸ�������������֮���� SQL �����Ҳ�� AND ��ϵ��������������һ�� NOT() ��ϵ��

��������޳��˳������� pub_date ���� 2005-1-3 ���Ҵ���� headline �� "Hello" �����в���(entry)��

```
Entry.objects.exclude(pub_date__gt=datetime.date(2005, 1, 3), headline='Hello')
```

�� SQL ����У���ȼ��ڣ�

```
SELECT ...
WHERE NOT (pub_date > '2005-1-3' AND headline = 'Hello')
```

��������޳��������� pub_date ���� 2005-1-3 ���ߴ������ "Hello" �����в��ģ�

```
Entry.objects.exclude(pub_date__gt=datetime.date(2005, 1, 3)).exclude(headline='Hello')
```

�� SQL ����У���ȼ��ڣ�

```
SELECT ...
WHERE NOT pub_date > '2005-1-3'
OR NOT headline = 'Hello'
```

Ҫע��ڶ����������кܶ����Ƶġ�

## ע��annotate(\*args, \*\*kwargs) ##

�ⲿ���� Django 1.1 �����ģ� ��鿴�汾�ĵ���
���ǿ���Ϊ QuerySet �е�ÿ���������ע�⡣����ͨ�������ѯ�����ÿ�������������Ķ��󼯺ϣ��Ӷ��ó��ܼ�ֵ(Ҳ������ƽ��ֵ���ܺͣ��ȵ�)����Ϊ QuerySet �ж����ע�⡣annotate() �е�ÿ���������ᱻ��Ϊע����ӵ� QuerySet �з��صĶ���

Django �ṩ��ע�⺯ʽ������� (ע�⺯ʽAggregation Functions) ����ϸ���ܡ�

ע���ʹ�ùؼ��ֲ�������Ϊע��ı����������κβ�����������һ������������ע�⺯ʽ�����ƺͱ�ע��� model ��ء�

���磬�����ڲ���һ�������б�����֪��һ�����;����ж���ƪ���ģ�

>>> q = Blog.objects.annotate(Count('entry'))
# The name of the first blog
>>> q[0].name
'Blogasaurus'
# The number of entries on the first blog
>>> q[0].entry__count
42
Blog model �౾��û�ж��� entry__count ���ԣ�������ʹ��ע�⺯ʽ�Ĺ�ϵ�ֲ������Ӷ��ı�ע���������

>>> q = Blog.objects.annotate(number_of_entries=Count('entry'))
# The number of entries on the first blog, using the name provided
>>> q[0].number_of_entries
42
Ҫ�����˽�ע�⣬����� ע��ָ��(the topic guide on Aggregation)��

order_by(*fields)

Ĭ������£� QuerySet ���صĲ�ѯ����Ǹ��� model ��� Meta �������ṩ�� ordering ���ж��������Ԫ�������ж�������ġ������ʹ�� order_by ��������֮ǰ QuerySet �е��������á�

���磺

Entry.objects.filter(pub_date__year=2005).order_by('-pub_date', 'headline')
���ؽ���ͻ��Ȱ��� pub_date �������������ٰ��� headline ���н������� "-pub_date" ǰ��ĸ���"?"��ʾ��������Ĭ���ǲ�����������Ҫ������򣬾�ʹ�� "?"�����磺

Entry.objects.order_by('?')
ע�⣺order_by('?') ���ܻ�ǳ����������Ĺ�����Դ����ȡ��������ʹ�õ����ݿ⡣

Ҫ�������� model �ֶ����������﷨�Ϳ��ϵ��ѯ���﷨��ͬ������˵���������������»���(__)���ӹ��� model �� Ҫ������ֶ�����, ���ҿ���һֱ���졣���磺

Entry.objects.order_by('blog__name', 'headline')
�������Թ����ֶ�������û��ָ�� Meta.ordering ������£�Django �����Ĭ���������ã����ǰ��չ��� model �����������������磺

Entry.objects.order_by('blog')
...�ȼ��ڣ�

Entry.objects.order_by('blog__id')
...������Ϊ Blog model û�������������ԭ�ʡ�

�����ʹ���� distinct() ��������ô�ڶԹ����ֶ�����ʱҪ���������������鿴 distinct() һ���˽���ʹ�� distinct() ʱ������ζ�Ԥ�ڵ��������������벻����Ӱ�졣

�� Django �����ǿ��԰��ն�ֵ�ֶΣ����� ManyToMany �ֶΣ���������ġ����������������Ȼ�Ƚ������ǲ���ʵ�á����������Ѿ���������˽������������е�ÿ�����󣬶�ֻ��һ��������Ķ���ʱ�������൱��ֻ��һ��һ��ϵʱ��������Ż������Ԥ�ڵĽ�������ԶԶ�ֵ�ֶ�����ʱҪ����ע�⡣

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
����㲻����κ��ֶ�����Ҳ����ʹ�� model ��ԭ�е��������ã���ô���Ե����޲����� order_by() ������

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
���ϵ������﷨�Ѿ��ı䣬�� Django 0.96 ������ͬ���ɰ汾��鿴 Django 0.96 documentation��

�����������Ƿ�Ӧ�ô�Сд���У�Django ��û���ṩ���÷���������ȫȡ���ں�˵����ݿ�������Сд��δ���

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
�������ĳ����ѯ����ǿ�����ģ�Ҳ�����ǲ�������ģ���ȡ���� QuerySet.ordered ���ԡ��������ֵ�� True ����ô QuerySet ���ǿ�����ġ�

reverse()

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
ʹ�� reverse() ������Բ�ѯ������з������򡣵������� reverse() �����൱������û�����Ĺ���

Ҫ�õ���ѯ��������������󣬿�������д��

my_queryset.reverse()[:5]
Ҫע�����ַ�ʽ�� Python �﷨�еĴ�β����Ƭ����ȫ��һ���ġ�������������У����ȵõ����һ��Ԫ�أ�Ȼ���ǵ����ڶ��������δ����������������һ�� Python ���У�ʹ�� seq[-5:]ʱ��ȴ���ȵõ������Ԫ�ء�Django ֮���Բ��� reverse ����ȡ�����ļ�¼������֧����Ƭ�ķ�����ԭ����Ǻ����� SQL ���������á�

����һ��Ҫע�⣬���� reverse() ����Ӧ��ֻ�������Ѷ����������� QuerySet (���磬�ڲ�ѯʱʹ����order_by()������������ model �൱��ֱ�Ӷ�����������). �����û����ȷ�����������ô���� QuerySet, calling reverse() ��ûʲôʵ�����壨��Ϊ�ڵ��� reverse() ֮ǰ������û�ж���������������֮��Ҳ�����������)

distinct()

����һ���µ� QuerySet ��������ִ�� SQL ��ѯʱʹ�� SELECT DISTINCT������ζ�ŷ��ؽ���е��ظ���¼�����޳���

Ĭ������£� QuerySet �����޳��ظ��ļ�¼����ʵ�ʵ��У��ⲻ��ʲô���⣬��Ϊ�� Blog.objects.all() �����Ĳ�ѯ����������ظ��ļ�¼�����ǣ������ʹ�� QuerySet ������ѯʱ���ͺܿ��ܻ�����ظ���¼����ʱ���Ϳ���ʹ�� distinct() ������

Note

�� order_by(*fields) �г��ֵ��ֶ�Ҳ������� SQL SELECT ���С������ distinct() ͬʱʹ�ã���ʱ���صĽ��ȴ��Ԥ��Ĳ�ͬ��������Ϊ�������Կ��ϵ�Ĺ����ֶν���������Щ�ֶξͻᱻ��ӵ���ѡȡ�����У���Ϳ��ܲ����ظ����ݣ����磬�����������ݶ���ͬ��ֻ�ǹ����ֶε�ֵ��ͬ���������� order_by �еĹ����ֶβ���������ڷ��ؽ���У����ǽ���������ʵ��order����������ʱ���ص����ݿ���ȥ�����ǲ�û�н��й� distinct ����һ����

ͬ����ԭ��������� values() ������ñ�ѡȡ���У��ͻᷢ�ְ����� order_by() (���� model ��� Meta �����õ�������)�е��ֶ�Ҳ���������棬�ͻ�Է��صĽ������Ӱ�졣

����ǿ���ľ�������ʹ�� distinct() ʱ��Ҫ�����Դ������ֶ�����ͬ���ģ���ͬʱʹ�� distinct() �� values() ʱ����������ֶβ�û�г����� values() ���صĽ���У���ôҲҪ����ע�⡣

values(*fields)

����һ�� ValuesQuerySet -- ����һ������� QuerySet �����к�õ��Ĳ�����һϵ�� model ��ʵ�������󣬶���һ���ֵ��б�

ÿ���ֵ䶼��ʾһ�����󣬶��������� model ������������ơ�

��������ӾͶ� values() �õ����ֵ��봫ͳ�� model ��������˶Աȣ�

# This list contains a Blog object.
>>> Blog.objects.filter(name__startswith='Beatles')
[<Blog: Beatles Blog>]

# This list contains a dictionary.
>>> Blog.objects.filter(name__startswith='Beatles').values()
[{'id': 1, 'name': 'Beatles Blog', 'tagline': 'All the latest Beatles news.'}]
values() ���Խ��տ�ѡ��λ�ò�����*fields�������ֶε����ƣ��������� SELECT ѡȡ�����ݡ������ָ�����ֶβ�����ÿ���ֵ�ͻ��� Key-Value ����ʽ��������ָ�����ֶ���Ϣ�����û��ָ����ÿ���ֵ�ͻ������ǰ���ݱ��е������ֶ���Ϣ��

���磺

>>> Blog.objects.values()
[{'id': 1, 'name': 'Beatles Blog', 'tagline': 'All the latest Beatles news.'}],
>>> Blog.objects.values('id', 'name')
[{'id': 1, 'name': 'Beatles Blog'}]
������Щϸ��ֵ��ע�⣺

values() ���������� ManyToManyField ���Ե��κ���Ϣ�������� ManyToManyField ��������Ϊ�������ݸ� values()���ͻ��׳��쳣��

�������һ����Ϊ foo ��ForeignKey �ֶΣ�Ĭ������µ��� values() ���ص��ֵ��а�������Ϊ foo_id ���ֵ����Ϊ����һ�������� model �ֶΣ���������������������ֵ( foo ����������ϵ������� model )������ʹ�� values() �������ֶ�����ʱ�� ����foo �� foo_id ����õ���ͬ�Ľ�� (�ֵ��еļ������Զ������㴫�ݵ��ֶ�����)��

���磺

>>> Entry.objects.values()
[{'blog_id: 1, 'headline': u'First Entry', ...}, ...]

>>> Entry.objects.values('blog')
[{'blog': 1}, ...]

>>> Entry.objects.values('blog_id')
[{'blog_id': 1}, ...]
�� values() �� distinct() ͬʱʹ��ʱ��Ҫע���������Ӱ�췵�صĽ����������鿴���� distinct() һ�ڡ�

�ⲿ������ Django 1.0 �������ģ� ��������İ汾�ĵ�
ǰ�����ᵽ�ģ��� values() ��ʹ�� blog_id ����Ч�ģ�ֻ���� blog������ Django 1.0 �������汾���÷���

ValuesQuerySet �Ƿǳ����õġ�����������Ϳ���ֻ�����������ǲ������ݣ�������ͬʱ��ȡ�������������ݡ�

���Ҫ���ѵ��ǣ�ValuesQuerySet �� QuerySet ��һ�����࣬������ӵ�� QuerySet ���еķ���������Զ������� filter() ���� order_by() �Լ�����������������������д���ǵȼ۵ģ�

Blog.objects.values().order_by('id')
Blog.objects.order_by('id').values()
Django �ı�д���Ǹ�ϲ���ڶ���д����������дӰ�� SQL �ķ�������дӰ������ķ���������������д order����дvalues ��������Щ���޹ؽ�Ҫ����ȫ�������ϲ�ö�����

values_list(*fields)

�ⲿ������ Django 1.0 �������ģ� ����İ汾�ĵ�
���� values() �ǳ����ƣ�ֻ�������߷��صĽ�����ֵ��б��� values() ���صĽ����Ԫ���б�ÿ��Ԫ�鶼�������ݸ� values_list() ���ֶ����ƺ����ݡ������һ��Ͷ�Ӧ�ŵ�һ���ֶΣ����磺

>>> Entry.objects.values_list('id', 'headline')
[(1, u'First entry'), ...]
����㴫����һ���ֶ���Ϊ��������ô�����ʹ�� flat �������������ֵ�� True������ζ�ŷ��ؽ�����ǵ�����ֵ��������Ԫ�顣��������ӻὲ�ø������

>>> Entry.objects.values_list('id').order_by('id')
[(1,), (2,), (3,), ...]

>>> Entry.objects.values_list('id', flat=True).order_by('id')
[1, 2, 3, ...]
������ݵ��ֶβ�ֹһ����ʹ�� flat �ͻᵼ�´���

�����û�� values_list() ���ݲ��������ͻᰴ���ֶ��� model ���ж����˳�򷵻����е��ֶΡ�

dates(field, kind, order='ASC')

����һ�� DateQuerySet ��������ȡ QuerySet ��ѯ�������������ڣ��������һ���µ� datetime.datetime ������б�

field ����� model �е� DateField �� DateTimeField �ֶ����ơ�

kind �� "year", "month" �� "day" ֮һ�� ÿ�� datetime.datetime ���󶼻���������� type ���нؼ���

"year" ��������ʱ��ֵ�з��ظ�������б�
"month" ��������ʱ��ֵ�з��ظ����꣯���б�
"day" ��������ʱ��ֵ�з��ظ����꣯�£����б�
order, Ĭ���� 'ASC'��ֻ������ȡֵ 'ASC' �� 'DESC'������������������

���ӣ�

>>> Entry.objects.dates('pub_date', 'year')
[datetime.datetime(2005, 1, 1)]
>>> Entry.objects.dates('pub_date', 'month')
[datetime.datetime(2005, 2, 1), datetime.datetime(2005, 3, 1)]
>>> Entry.objects.dates('pub_date', 'day')
[datetime.datetime(2005, 2, 20), datetime.datetime(2005, 3, 20)]
>>> Entry.objects.dates('pub_date', 'day', order='DESC')
[datetime.datetime(2005, 3, 20), datetime.datetime(2005, 2, 20)]
>>> Entry.objects.filter(headline__contains='Lennon').dates('pub_date', 'day')
[datetime.datetime(2005, 3, 20)]
none()

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
����һ�� EmptyQuerySet -- ����һ������ʱֻ���ؿ��б�� QuerySet���������������ֳ��ϣ���Ҫ����һ�����б����ǵ�����ȴ��Ҫ����һ�� QuerySet ���󡣣���ʱ���Ϳ�������������б�

���磺

>>> Entry.objects.none()
[]
all()

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
���ص�ǰ QuerySet (�����Ǵ��ݵ� QuerySet ����)��һ�ֿ����� ����ĳЩ�����Ǻ��õģ����磬�����һ�� model manager ����һ�� QuerySet �Ĳ�ѯ�������һ���Ĺ��ˡ���Ϳ��Ե��� all() ���һ�ֿ����Լ����������Ӷ���֤ԭ QuerySet �İ�ȫ��

select_related()

����һ�� QuerySet ��������ִ�в�ѯʱ�Զ����������ϵ���Ӷ�ѡȡ�������Ķ������ݡ�����һ����Ч������Ȼ�ᵼ�½ϴ�����ݲ�ѯ����ʱ��ǳ��󣩣����ǽ�������ʹ�������ϵ��ù�������ʱ���ͻ᲻�ٴζ�ȡ���ݿ��ˡ�

���������չʾ�ڻ�ù�������ʱ��ʹ�� select_related() �Ͳ�ʹ�õ����������ǲ�ʹ�õ����ӣ�

# Hits the database.
e = Entry.objects.get(id=5)

# Hits the database again to get the related Blog object.
b = e.blog
��������ʹ�� select_related �����ӣ�

# Hits the database.
e = Entry.objects.select_related().get(id=5)

# Doesn't hit the database, because e.blog has been prepopulated
# in the previous query.
b = e.blog
select_related() �ᾡ���ܵ��������������ӡ����磺

class City(models.Model):
    # ...

class Person(models.Model):
    # ...
    hometown = models.ForeignKey(City)

class Book(models.Model):
    # ...
    author = models.ForeignKey(Person)
...���������� Book.objects.select_related().get(id=4) ����������� Person �� City��

b = Book.objects.select_related().get(id=4)
p = b.author         # Doesn't hit the database.
c = p.hometown       # Doesn't hit the database.

b = Book.objects.get(id=4) # No select_related() in this example.
p = b.author         # Hits the database.
c = p.hometown       # Hits the database.
Ҫע����ǣ�Ĭ������£�select_related() �������� null=True �������ϵ��

һ������£�ʹ�� select_related() �Ἣ��ĸ������ܣ���Ϊ�����Ա����������ݿ���������ǣ��ڹ�ϵǶ����ȹ��������£�select_related() ��ʱ������Թ�ϵ�ĸ��٣�������Ϊ���ɵĲ�ѯ��ǳ���󣬻ᵼ�²���������

����������£������ʹ�� depth ��������ӵ� select_related()�дӶ�����Ҫ���ٵĹ�ϵ������

b = Book.objects.select_related(depth=1).get(id=4)
p = b.author         # Doesn't hit the database.
c = p.hometown       # Requires a database call.
��ʱ����� model ���ж�������ֶΣ�����ֻ��һ�Է������е�ĳ��������ʱ��Ϳ��Խ���Щ�ֶε�������Ϊ�������ݸ� select_related() ��Ȼ���ֻ�������������Ĺ�ϵ�����١�������������ʹ�ù�����������������ʹ��˫�»�������ʾ model ֮��Ĺ��������磺

class Room(models.Model):
    # ...
    building = models.ForeignKey(...)

class Group(models.Model):
    # ...
    teacher = models.ForeignKey(...)
    room = models.ForeignKey(Room)
    subject = models.ForeignKey(...)
...�����ֻ����� room �� subject ���ԣ���������д��

g = Group.objects.select_related('room', 'subject')
����дҲ����ȷ�ģ�

g = Group.objects.select_related('room__building', 'subject')
...����Ҳ�Ὣ building ��ϵ���뵽�����С�

��ֻ�ܽ�����ֶ� ForeignKey ���ݸ� select_related��������ô���������Ϊ�������������� null=True ��������ϵ (��Ĭ�ϵ� select_related() ��ͬ)���������ͬһ�� select_related() ��ͬʱʹ���ֶ����ƺ� depth �������ͻᵼ�´�����Ϊ������ì�ܵ�����ѡ�

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
�� select_related() ��ͬʱʹ�� depth ������ָ�������ֶ������� Django 1.0 ��������汾���ǿ��õġ�

extra(select=None, where=None, params=None, tables=None, order_by=None, select_params=None)

��Щ����£�Django �Ĳ�ѯ�﷨���Լ����ر�︴�ӵ� WHERE �Ӿ䡣�������������Django �ṩ�� extra() QuerySet �޸Ļ��ƣ�������QuerySet ���ɵ� SQL �Ӿ���ע�����Ӿ䡣

���ڲ�Ʒ�����ԭ����Щ�Զ���Ĳ�ѯ���Ա����ڲ�ͬ�����ݿ�֮�����(��Ϊ����д SQL �����ԭ��)������Υ���� DRY ԭ��������Ǳ�Ҫ�����Ǿ�������д extra��

�� extra ����ָ��һ������ params �������� select��where �� tables�����в������ǿ�ѡ�ģ���������Ҫʹ��һ����

select
select �������������� SELECT �Ӿ�����������ֶ���Ϣ����Ӧ����һ���ֵ䣬������������� SQL �Ӿ��ӳ�䡣

���磺

Entry.objects.extra(select={'is_recent': "pub_date > '2006-01-01'"})
�����ÿ�� Entry ������һ������� is_recent ���ԣ�����һ������ֵ����ʾ pub_date �Ƿ�����2006��1��1�š�

Django ��ֱ���� SELECT �м����Ӧ�� SQL Ƭ�ϣ�����ת����� SQL ���£�

SELECT blog_entry.*, (pub_date > '2006-01-01')
FROM blog_entry;
����������Ӹ�����һЩ��������ÿ�� Blog ���������һ�� entry_count ���ԣ���������һ���Ӳ�ѯ���õ�������� Entry �����������

Blog.objects.extra(
    select={
        'entry_count': 'SELECT COUNT(*) FROM blog_entry WHERE blog_entry.blog_id = blog_blog.id'
    },
)
(��������������У�����Ҫ�˽������ʵ������ blog_blog ���Ѿ������� FROM �Ӿ��С�)

����� SQL ���£�

SELECT blog_blog.*, (SELECT COUNT(*) FROM blog_entry WHERE blog_entry.blog_id = blog_blog.id) AS entry_count
FROM blog_blog;
Ҫע����ǣ���������ݿ���Ҫ���Ӿ�����������ţ����� Django �� select �Ӿ���ȴ����������ͬ��Ҫ����ע����ǣ���ĳЩ���ݿ��У�����ĳЩ MySQL �汾���ǲ�֧���Ӳ�ѯ�ġ�

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
ĳЩʱ���������� extra(select=...) �е� SQL ��䴫�ݲ�������ʱ�Ϳ���ʹ�� select_params ��������Ϊ select_params ��һ�����У��� select ������һ���ֵ䣬����������ƥ��ʱӦ��ȷ��һһ��Ӧ��������������У���Ӧ��ʹ�� django.utils.datastructures.SortedDict ƥ�� select ��ֵ��������ʹ��һ��� Python ���С�

���磺

Blog.objects.extra(
    select=SortedDict([('a', '%s'), ('b', '%s')]),
    select_params=('one', 'two'))
��ʹ�� extra() ʱҪ������ select �ִ����� "%%s" �Ӵ��� ������Ϊ�� Django �У����� select �ִ�ʱ���ҵ��� %s ������ת���� % �ַ������������ % ������ת�壬�����ò�����ȷ�Ľ����

where / tables
�����ʹ�� where ������ʾ���� SQL �е� WHERE �Ӿ䣬��ʱҲ�������з���ʽ�����ӡ��㻹����ʹ�� tables �ֶ��ظ� SQL FROM �Ӿ����������

where �� tables �������ַ����б���Ϊ���������е� where �����˴�֮�䶼�� "AND" ��ϵ��

���磺

Entry.objects.extra(where=['id IN (3, 4, 5, 20)'])
...���¿��Է���Ϊ���µ� SQL:

SELECT * FROM blog_entry WHERE id IN (3, 4, 5, 20);
��������� tables ������:

queryset.extra(tables=['(select * from table) as k'])
����� SQL ���£�

select ........ from `self_table`, `(select * from table) as k`
��չʾ����������Ӳ�ѯ��

��ʹ�� tables ʱ�������ָ���ı��ڲ�ѯ���ѳ��ֹ�����ôҪ����С�ġ�����ͨ�� tables ��������������ݱ�ʱ�����������Ѿ��������ڲ�ѯ�У���ô Django �ͻ���Ϊ������һ�ΰ����������͵�����һ�����⣺�����ظ����ֶ�εı�ᱻ����һ�����������Գ��˵�һ��֮�⣬ÿ���ظ��ı�������ֱ��� Django ����һ�����������ԣ������ͬʱʹ���� where �������������õ���ĳ���ظ���ȴ��֪���ı�������ô�ͻᵼ�´���

һ������£���ֻ�����һ��δ�ڲ�ѯ�г��ֵ��±���������������ᵽ��������������ˣ���ô���Բ������´�ʩ��������ȣ��ж��Ƿ��б�ҪҪ�����ظ��ı��ܷ��ظ��ı�ȥ�����������в�ͨ�������Ű� extra() ���÷��ڲ�ѯ�ṹ����ʼ������Ϊ�״γ��ֵı������ᱻ�����������Կ����ܽ�����⡣�����Ҳ���У��ǾͲ鿴���ɵ� SQL ��䣬�����ҳ��������ݿ�ı�����Ȼ��������д where ��������ΪֻҪ��ÿ�ζ���ͬ���ķ�ʽ���ò�ѯ(queryset)����ı��������ᷢ���仯�����������ֱ��ʹ�ñ�ı��������� where��

order_by
�������ͨ�� extra() ��������ֶλ������ݿ⣬��ʱ��������ֶν������򣬾Ϳ��Ը� extra() �е� order_by ��������һ�������ַ������С��ַ��������� model ԭ�����ֶ���(��ʹ����ͨ�� order_by() ����һ��)��Ҳ������ table_name.column_name ������ʽ������������ extra() �� select ����������ֶΡ�

���磺

q = Entry.objects.extra(select={'is_recent': "pub_date > '2006-01-01'"})
q = q.extra(order_by = ['-is_recent'])
��δ��밴�� is_recent �Լ�¼���������ֶ�ֵ�� True ������ǰ�棬False �����ں��档(True �ڽ�������ʱ������ False ��ǰ��)��

˳��˵һ�£�������δ���ͬʱҲչʾ��������������Ը��������ε��� extra() ����(ÿ������µ����ṹ����)��

params
�����ᵽ�� where �����������ñ�׼�� Python ռλ�� -- '%s' �������Ը������ݿ������Զ������Ƿ�������š� params �����������滻ռλ�����ַ����б�

���磺

Entry.objects.extra(where=['headline=%s'], params=['Lennon'])
ʹ�� params �滻 where ����Ƕ��ֵ��һ���ǳ��õ�������������Ϊ params ���Ը���������ݿ��ж�Ҫ��Ҫ������ֵ������ţ����磬����ֵ�е����Żᱻ�Զ�ת�壩��

���õ��÷���

Entry.objects.extra(where=["headline='Lennon'"])
���ŵ��÷���

Entry.objects.extra(where=['headline=%s'], params=['Lennon'])
defer(*fields)

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
��ĳЩ���ݸ��ӵĻ����£���� model ���ܰ����ǳ�����ֶΣ�����ĳЩ�ֶΰ����ǳ��������(���磬�ĵ��ֶ�)�����߽���ת��Ϊ Python ��������ķǳ������Դ������������£���ʱ����ܲ�����Ҫ�����ֶε���Ϣ����ô������� Django ����ȡ���ǵ����ݡ�

������������ֶε����ƴ��� defer() �������Ϳ��������Ӻ����룺

Entry.objects.defer("lede", "body")
�Ӻ�����ֶεĲ�ѯ���ص����� model ���ʵ������������Ӻ������ֶ�ʱ�����Կ��Ի���ֶε����ݣ�����ͬ���ǣ���������������Ӻ��ֶ�ʱ�Ŷ�ȡ���ݿ�ģ�����ͨ�ֶ��������в�ѯ(queryset)ʱ��һ���Դ����ݿ��ж�ȡ���ݵġ�

����Զ�ε��� defer() ������ÿ�����ö���������µ��Ӻ������ֶΣ�

# Defers both the body and lede fields.
Entry.objects.defer("body").filter(headline="Lennon").defer("lede")
���Ӻ������ֶν��������ǲ��������õģ��ظ�����Ӻ������ֶ�Ҳ�����кβ���Ӱ�졣

��Ҳ�����Ӻ�������� model �е��ֶ�(ǰ������ʹ�� select_related() �����˹��� model)���÷�Ҳ����˫�»������ӹ����ֶΣ�

Blog.objects.select_related().defer("entry__lede", "entry__body")
�����������Ӻ���������ã�ֻҪʹ�ý� None ��Ϊ�������� defer() ���ɣ�

# Load all fields immediately.
my_queryset.defer(None)
��Щ�ֶ����������ָ���������ᱻ�Ӻ���ء����磬����Զ�����Ӻ���������ֶΡ������ʹ�� select_related() ��ù��� model �ֶ���Ϣ����ô��Ͳ����Ӻ�������� model ��������������������ˣ���Ȼ�����׳�������ʵ��ȴ������Ӻ���أ�

ע��

defer() ����(������ᵽ�� only() ����) ��ֻ�������ض�����µĸ߼����ԡ����ǿ����ṩ�����ϵ��Ż�������ǰ�������Ѿ������õ��Ĳ�ѯ�й�������ϸ�µķ������ǳ��������Ҫ�ľ�������Щ��Ϣ�������Ѿ���������Ҫ�����ݺ�Ĭ������·��ص��������ݽ��бȶԣ��������֮��Ĳ��졣���������������֮����ʹ�������ַ��������Ż�����������ġ����Ե���տ�ʼ�������Ӧ��ʱ���Ȳ�Ҫ����ʹ�� defer() �����������Ѿ�д���ѯ���ҷ�������Щ�������ȵ�Ӧ���Ժ�����Ҳ���١�

only(*fields)

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
only() ������������ defer() �������෴�����������ȡ����ʱϣ��ĳ���ֶβ�Ӧ�ñ��Ӻ����룬��Ӧ���������룬��ô��Ϳ�����ʹ�� only() �����������һ�� model ����ϣ�������е��ֶζ��Ӻ���أ�ֻ��ĳ�����ֶ�����������ģ���ô���Ӧ��ʹ�� only() ������

�������һ�� model������ name, age �� biography �����ֶΣ���ô��������д��Ч��һ���ģ�

Person.objects.defer("age", "biography")
Person.objects.only("name")
�����ۺ�ʱ���� only()�����������̸����������á��������������ǳ������ֻ�� only �е��ֶλ��������룬�������������Ӻ�����ġ���ˣ��������� only() ʱ��ֻ�����һ�� only �����Ż���Ч��

# This will defer all fields except the headline.
Entry.objects.only("body", "lede").only("headline")
���� defer() ���Ե�����ÿ�ζ�����ֶε��Ӻ�������б��У�����������Խ� only() �� defer() �����һ��ʹ�ã���ע��ʹ��˳���� only ���� defer��

# Final result is that everything except "headline" is deferred.
Entry.objects.only("headline", "body").defer("body")

# Final result loads headline and body immediately (only() replaces any
# existing set of fields).
Entry.objects.defer("body").only("headline", "body")
�����ز�ѯ�ķ���(QuerySet methods that do not return QuerySets)

�������е� QuerySet ���������� QuerySet��ȴ�������� other than a QuerySet��

��Щ��������ʹ�û���(��鿴 �������ѯ(Caching and QuerySets))����������������ʱ��������ȡ���ݿ�ġ�

get(**kwargs)

������������ɸѡ������ƥ��Ķ���ɸѡ������ �ֶ�ɸѡ����(Field lookups) һ��������ϸ���ܡ�

��ʹ�� get() ʱ���������ɸѡ�����Ķ��󳬹�һ�����ͻ��׳� MultipleObjectsReturned �쳣��MultipleObjectsReturned �� model ���һ�����ԡ�

��ʹ�� get() ʱ�����û���ҵ�����ɸѡ�����Ķ��󣬾ͻ��׳� DoesNotExist �쳣������쳣Ҳ�� model �����һ�����ԡ����磺

Entry.objects.get(id='foo') # raises Entry.DoesNotExist
DoesNotExist �쳣�̳��� django.core.exceptions.ObjectDoesNotExist�����������ֱ�ӽػ� DoesNotExist �쳣�����磺

from django.core.exceptions import ObjectDoesNotExist
try:
    e = Entry.objects.get(id=3)
    b = Blog.objects.get(id=1)
except ObjectDoesNotExist:
    print "Either the entry or blog doesn't exist."
create(**kwargs)

��������ͬʱ�������Ŀ�ݷ�����

p = Person.objects.create(first_name="Bruce", last_name="Springsteen")
��

p = Person(first_name="Bruce", last_name="Springsteen")
p.save(force_insert=True)
����ͬ�ġ�

force_insert �����ڱ�����ϸ���ܣ�����ʾ�ѵ�ǰ model ����һ���¶�����������һ������£��㲻�ص�����һ�㣬���������� model �����������ֶ�ָ���ģ���������ֵ�Ѿ������ݿ��д��ڣ���ô���� create() �ͻ�ʧ�ܣ����׳� IntegrityError��������Ϊ����ֵ������Ψһ�ġ����Ե����ֶ�ָ������ʱ���ǵ�Ҫ���ô����쳣��׼����

get_or_create(**kwargs)

����һ������ʵ��Ӧ�õķ�����������������ɸѡ������ѯ����������󲻴��ھʹ���һ���¶���

�����ص���һ�� (object, created) Ԫ�飬���е� object ������ȡ���Ǵ����Ķ��󣬶� created ����һ������ֵ������ʾǰ���ᵽ�� object �Ƿ����´����ġ�

����ζ����������Ч�ؼ��ٴ��룬���ҶԱ�д���ݵ���ű��ǳ����á����磺

try:
    obj = Person.objects.get(first_name='John', last_name='Lennon')
except Person.DoesNotExist:
    obj = Person(first_name='John', last_name='Lennon', birthday=date(1940, 10, 9))
    obj.save()
����Ĵ�������� model ���ֶ������ļ������������ӹ�ס��������� get_or_create() ��д��

obj, created = Person.objects.get_or_create(first_name='John', last_name='Lennon',
                  defaults={'birthday': date(1940, 10, 9)})
������Ҫע�� defaults ��һ���ֵ䣬���������ڴ�������ʱΪ�ֶθ�ֵ�������������ڲ����Ѵ��ڵĶ��� get_or_create() �����յĹؼ��ֲ��������ڵ��� get() ʱ��ʹ�ã���һ���������⣬���� defaults����ʹ��get_or_create() ʱ����ҵ��˶��󣬾ͻ᷵���������� False�����û���ҵ����ͻ�ʵ����һ���¶��󣬲����䱣�棻ͬʱ��������¶���� True�������¶���Ĳ���������£�

defaults = kwargs.pop('defaults', {})
params = dict([(k, v) for k, v in kwargs.items() if '__' not in k])
params.update(defaults)
obj = self.model(**params)
obj.save()
����Ȼ�����������ӷ� 'defaults' �ؼ��ֲ������ų�����˫�»��ߵĲ�������Ϊ˫�»��߱�ʾ�Ǿ�ȷ��ѯ����Ȼ������� defaults �ֵ�����ݣ�������������еĹؼ��ֲ����ظ������� defaults �е�����Ϊ׼, Ȼ�������Ĺؼ��ֲ������ݸ� model �ࡣ��Ȼ����ֻ���㷨�ļ�������ʵ���϶Ժܶ�ϸ��û���ἰ��������쳣�ͱ߽������Ĵ��������Դ˸���Ȥ��������һ��ԭ���롣

������ model ǡ����һ���ֶΣ��������� defaults������������ get_or_create() ��������Ϊ��ȷ��ѯ������, �͵�ʹ�� 'defaults__exact' (֮ǰ��� defaults ֻ���ڴ���ʱ�Զ���ֵ�������ܽ��в�ѯ)��������������

Foo.objects.get_or_create(defaults__exact='bar', defaults={'defaults': 'baz'})
������ֶ�ָ������������ôʹ�� get_or_create() ����ʱҲ���� create() һ�����׳����Ƶ��쳣�������ֶ�ָ����������������ֵ�Ѿ������ݿ��д��ڣ��ͻ��׳�һ�� IntegrityError �쳣��

�����һ���� Django ��ͼ(views)��ʹ�� get_or_create() ʱҪע���һ�㡣������˵�������ڽű��з������ݺ���������ݶ��ԣ�get_or_create() �Ƿǳ����õġ����������������ͼ��ʹ�� get_or_create() ����ô��Ҫ�������⣬Ҫȷ������ POST ������ʹ�ã��������кܱ�Ҫ�ͺܳ�ֵ����ɲŲ���ô�������� GET ������ʹ�õĻ�����������ݲ����κ����á���ʹ�� POST �Ļ���ÿ������ҳ������󶼻��������һ���ĸ����á�Ҫ�˽���࣬��鿴 HTTP �淶�е� ��ȫ����(Safe methods)��

count()

�������ݿ���ƥ���ѯ(QuerySet)�Ķ��������� count() �����׳��κ��쳣��

���磺

# Returns the total number of entries in the database.
Entry.objects.count()

# Returns the number of entries whose headline contains 'Lennon'
Entry.objects.filter(headline__contains='Lennon').count()
count() ���ں��ִ�� SELECT COUNT(*) ������������Ӧ�þ���ʹ�� count() �����ǶԷ��صĲ�ѯ���ʹ�� len() ��

��������ʹ�õ����ݿ�(���� PostgreSQL �� MySQL)��count() ���ܻ᷵�س����ͣ���������ͨ�� Python ��������ȷʵ��һ���ܹŹֵľٴ룬û��ʲôʵ�����塣

in_bulk(id_list)

����һ������ֵ�б�Ȼ�����ÿ������ֵ�����Ӧ�Ķ��󣬷���һ������ֵ������ӳ���ֵ䡣

Example:

>>> Blog.objects.in_bulk([1])
{1: <Blog: Beatles Blog>}
>>> Blog.objects.in_bulk([1, 2])
{1: <Blog: Beatles Blog>, 2: <Blog: Cheddar Talk>}
>>> Blog.objects.in_bulk([])
{}
������ in_bulk() ���ݵ���һ�����б������õ�����һ�����ֵ䡣

iterator()

���в�ѯ(QuerySet)��Ȼ����ݽ������һ�� ������(iterator�� ��Ϊ�Ƚϣ�ʹ�� QuerySet ʱ�������ݿ��ж�ȡ���м�¼��һ���Խ����м�¼ʵ����Ϊ��Ӧ�Ķ��󣻶� iterator() ���Ƕ�ȡ��¼���Ƿֶ�ζ�����ʵ�������õ��ĸ������ʵ�����ĸ����������һ���Է��غܶ����� QuerySet��ʹ�õ���������Ч�ʸ��ߣ����Ҹ���ʡ�ڴ档

Ҫע����ǣ������ iterator() ������ QuerySet���Ǿ���ζ�Ż���һ�����в�ѯ������˵���������β�ѯ��

latest(field_name=None)

����ʱ���ֶ� field_name �õ����µĶ���

����������Ӹ��� pub_date �ֶεõ����ݱ������µ� Entry ����

Entry.objects.latest('pub_date')
������� model �� Meta ������ get_latest_by ��, ��ô�������ȥ field_name ������Django �Ὣ get_latest_by ��ΪĬ�����á�

�� get(), latest() һ�������������������û���ҵ�ƥ��Ķ��󣬾ͻ��׳� DoesNotExist �쳣��

ע�� latest() �Ǵ���Ϊ�������׶������ڵķ�����

aggregate(*args, **kwargs)

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
ͨ���� QuerySet ���м��㣬����һ���ۺ�ֵ���ֵ䡣 aggregate() ��ÿ��������ָ��һ���������ֵ��еķ���ֵ��

������� �ۺϺ�ʽ(Aggregation Functions) ���жԾۺϺ�ʽ����ϸ������

�ۺ�ʹ�ùؼ��ֲ�����Ϊע������ơ�ÿ����������һ��Ϊ�䶩�������ƣ��������ȡ���ھۺϺ�ʽ�ĺ������;ۺ��ֶε����ơ�

���磬�����ڴ����ģ�����֪��������һ���ж���ƪ���ģ�

>>> q = Blog.objects.aggregate(Count('entry'))
{'entry__count': 16}
ͨ���� aggregate ָ���ؼ��ֲ���������Կ��Ʒ��صľۺ����ƣ�

>>> q = Blog.objects.aggregate(number_of_entries=Count('entry'))
{'number_of_entries': 16}
Ҫ��������˽� aggregation����鿴 �ۺ�ָ��(the topic guide on Aggregation).

exists()

������ Django �������������ġ�
��� QuerySet ���������ݣ��ͷ��� True ����ͷ��� False��������������򵥵Ĳ�ѯ�����ˣ�������ȷ�����в�ѯ��ĳ�̶ֳ�������ζ��ʹ�� QuerySet.exists() �� bool(some_query_set) ���졣

�ֶ�ɸѡ����(Field lookups)

�ֶ�ɸѡ��������������ι��� SQL ����е� WHERE �Ӿ䡣���Ǳ�ָ��Ϊ QuerySet �� filter()��exclude() �� get() �����Ĺؼ��ֲ�����

Ҫ�˽��ⲿ�����ݣ����Բ鿴 �ֶβ�������(Field lookups) һ�ڡ�

exact

��ȷƥ�䡣���ָ����ֵ�� None���ͻᷭ��� SQL �е� NULL (������鿴 isnull )��

���磺

Entry.objects.get(id__exact=14)
Entry.objects.get(id__exact=None)
�ȼ۵� SQL��

SELECT ... WHERE id = 14;
SELECT ... WHERE id IS NULL;
�� Django 1.0 �����Ķ��� id__exact=None �������� Django 1.0 ���Ѿ������ı䡣֮ǰ���������� SQL �з���Ϊ WHERE id = NULL�����ǲ�ƥ���κ����ݡ���������������ȴ�� id__isnull=True һ����
MySQL ��ʾ

�� MySQL �У����ݱ�� "collation" ���þ����� exact �Ƚ��ǲ��Ǵ�Сд���еġ�����һ�����ݿ����ã�������һ�� Django ���á����Ը��� MySQL ���ݿ�����þ��ܾ����Ƿ�Դ�Сд���У����Ǿ���Ҫ��Ҫ��ô��������Ҫ����ʵ���������Ȩ�⿼�ǡ����ⷽ��ϸ�ڣ���鿴 ���ݿ�(databases) �ĵ��� collation section һ�ڡ�

iexact

���Դ�Сд��ƥ�䡣

���磺

Blog.objects.get(name__iexact='beatles blog')
�ȼ������� SQL ��

SELECT ... WHERE name ILIKE 'beatles blog';
Ҫע������ƥ�� 'Beatles Blog', 'beatles blog', 'BeAtLes BLoG'���ȵȡ�

SQLite �û�Ҫע��

��ʹ�� SQLite ��Ϊ���ݿ⣬����Ӧ�� Unicode (non-ASCII) �ַ���ʱ�����Ȳ鿴 database note �й����ַ����ȶ���һ�����ݡ�SQLite �� Unicode �ַ������޷������Դ�Сд��ƥ�䡣

contains

��Сд���еİ���ƥ�䡣

���磺

Entry.objects.get(headline__contains='Lennon')
�ȼ��� SQL ��

SELECT ... WHERE headline LIKE '%Lennon%';
Ҫע�⣬������佫ƥ������ 'Today Lennon honored' ��������ƥ�� 'today lennon honored'��

SQLite ��֧�ִ�Сд���е� LIKE ��䣻���Զ� SQLite ʹ�� contains ʱ�ͺ�ʹ�� icontains һ����

icontains

���Դ�Сд�İ���ƥ�䡣

���磺

Entry.objects.get(headline__icontains='Lennon')
�ȼ��� SQL��

SELECT ... WHERE headline ILIKE '%Lennon%';
SQLite �û���ע��

ʹ�� SQLite ���ݿⲢӦ�� Unicode (non-ASCII) �ַ���ʱ�����Ȳ鿴 database note �ĵ��й����ַ����ȶ���һ�����ݡ�

in

�Ƿ���һ���������б��С�

���磺

Entry.objects.filter(id__in=[1, 3, 4])
�ȼ��� SQL��

SELECT ... WHERE id IN (1, 3, 4);
��Ҳ���԰Ѳ�ѯ(queryset)���������̬���б��Ӷ�����̶����б�

inner_qs = Blog.objects.filter(name__contains='Cheddar')
entries = Entry.objects.filter(blog__in=inner_qs)
����̬�б�� queryset ����ʱ�ͻᱻ��Ϊһ���Ӳ�ѯ��

SELECT ... WHERE blog.id IN (SELECT id FROM ... WHERE NAME LIKE '%Cheddar%')
����Ĵ���Ҳ��������д��

inner_q = Blog.objects.filter(name__contains='Cheddar').values('pk').query
entries = Entry.objects.filter(blog__in=inner_q)
�� Django 1.1 �����з����ı䣺 �� Django 1.0 �У�ֻ�����һ�������ǿ��õġ�
Django 1.0 ���ִ�����ʽ����̫��Ȼ�������е��Ѷ����������������ڲ��� query ���ԣ�����Ҫ�õ� ValuesQuerySet�������Ĵ��벻��Ҫ���� Django 1.0����ôʹ�õ�һ����ʽ��ֱ�Ӵ���һ�� queryset �ͺá�

����㴫����һ�� ValuesQuerySet �� ValuesListQuerySet (�����ǵ��ò�ѯ���� values() �� values_list() �����ķ��ؽ��) ��Ϊ __in ������ֵ����ô��Ҫȷ��ֻƥ�䷵�ؽ���е�һ���ֶΡ����磬����Ĵ����������Ĺ���(�Բ������ƽ��й���)��

inner_qs = Blog.objects.filter(name__contains='Ch').values('name')
entries = Entry.objects.filter(blog__name__in=inner_qs)
����Ĵ���ȴ���׳��쳣��ԭ�����ڲ��Ĳ�ѯ�᳢��ƥ�������ֶ�ֵ����ֻ��һ�������õģ�

# Bad code! Will raise a TypeError.
inner_qs = Blog.objects.filter(name__contains='Ch').values('name', 'id')
entries = Entry.objects.filter(blog__name__in=inner_qs)
����

query ���Ա���һ�����������ڲ����ԣ���Ȼ��������Ĵ����й����úܺã���������API�ܿ��ܻ��ڲ�ͬ�� Django �汾�о����䶯��

���ܿ���

Ҫ����ʹ��Ƕ�ײ�ѯ������Ҫ���������õ����ݿ����������˽�(������˽⣬��ȥ��һ�����ܲ���)����Щ���ݿ⣬����������MySQL���Ͳ��ܺܺõ��Ż�Ƕ�ײ�ѯ������������İ����У����ڵ�һ����ѯ����ȡֵ�б�Ȼ���ٽ��䴫�ݸ��ڶ�����ѯ����������нϸߵ�������˵���ˣ�������������Ч�Ĳ�ѯ�滻��һ����Ч�Ĳ�ѯ��

values = Blog.objects.filter(
        name__contains='Cheddar').values_list('pk', flat=True)
entries = Entry.objects.filter(blog__in=values)
gt

���ڡ�

���磺

Entry.objects.filter(id__gt=4)
�ȼ��� SQL��

SELECT ... WHERE id > 4;
gte

���ڵ��ڡ�

lt

С�ڡ�

lte

С�ڵ��ڡ�

startswith

��Сд���е���....��ͷ��

���磺

Entry.objects.filter(headline__startswith='Will')
�ȼ��� SQL��

SELECT ... WHERE headline LIKE 'Will%';
SQLite ��֧�ִ�Сд���е� LIKE ��䣻������ SQLite ��ʹ�� startswith �ͺ�ʹ�� istartswith һ����

istartswith

���Դ�Сд����....��ͷ��

���磺

Entry.objects.filter(headline__istartswith='will')
�ȼ��� SQL��

SELECT ... WHERE headline ILIKE 'Will%';
SQLite �û���ע��

��ʹ�� SQLite ���ݿⲢӦ�� Unicode (non-ASCII) �ַ���ʱ�����Ȳ鿴 database note �ĵ����й��ַ����Ա���һ�е����ݡ�

endswith

��Сд���е���....��β��

���磺

Entry.objects.filter(headline__endswith='cats')
�ȼ��� SQL��

SELECT ... WHERE headline LIKE '%cats';
SQLite ��֧�ִ�Сд���е� LIKE ��䣻������ SQLite ��ʹ�� endswith ����ʹ�� iendswith һ����

iendswith

���Դ�Сд����....��β��

���磺

Entry.objects.filter(headline__iendswith='will')
�ȼ��� SQL��

SELECT ... WHERE headline ILIKE '%will'
SQLite users

��ʹ�� SQLite ���ݿ��Ӧ�� Unicode (non-ASCII) �ַ���ʱ�����Ȳ鿴 database note �ĵ����й��ַ����Ա���һ�����ݡ�

range

�����ķ�Χ��

���磺

start_date = datetime.date(2005, 1, 1)
end_date = datetime.date(2005, 3, 31)
Entry.objects.filter(pub_date__range=(start_date, end_date))
�ȼ��� SQL��

SELECT ... WHERE pub_date BETWEEN '2005-01-01' and '2005-03-31';
����԰� range ���� SQL �е� BETWEEN ���ã��������ڣ����֣��������ַ���

year

�����ڣ�ʱ���ֶξ�ȷƥ����֣��������λ���ֱ�ʾ��

���磺

Entry.objects.filter(pub_date__year=2005)
�ȼ��� SQL��

SELECT ... WHERE EXTRACT('year' FROM pub_date) = '2005';
(��ͬ�����ݿ������У�����õ��� SQL Ҳ������ͬ��)

month

�����ڣ�ʱ���ֶξ�ȷƥ���·֣���������ʾ�·֣����� 1 ��ʾһ�£�12 ��ʾʮ���¡�

���磺

Entry.objects.filter(pub_date__month=12)
�ȼ��� SQL��

SELECT ... WHERE EXTRACT('month' FROM pub_date) = '12';
(��ͬ�����ݿ������У�����õ��� SQL Ҳ������ͬ��)

day

�����ڣ�ʱ���ֶξ�ȷƥ�����ڡ�

���磺

Entry.objects.filter(pub_date__day=3)
�ȼ��� SQL��

SELECT ... WHERE EXTRACT('day' FROM pub_date) = '3';
(��ͬ�����ݿ������У�����õ��� SQL Ҳ������ͬ��)

Ҫע����ǣ����ƥ��ֻ��õ����� pub_date �ֶ������Ǳ�ʾ ĳ�µĵ����� �ļ�¼����һ�����ţ��������š���ʮ�¶�ʮ���žͲ��ڴ��С�

week_day

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
�����ڣ�ʱ���ֶ�ƥ�����ڼ�

���磺

Entry.objects.filter(pub_date__week_day=2)
�ȼ��� SQL��

SELECT ... WHERE EXTRACT('dow' FROM pub_date) = '2';
(��ͬ�����ݿ������У�����õ��� SQL Ҳ������ͬ��)

Ҫע����ǣ���δ��뽫�õ� pub_date �ֶ�������һ�����м�¼ (����ϰ���ڽ�����һ����һ�ܵĵڶ���)��������������Ϣ�޹ء���������������Ϊ��һ�죬����������Ϊ���һ�졣

isnull

���� SQL ��ѯ�ǿ� IS NULL ���Ƿǿ� IS NOT NULL��������Ӧ�� True �� False��

���磺

Entry.objects.filter(pub_date__isnull=True)
�ȼ��� SQL��

SELECT ... WHERE pub_date IS NULL;
search

����ȫ��������ȫ������������ contains ���ƣ���ʹ��ȫ�����������������һЩ��

���磺

Entry.objects.filter(headline__search="+Django -jazz Python")
�ȼ��ڣ�

SELECT ... WHERE MATCH(tablename, headline) AGAINST (+Django -jazz Python IN BOOLEAN MODE);
Ҫע����������������� MySQL ������Ҫ������ȫ��������Ĭ������� Django ʹ�� BOOLEAN MODE ģʽ����� Please check MySQL documentation for additional details.

regex

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
��Сд���е�������ʽƥ�䡣

��Ҫ�����ݿ�֧��������ʽ�﷨���� SQLite ȴû���ڽ�������ʽ֧�֣���� SQLite �������������һ����Ϊ REGEXP �� Python ����ʵ�ֵģ�����Ҫ�õ� Python ������� re.

���磺

Entry.objects.get(title__regex=r'^(An?|The) +')
�ȼ��� SQL��

SELECT ... WHERE title REGEXP BINARY '^(An?|The) +'; -- MySQL

SELECT ... WHERE REGEXP_LIKE(title, '^(an?|the) +', 'c'); -- Oracle

SELECT ... WHERE title ~ '^(An?|The) +'; -- PostgreSQL

SELECT ... WHERE title REGEXP '^(An?|The) +'; -- SQLite
����ʹ��ԭ���ַ��� (���磬�� r'foo' �滻 'foo') ��Ϊ������ʽ��

iregex

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
���Դ�Сд��������ʽƥ�䡣

ƥ�䣺

Entry.objects.get(title__iregex=r'^(an?|the) +')
�ȼ���SQL ��

SELECT ... WHERE title REGEXP '^(an?|the) +'; -- MySQL

SELECT ... WHERE REGEXP_LIKE(title, '^(an?|the) +', 'i'); -- Oracle

SELECT ... WHERE title ~* '^(an?|the) +'; -- PostgreSQL

SELECT ... WHERE title REGEXP '(?i)^(an?|the) +'; -- SQLite
�ۺϺ�ʽ(Aggregation Functions)

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
Django Ϊ������ django.db.models �� module ���ṩ��һϵ�еľۺϺ�ʽ��Ҫ��ϸ�˽����ʹ����Щ�ۺϺ�ʽ����鿴 the topic guide on aggregation��

Avg

class Avg(field)
���������ֶε�ƽ��ֵ��

Ĭ�ϱ�����<field>__avg
�������ͣ� float
Count

class Count(field, distinct=False)
���������Ĺ����ֶη��ر����� model ��������

Ĭ�ϱ����� <field>__count
�������ͣ� integer
����һ����ѡ������

distinct
��� distinct=True����ôֻ���ز��ظ���ʵ���������൱�� SQL �е� COUNT(DISTINCT field)��Ĭ��ֵ�� False��
Max

class Max(field)
���������ֶε����ֵ��

Ĭ�ϱ����� <field>__max
�������ͣ� �������ֶ�ֵ��ͬ
Min

class Min(field)
���������ֶε���Сֵ��

Ĭ�ϱ����� <field>__min
�������ͣ� �������ֶ���ͬ
StdDev

class StdDev(field, sample=False)
���������ֶ�ֵ�ı�׼�

Ĭ�ϱ����� <field>__stddev
�������ͣ� float
����һ����ѡ������

sample
Ĭ������£� StdDev ����һ������ƫ��ֵ��������� sample=True���򷵻�һ������ƫ��ֵ��
SQLite

SQLite �������ṩ StdDev ֧�֣�����ʹ�� SQLite ������ģ��ʵ��������ܡ�������鿴��Ӧ�� SQLite �ĵ����˽���λ�úͰ�װ��չ��

Sum

class Sum(field)
���������ֶ�ֵ���ܺ�

Ĭ�ϱ����� <field>__sum
�������ͣ� �������ֶ���ͬ
Variance

class Variance(field, sample=False)
���������ֶ�ֵ�ı�׼���

Ĭ�ϱ����� <field>__variance
�������ͣ� float
����һ����ѡ������

sample
Ĭ������£� Variance ���ص������巽���� sample=True�����ص�������ʽ���
SQLite

SQLite �������ṩ Variance ֧�֣�����ʹ�� SQLite ������ģ��ʵ��������ܡ�������鿴��Ӧ�� SQLite �ĵ����˽���λ�úͰ�װ��չ��