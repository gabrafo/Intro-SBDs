# Modelo Entidade Relacional
O **modelo relacional**, introduzido por **Edgar F. Codd** em 1970, é um dos principais modelos usados para organizar dados em sistemas de gerenciamento de bancos de dados (SGBD). Ele é baseado em conceitos matemáticos da teoria de conjuntos e da lógica de predicados de primeira ordem. A partir de 1980, ele começou a ser amplamente utilizado em implementações comerciais de bancos de dados.

## Conceitos básicos
O modelo relacional representa o banco de dados como uma **coleção de relações**. 

Assim, os dados são organizados em relações, que podem ser pensadas como **tabelas bidimensionais**. Cada relação é composta por um **conjunto de linhas (tuplas) e colunas (representando diversos valores de um mesmo atributo)**. 

Cada linha da tabela contém uma coleção de valores de dados relacionados, que podem ser interpretados como fatos descrevendo uma entidade, ou um relacionamento no mundo real. Além disso, o nome da tabela e os nomes das colunas são usados para ajudar na interpretação do significado dos valores em cada linha da tabela.

![Imagem 34](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2034.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=TvFdpcfjo-A)).

Na imagem acima, temos cinco tuplas, representando cinco entidades diferentes, além de sete atributos diferentes, com valores que variam para cada tupla da relação (tabela).

## Domínio
O tipo de dado que descreve os valores que um atributo pode ter é chamado **domínio**. Cada domínio é um conjunto de valores atômicos/indivisíveis.

### Exemplos de domínios
- **Nome**: O domínio para o atributo "Nome" pode ser um conjunto de cadeias de caracteres que contenham apenas letras.
- **Idade_Aluno**: O domínio para o atributo "Idade_Aluno" pode ser um número inteiro entre 0 e 80.
- **CPF**: O domínio pode ser uma string que segue o formato `ddd.ddd.ddd-dd`, onde cada `d` é um dígito entre 0 e 9.
- **Salário**: O domínio pode ser um número real positivo com duas casas decimais, como `3000.50`, representando um salário.

## Esquema Relacional
É uma expressão da fórmula R(A1, A2, ..., An), onde **R** é o nome da elação, **Ai** é o nome de um atributo (estando associado a um domínio de valores denotado como **dom(Ai)**, que define os valores válidos que esse atributo pode assumir) e **n** é o grau da relação, isto é, o número de atributos presentes na relação.

### Exemplos de Esquema Relacional

1. **Estudante(nome, matrícula, endereço, telefone, dataNasc)**:
    - A relação **Estudante** tem cinco atributos: **nome**, **matrícula**, **endereço**, **telefone**, e **dataNasc**.
    - Cada um desses atributos possui um domínio associado. Por exemplo, **nome** pode estar no domínio de cadeias de caracteres, **dataNasc** no domínio de datas, e assim por diante.

2. **Disciplina(nome, código, cargaHorária, numCréditos)**:
    - A relação **Disciplina** tem quatro atributos: **nome**, **código**, **cargaHorária**, e **numCréditos**.
    - Cada atributo está associado ao seu respectivo domínio. Por exemplo, **código** pode ser uma sequência alfanumérica, e **numCréditos** um número inteiro.

## Relação
Uma relação **r** de um esquema **R**, denotada por **r(R)**, é um conjunto de **n** tuplas: **r = {t1, t2, ..., tn}**. Cada tupla é uma lista ordenada de **m** valores: **t = <v1, v2, ..., vm>**, onde cada valor **vi** (para **1 ≤ i ≤ m**) pertence ao domínio **dom(Ai)** ou pode ser um valor nulo.

```txt
R(A1, A2, ..., Am)
+-----------------------------+
| A1   | A2   | ... | Am       |
+-----------------------------+
| v11  | v12  | ... | v1m      |  <- Primeira tupla (t1)
| v21  | v22  | ... | v2m      |  <- Segunda tupla (t2)
| ...  | ...  | ... | ...      |  <- Continua para as próximas tuplas
| vn1  | vn2  | ... | vnm      |  <- Última tupla (tn)
+-----------------------------+
```
Na tabela acima:
- **R** é a relação.
- **A1, A2, ..., Am** são os atributos (colunas), onde **m** é o número de atributos.
- Cada valor **vi,j** representa o valor do atributo **Ai** na tupla **tj**. Por exemplo:
    - **v11** é o valor do **atributo A1** na **tupla 1**.
    - **v12** é o valor do **atributo A2** na **tupla 1**.
    - E assim por diante para os outros atributos e tuplas.

O valor **NULL** pode aparecer em qualquer uma dessas posições, caso o dado seja desconhecido ou ausente.

Formalmente, uma relação **r(R)** é um subconjunto do produto cartesiano dos domínios que definem **R**:

![Imagem 35](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2035.png)

O produto cartesiano especifica todas as possíveis combinações de valores dos domínios fundamentais. Cada tupla na relação r(R) é uma combinação específica de valores que representa um registro real. Não estamos considerando todas as combinações possíveis (que o produto cartesiano geraria), mas apenas aquelas que realmente existem e são relevantes.

### Características das relações
Uma relação no modelo relacional é composta por tuplas que representam dados específicos. 

- **Ordem das Tuplas**: A ordem das tuplas é irrelevante. 
- **Ordem dos Valores**: A ordem dos valores dentro de uma tupla é relevante, a menos que se estabeleça uma correspondência entre esses valores e os atributos definidos. 
- **Unicidade das Tuplas**: Cada tupla de uma relação é única. 
- **Valores Atômicos**: O valor de cada atributo em uma tupla é atômico; atributos compostos e multivalorados não são permitidos. 

Ademais, o esquema de uma relação pode ser interpretado como uma declaração ou um tipo de afirmação (asserção), com cada tupla podendo ser interpretada como um fato ou uma instância em particular da afirmação.

#### Valores nulos
Podemos ter valores nulos (`NULL`), que representam valores desconhecidos para determinado atributo ou que não se aplicam a esta tupla. Valores `NULL` geralmente são interpretados como: 
- Valores desconhecidos 
- Valores que existem, mas não estão disponíveis 
- Valores indefinidos (atributo não se aplica à tupla)

#### Exemplo de tupla
```txt
t = <BD, 032, 72, 4, NULL>
```
Nesta tupla, os valores representam:
- `BD`: Nome da disciplina
- `032`: Código da disciplina
- `72`: Carga horária da disciplina
- `4`: Número de créditos da disciplina
- `NULL`: Semestre da disciplina (valor desconhecido ou não aplicável)

##### Exemplo de valores em diferentes ordens
- **Tupla 1**:
```txt
t1 = <(nome, BD), (código, 032), (cargaHorária, 72), (numCreditos, 4), (semestre, NULL)>
```
Os valores são apresentados com seus respectivos atributos.

- **Tupla 2**:
```txt
t2 = <(código, 032), (nome, BD), (numCreditos, 4), (semestre, NULL), (cargaHorária, 72)>
```
 Aqui, a ordem dos valores foi alterada, o que pode levar a uma interpretação incorreta se não houver uma correspondência estabelecida entre os valores e os atributos.
 
 ## Esquema de um BD Relacional
 Um **esquema de banco de dados relacional** (denotado por **S**) define dois elementos principais:

- **Um conjunto de esquemas de relações** (**R**): Representado por **R = {R1, R2, ..., Rn}**, onde cada **Ri** é um **esquema de relação**, ou seja, **uma tabela no banco de dados**. Essas tabelas possuem colunas (atributos) e descrevem como os dados serão organizados.
  Exemplo:
- **R1**: Esquema da tabela "Estudantes"
- **R2**: Esquema da tabela "Cursos"

- **Um conjunto de restrições de integridade** (**I**): Representado por **I = {I1, I2, ..., Im}**, onde cada **Ii** é uma **restrição de integridade** (que terá mais detalhes a seguir). Essas restrições são regras que os dados precisam seguir. Por exemplo, uma regra pode dizer que nenhum valor pode ser `NULL` em uma coluna específica, ou que um campo deve ser único (como uma chave primária).

### Estado de um Banco de Dados
O **estado** de um banco de dados (**BD**) reflete o **conjunto atual de dados que está armazenado**. O estado é composto por um conjunto de estados de relação, denotado por **BD = {r1, r2, ..., rn}**, onde cada **ri** é uma instância (ou seja, um conjunto de dados reais) da relação **Ri**.

- **ri**: Representa os dados de uma tabela em um dado momento. Por exemplo, se **R1** for a tabela "Estudantes", **r1** representa os dados que estão atualmente dentro dessa tabela.

Cada estado de relação **ri** deve obedecer às restrições de integridade em **I**. Isso significa que, por exemplo, se houver uma restrição dizendo que a coluna "Matrícula" de um aluno não pode ser nula, o estado atual **r1** da tabela "Estudantes" deve seguir essa regra.

Resumindo, um estado do banco de dados é a situação atual dos dados, ou seja, o conjunto de registros que segue essas regras. Isso pode ser representado por **S = (R, I)**.

## Restrições do Modelo Relacional
No modelo relacional, existem diferentes tipos de restrições que garantem a consistência e integridade dos dados. Elas podem ser classificadas em três categorias principais:

1. **Restrições inerentes (ou implícitas)**:
    - São baseadas no próprio modelo relacional.
    - Não precisam ser declaradas explicitamente, pois fazem parte das regras fundamentais do modelo.
    - Exemplo: A exigência de que uma tupla em uma relação seja única.

2. **Restrições baseadas em esquemas (ou explícitas)**:
    - Podem ser expressas diretamente nos esquemas do modelo de dados.
    - Geralmente são declaradas durante a criação do esquema e dizem respeito aos domínios dos atributos, chaves primárias, chaves estrangeiras, entre outros.
    - Exemplo: Definir que a coluna **código** de uma tabela **Aluno** deve ser única.

3. **Restrições baseadas na aplicação (ou semânticas / regras de negócio)**:
    - Não podem ser diretamente expressas nos esquemas do modelo relacional.
    - São expressas e impostas por meio dos programas de aplicação, ou seja, pelo código da aplicação que interage com o banco de dados.
    - Exemplo: Definir que a carga horária de uma disciplina não pode exceder 100 horas, o que seria uma regra específica de uma aplicação e precisaria ser validada em nível de programação.

### Sobre as restrições explícitas
São formas de restrição explícita:
- Restrição de domínio
  O valor de cada atributo deve ser atômico no domínio do atributo. Isso significa que cada campo em uma tupla contém um único valor, e não uma lista ou conjunto de valores, que obrigatoriamente obedece ao domínio do atributo (exemplo: um nome tem que ser uma sequência de letras).
  
- Restrição de chave 
  **Chave**: Uma chave é um conjunto mínimo de valores dos atributos que identifica unicamente uma tupla. Se há mais de uma chave em um esquema de relação, cada uma é chamada de **chave candidata**, sendo uma delas arbitrariamente escolhida como **chave primária**, enquanto as outras chaves candidatas são chamadas **chaves secundárias/alternativas**. Normalmente, escolhe-se como chave primária a combinação de chaves com o **menor número de atributos**, visando melhor eficiência e simplicidade.
  
  ![Imagem 36](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2036.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=TvFdpcfjo-A)).
  
- Restrição sobre valores nulos 
  Especifica se valores `NULL` são permitidos ou não para cada atributo. Caso um atributo precise ter um valor válido (ou seja, não pode ser `NULL`), deve ser especificado como `NOT NULL` (não nulo). Caso o atributo possa ter um valor nulo, então ele deve ser especificado como `NULL`.

- Restrição de integridade de entidade 
  A chave primária não pode ter valor nulo, justamente por servir para identificar tuplas individualmente.
  
- Restrição de integridade referencial
  A **restrição de integridade referencial** é uma regra que mantém a consistência entre as tuplas de duas relações (ou tabelas) relacionadas em um banco de dados. Ela **garante que, quando uma tupla em uma relação faz referência a outra tupla em outra relação, essa referência é válida**.
  
  **Chave estrangeira**: A integridade referencial é implementada através do conceito de **chave estrangeira**. Uma chave estrangeira é um **conjunto de um ou mais atributos (colunas) em uma relação (tabela) que estabelece um vínculo entre essa relação e outra**.
  
   **A chave estrangeira referencia a chave primária (PK) de outra relação**. Isso significa que o **valor da chave estrangeira deve corresponder a um valor existente na chave primária da tabela referenciada**.
   
   Um conjunto de atributos **FK** em um esquema de relação **R1** é uma chave estrangeira de **R1** que referencia uma relação **R2** se ele satisfaz as duas regras seguintes:
   
   1. **Domínio Correspondente**: Os atributos de **FK** devem ter os mesmos domínios dos atributos da chave primária **PK** de **R2**. Isso implica que os **tipos de dados e as restrições aplicáveis aos atributos devem ser compatíveis**, garantindo que os valores possam ser corretamente comparados e utilizados nas referências.

   2. **Referência Válida**: Um valor de **FK** na tupla **t1** da instância **r1** (da relação **R1**) deve satisfazer uma das duas condições:
    - O valor ocorre como um valor de **PK** para alguma tupla **t2** na instância **r2** (da relação **R2**), o que significa que a referência é válida e aponta para uma tupla existente.
    - Ou o valor é **nulo**, indicando que a tupla **t1** não está associada a nenhuma tupla na relação **R2**, o que também é permitido se a chave estrangeira foi definida para aceitar valores nulos.

**Outra notação para restrição de integridade referencial**  
A notação para a restrição de integridade referencial pode ser expressa como:

![Notação para restrição de integridade referencial](https://latex.codecogs.com/png.image?\dpi{110}\bg{black}&space;R1[FK]\rightarrow&space;opR2[PK])

onde **op** representa a opção de exclusão, dentre as seguintes:

- **Bloqueio (*restrict*)**: Se alguma tupla referencia a tupla a ser excluída, então a exclusão não é efetuada.
- **Propagação (*cascade*)**: Todas as tuplas que referenciam a tupla a ser excluída são excluídas também, automaticamente.
- **Substituição por nulos (*set null*) ou *set default***: Todas as tuplas que referenciam a tupla a ser excluída têm os valores dos atributos da chave estrangeira modificados para nulo (se for permitido nulo) ou pelo valor default, respectivamente, e a exclusão é efetuada.
### Outros Tipos de Restrições
- **Restrições de integridade semântica**  
    Especifica **regras de negócio** da aplicação. Essas regras devem ser especificadas nos programas da aplicação.  Podem também ser especificadas por meio de *triggers* e *assertions*, usando a linguagem SQL.
    Exemplo: O salário de um funcionário não pode ser superior ao salário de seu supervisor.  
    Exemplo: O gerente de um departamento deve trabalhar para aquele departamento.  

- **Dependência funcional**  
    Especifica que o valor de um conjunto de atributos **X** determina um valor exclusivo para outro conjunto de atributos **Y**.  
    É usada no processo de normalização de dados.
    Exemplo: Se sabemos o CPF de um funcionário, podemos determinar exatamente qual é o nome dele.

## Operações de atualização
- **Inserção** (`INSERT`): Insere nova(s) tupla(s) em uma relação. Devemos tomar cuidado com essa operação, pois ela pode violar qualquer dos cinco tipos de restrições discutidas caso não seja feita com cuidado.
- **Exclusão** (`DELETE`): Exclui determinada(s) tupla(s) de uma relação. Essa operação pode violar somente restrição de integridade referencial, caso não seja feita com cuidado.
- **Modificação** (`UPDATE` ou `MODIFY`): Altera os valores de alguns atributos em tuplas existentes. Essa operação pode violar qualquer dos cinco tipos de restrições discutidas, dependendo das alterações realizadas.
	- Modificar um atributo que não é chave primária nem chave estrangeira pode violar **somente as restrições de domínio e de valores nulos**.
	- Modificar a chave primária é **similar a excluir uma tupla e inserir uma nova no seu lugar,** o que pode resultar na violação de qualquer uma das restrições.
	- Alterar um atributo de uma chave estrangeira **pode violar a restrição de integridade referencial ou de domínio**, pois pode resultar em referências inválidas a tuplas não existentes.

