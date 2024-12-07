# Lista 6 - Álgebra Relacional

[Relações e tuplas](https://ibb.co/4tJ1Dvs)

[Relações - MySQL Workbench](https://ibb.co/zQRx0cD)

- Selecione o endereço e o salário do funcionário de nome ‘Luciana S. Santos’.
  
**R:** `result = π endereco, salario [σ nomeFunc = Luciana S. Santos (Funcionario)]`

- Selecione o nome e o salário dos funcionários que nasceram entre os anos de 1960 e 1969,
inclusive, do sexo feminino e que ganham menos de 1000.

**R:** `result = π nome, salario [σ dataNasc <= 31/12/1969 AND dataNasc >= 01/01/1960 AND sexo = 'F' AND salario < 1000 (Funcionario)]`

- Selecione o nome dos dependentes do funcionário de nome ‘João B. Silva’.

**R:** `idFuncJoaoTmp = π idFunc [σ nomeFunc = João B. Silva (Funcionario)]`
  
`result = π nomeDep[σ Dependente.idFunc = idFuncJoaoTmp.idFunc (Dependente x idFuncJoaoTmp)]`

- Selecione o nome dos projetos que o funcionário de nome ‘Frank T. Santos’ trabalha.

**R**:  `idFrankTmp = π idFunc [σ nomeFunc = Frank T. Santos (Funcionario)]`

`idProjetoTmp = π idProj (Trabalha * idFrankTmp)`

`result = π nomeProj (Projeto * idProjetoTmp)`

- Selecione o nome dos funcionários que trabalham em projetos controlados pelo departamento
de nome ‘ Construção’

**R**:  `idConstrucaoTmp = π idDepto [σ nomeDepto = Construçao (Departamento)]`

`idProjetoTmp = π idProj (Projeto * idConstrucaoTmp)`

`result = π nome (Funcionario * idProjetoTmp)`

- Selecione o nome dos funcionários supervisionados pelo funcionário de nome ‘Frank T.
Santos’.

**R:** `idFrankTmp = π idFunc [σ nomeFunc = Frank T. Santos (Funcionario)]`

`result = π nome [σ idFrankTmp.idFunc = Funcionario.idSuperv (idFrankTmp x Funcionario)]`

- Selecione o nome e endereço dos funcionários que não tem nenhum dependente.

**R:** `sem_dependentes = π idFunc (Funcionario) − π idFunc (Dependente)`

`result = π nome, endereco (sem_dependentes * Funcionario)`

- Selecione o nome dos funcionários que trabalham no departamento de nome ‘Pesquisa’ ou que trabalham no projeto de nome ‘N. Benefícios’.
**R:** `idPesquisaTmp = π idDepto [σ nomeDepto = Pesquisa (Departamento)]`

`idNBeneficiosTmp = π idProj [σ nomeProj =  N. Benefícios(Projeto)]`

`nomeFuncsPesquisaTmp =  π nome (Funcionario * idPesquisaTmp)`

`idFuncsNBeneficiosTmp = π idFunc [σ Trabalha.idProj = idNBeneficiosTmp.idProj (Trabalha x idNBeneficiosTmp)]`

`nomeFuncsNBeneficiosTmp = π nome (Funcionario x idFuncsNBeneficiosTmp)`

`result = nomeFuncsPesquisaTmp U nomeFuncsNBeneficiosTmp`
