๐ฒTIL-8๐ฒ

# ๋ชจ๋ธ ๊ฐ์ฒด
- ์ฅ๊ณ  db์ row๋ฅผ ๋ปํ๋ค. 
## ์ ์ฅํ๊ธฐ
### view.py
```py
elif request.method == 'POST':
          // POST๋ก ๋ฐ์ ๋ฐ์ดํฐ๋ค์ ๋ณ์๋ก ์ ์ฅ
        email = request.POST.get('email', None)
        username = request.POST.get('username', None)
        password = request.POST.get('password', None)
        re_password = request.POST.get('re-password', None)
        
        // ๊ฐ ๋ณ์๋ฅผ ๋ชจ๋ธ ํด๋์ค์ ๋งค๊ฐ๋ณ์=์ธ์๊ฐ ์ผ๋ก ๋ฃ์ด์ค
        user = User(email=email, username=username,
                    password=make_password(password))  
        user.save()  // ์ ์ฅ
          return render(request, 'home.html', res_data)
```
- View์ POST ์ฒ๋ฆฌ์์ form์ input ํ๊ทธ๋ค์ ๊ฐ์ ๊ฐ์ ธ์์ ์ ์ฅํ๋ค. ํญ์ ๋ง์ง๋ง์ `๊ฐ์ฒด.save()` ๋ฅผ ํด์ผ ํ  ๊ฒ์ ์ ๋ํ์.
## ๊ฐ์ ธ์ค๊ธฐ
### view.py
```py
email = request.POST.get('email', None)
user = User.objects.get(email=email)
email = user.email
password = user.email
```
- ํด๋น ๊ฐ์ฒด๋ฅผ ํน์  ์กฐ๊ฑด์ผ๋ก ๊ฐ์ ธ์์ db์ row์ colum์ ์ ๊ทผ ํ  ์ ์๋ค.
#### get
```py
user = User.objects.get(email=email)
```
- email ๋ณ์์ ๊ฐ์ ๊ฒ๋ง ๋ฐํ ํ๋ค. get์ ํด๋น ๊ฐ์ฒด๊ฐ 2๊ฐ ์ด์์ผ ๊ฒฝ์ฐ error๊ฐ ๋ฐ์ํ๋ค.
- ๋ณดํต ๊ฐ์ฒด ๋ง๋ค ๋ถ์ฌ๋๋ ๊ณ ์ ์ ์ซ์(๋ฒํธ, ์์)์ธ `pk`๋ฅผ ํตํด get ํ๋ค.
#### all
```py
user = User.objects.all()
```
- ํด๋น ๊ฐ์ฒด๋ฅผ ์กฐ๊ฑด์์ด ๋ชจ๋ ๊ฐ์ ธ์จ๋ค.
#### filter
```py
user = User.objects.filter(email=email)
```
- get๊ณผ ๊ฐ์ด ํน์  ์กฐ๊ฑด์ผ๋ก ๊ฐ์ฒด๋ฅผ ๋ฐํ ๋ฐ๋๋ฐ, get๊ณผ ๋ค๋ฅด๊ฒ ์ฌ๋ฌ ๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ค.
#### exclude
```py
user = User.objects.exclude(email=email)
```
- ํด๋น ์กฐ๊ฑด์ ๋ฐฐ์ ํ๊ณ  ๋ชจ๋  ๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ค.
#### count
```py
user = User.objects.count()
```
- row(๊ฐ์ฒด)์ ์๋ฅผ ๋ฐํ ๋ฐ์ ์ ์๋ค.
```py
user = User.objects.filter(email=email).count()
```
- ์ ์ฒ๋ผ fillter๋ฅผ ์ถ๊ฐํ๋ฉด ํน์ ํ ์กฐ๊ฑด์ผ๋ก row(๊ฐ์ฒด)์ ์๋ฅผ ๋ฐํ ๋ฐ์ ์ ์๋ค.
#### order_by
```py
user = User.objects.order_by('email','-make_date')
```
- `email`์ email์ ๊ธฐ์ค์ผ๋ก ์ฌ๋ฆผ์ฐจ์, `-make_date`์ make_date๋ฅผ ๊ธฐ์ค์ผ๋ก ๋ด๋ฆผ์ฐจ์ ์ผ๋ก ์ ๋ ฌํ๋ค.
#### first
```py
user = User.objects.first(email=email)
```
- ์ ์ผ ์ฒ์์ row ์ฆ, ๊ฐ์ฅ ๋์ pk ๊ฐ์ row(๊ฐ์ฒด)๊ฐ ๋ฐํ๋๋ค.
#### last
```py
user = User.objects.last(email=email)
```
- ์ ์ผ ๋ง์ง๋ง์ row ์ฆ, ๊ฐ์ฅ ๋ฎ์ pk ๊ฐ์ row(๊ฐ์ฒด)๊ฐ ๋ฐํ๋๋ค.

# session
- session์ด๋ผ๋ ๋ณ์์ ์ ์ฅ๋์ด web์ cookie์ ๋จ๊ฒ ๋๋ค.
- ํ๋ฒ ์ ์ฅ๋๋ฉด ๋ค๋ฅธ url ์ฆ, ๋ค๋ฅธ view์ ํจ์์์๋ ์ฌ์ฉํ  ์ ์๋ ๋ฐ์ดํฐ์ด๋ค.
- session์ key, value๋ฅผ ๊ฐ์ง๋ ๋์์ด๋ฆฌ ๋ณ์์ด๋ค
```py
request.session['user_email'] = user.email  # session ๋ณ์์ ์ ์ฅ
```
- ์ธ์ ๋ณ์์ ์ ์ฅ
```py
user_session = request.session.get('user_email')  # ์ ์ฅํ session์์ ๊ฐ ๊ฐ์ ธ์ค๊ธฐ
```
- ์ธ์ ๋ณ์์ user_email ์ด๋ผ๋ key์ ์ ์ฅ๋ ๊ฐ์ ๊ฐ์ ธ์ด
