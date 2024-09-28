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
