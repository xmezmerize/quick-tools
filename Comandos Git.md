
# Buscando repositório remoto

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


# Lidando com branch

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
```


# Recuperar um repositório

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


# Desfazer mudanças

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


# Outros comandos

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


# Puxar alterações do repositório remoto

Inicializa a conexão com GitHub:
```
git init
```

Abre conexão com o repositório em evidência:
```
git remote add origin <link>
```

Baixa o histórico de atualizações e todas as ramificações do servidor remoto para a máquina local:
```
git fetch origin
```

Troca para a branch desejada:
```
git checkout <branch>
```

Aplica todas as alterações encontradas no servidor remoto na máquina local:
```
git pull origin <branch>
```

Força a branch local a apontar exatamente para o mesmo ponto da remota 
```
git reset --hard origin/production 
```

Apaga todos os arquivos e pastas locais que não estão rastreados no GitHub 
```
git clean -fd
```
