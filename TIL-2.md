๐ดTIL-2๐ด

# static ํด๋๊ด๋ฆฌ
: CSS๋ JS๋ฅผ ์ํ ํด๋์ด๋ค.
1. settings์ ์ ์ผ ํ๋จ์ `STATICFILES_DIRS = [os.path.join(BASE_DIR,'static')]` ์์ฑ
2. bootstrap 4.3 theme free ๊ฒ์ ํ bootswatch์์ ์ํ๋ ํ๋ง ๋ค์ด
3. static ํด๋์ ๋๋๋&๋๋ํ๊ธฐ
4. html์์ link ์ค์ ํ๊ธฐ

# ํ์ด์ง ๋ณ๊ฒฝ์ ํ๋ฆ
### 1. urls.py (project)
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('user/', include('user.urls')),  # community url-> user url
]
```
: ๋ง์ฝ url์ด `user/`๋ก ์์ํ๋ฉด ๊ทธ๊ฒ์ user์ urls.py๋ก ๊ฐ๋ค.  (user๋ app ์ด๋ฆ)

### 2. urls.py  (app)
```python
urlpatterns = [
   path('login/', views.login)
]
```
: ๋ง์ฝ url์ด `login/` ์ด๋ฉด views์ login ํจ์๋ฅผ ํธ์ถํ๋ค.

### 2. views.py
```python
def login(request):
    return render(request, 'login.html')
```
: login ํจ์๋ login.html ํ์ผ์ ๋ฐํํ๋ค.

### 3. login.html ํ์ผ์ด ์คํ๋์ด ๋ณด์ฌ์ง๋ค.

# ์๋ก์ด ํ์ด์ง ๋ง๋ค๊ธฐ
- ํ์ด์ง ๋ณ๊ฒฝ ํ๋ฆ์ ๋ฐ๋ผ ๋ง๋ค๊ธฐ, import ์ฃผ์
- project์์ ํ๋ฒ ์ง์ ํด์ฃผ๊ณ  app์์ ํ๋ฒ ์ง์ ํด ์ฃผ๋๊ฒ์ด url ๊ฒฝ๋ก๊ฐ ๋๋ค.
- ์์ ๊ฒฝ์ฐ `http://127.0.0.1:8000/user/login`    
    
