
Criar:
```sql
INSERT INTO <table>(<add>, <add>, <add>)
VALUES (%s, %s, %s)
RETURNING <add>, <add>, <add>
```

Buscar:
```sql
SELECT <add>, <add>, <add>
FROM <table>
WHERE <add> = %s
```

Buscar todos:
```sql
SELECT <add>, <add>, <add>
FROM <table>
```

Atualizar:
```sql
UPDATE <table>
SET <add> COALESCE(%s, <add>),
	<add> COALESCE(%s, <add>),
	<add> COALESCE(%s, <add>)
WHERE <add> = %s
RETURNING <add>, <add>, <add>;
```

Deletar:
```sql
DELETE FROM <table>
WHERE <add> = %s
RETURNING <add>;
```
