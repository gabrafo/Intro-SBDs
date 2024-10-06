# Modelo Entidade Relacional
**OBS**: A partir daqui, muitas das minhas anotações terão como base, quase que exclusivamente, o conteúdo das [videoaulas do Prof. Denilson](https://www.youtube.com/playlist?list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n), já que há uma abordagem mais direta dos conceitos estudados lá. Para quem preferir se orientar pelo livro-texto, estamos tratando (usando como orientação a sexta edição), do capítulo 7.

O Modelo de Entidades e Relacionamentos (ER) é um modelo **conceitual** usado para projeto de aplicações de banco de dados, não se preocupando com aspectos de implementação, mas sim com a representação de como queremos a organização daquele sistema logicamente.
Esse modelo é **baseado na percepção do mundo real como conjuntos de objetos básicos** chamados entidades e nos **relacionamentos entre esses objetos**.

## Entidades e atributos
### Entidades
O objeto básico que o modelo ER representa é uma **entidade**, que é **algo no mundo real com uma existência independente**. Uma entidade pode ser um objeto com uma existência física (exemplo: um carro), ou uma existência conceitual (exemplo: um cargo empresarial). 

Já o **tipo entidade** define uma coleção (classe) de entidades que têm os mesmos atributos. A função do **tipo entidade** é descrever o esquema para um conjunto de entidades. Costuma ser representada por um retângulo no diagrama.

![Imagem 9.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%209.png)

Representação de um tipo entidade.

E um **conjunto de entidades** é um conjunto com entidades de um mesmo tipo de entidade, assim, o conjunto de todos os funcionários pode ser definido como um conjunto de entidades `Funcionário`, onde todos os objetos (funcionários) partilham do mesmo tipo entidade (`Funcionário`).

### Atributos

Cada entidade possui **atributos**, que são propriedades especificas que a descreve. Por exemplo, uma entidade `FUNCIONARIO` pode ser descrita pelo nome, idade, endereço, salário e cargo do funcionário.

**Tipos de atributos**:
- Simples ou compostos

  Resumidamente, dita se um atributo pode ser subdividido em outros atributos menores ou não.
  
  ![Imagem 10.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2010.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
- Monovalorados ou multivalorado

  Resumidamente, dita se um atributo pode ter apenas um valor associado a ele (exemplo: uma empresa, normalmente, só tem um nome) ou se pode ter mais de um (uma empresa pode ter várias filiais e, portanto, várias localizações distintas).
  
  ![Imagem 11.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2011.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
- Armazenados ou derivados

  Resumidamente, dita se um atributo está, de fato, armazenado no banco de dados ou se não está armazenado, mas que pode ser obtido a partir da manipulação do(s) valor(es) de outro(s) atributo(s).
  
  ![Imagem 12.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2012.png)
  
  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).

- Complexos

  É um atributo que pode ter vários valores associados a ele e também pode ser subdividido em diversos atributos menores (que o compõem).
  
  ![Imagem 13.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2013.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).

- Nulos

  Pode receber o valor **nulo**, ou seja, podem receber um valor "desconhecido".
  
  ![Imagem 14.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2014.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
- Chaves

  Serve como identificador de um objeto, sendo único para cada uma das entidades do conjunto todo de entidades.
  
  ![Imagem 15.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2015.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).
  
  Um tipo entidade pode ter mais de um atributo chave, sendo, cada um, uma chave (de maneira isolada), ou pode ter um atributo chave composto, subdividido em diversos outros atributos, sendo a combinação de todos esses atributos única para cada entidade.
  
  ![Imagem 16.png](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2016.png)

  (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/w-uUcd227xA?si=cnFS1HVaPDTLmNLI)).

## Relacionamento
Um **relacionamento** é uma **associação entre entidades** que representa um fato do mundo real.

Já um **tipo relacionamento** define um conjunto de associações entre diferentes tipos entidade. 

Por exemplo, um tipo relacionamento chamado `Matrícula` poderia descrever a associação entre entidades do tipo `Aluno` e entidades do tipo `Curso`, estabelecendo como alunos estão matriculados em cursos. 

Poderíamos descrever também o tipo relacionamento `trabalha_para` entre os tipos entidades `Funcionário` e `Departamento`, que associa cada funcionário com o departamento para o qual ele trabalha. No exemplo abaixo, a cardinalidade (que logo será explicada) aponta que um objeto do tipo `Funcionário` pode trabalhar apenas para um `Departamento`, mas um `Departamento` pode ter vários objetos do tipo `Funcionário` trabalhando para ele.

![Imagem 17](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2017.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://www.youtube.com/watch?v=KPzgL_4zuxc&list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n&index=14&ab_channel=DenilsonAlvesPereira).

### Grau de um tipo relacionamento
