๐ฆTIL-3๐ฆ

# django MTV

# Model
### 1. model.py ์ค์ 
```python
class User(models.Model):
    email = models.EmailField(max_length=128, verbose_name="์์ด๋")
    username = models.CharField(max_length=64, verbose_name="์ฌ์ฉ์๋ช")
    password = models.CharField(max_length=64, verbose_name="๋น๋ฐ๋ฒํธ")
    registerd_date = models.DateTimeField(auto_now_add=True, verbose_name='๋ฑ๋ก์๊ฐ')
    
    def __str__(self):
        return self.email
        
    class Meta:
        db_table = 'hasik_user'
        verbose_name = '์ฌ์ฉ์ ๋ช๋จ'
        verbose_name_plural = '์ฌ์ฉ์ ๋ช๋จ'  # ๋ณต์๋ช ์ค์ 
```
- ํด๋์ค์์ ํด๋์ค๋ฅผ ๋ง๋ฌ์ผ๋ก์จ db์ ํ์ด๋ธ ์ด๋ฆ์ ์ง์  ํ  ์ ์๋ค.

### 2. admin.py ์ค์ 
```py
from django.contrib import admin
from .models import User
# Register your models here.

class UserAdmin(admin.ModelAdmin):
    list_display =('email','password','username','registerd_date')

admin.site.register(User, UserAdmin)
```
### 3. ๋ช๋ น์ด
- `py manage.py makemigrations` ๋ฅผ ํตํด ๋ชจ๋ธ ๋ง๋ค๊ธฐ
-  `py manage.py migrate`๋ฅผ ํตํด ๋ชจ๋ธ ๋ฑ๋กํ๊ธฐ

# Templates
- ๊ฐ ์ฑ๋ง๋ค `templates`๋ฅผ ํด๋๋ฅผ ์ง์  ๋ง๋ค์ด์ผ ํ๋ค.
- `templates` ํด๋ ์์์ html ํ์ผ์ ๋ง๋ค์ด ์์ฑํ๋ค.
- form ํ๊ทธ์ submit์ ํตํด view์์ ์๊ธฐ ์์ ์ ๋ฐํ ํ๋ ํจ์๋ฅผ ๋ค์ ์คํ ์ํฌ ์ ์๋ค.
  - form์ button์ ๊ธฐ๋ณธ์ ์ผ๋ก submit์ ์ํํ๊ธฐ ๋๋ฌธ์ ๋ฒํผ ํด๋ฆญ์ POST ์์ฒญ์ด ๋๋ ๊ฒ์ด๋ค.
- css ํ์ผ์ `static`ํด๋์์ ๊ด๋ฆฌํ๋ค.
- ๋ฐํ ๋ฐ์ ๋์์ด๋ฆฌ ๋ณ์๋ฅผ `{{key_์ด๋ฆ}}` ๊ณผ ๊ฐ์ด key ๊ฐ์ ์ด์ฉํด ์ฌ์ฉ ๊ฐ๋ฅํ๋ค.

# View
- ์คํ ์ํฌ ๊ฐ ํจ์๋ฅผ ์์ฑํด์ html ํ์ผ์ ๋ฐํ ์ํฌ ์ ์๋ค.
- request๊ฐ GET, POST์ ๋ฐ๋ผ ๋ค๋ฅด๊ฒ ๋ฐํ ๊ฐ์ ๋ถ์ฌ ํ  ์ ์๋ค.
- html์ formํ๊ทธ์์ submit์ ํ๋ค๋ฉด POST ์์ฒญ์ผ๋ก ํจ์๊ฐ ์คํ ๋  ์ ์๋ค.
- __key, value๋ฅผ ๊ฐ์ง๋ ๋์์ด๋ฆฌ ๋ณ์๋ฅผ ์ ์ธํ์ฌ html ํ์ผ๋ก ๋ฐํ ํ  ์ ์๋ค.__
