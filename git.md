# Git

*Guia feito usando Ubuntu, outros sistemas operacionais podem conter mudanças sutis na sintaxe.*

---
1. Primeiro, crie um `novo repositório` no github.
2. Depois, crie uma pasta em seu computador, acesse a pasta pelo terminal dê o comando `git init`.
3. Em seu github, clique em `<> code` e copie o link _https_ (ou _ssh_, porém será necessário configurar uma chave). Volte para o terminal e dê `git remote <link_copiado>`.
4. Depois desses passos iniciais, basta seguir os comandos na ordem **↓↓↓** até o `git push` (onde os arquivos irão ser enviados para o github). Você também pode adicionar arquivos pelo próprio github e puxar esses arquivos para a pasta conectada com `git remote`, dando um `git pull` no terminal.
---
Cria um novo repositório Git no diretório atual, inicializando a estrutura de controle de versão.
```
git init
```

Faz conexão com repositório do github.
```
git remote <https://github.com/user/example.git>
```

Acessa a branch onde será possível puxar _pull_ ou enviar _push_ arquivos.
```
git checkout <branch>
```

A flag `-b` cria e acessa uma nova branch.
```
git checkout -b <branch>
```

Visualiza todas as branchs disponíveis.
```
git branch
```

Mostra o estado atual do repositório.
```
git status
```

Cria pacote de alterações que podem ser salvos no checkpoint.
```
git add .
```

Salva checkpoint.
```
git commit -m "messagem"
```

Envia tudo salvo no checkpoint.
```
git push
```

Busca atualizações do checkpoint no repositório remoto e adiciona no diretório da máquina local.
```
git pull
```

Integra as alterações de uma branch em outra. (cuidado ao usar)
```
git merge <branch>

Ex.
git checkout main
git merge master # Manda todo conteúdo de master para main.
```

Baixa as atualizações do repositório remoto sem aplicar na branch atual.
```
git fetch <branch>
```

Exibe o histórico de commits do repositório.
```
git log
```

Atualiza a branch com o repositório remoto e adiciona os commits. (Usado em erro)
```
git pull --rebase origin master
```

Remove o .git.
```
rm -rf .git
```
