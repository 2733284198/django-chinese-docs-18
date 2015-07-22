<!--
  ��Դ��http://django-chinese-docs.readthedocs.org/
-->

# ��д��ĵ�һ�� Django ���� ��3���� #

���̳��Ͻ� �̳� ��2���� �����ǽ����� ���� Web-poll Ӧ�ò���רע�ڴ����������� �C ����ͼ ��views ������

## ���� ##

�� Django Ӧ�ó����У���ͼ��һ���ࡱ�����ض����ܺ�ģ�����ҳ�� ���磬��һ������Ӧ�ó����У�����ܻ���������ͼ��

+ ������ҳ �C ��ʾ���·���Ĳ��͡�
+ ������ϸҳ�� �C һƪ���͵Ķ���ҳ�档
+ ������ݵĹ鵵ҳ �C ��ʾ��������з����͵������·ݡ�
+ �����·ݵĹ鵵ҳ �C ��ʾ�����·��з����͵��������ڡ�
+ �������ڵĹ鵵ҳ �C ��ʾ���������з�������еĲ��͡�
+ ���۹��� �C Ϊһƪ�������ͷ������ۡ�

�����ǵ� poll Ӧ�ó����У����������ĸ���ͼ��

+ Poll ��index�� ҳ �C ��ʾ���·�����������顣
+ Poll ��detail�� ҳ �C ��ʾһ���������ľ������⣬����ʾ�����ͶƱ��������Խ���ͶƱ�� form ��
+ Poll ��results�� ҳ �C ��ʾһ���������������ͶƱ�����
+ ͶƱ���� �C Ϊһ�������������鴦��ͶƱѡ�

�� Django �У���ҳ����������������ͼ��չ�ֵġ���ÿ����ͼ����һ���򵥵� Python �������򷽷��� ���ڻ��������ͼ����£���Django ��ͨ������������ URL ��ȷ�е�˵������֮����ǲ��� URL����ƥ��һ����ͼ��

ƽʱ��������ʱ����ܻ������� ��ME2/Sites/dirmod.asp?sid=&type=gen&mod=Core+Pages&gid=A6CD4967199A42D9B65B1B�� ������������� URL�� �������ܸ���֪�� Django ��������ʹ�ñ������ŵ� URL ģʽ ��չ�� URL��

URL ģʽ����һ���򵥵�һ����ʽ�� URL - ����: `/newsarchive/<year>/<month>/`.

Django ��ͨ�� ��URLconfs�� �� URL ��ȡ����ͼ�ġ��� URLconf �ǽ� URL ģʽ ( ��������ʽ�������� ) ӳ�䵽��ͼ��һ�����á�

���̳��н�����ʹ�� URLconfs �Ļ���ָ�����Բ��� django.core.urlresolvers ����ȡ������Ϣ��

## ��д��ĵ�һ����ͼ ##

�����Ǳ�д��һ����ͼ�����ļ� polls/views.py ���������������� Python ����

```
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the poll index.")
```

�� Django �����������򵥵���ͼ�ˡ�Ϊ�˵��������ͼ��������Ҫ����ӳ�䵽һ�� URL �C Ϊ��������Ҫ����һ��URLconf ��

�� polls Ŀ¼�´���һ����Ϊ urls.py �� URLconf �ĵ��� ���Ӧ��Ŀ¼���ڿ�����������

```
polls/
    __init__.py
    admin.py
    models.py
    tests.py
    urls.py
    views.py
```

�� polls/urls.py �ļ����������´��룺

```
from django.conf.urls import patterns, url

from polls import views

urlpatterns = patterns('',
    url(r'^$', views.index, name='index')
)
```

��һ���ǽ� polls.urls ģ��ָ�� root URLconf ���� mysite/urls.py �в���һ�� include() ��������������������ʾ

```
from django.conf.urls import patterns, include, url

from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', include(admin.site.urls)),
)
```

�������� URLconf �������� index ��ͼ��ͨ����������� http://localhost:8000/polls/ ����ͬ���� index ��ͼ�ж����һ�����㽫���� ��Hello, world. You��re at the poll index.�� ���֡�

url() �������ĸ���������������ģ� regex �� ``view``�� ������ѡ�ģ� ``kwargs``�� �Լ� ``name``�� ����������̽������Щ���������塣

## url() ����: regex #

regex �� regular expression �ļ�д�������ַ����е�ģʽƥ���һ���﷨�� �� Django �о����� url ƥ��ģʽ�� Django ������� URL ������������ƥ���б��е�������ʽ��ֱ��ƥ�䵽һ��Ϊֹ��

��Ҫע����ǣ���Щ������ʽ����ƥ�� GET �� POST �������Լ������� ���磺��� http://www.example.com/myapp/ ��һ����URLconf ��ֻ���� myapp/``������ ``http://www.example.com/myapp/?page=3 �� URLconf Ҳ������ myapp/ ��

�������Ҫ������ʽ����İ���������� Wikipedia��s entry �ͱ��ĵ��е� re ģ�顣 ���⣬O��Reilly ������� Jeffrey Friedl ���� ��Mastering Regular Expressions�� Ҳ�ǲ���ġ� ���ǣ�ʵ���ϣ��㲢����Ҫ��Ϊһ��������ʽ��ר�ң�������Ҫ֪����β���򵥵�ģʽ�� ��ʵ�ϣ����ӵ�������ʽ�ή�Ͳ������ܣ�����㲻����ȫ����������ʽ�Ĺ��ܡ�

����и������ϵ���ʾ����Щ������ʽ�� URLconf ģ���һ�μ���ʱ�ᱻ���롣 ��������ٶȳ��� ( �������ᵽ������ֻҪ���ҵĲ���̫���� )��

## url() ������ view ##

�� Django ƥ����һ��������ʽ�ͻ����ָ������ͼ���ܣ�����һ�� HttpRequest ʵ����Ϊ��һ��������������ʽ ������ ��һЩֵ����Ϊ���������� ���ʹ�ü򵥵����򲶻񣬽���˳��λ�ô���������������������򲶻񣬽����ؼ��ִ�����ֵ�� �й���һ�����ǻ����һ�����ӡ�

## url() ������ kwargs ##

����ؼ��ֲ����ɴ�һ���ֵ���Ŀ����ͼ���ڱ��̳��У����ǲ�������ʹ�� Django ��һ���ԡ�

## url() ������ name ##

������� URL �������� Django �������ط���ȷ�����������ر�����ģ���С� ��һǿ��Ĺ��ܿ�������ͨ��һ���ļ��Ϳ�ȫ���޸���Ŀ�е� URL ģʽ��

## ��д������ͼ ##

�������������һЩ��ͼ�� polls/views.py ��ȥ����Щ��ͼ��֮ǰ�����в�ͬ����Ϊ ������һ��������:

```
def detail(request, poll_id):
    return HttpResponse("You're looking at poll %s." % poll_id)

def results(request, poll_id):
    return HttpResponse("You're looking at the results of poll %s." % poll_id)

def vote(request, poll_id):
    return HttpResponse("You're voting on poll %s." % poll_id)
```

������ͼ��������ʾ�� url() ������ӵ� polls.urls ģ����ȥ��:

```
from django.conf.urls import patterns, url

from polls import views

urlpatterns = patterns('',
    # ex: /polls/
    url(r'^$', views.index, name='index'),
    # ex: /polls/5/
    url(r'^(?P<poll_id>\d+)/$', views.detail, name='detail'),
    # ex: /polls/5/results/
    url(r'^(?P<poll_id>\d+)/results/$', views.results, name='results'),
    # ex: /polls/5/vote/
    url(r'^(?P<poll_id>\d+)/vote/$', views.vote, name='vote'),
)
```

�����������з��� http://localhost:8000/polls/34/ �������� detail() ����������ʾ���� URL ���ṩ������ ID �����ŷ��� http://localhost:8000/polls/34/results/ �� http://localhost:8000/polls/34/vote/ �C ������ʾ��Ӧ�Ľ��ҳ��ͶƱҳ��

�����˷��������վҳ���� �� /polls/34/ �� ʱ��Django ����� mysite.urls ģ�飬������Ϊ ROOT_URLCONF ����ָ�����������ڸ�ģ����Ѱ����Ϊ``urlpatterns`` �ı���������ƥ�����е�������ʽ�� include() �������Ǳ������������� URLconfs ����ע�� include() �е�������ʽû�� $ (�ַ�����β��ƥ��� match character) ��β����һ����б�ܡ��� Django ���� include() ʱ������ȡƥ��� URL �ǲ��ֶ���ʣ����ַ������� ���ؽ����� URLconf ����һ������

include() �������ص��뷨��ʹ URLs ���弴�á� ���� polls ���Լ��� URLconf(polls/urls.py) �У�������ǿ��Ա������� ��/polls/�� ·���£��� ��/fun_polls/�� ·���£��� ��/content/polls/�� ·���£�����������·������Ӧ���Կ������С�

�����ǵ��û����� ��/polls/34/�� ·��ʱϵͳ�н��������£�

+ Django ��Ѱ�� '^polls/' ��ƥ��
+ ���ţ�Django ��ȡƥ���ı� ("polls/") ��ʣ����ı� �C "34/" �C ���ݵ� ��polls.urls�� URLconf ������һ������ �ٽ�ƥ�� r'^(?P<poll_id>\d+)/$' �Ľ����Ϊ�������� detail() ��ͼ

```
detail(request=<HttpRequest object>, poll_id='34')
```

poll_id='34' �ⲿ�־������� (?P<poll_id>\d+) ƥ��Ľ���� ʹ�����Ű�Χһ�� ������ʽ�������񡱵��ı�����Ϊһ������������ͼ������``?P<poll_id>`` ���ᶨ���������ڱ�ʶƥ������ݣ� �� \d+ ��һ������ƥ���������У���һ�����֣���������ʽ��

��Ϊ URL ģʽ��������ʽ����������Ժ������Ƶ�ʹ�����ǡ����ǲ�Ҫ���� URL ����Ĳ����� .html �C �������룬�������������������:

```
(r'^polls/latest\.html$', 'polls.views.index'),
```

��ģ���Ҫ�����������ɵ��

## ����ͼ�����Щʵ�ʵĹ��� ##

ÿ����ͼֻ���������������е�һ��������һ�� HttpResponse �������а�����������ҳ������ݣ� �����׳�һ���쳣������ Http404 ��ʣ�µľ�������ʵ���ˡ�

�����ͼ���Զ�ȡ���ݿ��¼�����߲��á�������ʹ��һ��ģ��ϵͳ������ Django �� �C ���ߵ������� Python ģ��ϵͳ �C ���á�����������һ�� PDF �ļ������ XML �� ��ʱ���� ZIP �ļ��� �����ʹ�������õ��κ� Python ���������������κ��¡�

�� Django ֻҪ����һ�� HttpResponse ��һ���쳣��

��Ϊ���ܷ��㣬����������ʹ�� Django �Լ������ݿ� API �ɣ� �� �̳� ��1���� ��������޸��� index() ��ͼ�� ������ʾϵͳ�����·����� 5 ���������⣬�Զ��ŷָ��������������:

```
from django.http import HttpResponse

from polls.models import Poll

def index(request):
    latest_poll_list = Poll.objects.order_by('-pub_date')[:5]
    output = ', '.join([p.question for p in latest_poll_list])
    return HttpResponse(output)
```

��������˸����⣬ҳ��������Ӳ��������ͼ�еġ��������ı�ҳ�����ۣ��ͱ����޸������ Python ���롣��ˣ�������ʹ�� Django ��ģ��ϵͳ����һ��ģ�����ͼ�ã���ʹҳ����ƴ� Python ������ ��������ˡ�

���ȣ��� polls Ŀ¼�´���һ�� templates Ŀ¼�� Django ��������Ѱ��ģ�塣

Django �� TEMPLATE_LOADERS �����а���һ��֪����δӸ�����Դ����ģ��Ŀɵ��õķ����б� ������һ��Ĭ��ֵ�� django.template.loaders.app_directories.Loader ��Django �ͻ���ÿ�� INSTALLED_APPS �� ��templates�� ��Ŀ¼�²���ģ�� - ����� Django ֪����ô�ҵ� polls ģ���ԭ�򣬼�ʹ���� û���޸� TEMPLATE_DIRS, ������ͬ�� �̳� ��2���� ������

> ��֯ģ��
> 
> ���� �ܹ� ��һ�����ģ��Ŀ¼��һ�����������е�ģ�壬�������ǻ����еúܺá� ���ǣ���ģ������ polls Ӧ�ã��������������һ���̳��д����Ĺ���ģ�岻ͬ�� ����Ҫ�����ģ�����Ӧ�õ�ģ��Ŀ¼ (polls/templates) �¶�������Ŀ��ģ��Ŀ¼ (templates) �� ���ǽ��� �����õ�Ӧ�ý̳� ����ϸ�������� Ϊʲô Ҫ��������

����ղŴ�����``templates`` Ŀ¼�£����ⴴ������Ϊ polls ��Ŀ¼���������д���һ�� index.html �ļ������仰˵�����ģ��Ӧ���� polls/templates/polls/index.html ������֪������������ app_directories ģ��������� ������еģ�����Բο� Django �ڵ�ģ��򵥵���Ϊ polls/index.html ģ�塣

> ģ�������ռ�
> 
> �������� Ҳ�� �ܹ�ֱ�Ӱ����ǵ�ģ����� polls/templates Ŀ¼�� ( ���������ⴴ�� polls ��Ŀ¼ ) �� ����ʵ������һ����ע�⡣ Django ����ѡ���һ���ҵ��İ�����ƥ���ģ�壬 ������� ��ͬ Ӧ��������ͬ�����Ƶ�ģ�壬Django ���޷��������ǡ� ������Ҫ�� Django ָ����ȷ��ģ�壬��򵥵ķ�����ͨ�� �����ռ� ��ȷ���� ���ǵ�ģ�塣Ҳ����˵����ģ����� ��һ�� Ŀ¼�²�����ΪӦ�ñ�������ơ�

�����´�����ӵ���ģ����:

```
{% if latest_poll_list %}
    <ul>
    {% for poll in latest_poll_list %}
        <li><a href="/polls/{{ poll.id }}/">{{ poll.question }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```

������������ index ��ͼ��ʹ�����ģ�壺

```
from django.http import HttpResponse
from django.template import Context, loader

from polls.models import Poll

def index(request):
    latest_poll_list = Poll.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = Context({
        'latest_poll_list': latest_poll_list,
    })
    return HttpResponse(template.render(context))
```

���뽫���� polls/index.html ģ�岢����һ�� context ������ The context is a dictionary mapping template variable names to Python �� context ������һ��ӳ���� Python ����ģ��������ֵ䡣

�����������м��� ��/polls/�� ҳ����Ӧ�ÿ���һ���б��������ڽ̳� ��1���� �д����� ��What��s up�� ���顣������ָ�� poll ����ϸҳ�档

## ��ݷ�ʽ: render() ##

����һ���ǳ�������ϰ��������ڼ���ģ�壬��������Ĳ�����һ������ģ����Ⱦ����� HttpResponse ���� Django �ṩ��һ�ֿ�ݷ�ʽ��������д������ index() ��ͼ

```
from django.shortcuts import render

from polls.models import Poll

def index(request):
    latest_poll_list = Poll.objects.all().order_by('-pub_date')[:5]
    context = {'latest_poll_list': latest_poll_list}
    return render(request, 'polls/index.html', context)
```

��ע�⣬һ��������������ͼ�ж��������ˣ����ǾͲ�����Ҫ���� loader �� Context �� HttpResponse ( �������Ȼ������ detail,``resutls``, ��``vote`` �������㻹����Ҫ���� HttpResponse ) ��

render() �����е�һ�������� request ���󣬵ڶ���������һ��ģ�����ƣ���������һ���ֵ����͵Ŀ�ѡ������ ��������һ�������и���ģ����ݸ�������������Ⱦ����� HttpResponse ����

## �׳� 404 �쳣 ##

���������ǽ�� poll ����ϸ��ͼ �C ��ҳ��ʾһ������ poll ����ϸ���⡣ ��ͼ����������ʾ��:

```
from django.http import Http404
# ...
def detail(request, poll_id):
    try:
        poll = Poll.objects.get(pk=poll_id)
    except Poll.DoesNotExist:
        raise Http404
    return render(request, 'polls/detail.html', {'poll': poll})
```

�����и��¸���������� poll �� ID �����ڣ�����ͼ���׳� Http404 �쳣��

�����Ժ������������ polls/detail.html ģ�壬�����������������������ӣ� ��ģ���ļ���������´��룺

```
{{ poll }}
```

��������������ˡ�

## ��ݷ�ʽ: get_object_or_404() ##

��ܳ���������ʹ�� get() ��ȡ����ʱ ����ȴ������ʱ�ͻ��׳� Http404 �쳣���Դ� Django �ṩ��һ����ݲ�����������ʾ��д detail() ��ͼ��

```
from django.shortcuts import render, get_object_or_404
# ...
def detail(request, poll_id):
    poll = get_object_or_404(Poll, pk=poll_id)
    return render(request, 'polls/detail.html', {'poll': poll})
```

get_object_or_404() ������Ҫһ�� Django ģ������Ϊ��һ�������Լ� һЩ�ؼ��ֲ�����������Щ�������ݸ�ģ�͹������е� get() ������ �����󲻴���ʱ���׳� Http404 �쳣��

> ����
> 
> Ϊʲô����Ҫʹ��һ�� get_object_or_404() �������� �������ڸ��߼����Զ����� ObjectDoesNotExist �쳣�� ������ģ�� API �׳� Http404 �쳣������ ObjectDoesNotExist �쳣��
> 
> ��Ϊ������ʹģ�Ͳ�����ͼ�������һ��Django ����Ҫ�����Ŀ��֮һ ���Ǳ�������ϡ�һЩ��������� django.shortcuts ģ���н��ܡ�

���и� get_list_or_404() �������� get_object_or_404() һ�� �C ����ִ�е��� filter() ������ get() �������ص��ǿ��б��׳� Http404 �쳣��

## ��дһ�� 404 ( ҳ��δ�ҵ� ) ��ͼ ##

��������ͼ���׳� Http404 ʱ��Django ������һ���ض�����ͼ������ 404 ����Django �������� root URLconf ( ������� root URLconf �У��������κεط����� handler404 ����Ч �������õ� handler404 ���������Ҹ���ͼ����������Ǹ� Python ����ʽ�ַ��� �C �ͱ�׼ URLconf �еĻص�������ʽ��һ���ġ� 404 ��ͼ����û��ʲô�����ԣ�������һ����ͨ����ͼ��

ͨ���㲻�ط���ȥ��д 404 ��ͼ������û������ handler404 ������Ĭ������»�ʹ�����õ� django.views.defaults.page_not_found() ��ͼ����������������ģ��Ŀ¼�µĸ�Ŀ¼�� ����һ�� 404.html ģ�塣�� DEBUG ֵ�� False ( ����� settings ģ���� ) ʱ�� Ĭ�ϵ� 404 ��ͼ��ʹ�ô�ģ������ʾ���е� 404 ���� ����㴴�������ģ�壬�������Щ�硰ҳ��δ�ҵ��� �����ݡ�

һЩ�й� 404 ��ͼ��Ҫע������� :

+ ��� DEBUG ��Ϊ True ( ����� settings ģ���� ) ��ô��� 404 ��ͼ����Զ���ᱻʹ�� ( ��� 404.html ģ��Ҳ����Զ���ᱻ��Ⱦ ) ��Ϊ��Ҫ��ʾ���Ǹ�����Ϣ��
+ �� Django �� URLconf �в����ҵ���ƥ���������ʽʱ 404 ��ͼҲ�������á�
��дһ�� 500 ( ���������� ) ��ͼ

���Ƶģ�������� root URLconf �ж��� handler500 �������ڷ�������������ʱ ������ָ�����ͼ��������������ָ��ͼ�������������ʱ����

ͬ��������ģ���Ŀ¼�´���һ�� 500.html ģ�岢�����Щ�񡰳����ˡ������ݡ�

## ʹ��ģ��ϵͳ ##

�ص����� poll Ӧ�õ� detail() ��ͼ�У�ָ�� poll ������``polls/detail.html`` ģ����ܿ��������� :

```
<h1>{{ poll.question }}</h1>
<ul>
{% for choice in poll.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>
```

ģ��ϵͳʹ���ˡ�����.���ԡ����﷨���ʱ���������ֵ�� ���� {{ poll.question }} �� ���� Django �� poll �������ֵ��ѯ�� ���� Django �᳢�����Բ�ѯ �C �ڱ��������Բ�ѯ�ɹ��ˡ� ������Բ�ѯ����ʧ���ˣ�Django ������ list-index ��ѯ��

�� {% for %} ѭ�����з�������: poll.choice_set.all ���� Python ���� poll.choice_set.all(),��������һ��ɵ����� Choice ���󣬿������� {% for %} ��ǩ�С�

����� ģ��ָ�� ���˽�ģ��ĸ������ݡ�

## �Ƴ�ģ����Ӳ����� URLS ##

�ǵ���? �� polls/index.html ģ���У��������ӵ� poll ��������Ӳ����������ӵģ�

```
<li><a href="/polls/{{ poll.id }}/">{{ poll.question }}</a></li>
```

�������Ӳ���룬�����ʹ���ڴ�����ģ�����޸� URLs ��Ϊ������ս�Ե���Ŀ�� ��������Ȼ���� polls.urls ģ���е� url() �����ж����� ������������ô�Ϳ����� url ������ʹ�� {% url %} ģ�������Ƴ��ض��� URL ·������:

```
<li><a href="{% url 'detail' poll.id %}">{{ poll.question }}</a></li>
```

> Note
> 
> ��� {% url 'detail' poll.id %} (������) �������У����� {% url detail poll.id %} (��������) ȴ�����У���ô��ζ����ʹ�õ� Djang ���� < 1.5 �档�����Ļ�������Ҫ��ģ���ļ��Ķ���������µ�������:
> 
```
{% load url from future %}
```
> 

��ԭ������� polls.urls ģ����Ѱ��ָ���� URL ���塣 ��֪������Ϊ ��detail�� �� URL ��������ʾ���������һ����:

```
...
# 'name' ��ֵ�� {% url %} ģ����������
url(r'^(?P<poll_id>\d+)/$', views.detail, name='detail'),
...
```

������뽫 polls �� detail ��ͼ�� URL �ĳ��������ӣ������� polls/specifics/12/ �����ӣ��ǾͲ���Ҫ��ģ�壨����ģ�弯�����޸Ķ�ֻҪ�� polls/urls.py �޸ľ�����:

```
...
# ���� 'specifics'
url(r'^specifics/(?P<poll_id>\d+)/$', views.detail, name='detail'),
...
```

## URL ���Ƶ������ռ� ##

���̳��е���Ŀֻ��һ��Ӧ�ã�``polls`` ����ʵ�ʵ� Django ��Ŀ�У������� 5��10��20 ���� �����Ӧ�á�Django ������������ǵ� URL ���Ƶ��أ�����˵��``polls`` Ӧ����һ�� detail ��ͼ�������ܻ���ͬһ����Ŀ����һ������Ӧ�õ���ͼ��Django �����֪�� ʹ�� {% url %} ģ���Ǵ���Ӧ�õ� url ʱѡ����ȷ�أ�

��������� root URLconf ��������������ռ䡣�� mysite/urls.py �ļ� (��Ŀ�� ``urls.py``������Ӧ�õ�) �У��޸�Ϊ���������ռ�Ķ���:

```
from django.conf.urls import patterns, include, url

from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    url(r'^polls/', include('polls.urls', namespace="polls")),
    url(r'^admin/', include(admin.site.urls)),
)
```

���ڽ���� polls/index.html ģ����ԭ���� detail ��ͼ:

```
<li><a href="{% url 'detail' poll.id %}">{{ poll.question }}</a></li>
```

�޸�Ϊ���������ռ�� detail ��ͼ:

```
<li><a href="{% url 'polls:detail' poll.id %}">{{ poll.question }}</a></li>
```

�����д��ͼ���������Ķ� �̳� ��4���� ��ѧϰ��δ���򵥵ı���ͨ����ͼ��