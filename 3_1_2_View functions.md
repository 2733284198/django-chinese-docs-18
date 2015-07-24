# ��д��ͼ #

һ����ͼ���������߼����˵������ͼ����һ���򵥵�Python������������web���󣬲��ҷ���web��Ӧ����Ӧ������һ����ҳ��HTML���ݣ�һ���ض���һ��404����һ��XML�ĵ�������һ��ͼƬ. . . ���κζ��������ԡ�������ͼ�������ʲô�߼�����Ҫ������Ӧ������д������Ҳ����ν��ֻҪ�������PythonĿ¼���档����֮��û�и����Ҫ���ˡ�������˵��û��ʲô����ĵط�����Ϊ���ܹ��Ѵ������ĳ���ط��������ǰ���ͼ���ڽ���views.py���ļ��У�Ȼ������ŵ������Ŀ����Ӧ��Ŀ¼�

## һ���򵥵���ͼ ##

������һ�����ص�ǰ���ں�ʱ����ΪHTML�ĵ�����ͼ��

```
from django.http import HttpResponse
import datetime

def current_datetime(request):
    now = datetime.datetime.now()
    html = "<html><body>It is now %s.</body></html>" % now
    return HttpResponse(html)
```

�����������Ķ�����Ĵ��룺

+ ���ȣ����Ǵ� django.httpģ�鵼����HttpResponse�࣬�Լ�Python��datetime�⡣
+ ���ţ����Ƕ�����current_datetime����������һ����ͼ������ÿ����ͼ������Ӧ����HttpRequest������Ϊ��һ��������һ�����request��
+ ע����ͼ���������Ʋ�����Ҫ������Ҫ��һ��ͳһ��������ʽ���������Ա���Djangoʶ���������ǽ�������Ϊcurrent_datetime������Ϊ��������ܹ���ȷ�ط�ӳ�����Ĺ��ܡ�
+ �����ͼ�᷵��һ��HttpResponse�������а������ɵ���Ӧ��ÿ����ͼ������Ҫ����HttpResponse���󡣣������⣬���ǽ������ὲ����

> Django�е�ʱ��
> 
> Django�а���һ��TIME_ZONE���ã�Ĭ��ΪAmerica/Chicago�����ܲ�������ס�ĵط�����������ܻ��������ļ����޸�����

## �����URLӳ�䵽��ͼ ##

���ԣ����ظ�һ�飬�����ͼ����������һ��������ǰ���ں�ʱ���HTMLҳ�档����Ҫ����URLconf��չʾ���ض���URL��һ��ͼ�� ���URL �ַ�����

## ���ش��� ##

��Django�з���HTTP�������൱���׵ġ���һЩHttpResponse�����������200����OK������HTTP״̬�롣�������request/response�ĵ����ҵ����п��õ����ࡣ����Է�����Щ�����һ��ʵ������������ͨ��HttpResponse ������ʾһ���������磺

```
from django.http import HttpResponse, HttpResponseNotFound

def my_view(request):
    # ...
    if foo:
        return HttpResponseNotFound('<h1>Page not found</h1>')
    else:
        return HttpResponse('<h1>Page was found</h1>')
```

����һЩ״̬�벻̫���ã����Բ���ÿ��״̬�붼��һ���ػ������ࡣȻ������HttpResponse�ĵ�����˵����������Ҳ������HttpResponse�Ĺ���������HTTP״̬�룬����������Ҫ���κ�״̬��ķ����ࡣ���磺

```
from django.http import HttpResponse

def my_view(request):
    # ...

    # Return a "created" (201) response code.
    return HttpResponse(status=201)
```

����404�����������HTTP�������Դ�����һ����ķ�ʽ�ǳ�������

## Http404�쳣 ##

**class django.http.Http404**

���㷵��һ����HttpResponseNotFound�����Ĵ���ʱ����������������ҳ���HTML��Ϊ�����

```
return HttpResponseNotFound('<h1>Page not found</h1>')
```

Ϊ�˱��������Ҳ��Ϊ���վ���и�һ�µ�404ҳ���Ǹ������⣬Django�ṩ��Http404�쳣�����������ͼ�����е��κεط��׳�Http404�쳣��Django���Ჶ���������Ҵ���HTTP404�����뷵����Ӧ�õı�׼����ҳ�档

��������

```
from django.http import Http404
from django.shortcuts import render_to_response
from polls.models import Poll

def detail(request, poll_id):
    try:
        p = Poll.objects.get(pk=poll_id)
    except Poll.DoesNotExist:
        raise Http404("Poll does not exist")
    return render_to_response('polls/detail.html', {'poll': p})
```

Ϊ�˾��������� Http404����Ӧ�ô���һ��������404�������ʱչʾ��ģ�塣���ģ��Ӧ�ý���404.html�����������ģ������λ����㡣

��������׳�Http404�쳣ʱ�ṩ��һ����Ϣ����DEBUGΪTrueʱ��������ڱ�׼404ģ���չʾ�С�����Խ���Щ��Ϣ���ڵ��ԣ�������ͨ����������404ģ�屾��

## �Զ��������ͼ ##

Django��Ĭ�ϵĴ�����ͼ���ڴ����webӦ���Ѿ��㹻�ˣ������������Ҫ�κ��Զ�����Ϊ����д�������ס�ֻҪ�����URLconf��ָ������Ĵ��������������κεط��������ǲ�����Ч����

handler404������page_not_found()��ͼ��

```
handler404 = 'mysite.views.my_custom_page_not_found_view'
```

handler500������server_error()��ͼ��

```
handler500 = 'mysite.views.my_custom_error_view'
```

handler403������permission_denied()��ͼ��

```
handler403 = 'mysite.views.my_custom_permission_denied_view'
```

handler400������bad_request()��ͼ��

```
handler400 = 'mysite.views.my_custom_bad_request_view'
```