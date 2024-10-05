# Arquitetura de um Banco de Dados
A arquitetura dos SGBDs tem evoluído desde os primeiros sistemas **monolíticos**, nos quais todo o software SGBD era um **sistema altamente integrado**, até os mais modernos, que têm um **projeto modular**, com arquitetura de **sistema cliente/servidor**.

## Arquiteturas Centralizadas
Nesse tipo de arquitetura apenas uma máquina (geralmente, um *mainframe*) oferece o processamento principal para todas as funções do sistema, incluindo programas de aplicação do usuário e programas de interface com o usuário, bem como toda a funcionalidade do SGBD. 

O motivo dessa arquitetura ter sido tão predominante no passado era que a maioria dos usuários acessava tais sistemas por terminais de computador, que não tinham poder de processamento e apenas ofereciam capacidades de exibição.

![Imagem 5.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%205.png)

## Arquitetura Cliente/Servidor
Geralmente, em uma arquitetura básica de SGBD cliente/servidor temos dois módulos: o **módulo cliente** e o **módulo servidor**.

O **módulo cliente** é projetado para ser executado em uma estação de trabalho ou computador pessoal. Em geral, os **programas de aplicação e interfaces com o usuário que acessam o banco de dados, o acessam a partir do módulo cliente**. Assim, esse módulo é encarregado de oferecer interfaces amigáveis ao usuário (formulários ou GUIs).

### Implementações básicas
A arquitetura cliente/servidor foi desenvolvida para lidar com ambientes de computação em que um grande número de PCs ou outros dispositivos. A ideia é modularizar o trabalho, definindo **servidores especializados** como funcionalidades específicas, assim: uma máquina pode ser, por exemplo, designada como um servidor de impressão, sendo conectada a várias impressoras e processando todas as solicitações de impressão. 

Os recursos fornecidos por um servidor especializado podem ser acessados por muitas **máquinas cliente**. Máquinas cliente oferecem ao usuário interfaces apropriadas para a utilização desses servidores, bem como poder de processamento local para que isso seja possível.

Resumindo:
- **Cliente**: Máquina que oferece capacidades de interface com o usuário e processamento local para executar aplicações locais.

- **Servidor**: Sistema de hardware e software que oferece serviços às máquinas cliente, tais como acesso a arquivos, acesso ao banco de dados, impressão, acesso a determinado serviço na Web, etc.
  
**Quando um cliente requer acesso a alguma funcionalidade adicional** - como acesso ao banco de dados - que não existe nessa máquina, **ele se conecta a um servidor que oferece a funcionalidade necessária**. Em geral, algumas máquinas têm instalados apenas softwares cliente, outras, apenas software servidor, e ainda outras podem incluir software cliente e servidor, conforme ilustrado na representação do funcionamento físico desse tipo de arquitetura disponível logo abaixo.

![Imagem 7.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%207.png)

Representação **física** de uma arquitetura cliente/servidor em duas camadas.

![Imagem 6.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%206.png)

Representação **lógica** da arquitetura cliente/servidor em duas camadas.

#### Implementação de duas camadas
Os componentes de software são distribuídos por dois sistemas: cliente e servidor.

- **Cliente**: Executam os programas da interface com o usuário e os programas de aplicação.

- **Servidor**: No SGBDs relacionais, fornecem as funcionalidades de consulta e de processamento de transações.

Para que isso seja feito, utilizamos dois padrões de comunicação:
- **Padrão ODBC (*Open Database Connectivity*)**: Oferece **interfaces de programação de aplicações** (**API** - *Application Programming Interface*), que **permite que os programas do cliente chamem o SGBD**, desde que as máquinas cliente e servidor tenham o software necessário instalado. A maioria dos vendedores de SGBD oferece drivers ODBC para seus sistemas.
  
- **Padrão JDBC (*Java Database Connectivity*)**: Permite que programas cliente em Java acessem um ou mais SGBDs por meio de uma interface-padrão.
  
#### Implementação de três camadas e *n* camadas
Muitas aplicações Web utilizam uma arquitetura chamada arquitetura de três camadas, que acrescenta uma camada intermediária entre o cliente e o servidor de banco de dados. Essa camada intermediária é chamada de **servidor de aplicação** ou **servidor Web**, dependendo da aplicação. Esse servidor desempenha um papel intermediário pela execução de programas de aplicação e armazenamento de regras de negócios, também podendo melhorar a segurança da aplicação a partir da criptografia. 

Outras arquiteturas também foram propostas. É possível dividir as camadas entre o usuário e os dados armazenados em outros componentes mais detalha dos, resultando, assim, em arquiteturas de *n* camadas, onde *n* pode ser quatro ou cinco camadas. Costumeiramente, a camada de lógica de negócios é dividida em várias camadas nesse tipo de arquitetura. As aplicações de *n* camadas têm a vantagem de que qualquer camada poder ser executada em um processador ou plataforma de sistema operacional adequado e ser tratada independentemente.

![Imagem 8.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%208.png)

Exemplo de arquitetura cliente/servidor de três camadas.

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

#### Tipos de DML
- Não procedural ou Alto nível:
  Usada para especificar operações de banco de dados complexas de forma concisa. Ela pode ser executada de forma interativa em um terminal, ou podem ser embutidas em uma linguagem de programação, necessitando de um pré-compilador no último caso. As DMLs de alto nível, como a SQL, podem especificar e recuperar muitos registros em uma única instrução DML; portanto, elas são chamadas de **DMLs de um conjunto de cada vez** ou **orientadas a conjunto**. Uma consulta em uma DML de alto nível normalmente **especifica quais dados recuperar, em vez de como recuperá-los**; portanto, essas linguagens também são chamadas **declarativas**.

- Procedural ou Baixo nível:
  Uma DML de baixo nível ou procedural deve ser embutida em uma linguagem de programação de uso geral. Esse tipo de DML, em geral, recupera registros individuais ou objetos do banco de dados e processa cada um deles separadamente, portanto, pode precisar de *looping* para ser eficiente em múltiplos objetos. Por tratarem apenas de um registro por vez, são chamadas de **DMLs que tratam um registro por vez**.
  
Sempre que comandos DML, sejam eles de alto ou de baixo nível, são incorporados em uma linguagem de programação de uso geral, ela é chamada de **linguagem hospedeira** e a DML é chamada de **sub-linguagem de dados**. Já uma DML de alto nível usada em uma maneira interativa é chamada **linguagem de consulta** (***query language***).

**OBS:** Em bancos de dados de objeto, as sub-linguagens hospedeiras e de dados formam urna linguagem integrada - por exemplo, C++ com algumas extensões, para dar suporte à funcionalidade de banco de dados.

## Ambiente de um Sistema de Bancos de Dados
### Módulos componentes do SGBD
O banco de dados, bem como seu catálogo, são, geralmente, **armazenados em memória**, portanto, estão sempre sucetíveis ao controle do **sistema operacional** (**SO**), que gerencia as operações de leitura e escrita em disco. Nesse sentido, muitos SGBDs têm seu próprio **gerenciador de buffer**, justamente para organizar por conta própria essas operações, visto que elas são primordiais para garantir um bom desempenho do banco de dados. A redução da leitura/escrita em disco melhora o desempenho de maneira considerável. Ainda, há um modulo **gerenciador de dados armazenados** que controla o acesso às informações do SGBD armazenadas em disco, trabalhando em conjunto com o SO para garantir que as restrições do banco de dados sejam respeitadas corretamente. 

![Imagem 4](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%204.png)

A imagem acima representa como diferentes usuários, a partir de diferentes interfaces de acesso, interagem com o banco de dados, e como isso só é possível a partir de operações de baixo-nível do sistema do BD.

Algo bastante importante também é mencionar como o catálogo é frequentemente consultado e atualizado para a realização de consultas/operações por parte do usuário.

**Compliador de consulta**: Responsável por analisar e validar a sintaxe das consultas enviadas pelos usuários, bem como o nome dos arquivos que as envolvem.

**Otimizador de consulta**: Responsável pelo rearranjo/reordenação de dados a partir de algoritmos inteligentes, removendo quaisquer redundâncias desnecessárias para diminuir ao máximo possível o custo computacional durante a execução de operações no banco de dados.  Ele consulta o catálogo do sistema em busca de informações estatísticas e outras informações físicas sobre os dados armazenados, gerando um código executável que realiza as operações necessárias para a consulta e faz chamadas ao processador em tempo de execução. 

**Pré-compilador**: Ao utilizar uma **linguagem hospedeira** para realizar operações em um banco de dados a partir de uma aplicação, há a necessidade de uma análise prévia dos comandos DML escritos pelo programa. Esses comandos são extraídos por um pré-compilador e enviados a um compilador DML, que os transforma em código objeto para o acesso ao banco de dados. O restante do programa é processado pelo compilador da linguagem hospedeira, e ambos os códigos objeto são combinados, resultando em uma **transação programada**, com um código executável que inclui chamadas ao banco de dados durante a execução. Assim, os usuários podem executar transações programadas, como saques bancários, fornecendo apenas os parâmetros necessários, e **cada execução é considerada uma transação separada**. 

**Processador do banco de dados em tempo de execução**: Recebe as operações de recuperação e modificação e as executa sobre o banco de dados, atualizando o catálogo com estatísticas conforme o necessário, além de utilizar o gerenciador de dados armazenados para que possa executar operações de entrada/saída em baixo nível entre o disco e a memória.

#### Utilitários
**Carregador**: Povoar o banco de dados a partir de um arquivo com dados já existentes.

***Backup***: Criar uma cópia de recuperação do banco de dados, para evitar problemas com falhas de software ou hardware.

**Reorganizador de arquivos**: Utilizado para, como o nome diz, reorganizar arquivos no disco rígido para melhorar a performance do banco de dados.

**Monitor de performance**: Monitora a performance do banco de dados, e oferece estatísticas para o DBA quanto ao desempenho do sistema.
