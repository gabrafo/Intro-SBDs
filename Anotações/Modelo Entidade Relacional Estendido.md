# Modelo Entidade Relacional Estendido
Esse modelo é uma expansão do modelo ER original (desenvolvido em 1976) devido à necessidade de modelar dados/relacionamentos mais complexos. 

Novos conceitos que surgiram com o EER (Modelo Entidade Relacional Estendido):
- Agregação
- Herança
- Tipo União

## Agregação
A **agregação** é uma abstração em que **um relacionamento entre entidades é tratado como uma entidade** por si só. Isso permite que o relacionamento seja envolvido em outro relacionamento. Em outras palavras, a **agregação permite representar um relacionamento como uma "entidade composta"**.

Supondo que algumas entrevistas de emprego resultem em oferta de emprego, e outras não, o diagrama abaixo representa essa ideia a partir do uso de agregação (tratando as entrevistas bem-sucedidas como um novo relacionamento: oferta de emprego usando um tipo entidade fraca para entrevistas):

![Imagem 29](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2029.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/jafii4Pf5is?si=QgkQs2kPQidLYdyc)).

## Herança
 A **herança** (ou **generalização/especialização**) é uma forma de modelar a relação "é-um". Nesse tipo de modelagem, uma entidade mais geral é subdividida em entidades mais específicas, ou seja, entidades "filhas" herdam atributos e relacionamentos da entidade "pai".
 
**Exemplo**: as entidades de um tipo entidade `Animal` podem ser agrupadas em `Felino`, `Réptil`, `Ave`, etc.

Cada um dos subconjuntos é chamado de subclasse do tipo entidade `Animal`, sendo `Animal` a superclasse desses subconjuntos. 

Uma entidade não pode existir no banco de dados como membro somente de uma subclasse, ela deve também ser membro da superclasse. Assim, se houver uma subclasse de `Felino` chamada `Gato`, ela obrigatoriamente herdará tanto de `Felino`, quanto de `Animal`.

No entanto, não é necessário que toda entidade em uma superclasse seja membro de alguma subclasse. Assim, podemos ter um `Animal` que não pertence a nenhuma de suas subclasses.
### Especialização
É o processo de definir um conjunto de subclasses de um tipo entidade (superclasse).

![Imagem 30](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2030.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/jafii4Pf5is?si=QgkQs2kPQidLYdyc)).

### Generalização
É o contrário da especialização. **As diferenças entre dois ou mais tipos entidades são suprimidas**, **suas características comuns são identificadas**, e é feita uma generalização em uma **única superclasse** da qual os tipos originais são subclasses especiais.

![Imagem 31](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2031.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/jafii4Pf5is?si=QgkQs2kPQidLYdyc)).

### Disjunção e Sobreposição
- **Disjunção**: uma entidade pode ser membro de, no máximo, uma das subclasses da especialização. 
  Exemplo: Imagine uma entidade `Veículo`, que pode ser especializada em `Carro` ou `Moto`. Um `Veículo` específico só pode ser ou `Carro` ou `Moto`, mas nunca ambos ao mesmo tempo.

- **Sobreposição**: uma entidade pode ser membro de mais de uma subclasse da especialização. 
  Exemplo:  Considere uma entidade `Pessoa`, especializada em `Professor` e `Artista`. Uma `Pessoa` pode ser simultaneamente um `Professor` e um `Artista`, pertencendo a ambas as subclasses.

### Completude
- **Total**: toda entidade na superclasse deve ser membro de pelo menos uma subclasse na especialização. 
  Exemplo:  Um `Veículo` (considerando apenas veículos automotivos) obrigatoriamente tem que ser um `Carro`, ou uma `Moto`, ou um `Caminhão`, etc.

- **Parcial**: uma entidade na superclasse não precisa ser membro de nenhuma subclasse na especialização. 
  Exemplo: Uma `Pessoa` não necessariamente precisa se especializar em uma profissão, podendo apenas ser uma `Pessoa`.

### Herança Múltipla
Ocorre quando uma subclasse descende de mais de uma superclasse.

No caso abaixo, `Gerente Engenheiro` é uma especialização conjunta entre de `Engenheiro` e `Gerente`. Além disso, todo `Gerente Engenheiro` precisa ser, obrigatoriamente, um `Funcionário Mensal`.

![Imagem 32](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2032.png)

(Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/jafii4Pf5is?si=QgkQs2kPQidLYdyc)).

## Tipo União (ou Categoria)
O **tipo união**, ou **categoria**, é usado para representar uma entidade que pode ser membro de mais de um tipo de entidade, mas de forma mutuamente exclusiva (ou "é um" ou "é outro", nunca os dois ao mesmo tempo). Além disso, uma categoria pode ser total ou parcial.

**Exemplo:** Considere uma entidade `Pagamento`. Um pagamento pode ser feito por um `Cliente` ou por um `Fornecedor`. A entidade `Pagamento` pode ser associada a qualquer uma dessas entidades, mas um pagamento específico só pode estar relacionado a um deles de cada vez. Assim, você usaria um tipo união para modelar essa relação.

![Imagem 33](https://github.com/gabrafo/Intro-SBDs/blob/main/Anexo/Imagem%2033.png)

Um `Correntista` pode ser ou do tipo`Empresa`, ou do tipo `Pessoa`. A categoria `Correntista` é **parcial**, podendo haver uma `Empresa` ou `Pessoa` que não seja `Correntista`. (Imagem do slide do prof. Denilson, disponível em suas [videoaulas](https://youtu.be/jafii4Pf5is?si=QgkQs2kPQidLYdyc)).
