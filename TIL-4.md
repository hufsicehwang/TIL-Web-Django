๐ถTIL-4๐ถ

# render
- render๋ฅผ ์ ์ฉํ๊ฒ ์ฌ์ฉํ๊ธฐ ์ํด์  request, htmlํ์ผ ๋ฟ๋ง ์๋๋ผ ๋์์ด๋ฆฌ ๋ณ์๋ฅผ ๋ฐํ ํด์ผ ํ๋ค.

### view
```py
def study(request):
  res_data = {}
  res_data['name'] = 'ํฉํ์'
  return render(request, index.html, res_data)
```
- html ํ์ผ์ ๋์์ด๋ฆฌ ๋ณ์์ธ res_data๋ฅผ ํจ๊ป ๋ฐํ ํ๋ค.

### templates (index.html)
```html
<a class="test">{{name}}๋ ์๋ํ์ธ์.</a>
```
- ๋ฐํ๋ ๋์์ด๋ฆฌ ๋ณ์ res_data์ key ๊ฐ์ธ name์ `{{name}}` ๊ณผ ๊ฐ์ ํํ๋ก ๋ณ์์ ์ ๊ทผ ํ  ์ ์๋ค.

# redirect
- `from django.shortcuts import redirect` import ํ๋ค์
- `return redirect('/login')` ๊ณผ ๊ฐ์ด ํน์  url์ ์ง์  ํ  ์ ์๋ค.
- render๋ ํด๋น ํจ์์์ render๋ฅผ ํตํด ๋ฐํ ํ์ง๋ง redirect๋ url์ ์ง์ ํ๊ธฐ ๋๋ฌธ์ ํด๋น url ๊ฒฝ๋ก์ ์ง์ ๋ view์ ๋ค๋ฅธ ํจ์์์ ๋ฐํํ๋ค.

