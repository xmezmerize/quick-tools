
_Guia rápido destrinchando uma URL por partes (o segredo do funcionamento da web)_

---

> [!info] Exemplo:
> https://api.exemplo.com:8443/users/42/orders/7?status=paid&limit=10

---
##### https (HyperText Transfer Protocol Secure)

É um protocolo de rede (_conjunto de regras oficiais que define como computadores trocam dados na internet_). Garante segurança na troca de dados sensíveis que seriam enviados como texto puro entre navegador/app.

---
##### api.exemplo.com

`exemplo.com` é o DNS (_Domain Name System_) é a "agenda telefônica" da internet. O seu computador não conhece `exemplo.com`. Ele faz uma consulta a servidores DNS para transformar esse nome em um endereço IP (ex: `192.168.1.50`). 

O Subdomínio (`api`): É uma convenção de arquitetura. Ele separa a infraestrutura da API do restante do site (`www.exemplo.com`). Isso permite que a empresa escale servidores específicos apenas para a API, sem sobrecarregar o site institucional.

Exemplo:
> [!question] A estrutura do domínio na TechStore
> 	
>A TechStore divide seus serviços para que cada um funcione de forma independente. Veja como eles organizam os subdomínios:
	>
www.techstore.com:
O site principal (_a "vitrine"_). É onde o cliente final navega, vê fotos e lê descrições. Ele é otimizado para navegadores e busca do Google (_SEO_).
    >
www.blog.techstore.com:
O blog. Fica em outro servidor para não lentificar a loja principal e ter uma estrutura de textos diferente.
    >
www.api.techstore.com:
A "fábrica de dados". Aqui não há fotos para humanos verem, apenas dados (_JSON/XML_). É a parte que recebe pedidos dos Aplicativos mobile (_iOS/Android_) ou sistemas parceiros.

 Por que eles separam o api.techstore.com?
 
1. Escalabilidade Independente: Se a Black Friday chegar e milhares de pessoas começarem a comprar pelo Aplicativo mobile, o tráfego pesado vai para `api.techstore.com`. Você pode aumentar a potência do servidor apenas da API, sem precisar gastar dinheiro aumentando o servidor do Blog ou do site institucional (`www`).
	
2. Segurança (_O conceito de "Zona de Isolamento"_): O (`www`) é aberto ao público e pode ser alvo de ataques constantes (spam, bots de busca). Você pode configurar um Firewall muito mais rígido para o `api.techstore.com`, permitindo apenas requisições autenticadas (_como tokens de usuário_), protegendo o banco de dados de acessos indevidos.
    
3. Configurações Específicas: O (`www`) geralmente precisa de configurações para carregar estilos, imagens e cookies de marketing. A (`api`) precisa de configurações de CORS (_Cross-Origin Resource Sharing_) para permitir que apenas aplicativos autorizados consigam "conversar" com ela.	   

> [!success] O fluxo na prática:
>Imagine que você está no App da TechStore:
	>
>1. O usuário clica em "Ver meus pedidos".
	>
>2. O App não acessa o `www.techstore.com`. Ele sabe que os dados ficam na "fábrica de dados". Então, ele envia a requisição para `api.techstore.com/meus-pedidos`.
    >
>3. O Servidor DNS recebe o pedido: "Ei, onde está o IP de `api.techstore.com`?".
    >
>4. O DNS responde com o IP (ex: _104.21.33.10_).
  >  
>5. A requisição chega ao servidor da API, que processa a lógica de banco de dados e devolve apenas as informações puras, economizando banda e tempo.

---
##### 8443

É a porta. Uma escolha técnica comum quando a porta 443 padrão já está sendo usada pelo servidor web principal ou quando, por questões de segurança (_especialmente em ambientes de desenvolvimento ou firewalls rígidos_), deseja-se usar uma porta alternativa para o tráfego de API. O servidor precisa estar configurado especificamente para "ouvir" (_listen_) nessa porta.

---
##### /users/42/orders/7

> [!info] Path parameters (_segmentos variáveis_)
> 
> `/users/{user_id}/orders/{orders_id}`
>
Eles influenciam no roteamento e identificam recursos.
A lógica de hierarquia: O path representa a "árvore" ou a estrutura de recursos.
	/users/42 → identifica um recurso único (o usuário 42).
    /orders/7 → é um sub-recurso (o pedido 7 daquele usuário).
    
Restful API: Em uma API REST bem desenhada, o path deve seguir uma lógica de substantivos e hierarquia. Você está navegando por um caminho lógico até chegar ao objeto que deseja manipular.

---
##### ?status=paid&limit=10

> [!info] Query parameters
> Separados por `chave=valor`, mudam consulta e não fazem parte do path. Você notou algo crucial: eles "não mudam o recurso".
	Path = O quê: Identifica o recurso (o conjunto de pedidos do usuário 42).
    Query = Como: Modifica a forma como você visualiza esse recurso.
    
`status=paid`: Você não quer todos os pedidos, quer filtrar apenas os pagos.
`limit=10`: Você não quer todos de uma vez (_paginação_), quer apenas 10.
