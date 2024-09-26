# Conceitos básicos

## O que são dados?
Fatos conhecidos que podem ser armazenados e que têm algum significado implícito. Dados, por si só, são "brutos" e só ganham significado quando organizados ou processados de alguma forma, tornando-se informações úteis.
*Exemplo*: Uma coleção de nomes, endereços e telefones das pessoas que você conhece.

## O que são bancos de dados?
Coleção de dados relacionados com as seguintes propriedades implícitas:
- **Representa algum aspecto do mundo real**, às vezes chamado de mini mundo ou de universo de discurso (UoD *Universe of Discourse*). As mudanças no minimundo são refletidas no banco de dados.
- É uma **coleção logicamente coerente de dados** com algum significado inerente. Ou seja, uma variedade aleatória de dados não pode ser corretamente chamada de banco de dados.
- É projetado, construído e "povoado" com dados para um **propósito específico**. Ele possui um grupo definido de usuários e algumas aplicações previamente concebidas nas quais esses usuários estão interessados.

Assim, um banco de dados tem **alguma fonte de origem para suas informações**, além de alguma **interação com eventos no mundo real** (a compra de um produto, por exemplo, vai gerar uma diminuição no estoque) e tem um **público-alvo interessado em seu conteúdo**.

Para que um banco de dados seja preciso e confiável o tempo todo, **ele precisa ser um reflexo verdadeiro do minimundo que representa**; para isso, as mudanças decorrentes de eventos no mundo real precisam ser refletidas no banco de dados o mais breve possível.

Bancos de dados podem ser gerados e mantidos manualmente (como uma [lista telefônica](https://pt.wikipedia.org/wiki/Lista_telef%C3%B4nica#:~:text=Lista%20telef%C3%B4nica(pt-BR)%20ou%20lista%20telef%C3%B3nica(pt)%20%C3%A9%20uma%20publica%C3%A7%C3%A3o%20destinada%20%C3%A0)), ou podem ser computadorizados (com a utilização de um Sistema Gerenciador de Bancos de Dados) e automatizados via software.

### E um Sistema Gerenciador de Bancos de Dados (SGBD)?
É uma coleção de programas que permite ao usuário criar e manter um banco de dados. O propósito desse software é facilitar os processos de **definição, construção, manipulação e compartilhamento** de bancos de dados entre várias aplicações e usuários. Outras funções de um SGBD incluem: **proteção do banco de dados** (contra falhas de hardware ou software, e também contra acesso não autorizado/malicioso) e **manutenção**.

Um SGBD pode ser de uso geral (os comercializados, como: ([MySQL](https://www.mysql.com/), [PostgreSQL](https://www.postgresql.org/), [OracleDB](https://www.oracle.com/database/#:~:text=Oracle%20Database%20on%20Oracle%20Cloud%20Infrastructure.%20Benefit%20from%20the%20computing), etc) ou de uso especial (nesse caso, sendo desenvolvido sob medida para o banco de dados a ser gerenciado).

- **Definir** um banco de dados envolve especificar os **tipos, estruturas e restrições** dos dados a serem armazenados. A definição ou informação descritiva do banco de dados também é armazenada pelo SGBD na forma de um catálogo ou dicionário, chamado de **metadados**.
  **Metadados** são a explicação do que cada dado representa. Isto é, em um banco de dados, "nome" é um metadado que auxilia no entendimento do dado "Gabriel".
  
- A **construção** do banco de dados é o processo de armazenar os dados em algum meio controlado pelo SGBD.
  
- A **manipulação** de um banco de dados inclui funções como consulta ao banco de dados para recuperar dados específicos, atualização do banco de dados para refletir mudanças no minimundo e geração de relatórios com base nos dados.
  Podemos simplificar a maioria das operações de manipulação na sigla **CRUD** (do inglês: *Create, Read, Update, Delete*).
  
- O compartilhamento de um banco de dados permite que diversos usuários e programas acessem-no simultaneamente.

### Aplicações de bancos de dados
Bancos de dados podem ser utilizados desde em sistemas comerciais tradicionais, a aplicações mais complexas envolvendo conteúdo multimídia ou de teor geográfico (dados de satélites, por exemplo). Existem também bancos de dados direcionados especificamente para o armazenamento e consulta de grandes volumes de informação (*Big Data*), geralmente tratados com o uso de modelos de dados não-relacionais.

Além disso, bancos de dados também podem ser utilizados em sistemas envolvendo *data warehouses* (armazéns de dados) e processamento analítico online (OLAP), onde, geralmente, faz-se uso de técnicas de mineração de dados para retirada de análises importantes daquele repositório de dados brutos.

Bancos de dados, assim como citado anteriormente, podem ser usados para o processo de mineração de dados, mas também em outras áreas, como recuperação de informação, análise de sentimentos, ciência de dados, etc.

### Sistema de Banco de Dados
Refere-se ao **conjunto completo** que inclui tanto o **SGBD** quanto o **banco de dados** (dados e suas estruturas) em si. 

![Imagem 1](https://github.com/gabrafo/Intro-SBDs/blob/7b5bfc1a92409b45988bef37608ce7cb33f754df/Anexo/Imagem%201.png)

### Diferenças entre abordagem: processamento de arquivo x banco de dados
- Processamento de arquivo (tradicional): cada usuário define e implementa os arquivos necessários para uma aplicação de software específica como parte da programação da aplicação.

  **Exemplo**: Em um hospital, a secretária e o médico podem ter necessidades diferentes em relação aos dados dos pacientes, levando à criação de arquivos separados.
  
  **Secretária**: Ela pode precisar de informações como nome, contatos de emergência e endereço do paciente para agendar consultas e fazer follow-ups. Portanto, ela mantém um arquivo específico com esses dados, por exemplo, "dados_contato_paciente.txt".
  
  **Médico**: Por outro lado, o médico pode estar mais interessado em informações clínicas, como tipo sanguíneo, peso e histórico médico do paciente. Ele pode criar um arquivo separado, chamado "dados_clinicos_paciente.txt", para armazenar essas informações.
  
  Essa situação geraria uma redundância, causando desperdício de espaço de armazenamento e em esforços para manter os dados comuns entre ambos os usuários atualizados.

- Banco de dados: na abordagem de banco de dados, um único repositório mantém dados que são definidos uma vez e depois acessados por vários usuários. 
  
  **Exemplo**: No sistema hospitalar mencionado acima, ambos os usuários (a secretária e o médico) acessariam o mesmo repositório de dados, buscando os dados que os interessam sobre aquele mesmo paciente. Isso, obviamente, tiraria um pouco da liberdade de nomear os elementos de dados, mas traria consequências positivas no que se diz respeito a facilidade de organização.
  
### Autodescrição de um sistema de banco de dados
Em um banco de dados, o sistema contém não apenas o próprio banco de dados, mas também uma **definição ou descrição completa de sua estrutura e restrições**. Essa definição é armazenada no catálogo do SGBD, sendo chamada de **metadados**.

O catálogo é **usado pelo software de SGBD e também pelos usuários do banco de dados** que precisam de informações sobre a estrutura do banco de dados.

A abordagem de processamento de arquivo faz com que seus programas responsáveis por lidar com os dados **trabalhem com apenas um banco de dados específico**, cuja estrutura é declarada nos programas de aplicação (podendo ser com uma sintaxe em C++, por exemplo), enquanto o **SGBD permite acessar múltiplos bancos de dados por meio do catálogo**, que contém as definições dos dados.

As definições de um catálogo são especificadas pelo projetista antes da criação do banco de dados real.

## Abstração de dados
A característica que permite a independência de dados do programa e a independência da operação do programa é chamada de **abstração de dados**. Um SGBD oferece aos usuários uma **representação conceitual de dados** que **não inclui muitos dos detalhes de como os dados são armazenados ou como as operações são implementadas.**

Resumindo, um **modelo de dados** é um tipo de abstração de dados usado para fazer essa representação conceitual. **O modelo de dados usa conceitos lógicos**, como objetos, suas propriedades e seus inter-relacionamentos, **que podem ser mais fáceis para os usuários entenderem** do que o que realmente acontece na memória do computador. 

Logo, **o modelo de dados oculta** (isto é, **abstrai**) **os detalhes de armazenamento e implementação que não são do interesse da maioria dos usuários de banco de dados.**

A implementação interna de um arquivo pode ser definida, em uma simplificação, por seu tamanho de registro - o número de caracteres (bytes) em cada registro - e cada item de dados pode ser especificado pelo byte inicial dentro de um registro e seu tamanho em bytes. No entanto, um usuário de banco de dados, geralmente, não quer saber essas informações técnicas, mas sim sobre o funcionamento lógico e intelectivo do sistema.

**Exemplos de modelos de dados são: modelo objeto-relacional, modelo orientado a objetos, modelos não-relacionais, etc.** 

Nos bancos de dados orientados a objeto e objeto-relacional, o processo de abstração inclui não apenas a estrutura dos dados, mas também as operações sobre os dados. Essas operações oferecem uma abstração das atividades do minimundo que são mais fáceis de o usuário entender.

### Independência de dados do programa
No processamento de arquivos tradicional, a estrutura dos arquivos de dados está embutida nos programas de aplicação, assim, se houver uma mudança nessa estrutura, pode haver uma exigência de mudança em todos os programas que acessam esse arquivo. Já em programas que acessam o SGBD isso é mais incomum, visto que **a estrutura dos arquivos de dados é armazenada no catálogo (separadamente dos programas de acesso)**.

### Independência da operação do programa
Esse conceito é comum em sistemas de banco de dados orientados a objetos e objeto-relacionais. A ideia é que, nesses sistemas, você pode definir **operações** que podem ser usadas pelos usuários para manipular os dados. Essas operações têm uma **interface** (ou assinatura), que define o nome da operação e os parâmetros que ela aceita, e uma **implementação**, que contém o código real que executa a operação. 

Assim, os programas que usam essas operações não precisam se preocupar com **como** elas são implementadas. Eles apenas chamam a operação pelo nome, passando os argumentos necessários, e o sistema cuida do resto.

Esse conceito é basicamente o mesmo que o de funções/métodos no contexto de linguagens de programação.

- Exemplo de assinatura:
```sql
calculaIdade(dataNascimento DATE) RETURNS INTEGER
```

- Exemplo de implementação (PostgreSQL):
```sql
CREATE FUNCTION calculaIdade(dataNascimento DATE) RETURNS INTEGER AS $$
BEGIN
   RETURN EXTRACT(YEAR FROM AGE(CURRENT_DATE, dataNascimento));
END;
$$ LANGUAGE plpgsql;
```
Os cifrões (`$$`) acima representam a delimitação de início/fim do corpo da função.

- Exemplo de chamada:
```sql
SELECT calculaIdade('2015-06-01');
```

### Visões de dados
Uma visão (ou *view*) pode ser um subconjunto do banco de dados ou conter **dados virtuais** que são derivados dos arquivos do banco de dados, mas não estão armazenados explicitamente. Alguns usuários não precisam saber se os dados a que se referem estão armazenados ou se são derivados.

### Processamento de transações
Em um SGBD com vários usuários, é provável que hajam múltiplos acessos ao banco de dados ao mesmo tempo. O SGBD precisa incluir um **software de controle de concorrência** para garantir que vários usuários tentando atualizar o mesmo dado façam isso de uma maneira controlada e segura para a integridade da informação consultada. 

Aplicativos com essa função geralmente são chamados de **aplicações de processamento de transação online** (***OLTP*** - *Online Transaction Processing*).

#### O que são transações?
**Uma transação é um programa em execução ou processo que inclui um ou mais acessos ao banco de dados.** Nesse sentido, uma transação só executa um acesso logicamente correto a um banco de dados quando ela é **executada de forma completa** e **sem interferência de outras transações**.

Propriedades de uma transação:
- **Isolamento**: Garante que cada transação pareça executar isoladamente das demais, mesmo que centenas de transações possam estar executando concorrentemente.
- **Atomicidade**: Garante que todas as operações em uma transação sejam executadas ou que nenhuma seja (em caso de falha de alguma delas).
