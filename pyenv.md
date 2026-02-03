# pyenv

*Guia feito usando Ubuntu, outros sistemas operacionais podem conter mudanças sutis na sintaxe.*

---
#### Gerenciamento de versões

Primeiro, faz-se instalação e desinstalação das versões do Python:
```python
pyenv install 3.XX.X              # instala versão do Python
pyenv uninstall 3.XX.X            # remove versão do Python
```
 
 Também podemos definir a versão do Python em diferentes escopos:
```python
pyenv global 3.XX.X               # define versão global do sistema
pyenv local 3.XX.X                # define versão no diretório do projeto
pyenv shell 3.XX.X                # define versão apenas para a sessão atual
```

É possível consultar a lista de versões disponíveis para instalar e também versões já instaladas:
```python
pyenv install -l                  # lista versões disponíveis
pyenv versions                    # mostra versões instaladas
```

---
#### Criação e ativação do ambiente virtual

Podemos consultar a versão, criar o ambiente virtual, ativar, desativar e remover:
```python
python --version                  # verifica versão do Python
python -m venv .venv              # cria ambiente virtual local
source .venv/bin/activate         # ativa ambiente virtual
deactivate                        # desativa ambiente virtual
rm -rf .venv                      # remove o ambiente virtual
```
Aqui, devemos lembrar que é preciso definir a versão do Python antes de criar o ambiente virtual, pois, o Python do ambiente virtual usará a princípio a versão de uso global.

Verificar binário em execução:
```python
which python                      # caminho do python que roda agora
pyenv which python                # mostra caminho do python ativo
which pip                         # verificar pip
pyenv rehash                      # atualiza shims depois de instalar/remover
```
É importante verificar qual caminho o Python roda, pois assim, você evita erros de ```ModuleNotFoundError``` e garante com que módulos e bibliotecas sejam instalados no ambiente correto.

Instalação, inspeção e validação de pacotes:
```python
python -m pip install <pacote>   # instala pacote no Python ativo
python -m pip list               # lista pacotes instalados
python -m pip show <pacote>      # detalhes do pacote
python -m pip check              # verifica conflitos de dependências
python -m pip freeze             # lista versões fixadas (para requirements)
```
