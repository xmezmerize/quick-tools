# poetry

*Guia feito usando Ubuntu, outros sistemas operacionais podem conter mudanças sutis na sintaxe.*

---
#### Configuração inicial

```python
poetry new .         # cria um projeto completo
poetry init          # cria apenas o pyproject.toml 
poetry install       # cria venv para o poetry e instala poetry.lock

rm -rf .venv         # caso apareça o erro descrito abaixo
poetry config virtualenvs.in-project true   # cria venv dentro do projeto
poetry env use 3.12  # força o Poetry a criar/usar a virtualenv do projeto com uma versão específica do Python
```
Ao usar ```poetry new .``` devemos ter cuidado, pois, primeiro cria-se o projeto e depois a venv, o contrário dá erro ```Destination /path/path exists and is not empty```.

---
#### Execução

```python
poetry run python app.py    # executa com o venv do projeto
```

---
#### Verificação

```python
ls -la                # verifica o que está oculto
poetry --version      # verifica se o Poetry está instalado
poetry env info       # verifica caminho completo, versão, local do executável e se o ambiente é venv ou global
poetry show           # lista pacotes instalados
poetry show --tree    # lista árvore de dependências
```

---
#### Instalação de pacotes

```python
poetry add <pacote>              # adiciona dependências
poetry remove <pacote>           # remove dependência
poetry update                    # atualiza dependências 
poetry lock                      # gera/atualiza poetry.lock
```

---
#### Shell

```python
poetry shell                     # entra no shell
exit                             # sai do shell
```

---
#### Desenvolvimento

```python
poetry add --group dev pytest    # adiciona dependências de desenvolvimento (não entra em build de produção)
poetry run pytest -q             # roda testes
```

---
#### Como consertar o Poetry

```sh
- poetry --version
- poetry env info
- poetry env remove python
- poetry install
- source .venv/bin/activate
```
