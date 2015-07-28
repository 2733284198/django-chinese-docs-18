<!--
  ���ߣ�Github@wizardforcel
-->

# �м�� #

��ƪ�ĵ�������Django�Դ��������м������� Ҫ�鿴�������ʹ�������Լ���α�д�Լ����м��������м��ʹ��ָ����

## ���õ��м�� ##

### �����м�� ###

**class UpdateCacheMiddleware[source]**

**class FetchFromCacheMiddleware[source]**

����ȫվ��Χ�Ļ��档 �����������Щ���棬�κ�һ����Django�ṩ��ҳ�潫�ᱻ���棬����ʱ����������CACHE_MIDDLEWARE_SECONDS�����ж���ġ���������ĵ���

### "����"���м�� ###

**class CommonMiddleware[source]**

����������������һЩ����������

+ ��ֹ����DISALLOWED_USER_AGENTS�����õ��û�������������Ӧ����һ���ѱ����������ʽ������б�
+ ����APPEND_SLASH��PREPEND_WWW����������дURL��

���APPEND_SLASH��ΪTrue����һ��ʼ�ĵ�URLû����б�߽�β��������URLconf��Ҳû�ҵ���Ӧ���壬��ʱ�γ�һ��һ��б�߽�β�µ�URL���������µ�URL������URLconf����ʱDjango���ض������������URL�ϣ�����һ��ʼ��URL�������������

���磬foo.com/bar���ᱻ�ض���foo.com/bar/�������û��Ϊfoo.com/bar������Ч�����򣬵���Ϊfoo.com/bar/��������Ч������

���PREPEND_WWW��ΪTrue��ǰ��ȱ�� "www."��url���ᱻ�ض�����ͬ������һ��"www."��ͷ��url��

����ѡ���Ϊ�˹淶��url�����е���ѧ���ǣ��κ�һ��urlӦ����һ���ط�������һ����������������url foo.com/bar  ������foo.com/bar/ --  �������������������ֿ����� -- ��ˣ����ʵ�����ǹ淶��url��

+ ����  USE_ETAGS  ����������ETag���������USE_ETAGSΪTrue��Django��ͨ��MD5-hashing����ҳ���������Ϊÿһ��ҳ���������Etag������������ʵĻ��������ᷢ��Я��Not Modified����Ӧ��

**CommonMiddleware.response_redirect_class**

```
Django 1.8������
```

Ĭ��ΪHttpResponsePermanentRedirect�����̳���CommonMiddleware������д���������Զ����м���������ض���

**class BrokenLinkEmailsMiddleware[source]**

+ ��MANAGERS�������������ʼ���������󱨸棩��

### GZip�м�� ###

**class GZipMiddleware[source]**

> ����
> 
> ��ȫ�о�Ա������֣���ѹ������������GZipMiddleware������һ����վ��ʱ����վ���ܵ�һЩ���ܵĹ��������⣬��Щ�������������ƻ�Django��CSRF�����������վ��ʹ��GZipMiddleware֮ǰ����Ӧ������ϸ����һ�����վ���Ƿ������ܵ���Щ������ ����㲻ȷ���Ƿ���ܵ���ЩӰ�죬Ӧ�ñ���ʹ�� GZipMiddleware�����the BREACH paper (PDF)��breachattack.com��

Ϊ֧��GZipѹ�����������һЩ�ִ����������ѹ�����ݡ�

���������м���ŵ��м�������б�ĵ�һ��������ѹ����Ӧ���ݵĴ���ᵽ���� ������

����������������Ļ������ݲ��ᱻѹ����

+ ��Ϣ��ĳ���С��200���ֽڡ�
+ ��Ӧ�Ѿ�������Content-EncodingЭ��ͷ��
+ �����������û�з��Ͱ���gzip��Accept-EncodingЭ��ͷ��

�����ͨ�����gzip_page()װ����ʹ�ö�����GZipѹ����

### �������жϵ�GET�м�� ###

**class ConditionalGetMiddleware[source]**

������������ж�״̬GET������ ���һ��������� ETag ����Last-ModifiedЭ��ͷ�������������If-None-Match��If-Modified-Since����ʱ��Ӧ�ᱻ �滻ΪHttpResponseNotModified��

���⣬��������Date��Content-Length��Ӧͷ��

### �����м�� ###

**class LocaleMiddleware[source]**

���������е����ݿ�������ѡ�� ������Ϊÿ���û����ж��ơ� ������ʻ��ĵ���

**LocaleMiddleware.response_redirect_class**

Ĭ��ΪHttpResponseRedirect���̳���LocaleMiddleware����д���������Զ����м���������ض���

### ��Ϣ�м�� ###

**class MessageMiddleware[source]**

��������cookie��Ự����Ϣ֧�֡������Ϣ�ĵ���

### ��ȫ�м�� ###

> ����
> 
> �����Ĳ��𻷾�����Ļ��������ǰ��web������չʾSecurityMiddleware�ṩ�Ĺ����Ǹ������⡣����һ����������κ�����û�б�Django�������羲̬ý����û��ϴ����ļ��������ǻ�ӵ�к���DjangoӦ�õ�������ͬ�ı�����

**class SecurityMiddleware[source]**

```
Django 1.8������
```

django.middleware.security.SecurityMiddlewareΪ����/��Ӧѭ���ṩ�˼��ְ�ȫ�Ľ���ÿһ�ֿ���ͨ��һ��ѡ�����������رա�

+ SECURE_BROWSER_XSS_FILTER
+ SECURE_CONTENT_TYPE_NOSNIFF
+ SECURE_HSTS_INCLUDE_SUBDOMAINS
+ SECURE_HSTS_SECONDS
+ SECURE_REDIRECT_EXEMPT
+ SECURE_SSL_HOST
+ SECURE_SSL_REDIRECT

### HTTP Strict Transport Security (HSTS) ###

������ЩӦ��ֻ��ͨ��HTTPS���ʵ�վ�㣬�����ͨ������HSTSЭ��ͷ��֪ͨ�ִ�����������ܾ��ò���ȫ�����������������������ή�����ܵ�SSL-stripping���м��ˣ�MITM�������ķ��ա�

����㽫SECURE_HSTS_SECONDS����Ϊһ������ֵ��SecurityMiddleware�������е�HTTPS��Ӧ���������Э��ͷ��

����HSTS��ʱ������ʹ��һ��С��ֵ���������Ǹ������⣬���磬��SECURE_HSTS_SECONDS = 3600Ϊһ��Сʱ��ÿ������������վ�㿴��HSTSЭ��ͷ���������ṩ��ʱ����ھ���ʹ�ò���ȫ��HTTP���ķ�ʽ���ӵ����������һ����ȷ����վ���ϵ����ж������԰�ȫ�ķ�ʽ�ṩ�����磬HSTS����������κ����飩���������������ֵ����������������վ����ο�Ҳ�ᱻ���������磬һ������Ϊ31536000�룬һ�꣩��

���⣬����㽫 SECURE_HSTS_INCLUDE_SUBDOMAINS����ΪTrue,��SecurityMiddleware�ὫincludeSubDomains��ǩ��ӵ�Strict-Transport-SecurityЭ��ͷ�С�ǿ���Ƽ�����������������������ȫʹ��HTTPS�����������վ���Ծ��п�����������Ĳ���ȫ���Ӷ��ܵ�������

> ����
> 
> HSTS����������������ж���Ӧ�ã�����������������Э��ͷ����Ӧ�е�url�����ԣ�����������������ΪHTTPS only����Ӧ��ֻʹ��HSTS���ԡ�
> 
> �ʵ���ѭHSTSЭ��ͷ�����������ͨ����ʾ����ķ�ʽ���ܾ����û����ӵ�֤����ڵġ�����ǩ��ġ���������SSL֤����Ч��վ�㡣�����ʹ����HSTS��ȷ�����֤�鴦��һֱ��Ч��״̬��

> ע��
> 
> ������վ�㲿���ڸ��ؾ��������߷������֮�󣬲���Strict-Transport-SecurityЭ��ͷû����ӵ������Ӧ�У�ԭ����Django�п�����ʶ��������һ����ȫ���ӡ��������Ҫ����SECURE_PROXY_SSL_HEADER��

### X-Content-Type-Options: nosniff ###

һЩ������᳢�Բ²������������ݵ����ͣ������Ƕ�ȡContent-TypeЭ��ͷ����Ȼ�������������ò����ķ�����������ʾ���ݣ���Ҳ�ᵼ�°�ȫ���⡣

������վ�������û��ϴ��ļ���һЩ������û����ܻ��ϴ�һ�����Ĺ�����ļ�������������޺���ʱ���ļ��ᱻ��������ͳ�HTML����Javascript��

��֪�����й����Э��ͷ���������δ����������ݣ��������IE��ȫ�����ж�������

Ҫ��ֹ������²��������ͣ�����ǿ����һֱʹ�� Content-TypeЭ��ͷ���ṩ�����ͣ�����Դ���X-Content-Type-Options: nosniffЭ��ͷ��SecurityMiddleware�����������Ӧ�����������SECURE_CONTENT_TYPE_NOSNIFF ����ΪTrue��

ע���ڴ����Django���漰�����ϴ��ļ��Ĳ��𻷾��У�������ò������κΰ��������磬������MEDIA_URL��ǰ��web������ֱ�Ӵ�������nginx��Apache�����������Ҫ�������������Э��ͷ��������һ���棬�����ʹ��Djangoִ��Ϊ�������ļ���������Ȩ֮������飬�����㲻��ʹ�����web����������Э��ͷ��������û�����á�

### X-XSS-Protection: 1; mode=block ###

һЩ������ܹ����ε�����XSS���������ݡ�ͨ��Ѱ��ҳ����GET����POST�����е�JavaScript������ʵ�֡����JavaScript�ڷ���������Ӧ�б��طţ�ҳ��ͻ�ֹͣ��Ⱦ����չʾһ������ҳ��ȡ����

X-XSS-ProtectionЭ��ͷ��������XSS�������Ĳ�����

Ҫ�������������XSS������������ǿ����һֱ���ο��ɵ�XSS�������������Э��ͷ�д���X-XSS-Protection: 1; mode=block��  ���SECURE_BROWSER_XSS_FILTER����ΪTrue��SecurityMiddleware����������Ӧ����������

> ����
> 
> �������XSS��������һ��ʮ����Ч���ֶΣ����ǲ�Ҫ�������������������ܼ�⵽���е�XSS������Ҳ���������������֧����һЭ��ͷ��ȷ����У��͹��������е���������ֹXSS������

### SSL�ض��� ###

�����ͬʱ�ṩHTTP��HTTPS���ӣ�������û���Ĭ��ʹ�ò���ȫ�ģ�HTTP�����ӡ�Ϊ�˸��ߵİ�ȫ�ԣ���Ӧ�ý�����HTTP�����ض���HTTP���ӡ�

����㽫SECURE_SSL_REDIRECT����ΪTrue��SecurityMiddleware�ὫHTTP�������õأ�HTTP 301��permanently���ض���HTTPS���ӡ�

> ע��
> 
> �����������أ������Django����ִ����Щ�ض�����nginx����ǰ�˸��ؾ��������߷�������������ִ�С�SECURE_SSL_REDIRECTר��Ϊ���ֲ����������ƣ����ⲻ��ѡ���ʱ��

���SECURE_SSL_HOST������һ��ֵ�������ض��򶼻ᷢ��ֵ�е�������������ԭʼ������������

�����վ���ϵ�һЩҳ��Ӧ����HTTP��ʽ�ṩ�����Ҳ���Ҫ�ض���HTTPS�������SECURE_REDIRECT_EXEMPT�������г�ƥ����Щurl��������ʽ��

> ע��
> 
> ������ڸ��ؾ��������߷��������������沿��Ӧ�ã�����Django���ܱ���ʲôʱ��һ�������ǰ�ȫ�ģ��������Ҫ����SECURE_PROXY_SSL_HEADER��

### �Ự�м�� ###

**class SessionMiddleware[source]**

�����Ự֧�֡�����Ự�ĵ���

### վ���м�� ###

**class CurrentSiteMiddleware[source]**

```
Django 1.7������
```

��ÿ�����յ���HttpRequest�������һ��site���ԣ���ʾ��ǰ��վ�㡣���վ���ĵ���

### ��֤�м�� ###

**class AuthenticationMiddleware[source]**

��ÿ�����յ���HttpRequest�������user���ԣ���ʾ��ǰ��¼���û������web�����е���֤��

**class RemoteUserMiddleware[source]**

ʹ��web�������ṩ��֤���м�������ʹ��REMOTE_USER������֤��

**class SessionAuthenticationMiddleware[source]**

```
Django 1.7������
```

���û��޸������ʱ��ʹ�û��ĻỰʧЧ������������ʱ�ĻỰʧЧ����MIDDLEWARE_CLASSES�У�����м�����������django.contrib.auth.middleware.AuthenticationMiddleware֮��

### CSRF�����м�� ###

**class CsrfViewMiddleware[source]**

��ӿ�վ������α��ı�����ͨ����POST�����һ�����صı��ֶΣ�������������Ƿ�����ȷ��ֵ�����CSRF�����ĵ���

### X-Frame-Options�м�� ###

**class XFrameOptionsMiddleware[source]**

ͨ��X-Frame-OptionsЭ��ͷ���м򵥵ĵ���ٳֱ�����

## �м�������� ##

������һЩ����Django�м���������ʾ��

**UpdateCacheMiddleware**

�����޸Ĵ���Э��ͷ���м��(SessionMiddleware, GZipMiddleware, LocaleMiddleware)֮ǰ��

**GZipMiddleware**

�����κο����޸Ļ�ʹ����Ӧ��Ϣ����м��֮ǰ��

����UpdateCacheMiddleware֮�󣺻��޸Ĵ�����Э��ͷ��

**ConditionalGetMiddleware**

����CommonMiddleware֮ǰ����USE_ETAGS = Trueʱ��ʹ������Etag Э��ͷ��

**SessionMiddleware**

����UpdateCacheMiddleware֮�󣺻��޸� ����Э��ͷ��

**LocaleMiddleware**

����SessionMiddleware������ʹ�ûỰ���ݣ��� CacheMiddleware������Ҫ�޸Ĵ���Э��ͷ��֮��������档

**CommonMiddleware**

�����κο����޸���Ӧ���м��֮ǰ����Ϊ��������ETags����

��GZipMiddleware֮�󣬲�����ѹ�������������ȥ����ETag��

�����ܷ��ڿ������λ�ã���ΪAPPEND_SLASH����PREPEND_WWW����Ϊ Trueʱ�ᱻ�ض���

**CsrfViewMiddleware**

�����κμ���CSRF�������������ͼ�м��֮ǰ��

**AuthenticationMiddleware**

����SessionMiddleware֮����Ϊ��ʹ�ûỰ�洢��

**MessageMiddleware**

����SessionMiddleware֮�󣺻�ʹ�û��ڻỰ�Ĵ洢��

**FetchFromCacheMiddleware**

�����κ��޸Ĵ���Э��ͷ���м��֮��Э��ͷ�������ӻ���Ĺ�ϣ���л�ȡֵ��

**FlatpageFallbackMiddleware**

Ӧ�÷�������£���Ϊ�����м���еĵ��ơ�

**RedirectFallbackMiddleware**

Ӧ�÷�������£���Ϊ�����м���еĵ��ơ�