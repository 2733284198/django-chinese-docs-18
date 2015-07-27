<!--
  ���ߣ�Github@wizardforcel
-->

# �м�� #

�м����һ������Django���������Ӧ�Ĵ�������еĹ��ӿ�ܡ�����һ�����������ײ�ġ������ϵͳ��������ȫ���޸�Django������������

�м��������δ���ĳЩ����Ĺ��ܡ����磬Django����һ���м�������AuthenticationMiddleware ��ʹ�ûỰ���û������������

��ƪ�ĵ��������м����ι�������μ����м�����Լ���α�д�Լ����м����Django������һЩ���õ��м������ֱ�ӿ��伴�á����Ǳ��鵵�� �����м���ο�.

## �����м�� ##

Ҫ����һ���м���������Ҫ������ӵ���Django�����ļ��е�MIDDLEWARE_CLASSES �б��С�

��MIDDLEWARE_CLASSES�У�ÿһ���м��������ַ����ķ�ʽ������һ��������Pythonȫ·�������м���������ơ����磬ʹ�� django-admin startproject�������̵�ʱ�����ɵ�Ĭ��ֵ��

```
MIDDLEWARE_CLASSES = (
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.auth.middleware.SessionAuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'django.middleware.security.SecurityMiddleware',
)
```

Django�ĳ����У��м�����Ǳ���� ��  ֻҪ��ϲ����MIDDLEWARE_CLASSES����Ϊ�� �� ����ǿ���Ƽ�������ʹ��CommonMiddleware��

MIDDLEWARE_CLASSES�е�˳��ǳ���Ҫ����Ϊһ���м����������������һ�������磬AuthenticationMiddleware�ڻỰ�д�������֤���û���������������SessionMiddleware֮�����С�һЩ����Django�м�����˳��ĳ�����ʾ�����Middleware ordering��

## ���Ӻ�Ӧ��˳�� ##

������׶��У�������ͼ֮ǰ��Django�ᰴ��MIDDLEWARE_CLASSES�ж����˳���Զ�����Ӧ���м�������õ��������ӣ�

+ process_request()
+ process_view()

����Ӧ�׶��У�������ͼ֮���м���ᰴ���෴��˳��Ӧ�ã��Ե����ϡ����õ��������ӣ�

+ process_exception() ��������ͼ�׳��쳣��ʱ��
+ process_template_response() ��������ģ����Ӧ��
+ process_response()

![](https://docs.djangoproject.com/en/1.8/_images/middleware.svg)

�����Ը��Ļ�������԰��������һ����У�ÿ���м�����ǰ�����ͼ��һ�㡰Ƥ����

ÿ�����ӵ���Ϊ��������������

## ��д�Լ����м�� ##

��д�Լ����м�������׵ġ�ÿ���м�������һ��������Python��class������Զ�һ�������������Щ������

### process_request ###

**process_request(request)**

request��һ��HttpRequest ����

��Django����ִ���ĸ���ͼ(view)֮ǰ��process_request()�ᱻÿ��������á�

��Ӧ�÷���һ��None ��һ��HttpResponse����������� None, Django����������������ִ������process_request()�м����Ȼ��process_view()�м����ʾ��Ӧ����ͼ�����������һ��HttpResponse����Django�㲻�ٻ�ȥ��������������(request), ��ͼ(view)�������м�������Ӧ����ͼ������HttpResponse���м���ᴦ���κη��ص���Ӧ(response)��

### process_view ###

**process_view(request, view_func, view_args, view_kwargs)**

request��һ��HttpRequest����view_func�� Django����õ�һ��Python�ĺ�����(��ȷʵ��һ���������󣬲��Ǻ������ַ����ơ�) view_args��һ���ᱻ���ݵ���ͼ��λ�ò����б���view_kwargs ��һ���ᱻ���ݵ���ͼ�Ĺؼ��ֲ����ֵ䡣 view_args�� view_kwargs ����������һ����ͼ����(request)��

process_view()����Django������ͼ(view)֮ǰ�����á�

��������None ��һ��HttpResponse ����������� None��������������������ִ��������process_view() �м����Ȼ����ʾ��Ӧ����ͼ���������HttpResponse����Django�Ͳ��ٻ�ȥ������������ͼ��view�����쳣�м����exception middleware�����Ӧ����ͼ ���������Ӧ�м��Ӧ�õ�HttpResponse�ϣ������ؽ����

> ע��
> 
> ���м���ڲ�����process_request����process_view�����з���request.POST����request.REQUEST�����谭���м� ��֮���������ͼ�޷��޸�request���ϴ��������  һ�����Ҫ��������ʹ�á�

> ��CsrfViewMiddleware���Ա���Ϊ�Ǹ�����     ����Ϊ���ṩ��csrf_exempt() �� csrf_protect()����������ͼ����ȷ����     ���ĸ�����Ҫ����CSRF��֤��

### process_template_response ###

**process_template_response(request, response)**

request��һ��HttpRequest����response��һ��TemplateResponse���󣨻�ȼ۵Ķ��󣩣���Django��ͼ�����м�����ء�

�����Ӧ��ʵ����render()������process_template_response()����ͼ�պ�ִ�����֮�󱻵��ã������������һ��TemplateResponse���󣨻�ȼ۵Ķ��󣩡�

����������뷵��һ��ʵ����render��������Ӧ�����������޸ĸ�����response����ͨ���޸� response.template_name��response.context_data���������Դ���һ��ȫ�µ� TemplateResponse��ȼ۵Ķ���

�㲻��Ҫ��ʽ��Ⱦ��Ӧ ���� һ�����е�ģ����Ӧ�м�������ã���Ӧ���Զ�����Ⱦ��

��һ����Ӧ�Ĵ����ڼ䣬�м�����෴��˳�����У������process_template_response()��

### process_response ###

**process_response(request, response)**

request��һ��HttpRequest����response��Django��ͼ�����м�����ص�HttpResponse����StreamingHttpResponse����

process_response()��������Ӧ���������֮ǰ�����á�

����������뷵��HttpResponse����StreamingHttpResponse���������Ըı����е�response�����ߴ����������µ�HttpResponse��StreamingHttpResponse����

���� process_request()��process_view()��������ʹͬһ���м�����е�process_request()��process_view()��������Ϊǰ���һ���м������HttpResponse����������process_response()�������ǻᱻ���á��ر��ǣ�����ζ�����process_response()��������������process_request()�����е����á�

��󣬼�ס����Ӧ�׶��У��м�����෴��˳��Ӧ�ã��Ե����ϡ���˼�Ƕ�����MIDDLEWARE_CLASSES����µ�������ȱ����С�

### ������ʽ��Ӧ ###

����HttpResponse��StreamingHttpResponse��û��content���ԡ����ԣ��м����Ҳ���ܼ���������Ӧ������content���ԡ����������Ҫ�������ݣ����Ǳ�������Ƿ�Ϊ��ʽ��Ӧ������Ӧ�ص����Լ�����Ϊ��

```
if response.streaming:
    response.streaming_content = wrap_streaming_content(response.streaming_content)
else:
    response.content = alter_content(response.content)
```

> ע��
> 
> ������Ҫ����streaming_content���ܻ�����ڴ����޷����ɡ���Ӧ�м�����ܻ������װ���µ��������У�����һ����Ҫ����������װһ���ʵ�ֳ�������
> 
```
def wrap_streaming_content(content):
    for chunk in content:
        yield alter_content(chunk)
```
> 

### process_exception ###

**process_exception(request, exception)**

request��һ��HttpRequest����exception��һ������ͼ�еķ����׳����� Exception����

��һ����ͼ�׳��쳣ʱ��Django�����process_exception()������process_exception()Ӧ�÷���һ��None ����һ��HttpResponse�������������һ��HttpResponse����ģ����Ӧ����Ӧ�м���ᱻӦ�ã���Ӧ����᷵�ظ��������Otherwise, default exception handling kicks in.

�ٴ����ѣ��ڴ�����Ӧ�ڼ䣬�м����ִ��˳���ǵ���ִ�еģ������process_exception�����һ���쳣������м��������һ����Ӧ��������м��������м���������ᱻ���á�

### \_\_init\_\_ ###

��������м���඼����Ҫһ����ʼ����������Ϊ�м�����ඨ�������Ϊprocess\_\*�ṩһ��ռλ���������ȷʵ��Ҫһ��ȫ�ֵ�״̬�ǾͿ���ͨ��\_\_init\_\_�����ء�Ȼ��Ҫ���������������棺

Django��ʼ������м�������κβ�������˲�Ҫ����һ���в�����\_\_init\_\_������
����process\_\*ÿ�����󵽴ﶼҪ����\_\_init\_\_ֻ�ᱻ����һ�Σ�������Web����������ʱ��


### ����м������ʹ�� ###

��ʱ������ʱ�����Ƿ�һ���м����Ҫ�������Ǻ����õġ� ����������£�����м���е� \_\_init\_\_���������׳�һ��django.core.exceptions.MiddlewareNotUsed�쳣��Django����м������������Ƴ��ⲿ���м�������ҵ�DEBUGΪTrue��ʱ����django.request��¼���м�¼������Ϣ��

```
1.8�е��޸ģ�

֮ǰ MiddlewareNotUsed�쳣���ᱻ��¼��
```

## ָ��׼�� ##

+ �м�����಻�����κ�������ࡣ
+ �м�����Դ�������Python·���е��κ�λ�á� Django�����ĵ�ֻ�Ǳ�������MIDDLEWARE_CLASSES�е����á�
+ ��Django��s available middleware��Ϊ������㿴����
+ �������Ϊ��д���м���齨���ܻ�����������ã��ǾͰ������������� ������֪���������ǻῼ�ǰ�����ӵ�Django�С�