# Algumas coisas no SQL que eu considero mais difíceis

---

## 📌 GROUP BY

### Sintaxe
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

👉 Junta as linhas que têm o mesmo valor e depois você pode usar funções como `COUNT()`, `AVG()`, etc.  

A instrução **GROUP BY** agrupa linhas (registros) que têm os mesmos valores.  
Ele pode ser usado em situações como:  
- Encontrar o número de clientes em cada país  
- Contar o número de vezes que um registro aparece  
- Buscar a quantidade de pedidos por dia  

"PostgresError: a coluna 'order.finished_at' deve aparecer na cláusula GROUP BY ou ser usada em uma função agregada."

Explicando de forma simples:

Quando você usa GROUP BY no PostgreSQL, todas as colunas selecionadas que não fazem parte do GROUP BY precisam ser usadas dentro de uma função agregada (como COUNT(), SUM(), AVG(), etc.).

No seu caso, order.finished_at está no SELECT, mas não está no GROUP BY nem dentro de uma função agregada, por isso o erro.

### Exemplo
```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

---

## 📌 MySQL INNER JOIN

A palavra-chave **INNER JOIN** seleciona registros que possuem valores correspondentes em **ambas as tabelas**.

### Exemplo 1
```sql
SELECT Orders.OrderID, Customers.CustomerName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

### Exemplo 2
```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```

---

## 📌 MySQL LEFT JOIN

A palavra-chave **LEFT JOIN** retorna todos os registros da **tabela da esquerda (table1)** e os registros correspondentes (se existirem) da **tabela da direita (table2)**.

### Sintaxe
```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

### Exemplo
```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
-- A palavra-chave LEFT JOIN retorna todos os registros da tabela da esquerda (Customers),
-- mesmo que não haja correspondências na tabela da direita (Orders).
-- Retorna tudo da: Customers.CustomerID mesmo se não tiver um registro correspondente aqui: Orders.CustomerID
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```

---

## 📌 MySQL RIGHT JOIN

A palavra-chave **RIGHT JOIN** retorna todos os registros da **tabela da direita (table2)** e os registros correspondentes (se existirem) da **tabela da esquerda (table1)**.

### Sintaxe
```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

---

## 📌 O Operador UNION no MySQL

O operador **UNION** é usado para **combinar** o conjunto de resultados de duas ou mais instruções **SELECT**.  

- O operador **UNION** remove automaticamente as linhas duplicadas do conjunto de resultados.  

### ✅ Requisitos para usar o UNION:
1. Cada instrução `SELECT` dentro do `UNION` deve ter o mesmo número de colunas.  
2. As colunas devem ter tipos de dados semelhantes.  
3. As colunas em cada instrução `SELECT` devem estar na mesma ordem.  

---

### Sintaxe
```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

📌 **Nota:** Os nomes das colunas no conjunto de resultados geralmente são iguais aos nomes das colunas da primeira instrução `SELECT`.

---

### Exemplo de SQL UNION
A seguinte instrução SQL retorna as **cidades (apenas valores distintos)** tanto da tabela `Customers` quanto da tabela `Suppliers`:

```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
```

📌 **Nota:** Se alguns clientes ou fornecedores tiverem a mesma cidade, cada cidade será listada apenas uma vez, porque o **UNION** seleciona apenas valores distintos.  
Use `UNION ALL` para também selecionar os valores duplicados!

---

### Outro exemplo
```sql
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
```
