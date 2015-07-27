<!--
  ���ߣ�wrongwat.cn
  1.8���£�Github@wizardforcel
-->

# ��������ڽ�ͨ����ͼ #

��дWebӦ�ÿ����ǵ����ģ���Ϊ����Ҫ���ϵ��ظ�ĳһ��ģʽ�� Django���Դ�model�� template���Ƴ�һЩ���������������Web��������Ȼ����view����ͼ���㾭�������ᷳ��

Django��ͨ����ͼ����������������һʹ�ࡣ���ǲ���ĳЩ������ϰ����ڿ����� ���з��ֵ�ģʽȻ������ǳ���������Ա����ܹ�д���ٵĴ�����ٵ�ʵ�ֻ�������ͼ��

�����ܹ�ʶ��һЩ���������񣬱���չʾ������б��Լ���д������չʾ�κζ���� �б����⣬�������ģ�Ϳ�����Ϊһ������Ĳ������ݵ�URLconf�С�

Djangoͨ��ͨ����ͼ���������һЩ���ܣ�

+ Ϊ��һ�Ķ���չʾ�б��һ����ϸҳ�档 ������Ǵ���һ��Ӧ����������飬��ô   һ�� TalkListView (�����б���ͼ)��һ�� RegisteredUserListView ��   ע���û��б���ͼ�������б���ͼ��һ�����ӡ�һ��������������Ϣҳ��������ǳ�   ֮Ϊ "��ϸ" ��ͼ�����ӡ�
+ ����/��/�չ鵵ҳ�棬�Լ���ϸҳ��͡���󷢱�ҳ���У�չʾ�����ݿ�Ϊ�����Ķ���
�����û����������º�ɾ������ -- ����Ȩ����������Ȩ�ķ�ʽ��

�ܵ���˵����Щ��ͼ�ṩ��һЩ�򵥵Ľӿ�����ɿ����������Ĵ�����ĳ�������

## ��չͨ����ͼ ##

ʹ��ͨ����ͼ���Լ������߿����ٶȣ��Ǻ������ʵġ� Ȼ���ڴ���������У� �ܻ�����ͨ����ͼ�޷����������ʱ�򡣵�ȷ�����������Django�������� �������������ʹ��ͨ����ͼ��ʹ�÷�Χ���㡣

����ͨ����ͼ��1.3�����б�������Ƶ�ԭ��֮һ - ֮ǰ�����ǽ�����һЩ������ͼ���� һ�������ɻ��ѡ����ڣ����𴫵ݴ��������õ�URLconf�У����Ƽ�����չͨ����ͼ�� ���������໯���ǣ�������д���ǵ����Ի��߷�����

�����˵��ͨ����ͼ��һЩ���ơ�����㽫�����ͼʵ��Ϊͨ����ͼ�����࣬��ͻᷢ�������ܹ�����Ч�ر�д����Ҫ�Ĵ��룬ʹ�����Լ��Ļ�������ܵ���ͼ��

��һЩ������Ӧ���У��и���ͨ����ͼ��ʾ��������������Լ������д��

## �����ͨ����ͼ ##

TemplateViewȷʵ�����ã����ǵ�����Ҫ ���������ݿ��е�����ʱDjango��ͨ����ͼ����Ļ���ӱ��������Ϊ������˳��� ������Django�ṩ��һ������õ�ͨ����ͼ��ʹ���ɶ����չʾ�б����ϸ��ͼ �ı�ü������ס�

����������һ����Щͨ����ͼ�е�"�����б�"��ͼ��

���ǽ�ʹ�������ģ�ͣ�

```
# models.py
from django.db import models

class Publisher(models.Model):
    name = models.CharField(max_length=30)
    address = models.CharField(max_length=50)
    city = models.CharField(max_length=60)
    state_province = models.CharField(max_length=30)
    country = models.CharField(max_length=50)
    website = models.URLField()

    class Meta:
        ordering = ["-name"]

    def __str__(self):              # __unicode__ on Python 2
        return self.name

class Author(models.Model):
    salutation = models.CharField(max_length=10)
    name = models.CharField(max_length=200)
    email = models.EmailField()
    headshot = models.ImageField(upload_to='author_headshots')

    def __str__(self):              # __unicode__ on Python 2
        return self.name

class Book(models.Model):
    title = models.CharField(max_length=100)
    authors = models.ManyToManyField('Author')
    publisher = models.ForeignKey(Publisher)
    publication_date = models.DateField()
```

����������Ҫ����һ����ͼ��

```
# views.py
from django.views.generic import ListView
from books.models import Publisher

class PublisherList(ListView):
    model = Publisher
```

�����ͼ���������url�ϣ�

```
# urls.py
from django.conf.urls import url
from books.views import PublisherList

urlpatterns = [
    url(r'^publishers/$', PublisherList.as_view()),
]
```

�����������������Ҫд��Python�����ˡ�

> ע��
> 
> ���ԣ��������磩DjangoTemplates��˵�APP_DIRSѡ����TEMPLATES������ΪTrueʱ��ģ���λ��Ӧ��Ϊ��/path/to/project/books/templates/books/publisher_list.html��

���ģ�彫��������һ��������(context)����Ⱦ�����context����һ����Ϊobject_list ��������publisher����ı�����һ���ǳ��򵥵�ģ����ܿ�����������������

```
{% extends "base.html" %}

{% block content %}
    <h2>Publishers</h2>
    <ul>
        {% for publisher in object_list %}
            <li>{{ publisher.name }}</li>
        {% endfor %}
    </ul>
{% endblock %}
```

��ȷʵ����ȫ�������ˡ� ����ͨ����ͼ����Ȥ�������������޸ı����ݵ�ͨ����ͼ�е�"��Ϣ" �ֵ䡣generic views reference�ĵ���ϸ ������ͨ����ͼ�Լ�����ѡ���ƪ�ĵ�ʣ��Ĳ��ֽ�������Զ����Լ���չͨ�� ��ͼ�ĳ���������


## ��д���Ѻõġ�ģ�������� ##

������Ѿ�ע�⵽�ˣ�������publisher�б�������а����е�publisher���� �ŵ� object_list �����С���Ȼ�������������������ģ�����߲����� "�Ѻõ�"������ֻ��Ҫ֪��������Ҫ����publishers�����ˡ�

��ˣ�������ڴ���һ��ģ��(model)�����������˵�Ѿ��㹻�ˡ� ���㴦�� һ��object����querysetʱ��Django�ܹ�ʹ���㶨�������ʾ�õ���������verbose name�����߸����������������ڶ����б������������(context)���ṩ��ӵ�Ĭ�ϵ� object_list ʵ���У����ǰ�����ȫ��ͬ�����ݣ�����publisher_list��

���������(���߸�����������) ��Ȼ���ܺܺõķ���Ҫ���� �����ֶ�������������(context)���������֡���һ��ͨ����ͼ�ϵ�context_object_name����ָ����Ҫʹ�õĶ��������ı�����

```
# views.py
from django.views.generic import ListView
from books.models import Publisher

class PublisherList(ListView):
    model = Publisher
    context_object_name = 'my_favorite_publishers'
```

�ṩһ�����õ�context_object_name���Ǹ������⡣����һ��������� ģ���ͬ�»��л��ġ�

## ��Ӷ���������� ##

����ʱ����ֻ����ҪչʾһЩ�������Ϣ�������ṩһЩͨ����ͼ�� ���磬���ǵ�ÿ��publisher ��ϸҳ���ϵ�ͼ���б��չʾ��DetailViewͨ����ͼ�ṩ��һ��publisher�����context���������������ģ������Ӹ�����Ϣ�أ�

��������DetailView��������get_context_data�������ṩ���Լ���ʵ�֡�Ĭ�ϵ�ʵ��ֻ�Ǽ򵥵� ��ģ�������Ҫչʾ�Ķ��󣬵����������������д��չʾ������Ϣ��

```
from django.views.generic import DetailView
from books.models import Publisher, Book

class PublisherDetail(DetailView):

    model = Publisher

    def get_context_data(self, **kwargs):
        # Call the base implementation first to get a context
        context = super(PublisherDetail, self).get_context_data(**kwargs)
        # Add in a QuerySet of all the books
        context['book_list'] = Book.objects.all()
        return context
```

> ע��
> 
> ͨ����˵��get_context_data�Ὣ��ǰ���е����������ݣ��ϲ������г����е����������ݡ�Ҫ�����Լ���Ҫ�ı������ĵ����б�����һ��Ϊ����Ӧ��ȷ���ڳ����е�����get_context_data�����û�����������ೢ�Զ�����ͬ�ļ����᷵���쳣�Ľ����Ȼ��������κ�һ���ೢ���ڳ������һ����������¸�д�����ڵ��ó���֮�󣩣��������κ����඼��Ҫ��ʽ�ڳ���֮�����������������Ҫȷ�����Ǹ�д�����г���Ļ��������������鷳����������ͼ�еķ�������˳��

## �鿴������Ӽ� ##

������������������鿴������һֱ���õ� model������model����ָ������ͼ���ĸ����ݿ�ģ��֮�Ͻ��в����������������е���Ҫ ����һ�������Ķ������һ�����󼯺ϵ�ͨ����ͼ��Ȼ����model����������Ψһ�ܹ�ָ����ͼҪ�����ĸ�������в����ķ��� --  ��ͬ������ʹ��queryset������ָ��һ�������б�

```
from django.views.generic import DetailView
from books.models import Publisher

class PublisherDetail(DetailView):

    context_object_name = 'publisher'
    queryset = Publisher.objects.all()
```

ָ��model = Publisher�ȼ��ڿ���������queryset = Publisher.objects.all()��Ȼ����ͨ��ʹ��queryset������һ�����˵Ķ����б�����Ը�����ϸ ���˽���Щ���󽫻ᱻ��ʾ����ͼ��(�μ�ִ�в�ѯ����ȡ������ڲ�ѯ������ĸ�����Ϣ���Լ��μ� ���������ͼ�ο�����ȡȫ�� ϸ��)��

���ǿ�����Ҫ��ͼ���б��ճ������ڽ���������ѡ��һ���򵥵����ӣ����Ұ� ����ķŵ�ǰ�棺

```
from django.views.generic import ListView
from books.models import Book

class BookList(ListView):
    queryset = Book.objects.order_by('-publication_date')
    context_object_name = 'book_list'
```

���Ǹ��ǳ��򵥵����ӣ��������ܺõ�ڹ���˴���˼·�� ��Ȼ����ͨ�������Ĳ�����ֻ�� �Զ����б���������������Ҫչ��ĳ�������̵�����ͼ���б������ʹ�� ͬ�����ַ���

```
from django.views.generic import ListView
from books.models import Book

class AcmeBookList(ListView):

    context_object_name = 'book_list'
    queryset = Book.objects.filter(publisher__name='Acme Publishing')
    template_name = 'books/acme_list.html'
```

ע�⣬���˾�������֮��Ĳ�ѯ����һ����Ļ��������Զ����ģ�����ơ�������ǲ���ô����ͨ����ͼ��ʹ�ú� "vanilla" �����б�����һ����ģ�壬��� �ܲ���������Ҫ�ġ�

������Ҫע�⣬�Ⲣ���Ǵ����ض������̵�ͼ��ķǳ����ŵķ����� �������  Ҫ��������һ��������ҳ�棬������Ҫ������⼸�д��뵽URLconf�У������ٶ༸�� �����̾ͻ������ô�����������ǻ�����һ���½ڴ���������⡣

> ע��
> 
> ������ڷ��� /books/acme/ʱ����404���󣬼��ȷ����ȷʵ��һ������Ϊ��ACME Publishing���ĳ����̡�ͨ����ͼ�����������ӵ��һ��allow_empty �Ĳ�����������������ͼ�ο���

## ��̬���� ##

��һ���ձ���������ڸ������б�ҳ���и���URL�еĹؼ��������˶��� ǰ�����ǰѳ��� �̵�����Ӳ���뵽URLconf�У��������������Ҫ��дһ����ͼ��չʾ�κ�publisher������ ͼ�飬Ӧ����δ���

�൱������ǣ� ListView ��һ��get_queryset() ��������������д����֮ǰ����ֻ�Ƿ���һ��queryset����ֵ�������������ǿ�����Ӹ�����߼���

�����ַ�ʽ�ܹ������Ĺؼ��㣬���ڵ�����ͼ������ʱ���������õĶ��󱻴洢��self�ϣ�ͬrequest()(self.request)һ�������а����˴�URLconf�л�ȡ����λ�ò��� (self.args)�ͻ������ֵĲ���(self.kwargs)(�ؼ��ֲ���)��

�������ӵ��һ������һ�鹩����Ĳ�����URLconf��

```
# urls.py
from django.conf.urls import url
from books.views import PublisherBookList

urlpatterns = [
    url(r'^books/([\w-]+)/$', PublisherBookList.as_view()),
]
```

���ţ����Ǳ�д��PublisherBookList��ͼ::

```
# views.py
from django.shortcuts import get_object_or_404
from django.views.generic import ListView
from books.models import Book, Publisher

class PublisherBookList(ListView):

    template_name = 'books/books_by_publisher.html'

    def get_queryset(self):
        self.publisher = get_object_or_404(Publisher, name=self.args[0])
        return Book.objects.filter(publisher=self.publisher)
```

������������queryset������Ӹ�����߼��ǳ����ף����������Ļ������ǿ��� ʹ��self.request.user�����˵�ǰ�û�������������������ӵ��߼���

ͬʱ���ǿ��԰ѳ�������ӵ��������У��������ǾͿ�����ģ����ʹ������

```
# ...

def get_context_data(self, **kwargs):
    # Call the base implementation first to get a context
    context = super(PublisherBookList, self).get_context_data(**kwargs)
    # Add in the publisher
    context['publisher'] = self.publisher
    return context
```

## ִ�ж���Ĺ��� ##

������Ҫ���ǵ����Ĺ�ͬģʽ�ڵ���ͨ����ͼ֮ǰ����֮����������Ŀ�����

����һ�£������ǵ�Author��������һ��last_accessed�ֶΣ�����ֶ����� ����ĳ�����һ�β鿴��������ߵ�ʱ�䡣

```
# models.py
from django.db import models

class Author(models.Model):
    salutation = models.CharField(max_length=10)
    name = models.CharField(max_length=200)
    email = models.EmailField()
    headshot = models.ImageField(upload_to='author_headshots')
    last_accessed = models.DateTimeField()
```

ͨ�õ�DetailView�࣬��Ȼ��֪����������ֶε����飬�����ǿ��Ժ����� �ٴα�дһ���Զ������ͼ������������ֶεĸ��¡�

���ȣ�������Ҫ�����������ҳ�Ĵ������õ�URLconf�У�ָ���Զ������ͼ��

```
from django.conf.urls import url
from books.views import AuthorDetailView

urlpatterns = [
    #...
    url(r'^authors/(?P<pk>[0-9]+)/$', AuthorDetailView.as_view(), name='author-detail'),
]
```

Ȼ�󣬱�д�����µ���ͼ -- get_object��������ȡ����ķ��� -- ������Ǽ򵥵� ��д������װ���ã�

```
from django.views.generic import DetailView
from django.utils import timezone
from books.models import Author

class AuthorDetailView(DetailView):

    queryset = Author.objects.all()

    def get_object(self):
        # Call the superclass
        object = super(AuthorDetailView, self).get_object()
        # Record the last accessed date
        object.last_accessed = timezone.now()
        object.save()
        # Return the object
        return object
```

> ע��
> 
> ����URLconfʹ�ò����������pk - ���������DetailView��������������ֵ��Ĭ�����ƣ������������ڹ��˲�ѯ����
> 
> �������Ҫ���ò�������������������������ͼ������pk_url_kwarg����� DetailView�ο���