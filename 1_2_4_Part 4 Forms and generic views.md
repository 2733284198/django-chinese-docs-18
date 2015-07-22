<!--
  ��Դ��http://django-chinese-docs.readthedocs.org/
-->

# ��д��ĵ�һ�� Django ���� ��4���� #

���̳��Ͻ� �̳� ��3���� �����ǽ� �������� Web-poll Ӧ�ò��ҹ�ע�ڴ���򵥵Ĵ�����Ż����ǵĴ��롣

## ��дһ���򵥵Ĵ��� ##

�����ǰ�����һƪ�̳��б�д�� poll �� detail ģ������£���ģ���а��� HTML �� <form> ���:

```
<h1>{{ poll.question }}</h1>

{% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

<form action="{% url 'polls:vote' poll.id %}" method="post">
{% csrf_token %}
{% for choice in poll.choice_set.all %}
    <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}" />
    <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br />
{% endfor %}
<input type="submit" value="Vote" />
</form>
```
�򵥵��ܽ���:

+ �����ģ����Ϊÿ��ͶƱѡ��������һ����ѡ��ť��ÿ����ѡ��ť�� value ��ͶƱѡ���Ӧ�� ID ��ÿ����ѡ��ť�� name ���� ``��choice��``������ζ�ţ�������ѡ����һ����ѡ��ť���ύ�˱������ᷢ�� �� POST ������ ``choice=3``������ HTML ���еĻ������
+ ���ǽ� form �� action ����Ϊ {% url 'polls:vote' poll.id %}``���Լ������� ``method="post" ��ʹ�� method="post" ( ������ method="get") �Ƿǳ���Ҫ�ģ���Ϊ�����ύ���ķ�ʽ��ı�������˵����ݡ� ���㴴��һ����Ϊ���޸ķ������˵�����ʱ����ʹ�� method="post" ���ⲻ�� Django �ض��ļ��ɣ���������� Web ����ʵ����
+ forloop.counter ��ʾ for ��ǩ��ѭ�����Ѿ�ѭ�����Ĵ���
+ ��������Ҫ����һ��POST form ( �����޸����ݵĹ��� )��������Ҫ���Ŀ�վ������α�� �� Cross Site Request Forgeries ���� ֵ�����ҵ��ǣ��㲻��̫������һ�㣬��Ϊ Django �Դ���һ���ǳ�����ʹ�õ�ϵͳ���������� ��֮�����е� POST form ����ڲ��� URLs ʱ��Ӧ��ʹ�� {% csrf_token %} ģ���ǩ��

���ڣ�������������һ�� Django ��ͼ�������ύ�����ݡ� �ǵ����� �̳� ��3���� �У�����Ϊ polls Ӧ�ô�����һ�� URLconf �����а�������һ�д���:

```
url(r'^(?P<poll_id>\d+)/vote/$', views.vote, name='vote'),
```

���ǻ�������һ������ʵ�ֵ� vote() �����������Ǵ���һ����ʵ�汾�ɡ��� polls/views.py ��������´���:

```
from django.shortcuts import get_object_or_404, render
from django.http import HttpResponseRedirect, HttpResponse
from django.core.urlresolvers import reverse
from polls.models import Choice, Poll
# ...
def vote(request, poll_id):
    p = get_object_or_404(Poll, pk=poll_id)
    try:
        selected_choice = p.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the poll voting form.
        return render(request, 'polls/detail.html', {
            'poll': p,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        return HttpResponseRedirect(reverse('polls:results', args=(p.id,)))
```

�����������Щ���ݻ�δ�ڱ��̳����ᵽ��:

request.POST ��һ�������ֵ�Ķ��󣬿������� ͨ���ؼ�����������ȡ�ύ�����ݡ��ڱ����У� request.POST['choice'] ��������ѡ���ͶƱ��Ŀ�� ID �����ַ�������ʽ�� request.POST ��ֵ��Զ���ַ�����ʽ�ġ�

��ע�� Django Ҳͬ�����ṩ��ͨ�� request.GET ��ȡ GET ���ݵķ��� �C �����ڴ�����������ȷ��ʹ���� request.POST ��������ȷ��������ͨ�� POST �������޸ĵġ�

��� choice δ�� POST �������ṩ request.POST['choice'] ���׳� KeyError ��δ���� choice ����ʱ����Ĵ�������⵽�׳����� KeyError �쳣�ͻ��� poll ��ʾһ��������Ϣ��

��������ͶƱѡ���ͳ�����󣬴��뷵��һ�� HttpResponseRedirect ��������ǳ����� HttpResponse ���� HttpResponseRedirect ������Ҫһ���������û������ض���� URL (���������ȥ�����������������ι��� URL ) ��

���������� Python ����ע�����������ɹ��Ĵ����� POST ���ݺ���Ӧ�����Ƿ���һ�� HttpResponseRedirect ���� ������ɲ����ض��� Django �ģ���������� Web ����ʵ����

�ڱ����У������� HttpResponseRedirect �Ĺ��췽����ʹ���� reverse() ������ �˺��������ڱ�������ͼ��Ӳ���� URL �Ĺ��ܡ���ָ����������Ҫ����ת����ͼ�������Լ���ͼ������ URL ģʽ��Ӧ�Ŀɱ�������ڱ����У�����ʹ���˽̳� ��3�����е� URLconf ���ã� reverse() ���᷵������������ʾ���ַ���

```
'/polls/3/results/'
```

... �ڴ� 3 ���� p.id ��ֵ�����ض��� URL ����� 'results' ��ͼ����ʾ����ҳ�档

�����ڽ̳� ��3�����ᵽ�ģ�``request`` ��һ�� HttpRequest �������˽� HttpRequest �����������ݣ������ request �� response �ĵ� ��

������ͶƱ��``vote()`` ��ͼ���ض���ͶƱ���ҳ������������д�����ͼ

```
def results(request, poll_id):
    poll = get_object_or_404(Poll, pk=poll_id)
    return render(request, 'polls/results.html', {'poll': poll})
```

�⼸���� �̳� ��3���� �е� detail() ��ͼ��ȫһ���� Ψһ���������ģ�����ơ� �Ժ����ǻ�������������⡣

���ڣ�����һ�� polls/results.html ģ��:

```
<h1>{{ poll.question }}</h1>

<ul>
{% for choice in poll.choice_set.all %}
    <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
{% endfor %}
</ul>

<a href="{% url 'polls:detail' poll.id %}">Vote again?</a>
```

���ڣ���������з��� /polls/1/ �����ͶƱ��ÿ��ͶƱ���㽫�ῴ�����ҳ���ݶ��и��¡� �����û��ѡ��ͶƱѡ����ύ�ˣ����ῴ���������Ϣ��

## ʹ��ͨ����ͼ���Ż����� ##

detail() ( �� �̳� ��3���� ��) �� results() ��ͼ ���ܼ� �C ���һ����������ᵽ���������⡣``index()`` ������ʾ polls �б�� index() ��ͼ (Ҳ�ڽ̳� ��3������)��Ҳ�Ǵ������Ƶ����⡣

��Щ��ͼ�����˻����� Web ������һ�ֳ��������⣺ ���� URL �еĲ��������ݿ��л�ȡ���ݣ�����ģ�岢������Ⱦ������ݡ�������������� ��������� Django �ṩ��һ�ֿ�ݷ�ʽ������֮Ϊ��ͨ����ͼ��ϵͳ��

ͨ����ͼ�����˳�����ģʽ���������㲻��Ҫ��д Python ��������дһ��Ӧ�á�

�����ǰ� poll Ӧ���޸ĳ�ʹ��ͨ����ͼϵͳ��Ӧ�ã��������Ǿ���ɾ��ɾ��һЩ�����Լ��Ĵ����ˡ� ���ǽ���ȡ���²����������޸ģ�

+ �޸� URLconf ��
+ ɾ��һЩ�ɵģ�����Ҫ����ͼ��
+ ���� URL ������Ӧ������ͼ��

������Ķ��˽���ϸ����Ϣ��

> ΪʲôҪ�ع����룿
> 
> ͨ������£������дһ�� Django Ӧ��ʱ�����������ͨ����ͼ�Ƿ��ʺϽ��������⣬ ����ʺ����Ӧ�ô�һ��ʼ��ʹ�����������ǽ��е�һ����ع���Ĵ��롣 ���Ǳ��̳�ֱ�����ڶ����⼯�н��ܡ�Ӳ���롱��ͼ����Ϊ��רע�ں��ĸ����ϡ�
> 
> ��������ʹ�ü�����ǰ��Ҫ֪����������ѧ֪ʶһ����

## �޸� URLconf ##

���ȣ��� polls/urls.py �� URLconf �����ļ����޸ĳ�������ʾ����

```
from django.conf.urls import patterns, url
from django.views.generic import DetailView, ListView
from polls.models import Poll

urlpatterns = patterns('',
    url(r'^$',
        ListView.as_view(
            queryset=Poll.objects.order_by('-pub_date')[:5],
            context_object_name='latest_poll_list',
            template_name='polls/index.html'),
        name='index'),
    url(r'^(?P<pk>\d+)/$',
        DetailView.as_view(
            model=Poll,
            template_name='polls/detail.html'),
        name='detail'),
    url(r'^(?P<pk>\d+)/results/$',
        DetailView.as_view(
            model=Poll,
            template_name='polls/results.html'),
        name='results'),
    url(r'^(?P<poll_id>\d+)/vote/$', 'polls.views.vote', name='vote'),
)
```

## �޸� views ##

�������ǽ�ʹ������ͨ����ͼ�� ListView �� DetailView ����������ͼ�ֱ�������ʾ���ֳ������ ����ʾһϵ�ж�����б� �� ����ʾһ���ض����͵Ķ������ϸ��Ϣҳ����

+ ÿ����ͼ����Ҫ֪��ʹ���ĸ�ģ�����ݡ������Ҫ�ṩ��Ҫʹ�õ� model ������
+ DetailView ͨ����ͼ������ URL �в�����Ϊ "pk" ������ֵ��������ǽ� poll_id ��Ϊ pk ��

Ĭ������£� DetailView ͨ����ͼʹ����Ϊ <Ӧ����>/<ģ����>_detail.html ��ģ�塣�����ǵ������У���ʹ����Ϊ "polls/poll_detail.html" ��ģ�塣 template_name �����Ǹ��� Django ʹ��ָ����ģ������������ʹ���Զ����ɵ�Ĭ��ģ������ ����Ҳָ���� results �б���ͼ�� template_name �C ��ȷ���� results ��ͼ�� detail ��ͼ��Ⱦʱ���в�ͬ����ۣ���Ȼ������һ�� DetailView ������Ļ��

ͬ���ģ�~django.views.generic.list.ListView ͨ����ͼʹ�õ�Ĭ��ģ����Ϊ <Ӧ����>/<ģ����>_list.html ������ָ���� template_name �������� ListView ʹ���Ѿ����ڵ� "polls/index.html" ģ�塣

��֮ǰ�Ľ̳��У�ģ���ṩ���������а����� poll �� latest_poll_list �����ı������� DetailView �� poll �������Զ��ṩ�� �C ��Ϊ����ʹ����һ�� Django ģ�� (Poll) ��Django �ܹ�Ϊ�����ı���ȷ���ʺϵ����ơ� ���� ListView �Զ����ɵ������ı������� poll_list ����Ҫ���Ǵ˱���������Ҫ�ṩ context_object_name ѡ� ������Ҫʹ�� latest_poll_list �����������Ϊһ�������ʽ������Ըı����ģ���� ƥ���µ�Ĭ�ϵ������ı��� �C ������һ���ǳ����׵ظ��� Django ʹ������Ҫ�ı����ķ�ʽ��

����������� polls/views.py ��ɾ�� index() �� detail() �� results() ��ͼ�ˡ� ���ǲ���Ҫ������ �C �������滻Ϊͨ����ͼ�ˡ���Ҳ����ɾ��������Ҫ�� HttpResponse ������ˡ�

���з�����������ʹ���»���ͨ����ͼ����ͶƱӦ�á�

�й�ͨ����ͼ��������ϸ��Ϣ������� ͨ����ͼ�ĵ�.

������Ϥ�˴����ͨ����ͼ�����Ķ� �̳� ��5���� ��ѧϰ�������ǵ�ͶƱӦ�á�