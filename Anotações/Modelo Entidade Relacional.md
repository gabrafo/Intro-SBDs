# Modelo Entidade Relacional

**OBS**: A partir daqui, muitas das minhas anotações terão como base, quase que exclusivamente, o conteúdo das [videoaulas do Prof. Denilson](https://www.youtube.com/playlist?list=PLpAVc-5L0TX-ryMY_4nN8f2BT28Wp_O_n), já que há uma abordagem mais direta dos conceitos estudados lá. Para quem preferir se orientar pelo livro-texto, estamos tratando (usando como orientação a sexta edição), do capítulo 7.

O Modelo de Entidades e Relacionamentos (ER) é um modelo **conceitual** usado para projeto de aplicações de banco de dados, não se preocupando com aspectos de implementação, mas sim com a representação de como queremos a organização daquele sistema logicamente.
Esse modelo é **baseado na percepção do mundo real como conjuntos de objetos básicos** chamados entidades e nos **relacionamentos entre esses objetos**.

## Entidades e atributos
O objeto básico que o modelo ER representa é uma **entidade**, que é **algo no mundo real com uma existência independente**. Uma entidade pode ser um objeto com uma existência física (exemplo: um carro), ou uma existência conceitual (exemplo: um cargo empresarial). 

Cada entidade possui **atributos**, que são propriedades especificas que a descreve. Por exemplo, uma entidade `FUNCIONARIO` pode ser descrita pelo nome, idade, endereço, salário e cargo do funcionário.
