# Lista SQL

1. Selecione o endereço e o salario do funcionário de nome ‘Luciana S. Santos’.
```sql
SELECT endereco, salario FROM Funcionario WHERE nomeFunc = "Luciana S. Santos";
```

2. Selecione o nome e o salário dos funcionários que nasceram entre os anos de 1960 e 1969,
inclusive, do sexo feminino e que ganham menos de 1000.
```sql
SELECT nomeFunc, salario 
FROM Funcionario 
WHERE salario < 1000.00 AND 
dataNasc BETWEEN '1960-01-01' AND '1969-12-31';
```

3. Selecione o nome dos dependentes do funcionário de nome ‘João B. Silva’.
```sql
SELECT nomeDep 
FROM Dependente 
WHERE idFunc = (
    SELECT idFunc 
    FROM Funcionario 
    WHERE nomeFunc = "João B. Silva");
```

4. Selecione o nome dos projetos que o funcionário de nome ‘Frank T. Santos’ trabalha.
```sql
SELECT nomeProj 
FROM Projeto 
WHERE idProj IN (
    SELECT idProj 
    FROM Trabalha 
    WHERE idFunc = (
        SELECT idFunc 
        FROM Funcionario 
        WHERE nomeFunc = "Frank T. Santos"
    )
);
```
