# Modelo ER-Relacional

## Introdução
- **Objetivo**: projetar um esquema de banco de dados relacional com base em um projeto de esquema conceitual (ER ou EER).

- **Metodologia**: uso de um algoritmo para conversão do modelo ER em relações.

## Qual seria o passo a passo?
### Entidade Regular
Uma **entidade regular** (ou *entidade forte*) é uma entidade que possui uma chave primária própria e pode ser identificada de forma única sem depender de outras entidades.

#### Regras para Mapear uma Entidade Regular para o Modelo Relacional
1. **Criar uma Relação (Tabela)**: Para cada tipo de entidade regular no modelo ER, crie uma relação (tabela) no banco de dados relacional.
2. **Atributos Simples**: Inclua todos os atributos simples da entidade como colunas na tabela.
3. **Atributos Compostos**: Se a entidade tiver atributos compostos, inclua cada componente simples desses atributos como colunas separadas.
4. **Escolha da Chave Primária**: Defina a chave primária da tabela com base na chave da entidade no modelo ER.  
   - Se a entidade possui uma chave composta, a chave primária será formada pelos componentes da chave composta.
   - Caso a entidade tenha várias chaves candidatas, escolha uma como chave primária e defina as outras como chaves secundárias.

#### Exemplo de Mapeamento
Considere a entidade `Funcionario` com os seguintes atributos:
- `cpf` (chave primária)
- `endereco`
- `salario`
- `sexo`

Neste exemplo, `nome` é um atributo composto que inclui: 
- `Pnome` (primeiro nome) 
- `Minicial` (inicial do nome do meio) 
- `sobrenome`

Para mapear `Funcionario` no modelo relacional:
1. Criamos uma tabela chamada `Funcionario`.
2. Adicionamos colunas para cada atributo simples: `cpf`, `endereco`, `salario` e `sexo`.
3. Dividimos o atributo composto em seus componentes mais simples e incluímos cada um como uma coluna separada.
4. Definimos `cpf` como a chave primária.

##### Estrutura da Tabela `Funcionario`

| cpf       | Pnome | Minicial | sobrenome | endereco   | salario | sexo |
| --------- | ----- | -------- | --------- | ---------- | ------- | ---- |
| 123456789 | Pedro | J        | Silva     | Rua A, 123 | 3000.00 | M    |
|           |       |          |           |            |         |      |

Essa tabela representa a entidade `Funcionario`, onde cada funcionário é identificado de forma única pelo seu `cpf`, que é a chave primária.

### Entidade Fraca
#### Regras para Mapear uma Entidade Fraca para o Modelo Relacional
1. **Criar a Tabela para a Entidade Fraca**: Para uma entidade fraca `F`, é criada uma relação (ou tabela) `R`, contendo todos os atributos simples de `F`. Se `F` tiver atributos compostos, devemos desmembrá-los e incluir cada componente simples como um atributo de `R`.
2. **Incluir Chaves Primárias da Entidade Forte**: A entidade fraca `F` depende de uma entidade forte `E`. Assim, incluímos na tabela `R` (que contém os atributos simples de `F`) todos os atributos da chave primária da tabela que representa `E`. Esses atributos servirão como uma **chave estrangeira** em `R`, estabelecendo a relação entre a entidade fraca e a entidade forte.
3. **Definir a Chave Primária da Entidade Fraca**: A chave primária de `R` será uma **combinação da chave primária de `E`** com a **chave parcial de `F`** (se existir). A chave parcial é um identificador único para a entidade fraca no contexto de sua entidade forte associada.

##### Tabela: `Funcionario`

|cpf|Pnome|Minicial|sobrenome|endereco|salario|sexo|
|---|---|---|---|---|---|---|
|123456789|Pedro|J|Silva|Rua A, 123|3000.00|M|

##### Tabela: `Dependente`

|cpfFunc|nomeDep|sexo|dataNasc|parentesco|
|---|---|---|---|---|
|123456789|Maria|F|12/12/1980|cônjuge|
|123456789|João|M|03/07/2004|filho|
|123456789|Ana|F|05/09/2006|filha|

### Atributos Multivalorados
#### Regras para Mapear um Atributo Multivalorado para o Modelo Relacional
1. **Identifique o atributo multivalorado em uma entidade**
    - Em uma entidade `E` (por exemplo, `Departamento`), encontramos um atributo multivalorado `A` (por exemplo, `localizacao`). Esse atributo representa uma característica da entidade que pode ter múltiplos valores. Por exemplo, um departamento pode estar localizado em vários locais.

2. **Crie uma nova relação (tabela) para o atributo multivalorado**
    - Como o atributo é multivalorado, ele precisa de uma tabela separada (chamada `R`) para armazenar essas informações. No nosso exemplo, criamos a tabela `LocalizacaoDepto` para representar as múltiplas localizações do departamento.

3. **Inclua o atributo multivalorado e a chave primária da entidade**
    - Na nova tabela `R` (ou `LocalizacaoDepto`), inclua:
        - O próprio atributo multivalorado `A` (aqui, `localizacao`).
        - A chave primária `K` da entidade original `E` como chave estrangeira (aqui, `numDepto`), para criar uma relação entre a tabela `R` e a entidade original `E`.

4. **Inclua os componentes simples se o atributo multivalorado for composto**
    - Se o atributo `A` for composto, inclua cada componente simples dele na nova tabela `R`. Por exemplo, se `localizacao` fosse um atributo composto como "cidade e bairro", incluiríamos `cidade` e `bairro` separadamente em `LocalizacaoDepto`.

5. **Defina a chave primária da nova tabela como a combinação de K e A**
    - A chave primária da nova tabela `R` será a combinação de `K` (chave estrangeira que liga a entidade original) e `A` (atributo multivalorado).
    - Isso impede que haja duplicidade. No exemplo, a chave primária da tabela `LocalizacaoDepto` é `(numDepto, localizacao)`, o que significa que cada localização única só pode aparecer uma vez para cada departamento.

##### Entidade: `Departamento`

| numDepto | nomeDepto |
| -------- | --------- |
| 1        | RH        |
| 2        | ADM       |


A tabela `Departamento` possui `numDepto` como chave primária.

##### Tabela para Atributo Multivalorado: `LocalizacaoDepto`

|numDepto|localizacao|
|---|---|
|1|centro|
|1|savassi|
|2|savassi|
