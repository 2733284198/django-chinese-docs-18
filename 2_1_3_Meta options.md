<!--
  ���ߣ�WrongWay [www.wrongway.me]
-->

# Ԫѡ�� #

## abstract ##

**Options.abstract**

Ϊ True�� �ͱ�ʾ model �� ������� (abstract base class).

## app_label##

**Options.app_label**

������ model ������Ĭ�ϵ� models.py ֮��(���磬�������õ� model �� myapp.models ��ģ�鵱��)���������� Django �� model �����ĸ�Ӧ�ã�

```
app_label = 'myapp'
db_table
```

**Options.db_table**

�� model ���õ����ݱ�����ƣ�

```
db_table = 'music_album'
```

## ���ݱ����� ##

Ϊ�˽�ʡʱ�䣬Django ���Զ�ָ�����ݱ����ƣ���������Ӧ�����ƵĽ�β��һ���»��ߣ��ټӸ� model �����ơ�

�ٸ����ӣ� bookstore Ӧ��(ʹ�� manage.py startapp bookstore ����)�������и���Ϊ Book �� model �������ݱ�����ƾ��� bookstore_book ��

���ݱ����ƿ����� SQL �����֣�Ҳ���԰�������������� Python �����е������ַ�(�������ַ�)��������Ϊ Django ���Զ��������ͱ���������š�

## db_tablespace ##

**Options.db_tablespace**

�ⲿ������ Django 1.0 �����ģ� ��鿴�汾�ĵ�
�� model ���õı�ռ䡣������ݿⲻ֧�ֱ�ռ䣬Django �ͻ���Ը�ѡ�

## get_latest_by ##

**Options.get_latest_by**

model ��ĳ�� DateField �� DateTimeField �����ƣ��� model �� Manager ��ʹ�� latest ����ʱҪ������Ϊ�����ֶΡ�

���磺

```
get_latest_by = "order_date"
```

��� latest() ��

## managed ##

**Options.managed**

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
Ĭ��ֵΪ True������ζ�Ÿ� model ������ syncdb �� reset �������������Ƴ���Ӧ�����ݱ����仰˵��Django ���������ݱ���������ڡ�

����� False��Django �Ͳ���Ϊ��ǰ model ������ɾ�����ݱ�ͨ������ model Ҫ��ʾĳ���Ѵ��ڵ����ݱ������ͼ�ĳ��ϡ�ʹ�÷��й� model (managed = False)����ͨ model ���������ڣ�

�����û�����������ֶΣ��͵��� model ���ֶ����һ�����������ֶΡ�Ϊ���ú����ĳ���Ա���Ķ�����ʱ��������⣬���������й� model �ж����ݱ��е����е��ֶζ����ж��塣

����������й� model ֮�� (managed=False) ʹ�� ManyToManyField ��������Ͳ��ᴴ���洢��Զ��ϵ���м��������ͨ model �ͷ��й� model ֮��Ķ�Զ��ϵ��Ȼ�ᴴ���м��

�����Ҫ����Ĭ�ϵ���Ϊ���͵���ʽ�����н� model �������м��(�� model Ҫ����managed=True)��Ȼ�������Դ model ���� ManyToManyField.through ָ���н� model ������ʵ�ֶ��ƵĶ�Զ��ϵ��

�����Ĳ��԰������й� model (managed=False)����ô�ڲ���֮ǰ��Ҫȷ�����Ѿ���������ȷ�����ݱ�

���������� model ����ĳ�� Python �㼶����Ϊ��������� managed=False ��Ȼ�󴴽� model �Ŀ������ڿ����ж����µ���Ϊ�������и����õİ취������ʹ�� ���� model (Proxy models).

## order_with_respect_to ##

**Options.order_with_respect_to**

���ݸ������ֶζ� model �����ڹ�����ϵ�У����������ڸ���Ŀ������Դ��������ĳ��ϡ��ٸ����ӣ�һ�� Answer ֻ����һ�� Question ���󣬶�һ�� question ����ȴ���Թ������ answer���󡣸��� question �� answer ����

```
class Answer(models.Model):
    question = models.ForeignKey(Question)
    # ...

    class Meta:
        order_with_respect_to = 'question'
ordering
```

**Options.ordering**

�ö����Ĭ��������������˶����б������

```
ordering = ['-order_date']
```

������һ���ַ���Ԫ����б�������ַ���ǰ����һ��"-"���ţ��ͱ�ʾ�������С�û��"-"���ţ��ͱ�ʾ�������С���һ��"?"�ʺţ��ͱ�ʾ�������

> ע��
> 
> ���� ordering ���ж����ֶΣ�Django �����ֻ̨ʹ�õ�һ���ַ�����

�ٸ����ӣ�Ҫ���� pub_date �ֶ����������У�ʹ�ã�

```
ordering = ['pub_date']
```

���� pub_date �ֶ����������У�ʹ�ã�

```
ordering = ['-pub_date']
```

�ȸ��� pub_date �����ٸ��� author ����ʹ�ã�

```
ordering = ['-pub_date', 'author']
```

## permissions ##

**Options.permissions**

�ڴ�������ʱ����ӵ�Ȩ�ޱ��еĸ���Ȩ����Ϣ��Django �Զ�Ϊÿ�������� admin �Ķ��󴴽�����ӣ�ɾ�����޸ĵ�Ȩ�ޡ������������չʾ��������һ�����ӵ�Ȩ�� can_deliver_pizzas ��

```
permissions = (("can_deliver_pizzas", "Can deliver pizzas"),)
```

��������Ƕ�Ԫ�飬Ҳ�������б� (permission_code, human_readable_permission_name) ��

## proxy ##

**Options.proxy**

�ⲿ������ Django 1.1 �������ģ� ��鿴�汾�ĵ�
�����Ϊ True����ʾ�� model �Ǹ���� ���� model (proxy model) ��

## unique_together ##

**Options.unique_together**

�������õĲ��ظ����ֶ���ϣ�

```
unique_together = (("driver", "restaurant"),)
```

����һ���ֶ����Ƶ��б��б��ڵ��ֶ���������ݿ�����Ψһ�����ظ��ģ�Ҳ����˵�����������������������б��е��ֶ�ֵ����ȫ��ͬ�ġ��������� Django �Ĺ����̨�������ݿ�㼶Լ�����ݡ�(���磬�� CREATE TABLE ����а��� UNIQUE ���)

�ⲿ������ Django 1.0 �������ģ� ��鿴�汾�ĵ�
Ϊ��ʹ�÷��㣬����Ը�������һ���������ֶ��б����ʾ�б���ÿ���ֶε�ֵ��������ȫ��Ψһ�ģ�

```
unique_together = ("driver", "restaurant")
```

## verbose_name ##

**Options.verbose_name**

�������ͱ����Ķ�������--������ʽ����������

```
verbose_name = "pizza"
```

���û�и�ֵ��Django ���ø� model ���Ƶķִ���ʽ��Ϊ�������� CamelCase ��� camel case��

## verbose_name_plural ##

**Options.verbose_name_plural**

�������ĸ�����ʽ��

```
verbose_name_plural = "stories"
```

���û�и�ֵ��Django ʹ�� verbose_name + "s" ��Ϊ�������ĸ�����ʽ��