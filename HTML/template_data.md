# template + data-* で動的に生成したHTMLを操作する
## template要素を使用して動的にHTMLを生成する
```html
<html>
<head>
    <title>template</title>
    <body>
        <template id="template">
            <p>テンプレート</p>
        </template>
        <div id="container"></div>
        <script>
            const template = document.getElementById('template');
            const container = document.getElementById('container');
            const clone = template.content.cloneNode(true);
            container.appendChild(clone);
        </script>
    </body>
</html>
```
## templateにdata-*(data-id, data-action) を付与してJSで操作する
```html
<html>
<head>
    <title>template</title>
    <body>
        <template id="template">
            <div data-id="">
            <h2></h2>
            <input type="text">
            <button data-action="submit">送信</button>
            <button data-action="clear">クリア</button>
            </div>
        </template>
        <div id="container"></div>
        <script>
            const data = [
                { id: 1, title: 'タイトル1' },
                { id: 2, title: 'タイトル2' },
                { id: 3, title: 'タイトル3' }
            ]
            const template = document.getElementById('template');
            const container = document.getElementById('container');
            for (let i = 0; i < 3; i++){
                const clone = template.content.cloneNode(true);

                // divにid付与
                clone.querySelector('div').dataset.id = data[i].id;

                // h2にタイトル付与
                clone.querySelector('h2').textContent = data[i].title;

                container.appendChild(clone);
            }

            container.addEventListener('click', (e) => {
                const button = e.target;
                const div = button.closest('div[data-id]'); 
                const id = div.dataset.id;
                const input = div.querySelector('input');

                if (button.dataset.action === 'submit'){
                    alert(`ID: ${id}\n入力値: ${input.value}`);
                } else if (button.dataset.action === 'clear'){
                    input.value = '';
                }
            });
            
        </script>
    </body>
</html>
```