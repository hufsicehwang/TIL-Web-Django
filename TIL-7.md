๐ฒTIL-7๐ฒ

# form ํ๊ทธ์์ ํ ํฐ
- django์์๋ ํฌ๋ก์ค ๋๋ฉ์ธ์ ๋ง๊ธฐ ์ํด์ formํ๊ทธ ๋ฐ๋ก ํ๋จ์ ํ ํฐ์ ์ง์ ํด์ผํ๋ค.
```html
<form id="login" action="" method="POST">
    {% csrf_token %}
    <!-- ํฌ๋ก์ค ๋๋ฉ์ธ์ ๋ง๊ธฐ ์ํด ์ฌ์ฉํ๋ ์ฝ๋ -->
    <input type="email" id="email" name="email" placeholder="Email">
    <input type="password" id="password" name="password" placeholder="password">
</form>
```

# template ์์
1. base๊ฐ ๋๋ html ์๋จ์ `{% load static %}` ์ถ๊ฐ
2. ` {%block content%}` , `{% endblock %}` ๊ตฌ๊ฐ ์ง์ ํ๊ธฐ
3. settings์ templates์์  `'DIRS': [os.path.join(BASE_DIR,'ํ๋ก์ ํธ์ด๋ฆ/templates')]` ์ค์ ํ๊ธฐ
4. ์์๋ฐ์ html์์, `{%extends 'base.html'%}` , `{% block content%}` , `{% endblock%}` ์ค์ ํ๊ธฐ

# template ๋ณ์
- view์์ htmlํ์ผ์ ๋ฐํํด์ฃผ๋ฉด์ ๋์์ด๋ฆฌ ๋ณ์๋ฅผ ๊ฐ์ด ๋ฐํ ํด์ฃผ๋ฉด ๋ณ์๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.

### view
```py
res_data = {}
res_data['username'] = "ํฉํ์"
return render(request, 'htmlํ์ผ', res_data)
```

### html
```html
<div> {{username}}</div>
```
- html ํ์ผ์์ `ํฉํ์`์ด ์ ์์ ์ผ๋ก ๋ณด์ฌ์ง๋ค.

# template ์กฐ๊ฑด๋ฌธ, ๋ฐ๋ณต๋ฌธ
- django์ html ํ์ผ์์ ์กฐ๊ฑด๋ฌธ๊ณผ ๋ฐ๋ณต๋ฌธ์ ์ฌ์ฉํ  ์ ์๋ค.

```html
<div class="list-wapper">
    {% if ... %}
        # if ์กฐ๊ฑด๋ฌธ ์ฒ๋ฆฌ
        {% for ... in ... %}
            # for ๋ฐ๋ณต๋ฌธ ์ฒ๋ฆฌ
        {% endfor%}
    {% else %}
        # else ์กฐ๊ฑด๋ฌธ ์ฒ๋ฆฌ
    {%endif%}
</div>       
```
- if ์กฐ๊ฑด๋ฌธ๊ณผ for ๋ฐ๋ณต๋ฌธ์ด ๋๋๋ฉด ํญ์ `{%endif%}` , `{% endfor%}` ๋ํ๋ด์ผ ํ๋ค.
