A arquitetura dos SGBDs tem evoluído desde os primeiros sistemas **monolíticos**, nos quais todo o software SGBD era um **sistema altamente integrado**, até os mais modernos, que têm um **projeto modular**, com arquitetura de **sistema cliente/servidor**.

## Arquitetura Cliente/Servidor
Geralmente, em uma arquitetura básica de SGBD cliente/servidor temos dois módulos: o **módulo cliente** e o **módulo servidor**.

O **módulo cliente** é projetado para ser executado em uma estação de trabalho ou computador pessoal. Em geral, os **programas de aplicação e interfaces com o usuário que acessam o banco de dados, o acessam a partir do módulo cliente**. Assim, esse módulo é encarregado de oferecer interfaces amigáveis ao usuário (formulários ou GUIs).

## Modelos de dados, esquemas e instâncias
Como mencionado nos [conceitos básicos](https://github.com/gabrafo/Intro-SBDs/blob/main/Anota%C3%A7%C3%B5es/Conceitos%20B%C3%A1sicos.md), uma característica fundamento da abordagem de banco de dados é a **abstração de dados**. A **abstração de dados**, geralmente, se refere à supressão de detalhes da organização e armazenamento dos dados., visando facilitar o entendimento lógico (e não, necessariamente, técnico) do que está sendo apresentado ao usuário. 

Um **modelo de dados** - uma **coleção de conceitos que podem ser usados para descrever a estrutura de um banco de dados** (ou seja, os tipos, relacionamentos e restrições que o compõem) - oferece os meios necessários para alcançar essa abstração. A maioria dos modelos de dados também inclui um **conjunto de operações básicas para especificar recuperações e atualizações** no banco de dados.

