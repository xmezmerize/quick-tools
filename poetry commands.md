
_Guia de comandos Poetry - para configuração e gerenciamento de um ambiente de desenvolvimento_

---
##### Instalação e Configuração Inicial

Depois de instalar o Poetry na sua máquina, verifique a versão em uso:
```python
poetry --version
```

Configura o Poetry para criar a venv dentro do projeto:
```python
poetry config virtualenvs.in-project true
```

Força o Poetry a criar/usar a virtualenv do projeto com uma versão específica do Python:
```python
poetry env use 3.12
```

---
##### Criação de projetos

Cria um projeto completo:
```python
poetry new .
```

Cria apenas o `pyproject.toml`:
```python
poetry init
```

---
##### Gerenciamento de Dependências e Ambiente

Instala pacotes usando poetry:
```python
poetry install <package>
```

Adiciona dependências:
```python
poetry add <package>
```

Adiciona dependências de desenvolvimento (não entra em build de produção):
```python
poetry add --group dev pytest
```

Remove dependência:
```python
poetry remove <package>
```

Atualiza dependências:
```python
poetry update
```

Gera/atualiza `poetry.lock`:
```python
poetry lock
```

---
##### Execução e testes

Executa o projeto:
```python
poetry run python app.py
```

Roda testes:
```python
poetry run pytest -q
```

Entra no `shell`:
```python
poetry shell
```

Sai do `shell`:
```python
exit
```

---
##### Inspeção e Diagnóstico

Lista pacotes instalados:
```python
poetry show
```

Lista árvore de dependências:
```python
poetry show --tree
```

Informações do Poetry na `venv` criada (_caminho completo, versão, local do executável e se o ambiente é venv ou global_):
```python
poetry env info
```

---
##### Manutenção

> [!DANGER] Troubleshoting
> Ao usar ```poetry new .``` devemos ter cuidado, pois, primeiro cria-se o projeto e depois a venv, o contrário dá erro ```Destination /path/path exists and is not empty```.
```python
rm -rf .venv
```

```python
poetry env remove python
```

```python
source .venv/bin/activate
```
