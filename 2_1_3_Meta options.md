<!--
  ���ߣ�Github@wizardforcel
-->

# ģ��Ԫѡ�� #

��ƪ�ĵ����������п��õ�Ԫѡ����������ģ�͵�Meta�����������ǡ�

## ���õ�Ԫѡ�� ##

### abstract ###

**Options.abstract**

��� abstract = True�� �ͱ�ʾģ���� ������� (abstract base class).

### app_label ###

**Options.app_label**

������ģ�Ͷ�����Ĭ�ϵ� models.py ֮��(���磬�������õ�ģ���� myapp.models ��ģ�鵱��)���������� Django ��ģ�������ĸ�Ӧ�ã�

```
app_label = 'myapp'
```

```
Django 1.7��������

һ��Ӧ���У�������models ģ�������ģ�ͣ�������Ҫapp_label��
```

### db_table ###

**Options.db_table**

��ģ�����õ����ݱ�����ƣ�

```
db_table = 'music_album'
```

#### ���ݱ����� ####

Ϊ�˽�ʡʱ�䣬Django �����ģ��������ƺͰ�������app�����Զ�ָ�����ݱ����ƣ�һ��ģ�͵����ݱ����ƣ������ģ�͵ġ�Ӧ�ñ�ǩ������ manage.py startapp��ʹ�õ����ƣ�֮������»�����ɡ�

�ٸ����ӣ�  bookstoreӦ��(ʹ��  manage.py startapp bookstore ����)�������и���Ϊ Book��ģ�ͣ������ݱ�����ƾ���  bookstore_book ��

ʹ�� Meta���е� db_table ��������д���ݱ�����ơ�

���ݱ����ƿ����� SQL �����֣�Ҳ���԰�������������� Python �����е������ַ���������Ϊ Django ���Զ��������ͱ���������š�

> �� MySQL��ʹ��Сд��ĸΪ������
> 
> ����ͨ��db_table��д������ʱ��ǿ���Ƽ�ʹ��Сд��ĸ�����������ر������������MySQL��Ϊ��ˡ����MySQLע������ ��

> Oracle�б����Ƶ����Ŵ���
> 
> Ϊ�����Oracle��30���ַ������ƣ��Լ�һЩ������Լ����Django�����̱�����ƣ����һ����ȫ��תΪ��д����db_table��ֵ��������������������������
> 
```
db_table = '"name_left_in_lowercase"'
```
> 
> ���ִ����ŵ�����Ҳ��������Django��֧�ֵ��������ݿ��ˣ����ǳ���Oracle�����Ų����κ����á���� Oracle ע������ ��

### db_tablespace ###

**Options.db_tablespace**

��ǰģ����ʹ�õ����ݿ��ռ� �����֡�Ĭ��ֵ����Ŀ�����е�DEFAULT_TABLESPACE����������ڵĻ��������˲���֧�ֱ�ռ䣬���ѡ����Ժ��ԡ�

### default_related_name ###

**Options.default_related_name**

```
Django 1.8��������
```

������ֻ�Ĭ�ϱ�����һ���������󵽵�ǰ����Ĺ�ϵ��Ĭ��Ϊ <model_name>_set��

����һ���ֶεķ�ת����Ӧ����Ψһ�ģ���������ģ���������ʱ��Ҫ����С�ġ�Ϊ�˹�����Ƴ�ͻ�����Ƶ�һ����Ӧ�ú���'%(app_label)s'��'%(model_name)s'�����ǻᱻӦ�ñ�ǩ�����ƺ�ģ�͵������滻�����߶���Сд�ġ��������ģ�͵Ĺ������ơ�

### get_latest_by ###

**Options.get_latest_by**

ģ����ĳ����������ֶε����ƣ�����DateField��DateTimeField����IntegerField����ָ����Manager��latest()��earliest()��ʹ�õ�Ĭ���ֶΡ�

���磺

```
get_latest_by = "order_date"
```

���latest() �ĵ���

### managed ###

**Options.managed**

Ĭ��ΪTrue����˼��Django��migrate�����д������ʵ����ݱ����һ��� flush �����������Ƴ����ǡ����仰˵��Django�������Щ���ݱ���������ڡ�

�����False��Django �Ͳ���Ϊ��ǰģ�ʹ�����ɾ�����ݱ������ǰģ�ͱ�ʾһ���Ѿ����ڵģ�ͨ�������������������ݿ���ͼ�������ݱ�����൱���á���������Ϊmanaged=FalseʱΨһ�Ĳ�֮ͬ����. ģ�ʹ���������κη��涼��ƽ��һ�����������

+ ����㲻�������Ļ����������ģ�������һ������������Ϊ�˱��������Ĵ�����ߴ������ң�ǿ���Ƽ�����ʹ��δ�������ģ��ʱ��ָ�����ݱ������е��С�
+ ���һ������managed=False��ģ�ͺ���ָ������δ������ģ�͵�ManyToManyField����ô��Զ����ӵ��н��Ҳ���ᱻ���������ǣ�һ��������ģ�ͺ�һ��δ������ģ��֮����н��ᱻ������

�������Ҫ�޸���һĬ����Ϊ�������н����Ϊ��ʽ��ģ�ͣ�����Ϊmanaged��������ʹ��ManyToManyField.throughΪ����Զ���ģ�ʹ���������

���ڴ���managed=False��ģ�͵Ĳ��ԣ���Ҫȷ���ڲ�������ʱ������ȷ�ı�

�������޸�ģ������Python�������Ϊ����Ȥ����������� managed=False �����Ҵ���һ���Ѿ�����ģ�͵Ĳ��֡��������������ʹ�ô���ģ�Ͳ��Ǹ��õķ�����

### order_with_respect_to ###

**Options.order_with_respect_to**

���ո������ֶΰ����������Ϊ��������ġ�����һ����ͨ���õ������������棬ʹ���ڸ����������򡣱��磬���Answer�� Question�������һ������������һ���𰸣����Ҵ𰸵�˳��ǳ���Ҫ���������������

```
from django.db import models

class Question(models.Model):
    text = models.TextField()
    # ...

class Answer(models.Model):
    question = models.ForeignKey(Question)
    # ...

    class Meta:
        order_with_respect_to = 'question'
```

��order_with_respect_to ����֮��ģ�ͻ��ṩ�����������úͻ�ȡ��������˳��ķ�����get_RELATED_order() ��set_RELATED_order()������RELATED��Сд��ģ�����ơ����磬����һ�� Question �����кܶ��������Answer���󣬷��ص��б��к��������Answer�����������

```
>>> question = Question.objects.get(id=1)
>>> question.get_answer_order()
[1, 2, 3]
```

��Question�����������Answer�����˳�򣬿���ͨ������һ�����Answer �������б������ã�

```
>>> question.set_answer_order([3, 1, 2])
```

������Ķ���Ҳ������������ get_next_in_order() ��get_previous_in_order()�����ڰ��պ��ʵ�˳��������ǡ�����Answer������ id������

```
>>> answer = Answer.objects.get(id=2)
>>> answer.get_next_in_order()
<Answer: 3>
>>> answer.get_previous_in_order()
<Answer: 1>
```

> �޸� order_with_respect_to
> 
> order_with_respect_to���Ի����һ��������ֶΣ�/���ݱ��е��У�����_order��������������״�Ǩ��֮����ӻ����޸���order_with_respect_to���ԣ�Ҫȷ��ִ�к�Ӧ���˺��ʵ�Ǩ�Ʋ�����

### ordering ###

**Options.ordering**

����Ĭ�ϵ�˳�򣬻�ȡһ��������б�ʱʹ�ã�

```
ordering = ['-order_date']
```

����һ���ַ������б��Ԫ�顣ÿ���ַ�����һ���ֶ�����ǰ����п�ѡ�ġ�-��ǰ׺��ʾ����ǰ��û�С�-�����ֶα�ʾ����ʹ��"?"����ʾ�������

���磬Ҫ����pub_date�ֶε�������������д��

```
ordering = ['pub_date']
```

����pub_date�ֶεĵ�����������д��

```
ordering = ['-pub_date']
```

�Ȱ���pub_date�ĵ��������ٰ��� author ��������������д��

```
ordering = ['-pub_date', 'author']
```

> ����
> 
> ���򲢲���û���κδ��۵Ĳ���������ordering������ӵ�ÿ���ֶζ�����������ݿ�Ŀ���������ӵ�ÿ�����Ҳ����ʽ��������Ĭ��˳��

### permissions ###

**Options.permissions**

���ô�������ʱȨ�ޱ��ж����Ȩ�ޡ����ӡ�ɾ�����޸�Ȩ�޻��Զ�Ϊÿ��ģ�ʹ������������ָ����һ�ֶ����Ȩ�ޣ�can_deliver_pizzas��

```
permissions = (("can_deliver_pizzas", "Can deliver pizzas"),)
```

����һ��������Ԫ���Ԫ������б���ʽΪ (permission_code, human_readable_permission_name)��

### default_permissions ###

**Options.default_permissions**

```
Django 1.7��������
```

Ĭ��Ϊ('add', 'change', 'delete')��������Զ�������б����磬������Ӧ�ò���ҪĬ��Ȩ���е��κ�һ����԰������óɿ��б���ģ�ͱ�migrate�����֮ǰ��������Ա��뱻ָ�����Է�һЩ��©�����Ա�������

### proxy ###

**Options.proxy**

���proxy = True, ��Ϊ��ģ���������һ��ģ�ͻᱻ��Ϊ����ģ�͡�

### select_on_save ###

**Options.select_on_save**

��ѡ�������Django�Ƿ����1.6֮ǰ�� django.db.models.Model.save()�㷨���ɵ��㷨ʹ��SELECT���ж��Ƿ������Ҫ���µ��С�����ʽ���㷨ֱ�ӳ���ʹ�� UPDATE����һЩС���ʵ�����У�һ���Ѵ��ڵ��е�UPDATE����������Django�ɼ�������PostgreSQL��ON UPDATE�������᷵��NULL����������£���ʽ���㷨�������ִ�� INSERT ��������ʹ��һ���Ѿ������ݿ��д��ڡ�

ͨ��������Բ���Ҫ���á�Ĭ��ΪFalse��

���ھ�ʽ����ʽ�����㷨����μ�django.db.models.Model.save()��

### unique_together ###

**Options.unique_together**

�������õĲ��ظ����ֶ���ϣ�

```
unique_together = (("driver", "restaurant"),)
```

����һ��Ԫ���Ԫ�飬���������ʱ�������Ψһ�ġ�����Django��̨�б�ʹ�ã������ݿ����Լ������(���磬��  CREATE TABLE  ����а���  UNIQUE���)��

Ϊ�˷������������һ�ֶεļ���ʱ��unique_together ������һά��Ԫ�飺

```
unique_together = ("driver", "restaurant")
```

ManyToManyField���ܰ�����unique_together�С�������ζ��ʲô������������������Ҫ��֤ManyToManyField������Ψһ�ԣ�����ʹ���źŻ�����ʽ�Ĺᴩģ��(explicit through model)��

```
Django 1.7���޸ģ�
��unique_together��Լ����Υ��ʱ��ģ��У���ڼ���׳�ValidationError�쳣��
```

### index_together ###

**Options.index_together**

�������ô����������ֶ���ϣ�

```
index_together = [
    ["pub_date", "deadline"],
]
```

�б��е��ֶν��Ὠ�����������磬����CREATE INDEX����б�ʹ�ã���

```
Django 1.7���޸ģ�
```

Ϊ�˷������������һ�ֶεļ���ʱ��index_together������һ��һά���б�

```
index_together = ["pub_date", "deadline"]
```

### verbose_name ###

**Options.verbose_name**

�����һ�������������ƣ�Ϊ������

```
verbose_name = "pizza"
```

�������û�����ã�Django���������ֿ�����Ϊ������������CamelCase ����camel case��

### verbose_name_plural ###

**Options.verbose_name_plural**

�ö�������ʽ�����ƣ�

```
verbose_name_plural = "stories"
```

�������û�����ã�Django ��ʹ�� verbose_name + "s"��