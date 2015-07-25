<!--
  ���ߣ�Github@wizardforcel
-->

# Ϊģ���ṩ��ʼ���� #

�����״ν���һ��Ӧ�õ�ʱ��Ϊ������ݿ�Ԥ�Ȱ�װһЩӲ��������ݣ��Ǻ����ô��ġ� �м��ַ���������Django�Զ�������Щ���ݣ������ͨ��fixtures�ṩ��ʼ���ݣ������ṩһ��������ʼ���ݵ�sql�ļ���

ͨ��������ʹ��fixtrue���Ӽ�࣬��Ϊ�������ݿ��޹صģ���ʹ��sql��ʼ��������

## �ṩ��ʼ���ݵ�fixtures ##

fixture�����ݵļ��ϣ���Django�˽���ε��뵽���ݿ��С�����fixture����ֱ�ӵķ�ʽ����ʹ��manage.py dumpdata���������ݿ����Ѿ�����һЩ���ݡ������������дfixtures��fixtures֧��JSON��XML����YAML����Ҫ��װPyYAML���ĵ������л��ĵ�����ϸ������ÿһ����֧�ֵ����л���ʽ��

�����������չʾ��һ���򵥵�Person ģ�͵�fixtrue������������JSON��

```
[
  {
    "model": "myapp.person",
    "pk": 1,
    "fields": {
      "first_name": "John",
      "last_name": "Lennon"
    }
  },
  {
    "model": "myapp.person",
    "pk": 2,
    "fields": {
      "first_name": "Paul",
      "last_name": "McCartney"
    }
  }
]
```

����������YAML��ʽ��

```
- model: myapp.person
  pk: 1
  fields:
    first_name: John
    last_name: Lennon
- model: myapp.person
  pk: 2
  fields:
    first_name: Paul
    last_name: McCartney
```

����԰���Щ���ݴ�������Ӧ�õ�fixturesĿ¼�С�

�������ݺܼ򵥣�ֻҪ����manage.py loaddata &lt;fixturename&gt;�ͺ��ˣ�����&lt;fixturename&gt;������������fixture�ļ������֡�ÿ��������loaddata��ʱ�����ݶ����fixture�����������ظ����ؽ����ݿ⡣ע������ζ�ţ�������޸���fixtrue������ĳһ�У�Ȼ���ٴ������� loaddata������޸Ľ��ᱻĨ����

## �Զ����س�ʼ���ݵ�fixtures ##

```
1.7�зϳ���

���һ��Ӧ��ʹ����Ǩ�ƣ��������Զ�����fixtures������Django 1.9�У�Ǩ�ƽ����Ǳ�Ҫ�ģ���һ��Ϊ��Ȩ��֮�󱻷ϳ��� ���������һ��Ӧ���м��س�ʼ���ݣ�����������Ǩ���м������ǡ�
```

����㴴����һ������Ϊ initial_data.[xml/yaml/json]��fixtrue������ÿ������migrate����ʱ��fixtrue���ᱻ���ء���ǳ����棬����Ҫע�⣺��ס��������ÿ������migrate����󶼻ᱻˢ�¡�So don��t use initial_data for data you��ll want to edit.

## Django������Ѱ��fixture�ļ� ##

ͨ����Django ��ÿ��Ӧ�õ�fixturesĿ¼��Ѱ��fixture�ļ������������FIXTURE_DIRSѡ��Ϊһ������Ŀ¼���б�Django�������Ѱ�ҡ�

����manage.py loaddata�����ʱ����Ҳ����ָ��һ��fixture�ļ���Ŀ¼�����Ḳ��Ĭ�������е�Ŀ¼��

> ���
> 
> fixtruesҲ�����ڲ��Կ�����һ���ԵĲ��Ի�����

## �ṩ��ʼSQL���� ##

```
1.7�зϳ���

���һ��Ӧ��ʹ��Ǩ�ƣ���ʼSQL���ݽ�������أ���������ض���SQL���ݣ�������Django 1.9�У�Ǩ�ƽ����Ǳ���ģ���һ��Ϊ��Ȩ��󱻷ϳ������������Ӧ����ʹ�ó�ʼSQL���ݣ�����������Ǩ����ʹ�����ǡ�
```

DjangoΪ���ݿ��޹ص�SQL�ṩ��һ�����ӣ���������migrate����ʱ��CREATE TABLE���ִ��֮��ͻ�ִ�����������ʹ���������������Ĭ�ϵļ�¼�����ߴ���SQL��������ͼ���������Լ�������

����ʮ�ּ򵥣�Django������Ӧ�õ�Ŀ¼��Ѱ�ҽ���sql/&lt;modelname&gt;.sql���ļ������� &lt;modelname&gt;��Сд��ģ�����ơ�

���������myappӦ���д���Personģ�ͣ���Ӧ����myappĿ¼���ļ�sql/person.sql��������ݿ��޹ص�SQL�����������չʾ���ļ����ܻ����ʲô��

```
INSERT INTO myapp_person (first_name, last_name) VALUES ('John', 'Lennon');
INSERT INTO myapp_person (first_name, last_name) VALUES ('Paul', 'McCartney');
```

ÿ���ṩ��SQL�ļ�����Ӧ�ú������ڲ������ݵ���Ч��SQL��䣨���磬��ʽ�ʵ���INSERT��䣬�÷ֺŷָ�����

��ЩSQL�ļ��ɱ�manage.py�е� sqlcustom��sqlall�����Ķ������manage.py�ĵ���

ע��������кܶ�SQL�����ļ�������ִ�е�˳���ǲ�ȷ���ġ�Ψһ����ȷ�����ǣ�������Զ��������ļ���ִ��֮ǰ���������ݱ����������ˡ�

> ��ʼSQL���ݺͲ���
> 
> ��һ���ɲ����Բ���Ŀ�������ṩ��ʼ���ݡ�Django�Ĳ��Կ����ÿ�β��Ժ󶼻�ˢ�²������ݿ�����ݡ����ԣ��κ�ʹ���Զ���SQL������ӵ����ݶ��ᶪʧ��
> 
> �������Ҫ�ڲ���������������ݣ���Ӧ���ڲ���fixture��������������ڲ���������setUp()����ӡ�


## ���ݿ����ض���SQL���� ##

û�й����ṩ������ض���SQL���ݡ����磬���зֱ�ΪPostgreSQL��SQLite׼���ĳ�ʼ�����ļ�������ÿ��Ӧ�ã�Django����Ѱ�ҽ���&lt;app_label&gt;/sql/&lt;modelname&gt;.&lt;backend&gt;.sql���ļ�������&lt;app_label&gt;��Сд��ģ�����ƣ�&lt;modelname&gt;��Сд��ģ�����ƣ�&lt;backend&gt;����������ļ�����ENGINE�ṩ��ģ�����Ƶ����һ���֣����磬����㶨����һ�����ݿ⣬ENGINE��ֵΪdjango.db.backends.sqlite3��Django��Ѱ��&lt;app_label&gt;/sql/&lt;modelname&gt;.sqlite3.sql����

����ض���SQL���ݻ����ں���޹ص�SQL����ִ�С����磬������Ӧ�ð�����sql/person.sql ��sql/person.sqlite3.sql�ļ����������Ѿ���װ��SQLiteӦ�ã�Django������ִ�� sql/person.sqlite3.sql�����ݣ���β���sql/person.sql��