
_Guia de comando rápido para terminal linux_

---
##### Packages management

Instalação/Atualização de pacotes:
```sh
sudo apt install <package>    # instala um pacote  

sudo apt update    # atualiza índices dos repositórios

sudo apt upgrade -y    # atualiza pacotes instalados (sem trocar dependências-chave)

sudo apt full-upgrade -y    # atualiza e pode instalar/remover dependências para resolver conflitos
```

Remoção/Limpeza de pacotes:
```sh
sudo apt remove <package>    # remove o pacote, mantendo arquivos de configuração

sudo apt purge <package>    # remove o pacote e também seus arquivos de configuração

sudo apt autoremove -y    # remove dependências órfãs

sudo apt clean    # limpa cache em /var/cache/apt/archives

sudo apt autoclean    # limpa apenas pacotes obsoletos do cache
```

informação e busca:
```sh
sudo apt list --upgradable    # lista pacotes que possuem atualização disponível

sudo apt show <package>    # mostra detalhes (descrição, dependências, versão)

sudo apt policy <package>    # mostra versões disponíveis e origem (repo)

sudo apt-cache show <package>    # (legado) informações do pacote

sudo apt-cache policy <package>    # (legado) versões e origem

sudo apt depends <package>    # exibe dependências

sudo apt rdepends <package>    # mostra pacotes que dependem dele
```

---
##### Navigation and interaction

list:
```sh  
ls    # lista

ls -l    # lista detalhada

ls -la    # inclui ocultos

ls -lh    # tamanhos legíveis

ls -lah    # detalhado + ocultos + legível

ls -t    # ordena por data

ls -S    # ordena por tamanho
```

change directory:
```sh
cd ./<folder>/...    # vai pro diretório selecionado

cd | cd ~    # vai pra HOME

cd -    # diretório anterior

cd ..    # sobe um nível

cd ../..    # sobe dois
```

path:
```sh
pwd    # caminho atual

realpath <file>    # caminho absoluto
```

tree:
```sh
tree    # árvore

tree -L 2    # abre níveis
```

make directory e remove directory:
```sh
mkdir <folder>    # cria pasta

mkdir -p a/b/c    # cria hierarquia

rmdir <folder>    # remove pasta vazia

rm -r <folder>    # remove pasta recursivo

rm -rf <folder>    # remove forçado (cuidado!)
```

touch:
```sh
touch <file.txt>    # cria arquivo

touch <file.txt> <file2.txt>    # cria vários arquivos

open <file.txt>    # abre o arquivo

rm <file.txt>    # remove arquivo
```

copy:
```sh
cp <file.txt> <copy.txt>    # copia

cp -r <dir> <dir_copy>    # copia diretório
```

move:
```sh
mv <file.txt> /home/pedrinho/docs/    # move para outra pasta

mv <old.txt> <new.txt>    # renomeia o arquivo

mv folder1/ folder2/    # move pasta1 para dentro de pasta2
```

file:
```sh
file <file.txt>    # tipo do arquivo

stat <file.txt>    # metadados (inode, perms, mtime)

wc -l <file.txt>    # conta linhas

wc -w <file.txt>    # conta palavras

wc -c <file.txt>    # bytes

nl <file.txt>    # numera linhas
```

histórico de comandos:
```sh
history    # mostra o histórico completo de comandos executados  
history | tail    # exibe as últimas entradas do histórico 

!42    # executa o comando de número 42 do histórico

fc -l    # lista histórico no formato usado pelo bash  
```

locale e idioma do sistema:
```sh 
locale    # exibe configurações regionais (idioma, moeda, data) 

localectl status    # mostra idioma e layout do teclado ativos
```

aliases:
```sh  
alias ll='ls -lah'    # cria um atalho (alias) para o comando ls detalhado

unalias ll    # remove um alias existente

alias    # lista todos os aliases ativos
```

---
##### Network security, analysis and monitoring

IP e interfaces de rede:
```sh  
ip a    # mostra interfaces de rede e endereços IP (ao lado de inet) 

ip link    # lista interfaces físicas e virtuais  

ip r    # mostra tabela de rotas (gateway, destinos)  

ip neigh    # exibe tabela ARP (vizinhos conhecidos)  

nmcli dev status    # mostra status de interfaces gerenciadas pelo NetworkManager

curl ifconfig.me    # mostra seu IP público externo 
```

ping e diagnóstico de conectividade:
```sh
ping -c 4 8.8.8.8    # testa conectividade e latência

ping <domain.com>    # testa conexão com um host por nome  

traceroute <domain.com>    # mostra o caminho (saltos) até o destino
 
mtr <domain.com>    # ferramenta interativa que combina ping + traceroute

whois domain.com    # infos do domínio (registro, DNS, datas)
```

monitoramento de portas e conexões:
```sh
sudo ss -tulpn    # lista portas abertas e processos associados
 
sudo lsof -i      # mostra conexões de rede abertas

sudo nmap -sS localhost    # varredura de portas locais (testa exposição)

sudo nmap -sV -p 1-1024 localhost    # escaneia serviços e versões nas portas principais
 
sudo ss -lntp    # lista apenas portas TCP abertas (listen)  

sudo ss -s    # estatísticas de sockets
```

auditoria e logs de segurança:
```sh
sudo last       # lista últimos logins bem-sucedidos

sudo lastb      # lista tentativas de login falhas
 
sudo who -a     # mostra sessões, logins e tempos de inatividade
```

curl e wget — requisições HTTP:
```sh
curl -I <https://site.com>    # exibe apenas os cabeçalhos HTTP da resposta   

curl -o arq.zip <https://site.com>    # baixa o conteúdo para um arquivo específico 
 
wget <https://site.com>    # baixa arquivo do endereço informado
 
wget -c <https://site.com>    # continua download interrompido
```

DNS — resolução de nomes:
```sh
host <domain.com>    # consulta DNS simples (A, AAAA, MX, etc.)  

dig <domain.com>    # consulta DNS detalhada   

nslookup <domain.com>    # consulta DNS (modo clássico)
```

análise e varredura:
```sh  
nmap host    # varre portas e serviços de um host

nmap -sP 192.168.2.0/24    # descobre dispositivos ativos na rede local

arp -n    # mostra tabela ARP (IPs ↔ MACs) 
```

ufw — firewall simplificado:
```sh
sudo ufw status    # mostra o estado atual do firewall e as regras ativas

sudo ufw enable    # ativa o firewall

sudo ufw disable    # desativa o firewall

sudo ufw reload    # recarrega as regras sem desativar o firewall

sudo ufw default deny incoming    # bloqueia todas as conexões de entrada por padrão

sudo ufw default allow outgoing    # permite todas as conexões de saída por padrão
  
sudo ufw limit 22/tcp    # protege contra brute force no SSH (limita tentativas)
  
sudo ufw logging on    # habilita logs de tráfego bloqueado e permitido
  
sudo ufw status verbose    # exibe status detalhado do firewall com políticas padrão
  
sudo ufw reset    # reseta todas as regras e políticas do firewall
```
