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

5. Selecione o nome dos funcionários que trabalham em projetos controlados pelo departamento de nome ‘Construção’.
```sql
SELECT Funcionario.nomeFunc
FROM Funcionario
NATURAL JOIN Departamento
WHERE nomeDepto = "Construção";
```

 6. Selecione o nome dos funcionários supervisionados pelo funcionário de nome ‘Frank T. Santos’.
```sql
SELECT F.nomeFunc
FROM Funcionario AS F
INNER JOIN Funcionario AS S
WHERE F.idSuperv = S.idFunc AND S.nomeFunc = "Frank T. Santos";
```

 7. Selecione o nome e endereço dos funcionários que não tem nenhum dependente.
```sql
SELECT nomeFunc, endereco
FROM Funcionario
WHERE idFunc NOT IN (
	SELECT idFunc
    FROM Dependente
    WHERE idFunc IS NOT NULL
    );
```

ou

```sql
SELECT Funcionario.nomeFunc, Funcionario.endereco
FROM Funcionario
LEFT JOIN Dependente
ON Funcionario.idFunc = Dependente.idFunc
WHERE Dependente.idFunc IS NULL;
```

 8. Selecione o nome dos funcionários que trabalham no departamento de nome ‘Pesquisa’ ou que trabalham no projeto de nome ‘N. Benefícios’.

 9. Selecione o nome dos funcionários que trabalham em algum projeto controlado pelo departamento cujo gerente é o funcionário de nome ‘Júnia B. Mendes’.

 10. Selecione o nome dos funcionários que trabalham em todos os projetos controlados pelo departamento cujo gerente é o funcionário de nome ‘Júnia B. Mendes’.

 11. Selecione o nome dos funcionários e o nome de seus dependentes. Deve incluir o nome dos funcionários sem dependentes.

 12. Selecione a quantidade de funcionários que trabalham no departamento que controla o projeto de nome ‘ProdZ’.

 13. Selecione o nome dos funcionários e a quantidade de projetos que cada um trabalha mais de 10 horas.

 14. Selecione o nome dos funcionários e a quantidade de projetos que cada um trabalha. Selecione apenas os funcionários que trabalham em mais de um projeto.

 15. Selecione a soma dos salários dos funcionários que trabalham em departamentos que controlam mais de um projeto. O resultado deve vir agrupado por departamento.

 16. Selecione o nome dos funcionários que ganham mais que o maior salário dos funcionários do departamento de nome ‘Construção’. O resultado deve vir ordenado alfabeticamente pelo nome.

 17. Selecione o nome do funcionário e o nome do seu supervisor para todos os funcionários que não são supervisionados pelo funcionario de nome 'Frank T. Santos'.

 18. Aumente em 10% o salários de todos os funcionários que trabalham em mais de um projeto.

 19. Exclua todos os projetos que não têm funcionários trabalhando neles.

 20. Crie uma visão que selecione, para cada departamento, sua identificação, seu nome, mais o nome e o salário de seu gerente. Depois, mostre também exemplos de como usar a visão criada.

 21. Crie um stored-procedure para reajustar o salário dos funcionários de um determinado departamento. A identificação do departamento e o percentual de reajuste são passados como parâmetros. Depois, mostre exemplos de uso do stored-procedure.

22. Crie um stored-procedure para adicionar um funcionário a um projeto. A identificação do funcionário, a identificação do projeto e o número de horas trabalhadas são passados como parâmetros. Depois, mostre exemplos de uso do stored-procedure.

 23. Um funcionário não pode ter um salário maior do que o do seu supervisor. Implemente essa restrição por meio de um conjunto de triggers. Depois, mostre exemplos de disparo dos triggers.

 24. Para um funcionário gerenciar um departamento, é necessário que ele pertença àquele departamento. Implemente essa restrição por meio de um trigger de UPDATE na tabela Departamento. Depois, mostre exemplos de disparo do trigger.

 25. Um funcionário não pode trabalhar mais de 40 horas na soma de horas de seus projetos. Implemente essa restrição por meio de um conjunto de triggers. Depois, mostre exemplos de disparo dos triggers.

 26. Crie um usuário e conceda permissões para que ele: (a) selecione dados de todas as tabelas, (b) execute o stored-procedure criado no exerc. 21 e (c) atualize os dados de funcionário, exceto o salário. Depois, mostre exemplos de testes das permissões. Em seguida, revogue cada permissão e mostre testes das permissões. 
