๐ฒTIL-6๐ฒ

# ๋๊ฐ์ POST ๋ฐ๋ก ์ฒ๋ฆฌํ๋ ๋ฐฉ๋ฒ
- ํ ํฌํ๋ฆฟ ์์ ๋๊ฐ์ form์ด ์กด์ฌํ์ฌ ์ํ๋ POST ์์ฒญ์ด ๋๊ฐ์ผ ๊ฒฝ์ฐ ์ด๋ป๊ฒ ์ฒ๋ฆฌ ํ  ๊ฒ์ธ๊ฐ?

## ํด๊ฒฐ ๋ฐฉ์
- ๋๊ฐ์ form์์ submit์ ๋ด๋นํ๋ ๋ฒํผ์ value ๊ฐ์ ์ฝ์ด ์์ ์ฒ๋ฆฌํ์!
- view์์ submit ๋ฒํผ์ post ๊ฐ์ value ์ด๋ค!

## html
```html
<form method="POST" id="makeroom" name="makeroom"  enctype="multipart/form-data">
  {% csrf_token %}
        <!-- ํฌ๋ก์ค ๋๋ฉ์ธ์ ๋ง๊ธฐ ์ํด ์ฌ์ฉํ๋ ์ฝ๋ -->
        <label for="">Room name
            <input type="text" value="{{string}}" class="room-name" id="room-name" name="room-name" readonly> 
        </label>
        <label for="">Password
            <input type="text" placeholder="Room ๋น๋ฐ๋ฒํธ๋ฅผ ์๋ ฅํ์ธ์." class="room-password" id="room-password" name="room-password" autocomplete="off">
        </label>
</form>

<form method="POST" id="edit" name="edit" enctype="multipart/form-data">
    {% csrf_token %}
    <label for="user-img-change" class="user-img-change">์ด๋ฏธ์ง ์ค์ ํ๊ธฐ</label>
    <input type="file" id="user-img-change" name="user-img-change" accept=".png, .jpeg, .jpg">
    <button class="user-img-btn" id="user-img-btn" name="user-img-btn" value="๋ชจ๋ฌ">๋ณ๊ฒฝํ๊ธฐ</button>
  </form>
```
- ์ด์ ๊ฐ์ด ๋๊ฐ์ ํผ์ด ์กด์ฌ ํ๋ค๋ฉด, ์๋ฅผ๋ค์ด ํ๋์ sumit ๋ฒํผ์ `value="๋ชจ๋ฌ"` ๊ณผ ๊ฐ์ด value๋ฅผ ๋ถ์ฌํ๋ค.

## view
```py
if request.method == 'GET':
     return render(request, 'makeroom.html', res_data)
elif request.method == 'POST':
    post_type = request.POST.get('user-img-btn')  # POST๋ฅผ ์์ํ ๋ value="๋ชจ๋ฌ"์ id๋ฅผ ํตํด์ value๋ฅผ ์ป๋๋ค.
    if post_type == "๋ชจ๋ฌ":  # ๋ฒํผ ๊ฐ์ ์ฝ์ด POST ๊ตฌ๋ถํ๋ค.
        # value = "๋ชจ๋ฌ"์ธ POST ์ฒ๋ฆฌ
        
    else: 
        # ๋ค๋ฅธ POST ์ฒ๋ฆฌ
```
- view์ ํจ์์์ POST๊ฐ ์์ํ์๋ง์ ๋ฒํผ์ value๋ฅผ ์ฝ์ด POST๋ฅผ ๊ตฌ๋ถํ๋ค.
