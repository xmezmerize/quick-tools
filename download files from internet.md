
```python
import requests

url = "https://site.com/imagens/foto.png"

resposta = requests.get(url)

with open("foto.png", "wb") as f:
    f.write(resposta.content)
```
