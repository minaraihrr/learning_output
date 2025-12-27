# bootstrapの画像について
## 画像幅が親要素を超えないようにする
- `<img class="img-fluid">` をつける  
- 親要素より大きい場合は縮小される
- 親要素より小さい場合は元サイズで表示
```html
    <div class="container">
        <div class="row">
            <div class="col-md-6 col-xl-4">
                <img src="images/test.jpg" class="img-fluid">
            </div>
        </div>
    </div>
```
- 親要素より小さいときに拡大する場合は`w-100`をつける
```html
    <img src="images/test_small.jpg" class="img-fluid w-100">
```