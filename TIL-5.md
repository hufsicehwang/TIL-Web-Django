๐ฑTIL-5๐ฑ

# GET
- requst๊ฐ GET์ผ ๊ฒฝ์ฐ๋ url์ ์๋ก ์ง์ ํ๊ฑฐ๋ ์ฒ์์ผ๋ก html ํ์ผ์ด ๋ฐํ ๋์์ ๋์ด๋ค.
- ๋ณดํต GET์ผ ๊ฒฝ์ฐ ํน๋ณํ ๋ฐํ์ ๊ฐ์ง์ง ์๊ณ  ๊ธฐ๋ณธ html์ ๋ฐํํ๋ค.

# POST
- requst๊ฐ POST์ผ ๊ฒฝ์ฐ๋ form ํ๊ทธ ์์์ submit ํ๊ฑฐ๋ ์๋ก๊ณ ์นจ(F5) ํ์ ๊ฒฝ์ฐ์ด๋ค.
- ์ผ๋ จ์ ๊ณผ์ ๋ค์ด POST๋ฅผ ํตํด์ ์ด๋ฃจ์ด์ง๋ ๋งํผ ์ค์ํ๋ค.

# POST ์์ฒญ์ input์ ๊ฐ ๊ฐ์ ธ ์ค๊ธฐ
## html
```html
<form method="POST">
  {% csrf_token %}
  <!-- ํฌ๋ก์ค ๋๋ฉ์ธ์ ๋ง๊ธฐ ์ํด ์ฌ์ฉํ๋ ์ฝ๋ -->
<input type="email" id="email" name="email" placeholder="Email">
<input type="password" id="password" name="password" placeholder="password">
</form>
```
- form์ method๋ `POST`๋ก ์ค์  ํด์ผํ๋ค.
- ํฌ๋ก์ค ๋๋ฉ์ธ์ ๋ง๊ธฐ์ํด `{% csrf_token %}` ๋ฅผ ํผ ํ๊ทธ ์๋์ ๋ฐ๋์ ์์ฑ ํด์ผํ๋ค.
- __inputํ๊ทธ์ id์ name ๊ฐ์__ ๋๋ค ๊ฐ๊ฒ ์ค์  ํด์ผํ๋ค.

## view
```py
def test(request):
    res_data = {}
    if request.method == 'GET':
        return render(request, 'home.html')
    elif request.method == 'POST':
        email = request.POST.get('email', None)
        password = request.POST.get('password', None)
```
- request์ ๋ฉ์๋๊ฐ POST์ผ๋ `request.POST.get('email', None)` ์ ๊ฐ์ด ID ๊ฐ์ผ๋ก input ํ๊ทธ์ ๊ฐ์ ์ ๊ทผ ํ  ์ ์๋ค.
