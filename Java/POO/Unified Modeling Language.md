Linguagem de Modelagem Unificada ou UML, é uma notação, que possibilita a representação gráfica do projeto.

Na UML, temos três conceitos necessários para compreendermos inicialmente:
**Diagramas**, **elementos** e **relacionamentos**.
![[Pasted image 20240627155818.png|300]]
## Diagramas estruturais

- **Diagrama de classe:** O Diagrama de Classes é utilizado para fazer a representação de, estruturas de classes de negócio, interfaces e outros componentes do sistema. Por esta característica, este diagrama é considerado o mais importante para a UML, pois auxilia a maioria dos demais diagramas.

- **Diagrama de objetos**: Este diagrama, representa os objetos existentes em um determinado instante ou fato na aplicação. Assim, conseguimos ter uma perspectiva do estado de nossos objetos, mediante a interação dos usuários no sistema.

>[! info]
>Existem outras categorias de diagramas estruturais e comportamentais, porém iremos focar nos citados acima.

## Diagrama de classe

O diagrama de classes, ilustra **graficamente** como classes serão estruturadas e interligadas entre si, diante da proposta do nosso software.

Em diagrama, a estrutura das classes é constituída por:
- ==Identificação:== Nome e/ou finalidade da classe;
- ==Atributos:== Propriedades e/ou características;
- ==Operações:== Ações e/ou métodos.

## Relacionamentos

Em um diagrama, as classes podem existir de forma independente, mas obviamente haverá, em alguma etapa da aplicação a necessidade de algumas se relacionarem, o que devemos compreender é, o nível de dependência entre elas:

### Associação

Uma associação, define um relacionamento entre duas classes, permitindo que, um objeto tenha acesso a estrutura de um outro objeto.
![[Pasted image 20240627162306.png|400]]
- **Agregação:** Em uma agregação, a classe principal contém uma relação com outra classe, mas ela pode existir, sem a classe agregadora. Imagina um cadastro de Candidatos, podemos encontrar candidatos que ainda não possuam uma profissão:
![[Pasted image 20240627163154.png|350]]
- **Composição:** A composição já caracteriza uma dependência existencial, entre a classe principal e a classe associada. Imaginamos que uma admissão só poderá existir, contendo suas informações básicas e a composição do candidato selecionado.
![[Pasted image 20240627163240.png|400]]
> Admissão é a classe principal e Candidato compõe a Admissão, logo este SURGIRA uma composição entre Admissão e Colaborador - ver DDD

#### Multiplicidade
Nem sempre o relacionamento entre as classes, será de **um para um**, em um determinado cenário poderá exigir multiplicidades específicas, conforme opções abaixo:

- 1. -> Representa uma associação, **contendo um elemento;**
- ~~asterístico~~ . -> Representa uma associação, **contendo uma lista de elementos;**
- 0..1 -> Representa uma associação, **contendo zero ou um elemento;**
- 0..* -> Representa uma associação, **contendo zero ou uma lista de elementos;**
- 1..* -> Representa uma associação. **contendo um ou uma lista de elementos**.

#### Visibilidade
Os atributos e métodos de uma classe, podem receber níveis de visibilidade, e na UML existem símbolos que representam cada um deles.

- (+) Visibilidade pública;
- (#) Visibilidade protegida (muito associada com herança);
- (-) Visibilidade privada.

#### Representação

![[Pasted image 20240627163725.png|400]]
>Ilustração utilizando a ferramenta Astah Community.

#### Ferramentas

- [Lucidchart](https://lucid.app/documents#/documents?folder_id=recent)
- [draw.io](https://app.diagrams.net/)
- [StarUML](https://staruml.io/)
