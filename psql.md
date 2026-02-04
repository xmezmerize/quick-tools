# psql

*Guia feito usando Ubuntu, outros sistemas operacionais podem conter mudanças sutis na sintaxe.*

---
#### Login

Entrar no console SQL como postgres _admin_:
```sql
sudo -u postgres psql 
```

Entrar como usuário:
```sql
psql -U <usuario> -d <banco>
```

Criar usuário:
```sql
CREATE USER <usuario> WITH PASSWORD 'senha_forte';
```

Excluir usuário:
```sql
DROP ROLE <usuario>;
```

Garantir privilégios ao usuário:
```sql
GRANT ALL PRIVILEGES ON DATABASE <banco> TO <usuario>;
```

Garantir usar o schema (pasta lógica) público para todos os usuários terem acesso:
```sql
GRANT ALL ON SCHEMA public TO <usuario>; 
```

---
#### Metacomandos

```sql
\l                         -- lista todos os bancos existentes
\conninfo                  -- mostra o banco, o usuário, o socket e a porta
\dn                        -- lista os schemas
\dt                        -- lista todas as tabelas
\du                        -- lista os usuários e suas permissões
\dv                        -- lista views
\df                        -- lista funções
\dp                        -- mostra permissões de tabelas
\d <tabela>                -- lista todas as características da tabela
\c <banco> <usuario>       -- conecta/troca o banco e/ou o usuário dentro do psql
\timing                    -- mostra tempo de execução das queries
\x                         -- ativa/desativa modo expandido (tabelas largas)
\q                         -- sair do psql
```

---
#### INSERT

Criar um banco:
```sql
CREATE DATABASE <banco>; 
```

Criar tabela:
```sql
CREATE TABLE <tabela> (
id UUID PRIMARY KEY  DEFAULT gen_random_uuid(),
name VARCHAR(50) NOT NULL,
amount INTEGER NOT NULL,
description TEXT
);
```

Inserir atributos em uma tabela já existente pelo psql:
```sql
INSERT INTO <tabela> (name, cnpj, endereco, contato, site)
VALUES (
    'Empresa X',
    '12.345.678/0001-99',
    'Rua A, 123',
    '(11) 99999-9999',
    'https://empresa.com'
);
```

---
#### DELETE

Deletar banco:
```sql
DROP DATABASE <banco>;
```

Deletar pelo id:
```sql
DELETE FROM <tabela> WHERE id = '000000000000000';
```

Apagar tabela:
```sql
DROP TABLE <tabela>;
```

Sai de qualquer transação pendente:
```sql
ROLLBACK; 
```

---
#### READ

Verificar usuário e banco de dados:
```sql
SELECT current_user, current_database();
```

Verificar schema ativo na sessão:
```sql
SELECT current_schema();
```

Mostra todos os campos da tabela:
```sql
SELECT * FROM <tabela>;
```

Filtrar resultados:
```sql
SELECT * FROM <tabela> WHERE <coluna> = 'BH';
SELECT COUNT(*) FROM <tabela>;
SELECT <coluna> FROM <tabela> ORDER BY <coluna> ASC;
```

---
#### UPDATE

Update simples:
```sql
UPDATE <tabela>
SET nome = 'Empresa Y'
WHERE id = 'uuid';
```

Update com condição:
```sql
UPDATE <tabela>
SET preco = preco * 1.1
WHERE categoria = 'eletronicos';
```

Upsert (insert ou update):
```sql
INSERT INTO <tabela> (id, nome, email)
VALUES ('uuid', 'Ana', 'ana@email.com')
ON CONFLICT (id)
DO UPDATE SET
nome = EXCLUDED.nome,
email = EXCLUDED.email;
```

---
#### Tipos de dados

```sql
CREATE TABLE exemplo_tipos (
    -- Identificadores
    id_serial        SERIAL PRIMARY KEY,
    id_big           BIGSERIAL,
    id_uuid          UUID DEFAULT uuid_generate_v4(),
	
    -- Inteiros
    int_pequeno      SMALLINT,
    int_normal       INTEGER,
    int_grande       BIGINT,
	
    -- Numéricos
    numero_exato     NUMERIC(10,2),
    numero_real      REAL,
    numero_duplo     DOUBLE PRECISION,
	
    -- Texto
    texto_curto      VARCHAR(100),
    texto_livre      TEXT,
    texto_fixo       CHAR(10),
	
    -- Booleano
    ativo            BOOLEAN DEFAULT true,
	
    -- Datas e tempo
    data_simples     DATE,
    hora_simples     TIME,
    data_hora        TIMESTAMP,
    data_hora_tz     TIMESTAMPTZ,
    intervalo        INTERVAL,
	
    -- JSON
    json_simples     JSON,
    json_estruturado JSONB,
	
    -- Arrays
    lista_texto      TEXT[],
    lista_int        INTEGER[],
	
    -- Binário
    dados_binarios   BYTEA,
	
    -- Enum
    status           VARCHAR(20) CHECK (status IN ('ativo', 'inativo', 'pendente')),
	
    -- Controle
    criado_em        TIMESTAMP DEFAULT now(),
    atualizado_em    TIMESTAMP
);
```

---
#### Roles (grupos)

Criar grupos (roles são grupos para gerenciamento de usuários):
```sql
CREATE ROLE <dev_read>;
CREATE ROLE <dev_write>;
```

Criar usuário e associar aos grupos (roles):
```sql
CREATE USER <usuario> WITH PASSWORD 'senha';

-- associar roles ao usuário
GRANT <dev_read>, <dev_write> TO <usuario>;
```

Permissões por role:
```sql
-- permissões de leitura
GRANT CONNECT ON DATABASE <banco> TO <dev_read>;
GRANT USAGE ON SCHEMA public TO <dev_read>;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO <dev_read>;

-- permissões de escrita
GRANT INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO <dev_write>;
```

---
#### Backup e Restore

Backup simples:
```sql
pg_dump <banco> > backup.sql
```

Criar banco onde vai ser restaurado:
```sql
createdb <novo_banco>
```

Restore:
```sql
psql <novo_banco> < backup.sql
```
