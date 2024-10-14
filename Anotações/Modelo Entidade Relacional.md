# Modelo Entidade Relacional
**OBS**: A partir daqui, muitas das minhas anotações terão como base, quase que exclusivamente, o conteúdo das [videoaulas do Prof. Denilson](https://www.youtube.com/playlist?list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n), já que há uma abordagem mais direta dos conceitos estudados lá. Para quem preferir se orientar pelo livro-texto, estamos tratando (usando como orientação a sexta edição), do capítulo 7.

O Modelo de Entidades e Relacionamentos (ER) é um modelo **conceitual** usado para projeto de aplicações de banco de dados, não se preocupando com aspectos de implementação, mas sim com a representação de como queremos a organização daquele sistema logicamente.
Esse modelo é **baseado na percepção do mundo real como conjuntos de objetos básicos** chamados entidades e nos **relacionamentos entre esses objetos**.

## Entidades e atributos
### Entidades
O objeto básico que o modelo ER representa é uma **entidade**, que é **algo no mundo real com uma existência independente**. Uma entidade pode ser um objeto com uma existência física (exemplo: um carro), ou uma existência conceitual (exemplo: um cargo empresarial). 

Já o **tipo entidade** define uma coleção (classe) de entidades que têm os mesmos atributos. A função do **tipo entidade** é descrever o esquema para um conjunto de entidades. Costuma ser representada por um retângulo no diagrama.

![Imagem 9](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%209.png)

Representação de um tipo entidade.

E um **conjunto de entidades** é um conjunto com entidades de um mesmo tipo de entidade, assim, o conjunto de todos os funcionários pode ser definido como um conjunto de entidades `Funcionário`, onde todos os objetos (funcionários) partilham do mesmo tipo entidade (`Funcionário`).

### Atributos

Cada entidade possui **atributos**, que são propriedades especificas que a descreve. Por exemplo, uma entidade `FUNCIONARIO` pode ser descrita pelo nome, idade, endereço, salário e cargo do funcionário.

**Tipos de atributos**:
- Simples ou compostos

  Resumidamente, dita se um atributo pode ser subdividido em outros atributos menores ou não.
  
  ![Imagem 10](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2010.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
- Monovalorados ou multivalorado

  Resumidamente, dita se um atributo pode ter apenas um valor associado a ele (exemplo: uma empresa, normalmente, só tem um nome) ou se pode ter mais de um (uma empresa pode ter várias filiais e, portanto, várias localizações distintas).
  
  ![Imagem 11](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2011.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
- Armazenados ou derivados

  Resumidamente, dita se um atributo está, de fato, armazenado no banco de dados ou se não está armazenado, mas que pode ser obtido a partir da manipulação do(s) valor(es) de outro(s) atributo(s).
  
  ![Imagem 12](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2012.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).

- Complexos

  É um atributo que pode ter vários valores associados a ele e também pode ser subdividido em diversos atributos menores (que o compõem).
  
  ![Imagem 13](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2013.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).

- Nulos

  Pode receber o valor **nulo**, ou seja, podem receber um valor "desconhecido".
  
  ![Imagem 14](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2014.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
- Chaves

  Serve como identificador de um objeto, sendo único para cada uma das entidades do conjunto todo de entidades.
  
  ![Imagem 15](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2015.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
  Um tipo entidade pode ter mais de um atributo chave, sendo, cada um, uma chave (de maneira isolada), ou pode ter um atributo chave composto, subdividido em diversos outros atributos, sendo a combinação de todos esses atributos única para cada entidade.
  
  ![Imagem 16](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2016.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).

## Relacionamento
Um **relacionamento** é uma **associação entre entidades** que representa um fato do mundo real.

Já um **tipo relacionamento** define um conjunto de associações entre diferentes tipos entidade. 

Por exemplo, um tipo relacionamento chamado `Matrícula` poderia descrever a associação entre entidades do tipo `Aluno` e entidades do tipo `Curso`, estabelecendo como alunos estão matriculados em cursos. 

Poderíamos descrever também o tipo relacionamento `trabalha_para` entre os tipos entidades `Funcionário` e `Departamento`, que associa cada funcionário com o departamento para o qual ele trabalha. No exemplo abaixo, a cardinalidade (que logo será explicada) aponta que um objeto do tipo `Funcionário` pode trabalhar apenas para um `Departamento`, mas um `Departamento` pode ter vários objetos do tipo `Funcionário` trabalhando para ele.

![Imagem 17](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2017.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira)).

### Grau de um tipo relacionamento
O grau de um tipo relacionamento é o número de tipos entidades participantes. Assim, no exemplo acima de `trabalha_para` entre `Funcionário` e `Departamento`, temos um grau 2 (binário), por haver apenas dois tipos entidades envolvidos.

![Imagem 18](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2018.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira)).
Perceba que, na imagem acima, apenas um funcionário se liga a um departamento a partir da relação `trabalha_para`, enquanto um departamento pode se ligar a vários funcionários a partir dessa mesma relação.

Já um relacionamento de grau 3 (ternário) pode ser exemplificado pela relação `Fornece`, envolvendo três entidades: `Fornecedor`, `Projeto` e `Peça`.

![Imagem 19](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2019.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira)).
Perceba que um fornecedor pode fornecer várias peças a vários projetos, assim, é uma relação *many-to-many-to-many*.

#### Relacionamento ternário
É um relacionamento que possui três entidades participantes. Para identificar as cardinalidades do relacionamento, é uma boa prática procurar, entre pares de entidade, quais são suas respectivas cardinalidades.

![Imagem 26](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2026.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=SaqrYuiAl8Y&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=16&ab_channel=DenilsonAlvesPereira)).

##### Como mapear um relacionamento ternário para binário?
Em geral, um tipo relacionamento ternário representa mais informação do que três tipos relacionamento binários.

Nos diagramas abaixo, a diferença se dá pela não-obrigatoriedade, no diagrama da direita, de estipularmos, por exemplo, qual peça um fornecedor está fornecendo e para qual projeto esse fornecimento está sendo feito. Além disso, falta o atributo `Quantidade`!

![Imagem 27](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2027.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=SaqrYuiAl8Y&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=16&ab_channel=DenilsonAlvesPereira)).

A solução para esse problema seria fazer uso de uma entidade fraca (conceito que será mais debatido a seguir). Assim, podemos criar um tipo de entidade fraca sem chaves parciais e com três relacionamentos identificadores, o que tornaria obrigatório, ao estabelecermos uma relação `Fornece`, a identificação explícita de todos os objetos das três entidades participantes.

![Imagem 28](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2028.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=SaqrYuiAl8Y&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=16&ab_channel=DenilsonAlvesPereira)).
### Relacionamento recursivo
Um relacionamento é recursivo quando o mesmo tipo entidade (ex: `Funcionário`) participa mais de uma vez de um relacionamento ocupando funções diferentes.
Assim, o funcionário com o CPF (atributo chave) 123.456.789-00 ocupa a função de supervisor, enquanto outro funcionário, com o CPF 234.567.890-11 ocupa a função de subordinado. Ambos os objetos nascem do mesmo tipo entidade, mas ocupam funções diferentes.

![Imagem 20](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2020.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira)).

Outro exemplo de relacionamento recursivo poderia ser a relação `presta_monitoria` entre dois objetos diferentes do tipo entidade `Aluno`,  um ocupando a função de solicitante e outro de monitor. No contexto da disciplina de Intro. a Sistemas de Bancos de Dados, poderíamos imaginar que, caso houvesse dificuldade com a disciplina, houvesse demanda para que um aluno com maior facilidade no conteúdo da matéria pudesse auxiliar outro(s) aluno(s) a estudar.

### Restrição de cardinalidade
Tomando como exemplo a relação `trabalha_para` entre o tipo entidade `Funcionário` e o tipo entidade `Departamento`, temos que a cardinalidade de uma relação pode assumir as seguintes configurações:
- **1:1** - um objeto do tipo entidade `Funcionário` só pode estar associado a, no máximo, um objeto do tipo entidade `Departamento`.
- **1:N** - um objeto do tipo entidade `Funcionário` pode estar associado a vários objetos do tipo entidade `Departamento`, mas um objeto `Departamento` só pode estar associado a um objeto de `Funcionário`.
- **M:N** - um objeto do tipo entidade `Funcionário` pode estar associado a vários objetos do tipo entidade `Departamento`, e vice-versa.

![Imagem 21](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2021.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira)).

### Restrição de participação
Especifica se a existência de uma entidade depende ou não de sua associação a outra entidade através de um relacionamento.
Cardinalidade mínima: **zero** (parcial) ou **um** (total).

Participação **total**: todos os objetos de um tipo entidade devem participar do relacionamento.
Participação **zero**: os objetos podem, ou não, participar do relacionamento.

![Imagem 23](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2023.png)

(Imagens do slide do prof. Denilson, disponíveis em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira)).

## Entidade fraca
É um tipo entidade que não tem atributos chave (sem identificação própria). É representada no diagrama pelo retângulo duplo.

![Imagem 24](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2024.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KoBP3n29V0c&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=15&ab_channel=DenilsonAlvesPereira)).

**Esse tipo está sempre associado a pelo menos um tipo entidade forte através de um relacionamento identificador** (representado pelo losango duplo), estando sempre com uma **restrição de participação total** com essa outra entidade.

Sua chave é formada pela combinação de uma chave do tipo entidade forte + uma chave parcial própria do tipo entidade fraca (representada pelo atributo "nome" no diagrama a seguir).

![Imagem 25](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2025.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KoBP3n29V0c&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=15&ab_channel=DenilsonAlvesPereira)).

Não devemos, nunca, adicionar uma chave do tipo entidade forte (como "cpf", por exemplo) como atributo do tipo entidade fraca, pois o relacionamento identificador já aponta onde está a chave forte da entidade.

## Diretrizes para escolha de nomes
**Entidades**: substantivos.
**Relacionamentos**: verbos.

Geralmente, as leituras de diagrama ER são feitas de esquerda para a direita, de cima para baixo, então é bom se atentar a isso.
