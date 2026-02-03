# .gitignore

*Guia feito usando Ubuntu, outros sistemas operacionais podem conter mudanças sutis na sintaxe.*

---
#### Criando o `.gitignore`

Na raiz do projeto, inicie o git:
```
git init
```

Depois, crie o arquivo:
```
touch .gitignore
```
Ou cria manualmente pelo editor.

---
#### Ignorando arquivos

Ignorar arquivos específicos:
```
.env config.json
```

Ignorar extensões:
```
*.log *.tmp
```

Ignorar pastas:
```
node_modules/ dist/ build/
```

Ignorar tudo de um tipo, menos um arquivo:
```
*.env !.env.example
```

Ignorar arquivos em qualquer pasta:
```
**/*.log
```

---
#### Verificação

O `.gitignore` **não funciona para arquivos que já foram commitados**.

Se o arquivo já está no Git, você precisa removê-lo do controle de versão:
```
git rm --cached arquivo.txt
```

Ou uma pasta inteira:
```
git rm -r --cached node_modules
```

Depois:
```
git commit -m "Remove arquivos ignorados"
```

Ver quais arquivos estão sendo ignorados:
```
git status --ignored
```

---
#### Geradores

Geradores prontos de `.gitignore` (geralmente usado em projetos profissionais):

 [https://www.toptal.com/developers/gitignore](https://www.toptal.com/developers/gitignore)

*Escolhe a linguagem (Node, Python, Java, etc.) e pronto*.
