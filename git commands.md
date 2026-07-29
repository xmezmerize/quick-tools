
> [!cite] Step-by-step
> 1. Primeiro, crie um `novo repositório` no github.
> 2. Depois, crie uma pasta em seu computador, acesse a pasta pelo terminal e dê o comando `git init`.
> 3. Em seu github, clique em `<> code` e copie o link _https_ (ou _ssh_, porém será necessário configurar uma chave). Volte para o terminal e dê `git remote add origin <link_copiado>`.
> 4. Depois desses passos iniciais, basta seguir os comandos na ordem **↓↓↓** até o `git push` (onde os arquivos irão ser enviados para o github).

---
##### Criar conexão

Cria um novo repositório Git no diretório atual, inicializando a estrutura de controle de versão:
```
git init
```

Faz conexão com repositório do github:
```
git remote add origin <https://github.com/user/example.git>
```

Mostra o estado atual do repositório:
```
git status
```

Cria pacote de alterações que podem ser salvos no checkpoint:
```
git add .
```

Salva checkpoint:
```
git commit -m "messagem"
```

Envia tudo salvo no checkpoint:
```
git push origin <branch>
```

---
##### Buscando repositório remoto

Baixar as informações do repositório remoto:
```
git fetch <branch>
```

Busca atualizações do checkpoint no repositório remoto e adiciona no diretório da máquina local:
```
git pull origin <branch>
```

Muda para uma branch específica (caso precise puxar algo mais específico):
```
git checkout <branch>
```

---
##### Lidando com branch

Acessa a branch onde será possível puxar _pull_ ou enviar _push_ arquivos:
```
git checkout <branch>
```

A flag `-b` cria e acessa uma nova branch:
```
git checkout -b <branch>
```

Apagar uma branch:
```
git branch -d <branch>
```

Visualiza todas as branchs disponíveis:
```
git branch
```

Integra as alterações de uma branch em outra (cuidado ao usar):
```
git merge <branch>

Ex.

git checkout main
git merge master # Manda todo conteúdo de master para main.
```

---
##### Recuperar um repositório

Listar o histórico de movimentos (ache o commit desejado pela mensagem e copie o hash):
```
git reflog
```

Voltar para um commit específico (local):
```
git reset --hard <hash-do-commit>
```

Após forçar o commit local, esse comando atualiza o repositório remoto com o estado recuperado:
```
git push origin <nome-da-branch> --force
```

---
##### Desfazer mudanças

Descartar alterações em arquivos modificados (não commitados):
```
git restore .
```

Remover arquivos novos (não rastreados):
```
git clean -fd
```

Desfazer o último commit (mantendo as alterações nos arquivos locais):
```
git reset --soft HEAD~1
```

Desfazer o último commit (apagando tudo):
```
git reset --hard HEAD~1
```

> [!DANGER] Troubleshoting
> O comando HEAD funciona como um ponteiro, então lembre-se que ao usar HEAD, o `~ + número` usando são referentes ao número de commits que você quer voltar.
> 
> Ex. `HEAD~2` volta 2 commits | `HEAD~3` volta 3 commits.

---
##### Outros comandos

Atualiza a branch com o repositório remoto e adiciona os commits (Usado em erro):
```
git pull --rebase origin master
```

Forçar o repositório local ficar igual ao Github (cuidado):
```
git reset --hard origin/<branch>
```

Verificar nome do usuário git:
```
git config --global user.name
```

Verificar email usado pelo usuário git:
```
git config --global user.email
```

Exibe o histórico de commits do repositório:
```
git log
```

Remove o .git:
```
rm -rf .git
```
