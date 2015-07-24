<!--
  ���ߣ�Github@wizardforcel
-->

# ��������ο� #

**class RelatedManager**

"����������"����һ�Զ���߶�Զ�Ĺ�����������ʹ�õĹ����������������������������

ForeignKey��ϵ�ġ���һ�ߡ�����������

```
from django.db import models

class Reporter(models.Model):
    # ...
    pass

class Article(models.Model):
    reporter = models.ForeignKey(Reporter)
```

������������У�������reporter.article_setӵ������ķ�����

ManyToManyField��ϵ�����ߣ�

```
class Topping(models.Model):
    # ...
    pass

class Pizza(models.Model):
    toppings = models.ManyToManyField(Topping)
```

��������У�topping.pizza_set ��pizza.toppings��ӵ������ķ�����

**add(obj1[, obj2, ...])**

��ָ����ģ�Ͷ�����ӵ����������С�

���磺

```
>>> b = Blog.objects.get(id=1)
>>> e = Entry.objects.get(id=234)
>>> b.entry_set.add(e) # Associates Entry e with Blog b.
```

������������У�����ForeignKey��ϵ��e.save()�ɹ������������ã�ִ�и��²�����Ȼ�����ڶ�Զ��ϵ��ʹ��add()����������κ� save()������������QuerySet.bulk_create()������ϵ���������Ҫ�ڹ�ϵ������ʱִ��һЩ�Զ�����߼��������m2m_changed�źš�

**create(\*\*kwargs)**

����һ���µĶ��󣬱�����󣬲�������ӵ���������֮�С������´����Ķ���

```
>>> b = Blog.objects.get(id=1)
>>> e = b.entry_set.create(
...     headline='Hello',
...     body_text='Hi',
...     pub_date=datetime.date(2005, 1, 1)
... )

# No need to call e.save() at this point -- it's already been saved.
```

����ȫ�ȼ��ڣ��������Ӽ���ڣ���

```
>>> b = Blog.objects.get(id=1)
>>> e = Entry(
...     blog=b,
...     headline='Hello',
...     body_text='Hi',
...     pub_date=datetime.date(2005, 1, 1)
... )
>>> e.save(force_insert=True)
```

Ҫע�����ǲ�����Ҫָ��ģ�������ڶ����ϵ�Ĺؼ��ʲ�����������������У����ǲ�û�д���blog������create()��Django�������µ� Entry����blog Ӧ����ӵ�b�С�

**remove(obj1[, obj2, ...])**

�ӹ����������Ƴ�ִ�е�ģ�Ͷ���

```
>>> b = Blog.objects.get(id=1)
>>> e = Entry.objects.get(id=234)
>>> b.entry_set.remove(e) # Disassociates Entry e from Blog b.
```

��add()���ƣ�����������У�e.save()�ɻ�ִ�и��²��������ǣ���Զ��ϵ�ϵ�remove()����ʹ��QuerySet.delete()ɾ����ϵ����˼�ǲ��������κ�ģ�͵���save()���������������һ����ϵ��ɾ��ʱִ���Զ���Ĵ��룬�����m2m_changed�źš�

����ForeignKey���������������null=Trueʱ���ڡ�����������ֶβ�������ΪNone (NULL)���������������ӵ���һ������֮ǰ�����Ƴ�������������������У���b.entry_set()�Ƴ�e�ȼ�����e.blog = None������blog��ForeignKeyû������null=True�������������Ч�ġ�

����ForeignKey���󣬸÷�������һ��bulk���������������ִ�в��������ΪTrue��Ĭ��ֵ����QuerySet.update()�ᱻʹ�á������bulk=False������ÿ��������ģ��ʵ���ϵ���save()��������ᴥ��pre_save��post_save�����ǻ�����һ�������ܡ�

**clear()**

�ӹ����������Ƴ�һ�ж���

```
>>> b = Blog.objects.get(id=1)
>>> b.entry_set.clear()
```

ע����������ɾ������ ���� ֻ��ɾ������֮��Ĺ�����

���� remove() ����һ����clear()ֻ���� null=True��ForeignKey�ϱ����ã�Ҳ���Խ���bulk�ؼ��ʲ�����

> ע��
> 
> ע������������͵Ĺ����ֶΣ�add()��create()��remove()��clear()�������ϸ������ݿ⡣���仰˵���ڹ������κ�һ�ˣ�������Ҫ�ٵ���save()������
> 
> ͬ����������ٶ�Զ��ϵ��ʹ�����м�ģ�ͣ�һЩ��������ķ����ᱻ���á�

## ֱ�Ӹ�ֵ ##

ͨ����ֵһ���µĿɵ����Ķ��󣬹������󼯿��Ա������滻����

```
>>> new_list = [obj1, obj2, obj3]
>>> e.related_set = new_list
```

��������ϵ����null=True�������������������new_list�е�����֮ǰ�����ȵ���clear()�����������������һ���Ѵ��ڶ���Ĺ��������� new_list�еĶ�������Ѵ��ڵĹ����Ļ����ϱ���ӡ�