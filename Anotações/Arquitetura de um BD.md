# Arquitetura de um Banco de Dados
A arquitetura dos SGBDs tem evoluído desde os primeiros sistemas **monolíticos**, nos quais todo o software SGBD era um **sistema altamente integrado**, até os mais modernos, que têm um **projeto modular**, com arquitetura de **sistema cliente/servidor**.

## Arquitetura Cliente/Servidor
Geralmente, em uma arquitetura básica de SGBD cliente/servidor temos dois módulos: o **módulo cliente** e o **módulo servidor**.

O **módulo cliente** é projetado para ser executado em uma estação de trabalho ou computador pessoal. Em geral, os **programas de aplicação e interfaces com o usuário que acessam o banco de dados, o acessam a partir do módulo cliente**. Assim, esse módulo é encarregado de oferecer interfaces amigáveis ao usuário (formulários ou GUIs).

## Modelos de dados, esquemas e instâncias
Como mencionado nos [conceitos básicos](https://github.com/gabrafo/Intro-SBDs/blob/main/Anota%C3%A7%C3%B5es/Conceitos%20B%C3%A1sicos.md), uma característica fundamento da abordagem de banco de dados é a **abstração de dados**. A **abstração de dados**, geralmente, se refere à supressão de detalhes da organização e armazenamento dos dados., visando facilitar o entendimento lógico (e não, necessariamente, técnico) do que está sendo apresentado ao usuário. 

Um **modelo de dados** - uma **coleção de conceitos que podem ser usados para descrever a estrutura de um banco de dados** (ou seja, os tipos, relacionamentos e restrições que o compõem) - oferece os meios necessários para alcançar essa abstração. A maioria dos modelos de dados também inclui um **conjunto de operações básicas para especificar recuperações e atualizações** no banco de dados.

### Categorias de modelos de dados
Modelos de dados de **alto nível** ou **conceituais** oferecem **conceitos que são próximos ao modo como muitos usuários percebem os dados**, enquanto os modelos de dados de **baixo nível** ou físicos oferecem **conceitos que descrevem os detalhes de como os dados são armazenados no computador**, em geral, em discos magnéticos. Normalmente, modelos de baixo nível são voltados para especialistas de computadores, e não usuários finais. 

Dentre esses dois extremos, estão os modelos de dados **representativos** (ou de **implementação**), que oferecem conceitos que **podem ser facilmente entendidos pelos usuários finais**, mas que **não estão muito longe do modo como os dados são organizados e armazenados no computador**.

#### Modelos de dados conceituais
Os modelos de dados conceituais utilizam conceitos como **entidades**, **atributos** e **relacionamentos**. 

- Entidade:
  Uma entidade **representa um objeto ou conceito do mundo real**, como um funcionário ou um projeto do minimundo que é descrito no banco de dados. 

- Atributo:
  Um atributo representa alguma **propriedade de interesse que descreve melhor uma entidade**, como o nome ou o salário do funcionário.

- Relacionamento:
  Um relacionamento entre duas ou mais entidades **representa uma associação** entre elas.

#### Modelos de dados representativos
Os modelos de dados representativos ou de implementação **são os usados com mais frequência** nos SGBDs comerciais tradicionais. Incluem o amplamente utilizado **modelo de dados relacional**, bem como os chamados modelos de dados legados - os **modelos de rede** e **hierárquicos** - que foram bastante usados no passado.

Os modelos de dados representativos mostram os dados usando **estruturas de registro** e, portanto, às vezes são denominados **modelos de dados baseados em registro**.

#### Modelos de dados de objeto
Podemos considerar o modelo de dados de objeto como um exemplo de uma **nova família de modelos de dados de implementação de nível mais alto e que são mais próximos dos modelos de dados conceituais**. Um padrão para bancos de dados de objeto, chamado modelo de objeto **ODMG**, foi proposto pelo grupo de gerenciamento de dados objeto (**ODMG** *Object Data Management Group*).

Os modelos de dados de objeto também são frequentemente utilizados como modelos conceituais de alto nível.

#### Modelos de dados físicos
Os modelos de dados físicos descrevem o armazenamento dos dados como arquivos no computador, com informações como formatos de registro, ordenações de registro e **caminhos de acesso** (estrutura que torna eficiente a busca por registros). Um índice é um exemplo de um caminho que permite o acesso direto aos dados usando um termo de índice ou uma palavra-chave.

### Esquemas, instâncias e estado do banco de dados
#### O que é um esquema? E um diagrama de esquema?
Há uma diferença, em qualquer modelo de dados, entre a descrição do banco de dados e o próprio banco de dados. A descrição é chamada de **esquema**, geralmente criada durante o projeto do sistema. A representação de um esquema é chamada de **diagrama de esquema** (em muitos modelos de dados, esquemas são representados por diagramas). 

![Imagem 2](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%202.png)

Exemplo de diagrama de esquema. 

O diagrama **apresenta a estrutura de cada tipo de registro**, mas **não as instâncias reais dos registros**. Chamamos cada objeto no esquema (como `ALUNO` ou `PRE_REQUISITO`) de **construtor do esquema**.

Um diagrama de esquema representa apenas **alguns aspectos de um esquema**, como os **nomes de tipos de registro** e **itens de dados**, e **alguns tipos de restrições**. A figura acima não mostra nem o tipo de dado de cada item de dados nem os relacionamentos entre os diversos arquivos, assim, sabemos que **muitos tipos de restrições não são apresentados nos diagramas de esquema**.

#### O que é o estado de um objeto no contexto de BDs?
Os dados no banco de dados em **determinado momento** no tempo são chamados de **estado** ou **instante** do banco de dados. Também são chamados de conjunto atual de **ocorrências** ou **instâncias** no banco de dados.

**Toda vez que inserimos ou excluímos um registro ou alteramos o valor de um item de dados em um registro, mudamos de um estado do banco de dados para outro.**

Quando definimos um novo banco de dados, especificamos seu esquema apenas para o SGBD. Nesse ponto, **o estado do banco de dados correspondente é o estado vazio**, sem dados. **Obtemos o estado inicial do banco de dados quando ele é populado ou carregado com os dados iniciais.** Daí em diante, a cada nova operação, obteremos um novo estado do banco de dados. Assim, a qualquer instante no tempo, o banco de dados tem um estado **atual**. **O SGBD é parcialmente responsável por garantir que todo estado do banco de dados seja um estado válido**, ou seja, ele **assegura que não hajam inconsistências** momento algum no histórico do BD.

Portanto, um bom esquema (composto por regras e restrições robustas e inteligentes) é capaz de garantir que o estado do banco de dados sempre seja válido. Para isso, o SGBD armazena as descrições das construções e restrições do esquema (os **metadados**) em seu **catálogo**.

O esquema às vezes é chamado de intenção, e um estado do banco de dados é chamado de extensão do esquema.

Por fim, apesar de sabermos que um esquema é feito para "durar", isto é, não ser alterado frequentemente, é possível que haja no futuro demanda de novas restrições ou de diferentes itens de dados, ou mesmo construtores. Esse processo é conhecido como **evolução do esquema** e realizado a partir de operações próprias para esse processo, visando não trazer instabilidade a um banco de dados em funcionamento.

### Arquitetura de três esquemas e independência de dados
O objetivo da arquitetura de três esquemas é separar as aplicações do usuário do banco de dados físico. 

- Nível interno:
  O nível interno tem um **esquema interno**, que descreve a **estrutura do armazenamento físico do banco de dados**. O esquema interno usa um **modelo de dados físico** e descreve os detalhes completos do armazenamento de dados e caminhos de acesso para o banco de dados.

- Nível conceitual:
  O nível conceitual tem um **esquema conceitual**, que **descreve a estrutura do banco de dados inteiro para uma comunidade de usuários**. Ele utiliza a abstração de dados para ocultar detalhes do armazenamento físico, se focando na descrição de entidades, tipos de dados, relacionamentos, operações do usuário e restrições.

- Nível externo:
  O nível externo ou de visão inclui uma série de **esquemas externos** ou **visões do usuário**. Cada esquema externo **descreve a parte do banco de dados em que um grupo de usuários em particular está interessado** e oculta o restante do banco de dados do grupo de usuários. Cada esquema externo é comumente implementado usando um modelo de dados representativo.

![Imagem 3](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%203.png)

Os processos de transformação de requisições e os resultados entre os níveis são chamados de **mapeamentos**.
#### Independência de dados
- Independência lógica de dados:
  **É a capacidade de alterar o esquema conceitual sem ter de alterar os esquemas externos ou os programas de aplicação.** Exemplo: se faço uma alteração no nível conceitual em uma tabela que não está ligada a uma *view*, a *view* deve seguir intacta após as mudanças.

- Independência física de dados
  **É a capacidade de alterar o esquema interno sem ter de alterar o esquema conceitual (bem como o esquema externo).**  Mudanças no esquema interno podem ser necessárias porque alguns arquivos físicos foram reorganizados para melhorar o desempenho da recuperação ou atualização. No entanto, se os mesmos dados de antes permanecerem no banco de dados, provavelmente não teremos de alterar o esquema conceitual ou externo.

Sempre que temos um SGBD de múltiplos níveis, **seu catálogo deve ser expandido para incluir informações sobre como mapear solicitações e dados entre os diversos níveis**. O SGBD usa software adicional para realizar esses mapeamentos, recorrendo à informação de mapeamento no catálogo.  Nesse sentido, a independência de dados só é possível, porque **quando determinado esquema é alterado, seu(s) esquema(s) de nível mais alto permanece(m) inalterado(s).** Assim, quando um esquema é alterado, apenas o mapeamento entre o esquema alterado e os esquemas de níveis superiores ou inferiores é ajustado, dependendo do nível onde a mudança ocorreu.

A arquitetura de três esquemas pode tornar mais fácil obter a verdadeira independência de dados, tanto física quanto lógica. Porém, os dois níveis de mapeamentos criam uma sobrecarga durante a compilação ou execução de uma consulta ou programa, levando a baixa eficiência do SGBD.

## Linguagens de um Banco de Dados
O sistema precisa oferecer linguagens e interfaces apropriadas para cada categoria de usuário.

Em muitos SGBDs, onde não há uma separação estrita de níveis, uma linguagem chamada **linguagem de definição de dados** (**DDL** - ***Data Definition Language***) é usada pelo DBA e pelos projetistas de banco de dados para **definir os esquemas conceitual e interno**. O **SGBD conta com um compilador da DDL** cuja função é **processar essas instruções, identificar as descrições dos construtores de esquema** (que definem a estrutura do banco de dados) **e armazenar essas informações no catálogo do SGBD**. 

Já **nos SGBDs que mantêm uma separação clara entre os níveis conceitual e interno**, a **DDL é usada para especificar apenas o esquema conceitual**. Outra linguagem, a **linguagem de definição de armazenamento** (**SDL** - ***Storage Definition Language***), é **utilizada para especificar o esquema interno**. 

Para uma verdadeira arquitetura de três esquemas, precisaríamos de uma terceira linguagem, a **linguagem de definição de visão** (**VDL** - ***View Definition Language***), para **especificar visões do usuário e seus mapeamentos ao esquema conceitual**, mas na maioria dos SGBDs a **DDL é usada para definir tanto o esquema conceitual como o externo**. Nos SGBDs relacionais, a **SQL é usada pela VDL para definir visões do usuário** ou da aplicação como resultados de consultas predefinidas.

Quando os esquemas são compilados e o banco de dados é populado, os usuários precisam de alguma forma de manipulá-lo. As manipulações típicas incluem recuperação, inserção, exclusão e modificação dos dados (CRUD). O SGBD oferece um conjunto de operações ou uma linguagem chamada **linguagem de manipulação de dados** (**DML** - ***Data Manipulation Language***) para essas finalidades.

Nos SGBDs atuais, esses tipos de linguagens nor malmente não são considerados linguagens distintas, visto que todas se encaixam como sub-linguagens da linguagem **SQL** (***Structured Query Language***), que é uma linguagem integrada e abrangente utilizada, geralmente, em bancos relacionais. No entanto, a definição do armazenamento físico, em geral, ainda é tratada separadamente, pois serve para ajustar o desempenho do sistema de banco de dados, o que é normalmente responsabilidade dos DBAs.

A linguagem SQL representa uma combinação de DDL, VDL e DML, bem como as instruções para especificação de restrição, evolução de esquema (ou seja, alterações na estrutura do banco de dados ao longo do tempo) e outros recursos. **A SDL era um componente nas primeiras versões da SQL, mas foi removida da linguagem para mantê-la apenas nos níveis conceitual e externo**.
