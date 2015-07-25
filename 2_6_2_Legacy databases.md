<!--
  ���ߣ�Github@wizardforcel
-->

# ���������ݿ����ϵ�Django #

��ȻDjango���ʺ����������µ�Ӧ�ã���Ҳ���Խ������ϵ����������ݿ��С�Django�����˺ܶ๤�ߣ��������Զ�������������⡣

��ƪ���¼������˽�Django�Ļ������֣������ڽ̳����ἰ��

һ�����Django����������֮������԰���������µ����̣���������������ݿ⡣

## ��Django�ṩ������ݿ���� ##

����Ҫ����Django������ݿ����Ӳ������Լ����ݿ�����ơ����޸�DATABASES���ã�Ϊ'Ĭ��' ���ӵ����¼���ֵ��

+ NAME
+ ENGINE
+ USER
+ PASSWORD
+ HOST
+ PORT

## �Զ�����ģ�� ##

Django�Դ�����inspectdb�Ĺ��ߣ����԰������е����ݿⴴ��ģ�͡��������������������鿴�����

```
$ python manage.py inspectdb
```

ͨ���ض���Unix��׼������������ļ���

```
$ python manage.py inspectdb > models.py
```

���������һ����ݷ�ʽ��������һ��ȷ����ģ�������������inspectdb�ĵ� ��

һ���㴴���������ģ�ͣ����ļ�����Ϊmodels.py��Ȼ������ŵ���Ӧ�õ�Python���С�Ȼ���Ӧ����ӵ����INSTALLED_APPS �����С�

Ĭ������£�inspectdb����δ�������ģ�͡������˵��ģ�͵�Meta���е�managed = False����Django��Ҫ����ÿ����Ĵ������޸ĺ�ɾ����

```
class Person(models.Model):
    id = models.IntegerField(primary_key=True)
    first_name = models.CharField(max_length=70)
    class Meta:
       managed = False
       db_table = 'CENSUS_PERSONS'
```

�����ϣ��Django�������������ڣ�����Ҫ��managedѡ���Ϊ True�����߼򵥵ذ����Ƴ�����ΪTrue��Ĭ��ֵ����

## ��װDjango���ı� ##

������������migrate��������װ��������Ķ�������ݿ��¼�������̨Ȩ�޺��������ͣ�

```
$ python manage.py migrate
```

## ���Ժ͵��� ##

����������л����Ĳ����� ���� ��ĿǰΪֹ�����Ҫ����Django�Զ����ɵ�ģ�ͣ�ֱ�����ǰ�������Ҫ�ķ�ʽ����������ͨ��Django���ݿ�API����������ݣ����ҳ���ʹ��Django��̨ҳ��༭�����Լ���Ӧ�ر༭ģ���ļ���