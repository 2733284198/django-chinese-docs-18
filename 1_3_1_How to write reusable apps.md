<!--
  ��Դ��http://python.usyiyi.cn/django/index.html
-->

# �߼��̳̣���α�д�����õ�Ӧ�� #

���߼��̳��Ͻӽ̳� 6�����ǽ������ǵ���ҳͶƱת����һ��������Python���������������������Ŀ�����û��߷���������ˡ�

��������û����ɽ̳�1�C6�����ǽ������Ķ�����ʹ�����ʾ����Ŀ��������������ƥ�䡣

## �����ú���Ҫ ##

��ơ����������Ժ�ά��һ����ҳӦ������๤��Ҫ�������Python �� Django ��Ŀ���г����Ĺ�ͬ���⡣������ǿ��Խ�ʡһЩ��Щ�ظ��Ĺ����᲻��ܰ���

����������Python ��һ�������̬�ȡ�Python������ (PyPI) ���й㷺�İ�������������Լ���Python������ʹ�á�����һ��Django Packages���Ѿ����ڵĿ����õ�Ӧ�ã�����Խ�����ǵ������Ŀ��Django ����Ҳֻ��һ��Python ��������ζ������Ի�ȡ�Ѿ����ڵ�Python����DjangoӦ�ò��������ںϵ����Լ�����ҳ��Ŀ����ֻ��Ҫ��д����Ŀ�Ķ��صĲ��֡�

����˵�������ڿ�ʼһ���µ���Ŀ����Ҫһ�����������ڱ�д��ͶƱӦ�á�������ø�Ӧ�ÿ����ã����˵��ǣ����Ѿ�����ȷ�ĵ�·�ϡ��ڽ̳� 3�У����ǿ������ǿ������ʹ��include��ͶƱӦ�ô���Ŀ�����URLconf ����ڱ��̳��У����ǽ�����һ���������Ӧ�����µ���Ŀ�����׵�ʹ�ò���ʱ���Է����������˰�װ��ʹ�á�

> ����Ӧ�ã�
> 
> Python �� �ṩ�ķ�ʽ�Ƿ�����ص�Python ���������׵����á�һ��������һ������Python���루Ҳ������ģ�顱����
> 
> ������ͨ��import foo.bar ��from foo import bar ���롣���һ��Ŀ¼������polls����Ҫ�γ�һ���������������һ��������ļ�__init__.py����ʹ����ļ�Ϊ�ա�
> 
> һ��Django Ӧ�� ֻ��һ��Python��������������Django��Ŀ�С�һ��Ӧ�ÿ���ʹ�ó�����Django Լ�����������models��tests��urls��views ��ģ�顣
> 
> ��������ʹ�ô���������������һ��Python����������������ڰ�װ�Ĺ��̡�����֪����������е����ˡ�

## �����Ŀ����Ŀ����õ�Ӧ�� ##

����ǰ��Ľ̳�֮�����ǵ���ĿӦ�ÿ���ȥ��������

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
    polls/
        __init__.py
        admin.py
        migrations/
            __init__.py
            0001_initial.py
        models.py
        static/
            polls/
                images/
                    background.gif
                style.css
        templates/
            polls/
                detail.html
                index.html
                results.html
        tests.py
        urls.py
        views.py
    templates/
        admin/
            base_site.html
```

���ڽ̳� 2�д�����mysite/templates ���ڽ̳� 3�д�����polls/templates�� ��������ܸ�������Ϊʲô����Ϊ��Ŀ��Ӧ��ѡ�񵥶���ģ��Ŀ¼������ͶƱӦ�õĲ���ȫ����polls�С���ʹ�ø�Ӧ���԰����Ҹ������׶���һ���µ���Ŀ�С�

���ڿ��Կ���pollsĿ¼��һ���µ�Django��Ŀ������ʹ�á�Ȼ���������ܳ��׼���õ���������������������㣬������Ҫ������Ӧ�������������������ڰ�װ��

## ��װһЩǰ������ ##

Python �����Ŀǰ״̬��Ϊ�ж��ֹ��߶����Ҳ��������ڱ��̳̣����Ǵ���ʹ��setuptools���������ǵİ��������Ƽ��Ĵ�����ߣ��Ѿ���distribute ��֧�ϲ��������ǻ���ʹ��pip����װ��ж������������Ӧ�ð�װ�����������������Ҫ����������Բο����ʹ��pip��װDjango�������ʹ��ͬ���ķ�����װsetuptools��

## ������Ӧ�� ##

Python packaging refers to preparing your app in a specific format that can be easily installed and used. Django �Լ����Էǳ����Ƶķ�ʽ��������ġ�����һ����polls������СӦ�ã�������̲���̫�ѡ�

���ȣ������Django��Ŀ֮�⣬Ϊpolls����һ����Ŀ¼�������Ŀ¼Ϊdjango-polls��

> Ϊ���Ӧ��ѡ��һ������
> 
> ��Ϊ��İ�ѡ��һ������ʱ�����һ��PyPI�е���Դ�Ա������Ѿ����ڵİ������ֳ�ͻ��������һ��Ҫ�����İ�ʱ�������ģ������ǰ�����django-ͨ�������á� ���������������ڲ���DjangoӦ�õ����������Ӧ����ר������Django�ġ�
> 
> Ӧ�õı�ǩ��Ӧ�õİ��ĵ��·������󲿷֣���INSTALLED_APPS�б���Ψһ������ʹ����Django��contrib �� ���κ�һ��ʹ����ͬ�ı�ǩ������auth��admin��messages��

��polls Ŀ¼�ƶ���django-pollsĿ¼��

����һ������һЩ���ݵ��ļ�django-polls/README.rst��

```
django-polls/README.rst
=====
Polls
=====

Polls is a simple Django app to conduct Web-based polls. For each
question, visitors can choose between a fixed number of answers.

Detailed documentation is in the "docs" directory.

Quick start
-----------

1. Add "polls" to your INSTALLED_APPS setting like this::

    INSTALLED_APPS = (
        ...
        'polls',
    )

2. Include the polls URLconf in your project urls.py like this::

    url(r'^polls/', include('polls.urls')),

3. Run `python manage.py migrate` to create the polls models.

4. Start the development server and visit http://127.0.0.1:8000/admin/
   to create a poll (you'll need the Admin app enabled).

5. Visit http://127.0.0.1:8000/polls/ to participate in the poll.
```

����һ��django-polls/LICENSE�ļ���ѡ��License�������̵̳ķ�Χ����ֵ��һ˵���ǹ��������Ĵ������û��License�Ǻ����ô��ġ�Django�������Django���ݵ�Ӧ����BSD License ������Ȼ��������������ѡ�Լ���License��ֻ��Ҫ֪�����License��ѡ��Ӱ��˭�ܹ�ʹ����Ĵ��롣

��һ�����ǽ�����һ��setup.py �ļ������ṩ��ι����Ͱ�װ��Ӧ�õ���ϸ��Ϣ�����ļ������Ľ��ͳ������̵̳ķ�Χ��setuptools �ĵ� �кܺõĽ��͡�����һ���ļ�django-polls/setup.py�����������£�

```
django-polls/setup.py
import os
from setuptools import setup

with open(os.path.join(os.path.dirname(__file__), 'README.rst')) as readme:
    README = readme.read()

# allow setup.py to be run from any path
os.chdir(os.path.normpath(os.path.join(os.path.abspath(__file__), os.pardir)))

setup(
    name='django-polls',
    version='0.1',
    packages=['polls'],
    include_package_data=True,
    license='BSD License',  # example license
    description='A simple Django app to conduct Web-based polls.',
    long_description=README,
    url='http://www.example.com/',
    author='Your Name',
    author_email='yourname@example.com',
    classifiers=[
        'Environment :: Web Environment',
        'Framework :: Django',
        'Intended Audience :: Developers',
        'License :: OSI Approved :: BSD License', # example license
        'Operating System :: OS Independent',
        'Programming Language :: Python',
        # Replace these appropriately if you are stuck on Python 2.
        'Programming Language :: Python :: 3',
        'Programming Language :: Python :: 3.2',
        'Programming Language :: Python :: 3.3',
        'Topic :: Internet :: WWW/HTTP',
        'Topic :: Internet :: WWW/HTTP :: Dynamic Content',
    ],
)
```

Ĭ��ֻ��Pythonģ��Ͱ�����������С������Ҫ����������ļ���������Ҫ����һ��MANIFEST.in�ļ�����һ���ᵽ��setuptools �ĵ�������ļ��и���ϸ�����ۡ����Ҫ����ģ�塢README.rst�����ǵ�LICENSE �ļ�������һ���ļ�django-polls/MANIFEST.in�����������£�

```
django-polls/MANIFEST.in
include LICENSE
include README.rst
recursive-include polls/static *
recursive-include polls/templates *
```

����ϸ���ĵ����������Ӧ���У����ǿ�ѡ�ģ���������������������һ���յ�Ŀ¼django-polls/docs���ڽ�������ĵ�����django-polls/MANIFEST.in�������һ�У�

```
recursive-include docs *
```

ע��docs�����������İ��г��������һЩ�ļ��������档���DjangoӦ�û�ͨ������readthedocs.org������վ���ṩ���ǵ������ĵ�.

����ͨ��python setup.py sdist ������İ�����django-polls���ڲ����У����ⴴ��һ��distĿ¼������һ���°�django-polls-0.1.tar.gz��

������ڴ������Ϣ���μ�Python �� ����ͷַ���Ŀ�Ľ̡̳�

## ʹ�����Լ��İ� ##

��Ϊ�����ǽ�polls Ŀ¼�Ƶ���Ŀ��Ŀ¼֮�⣬�����ٹ����ˡ����ǽ�ͨ����װ���ǵ��µ�django-polls�����޸�����

> ��װ��ĳ���û��Ŀ�
> 
> ���µĲ��轫��װdjango-polls ��ĳ���û��Ŀ⡣�����û���װ���ϵͳ��Χ�İ�װ��������ŵ㣬��������û�й���ԱȨ�޵�ϵͳ���Լ���ֹ��İ�Ӱ��ϵͳ�ķ���ͻ����ϵ������û���
> 
> ע������û��İ�װ��Ȼ����Ӱ���Ը��û�������е�ϵͳ���ߣ�����virtualenv �Ǹ���׳�Ľ���취�������ģ���

��װ�������ʹ��pip�����Ѿ���װ�����ˣ��԰ɣ�����

```
pip install --user django-polls/dist/django-polls-0.1.tar.gz
```

������ˣ����Django ��Ŀ����Ӧ�ÿ����ٴ���ȷ���������������з�������֤ʵ��㡣

��Ҫж���������ʹ��pip��

```
pip uninstall django-polls
```

## �������Ӧ�ã� ##

��Ȼ�����Ѿ���������Թ�django-polls����ʱ�������繲�����ˣ�Ҫ�����������Ǹ����ӣ������ڿ��ԣ�

+ ����������ʼ����͸����ѡ�
+ �ϴ�������������վ�ϡ�
+ �ϴ��������һ�������Ĳֿ⣬����Python ������ (PyPI)��packaging.python.org has a good tutorial for doing this.

## ʹ�� virtualenv ��װPython �� ##

ǰ�棬���ǽ�poll ��װ��һ���û��Ŀ⡣����һЩȱ�㣺

+ �޸�����û��Ŀ����Ӱ�����ϵͳ�ϵ�����Python �����
+ �㽫����������������Ķ���汾�����߾�����ͬ���ֵ�����������

�ر���һ����ά������Django��Ŀ����Щ����ͻ���֡����ȷʵ���֣���õĽ���취��ʹ��virtualenv���������������ά����������Python������ÿ�����������Լ��Ŀ�Ͱ��������ռ䡣