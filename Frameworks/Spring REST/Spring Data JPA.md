## Implementando Consultas JPQL
O Spring Data JPA oferece uma forma elegante e concisa de realizar consultas em bancos de dados relacionais através da interface `JpaRepository`. Uma das suas principais características é a capacidade de criar consultas JPQL (Java Persistence Query Language) de forma intuitiva, baseando-se nos nomes dos métodos nos repositórios.

### Criando Consultas Simples

Para criar consultas simples, basta seguir a convenção de nomenclatura dos métodos nos repositórios:

```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    List<Produto> findByNome(String nome);
    List<Produto> findByPrecoGreaterThan(Double preco);
}
```

* **findByNome(String nome):** Encontra todos os produtos com o nome igual ao passado como parâmetro.
* **findByPrecoGreaterThan(Double preco):** Encontra todos os produtos com o preço maior que o passado como parâmetro.

**Convenções de nomenclatura:**

* **findBy:** Inicia o nome do método.
* **Propriedades:** Os nomes das propriedades da entidade são concatenados, iniciando com letra maiúscula após "by".
* **Operadores:** Podem ser usados operadores como `Equals`, `GreaterThan`, `LessThan`, `Containing`, etc.

### Consultas Complexas com @Query

Para consultas mais complexas, podemos utilizar a anotação `@Query`:

```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    @Query("SELECT p FROM Produto p WHERE p.nome LIKE %?1%")
    List<Produto> findByNomeContaining(String nome);
}
```

* **@Query:** Indica que o método possui uma consulta JPQL personalizada.
* **%?1%:** O parâmetro `?1` corresponde ao primeiro parâmetro do método.

### Utilizando JPQL com Join

Para realizar joins entre entidades, utilizamos a sintaxe padrão do JPQL:

```java
public interface PedidoRepository extends JpaRepository<Pedido, Long> {
    @Query("SELECT p FROM Pedido p JOIN p.cliente c WHERE c.nome = :nomeCliente")
    List<Pedido> findByClienteNome(@Param("nomeCliente") String nomeCliente);
}
```

* **@Param:** Define um parâmetro nomeado para a consulta.

### Funções e Agrupamentos

JPQL oferece diversas funções e operadores para realizar cálculos e agrupamentos:

```java
@Query("SELECT COUNT(p) FROM Produto p")
Long contarProdutos();

@Query("SELECT AVG(p.preco) FROM Produto p")
Double calcularMediaPrecos();
```

### Customizando a Implementação

Para personalizar ainda mais as consultas, podemos criar uma implementação customizada do repositório:

```java
public interface CustomProdutoRepository {
    List<Produto> findByCategoriaAndPreco(Categoria categoria, Double preco);
}

public class ProdutoRepositoryImpl implements CustomProdutoRepository {
    // Implementação da consulta utilizando EntityManager
}
```

### Boas Práticas

* **Utilizar os métodos padrão do JpaRepository:** Aproveite os métodos já implementados como `save`, `findAll`, `deleteById`, etc.
* **Criar consultas legíveis:** Utilize aliases para tabelas e campos, e formate o JPQL de forma clara.
* **Utilizar parâmetros nomeados:** Melhora a legibilidade e evita problemas de SQL injection.
* **Testar as consultas:** Crie testes unitários para garantir que as consultas retornam os resultados esperados.
* **Considerar a performance:** Utilize índices e otimize as consultas para melhorar o desempenho.
---
## Criando um Repositório com Spring Data JPA (SDJ)

O Spring Data JPA simplifica significativamente a interação com bancos de dados relacionais em aplicações Java. Ele permite criar repositórios de forma declarativa, utilizando convenções de nomenclatura para gerar consultas JPQL automaticamente.

**Entendendo o Conceito:**

* **Repositório:** É a interface entre a sua aplicação e a camada de persistência. Ele define os métodos para acessar e manipular os dados.
* **Spring Data JPA:** É um framework que fornece uma abstração sobre o JPA (Java Persistence API), facilitando a criação de repositórios e a execução de consultas.
* **JPQL:** Java Persistence Query Language, é uma linguagem de consulta orientada a objetos para bancos de dados relacionais.

**Criando um Repositório Básico:**

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    List<Produto> findByNome(String nome);
}
```

* **@Repository:** Anotação que indica que esta classe é um repositório.
* **JpaRepository:** Interface principal do Spring Data JPA.
* **Produto:** A entidade que representa a tabela "produto" no banco de dados.
* **Long:** Tipo do identificador da entidade.
* **findByNome:** Método que encontra todos os produtos com o nome especificado.

**Convenções de Nomenclatura:**

O Spring Data JPA utiliza convenções de nomenclatura para gerar consultas JPQL automaticamente. Os métodos nos repositórios devem seguir um padrão:

* **findBy:** Inicia o nome do método.
* **Propriedades:** Os nomes das propriedades da entidade são concatenados, iniciando com letra maiúscula após "by".
* **Operadores:** Podem ser usados operadores como `Equals`, `GreaterThan`, `LessThan`, `Containing`, etc.

**Exemplo de Outros Métodos:**

```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    List<Produto> findByPrecoGreaterThan(Double preco);
    List<Produto> findByNomeContaining(String nome);
    List<Produto> findByCategoriaAndPreco(Categoria categoria, Double preco);
}
```

**Consultas Personalizadas com @Query:**

Para consultas mais complexas, podemos utilizar a anotação `@Query`:

```java
@Query("SELECT p FROM Produto p WHERE p.nome LIKE %?1%")
List<Produto> findByNomeContaining(String nome);
```

**Funcionalidades Adicionais:**

* **Paging and Sorting:** O `JpaRepository` oferece métodos para paginação e ordenação dos resultados.
* **Counting:** Contar o número de entidades.
* **Deleting:** Remover entidades.
* **Saving:** Persistir novas entidades ou atualizar entidades existentes.
* **Specifications:** Criar consultas dinâmicas e complexas.

**Exemplo Completo:**

```java
@Entity
public class Produto {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nome;
    private Double preco;
    // ... outros atributos
}

@Repository
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    // Métodos personalizados
}

@Service
public class ProdutoService {
    @Autowired
    private ProdutoRepository produtoRepository;

    public List<Produto> buscarProdutosPorNome(String nome) {
        return produtoRepository.findByNome(nome);
    }
}
```

---
## Criando Consultas com Query Methods
O Spring Data JPA oferece uma maneira intuitiva e poderosa de criar consultas em bancos de dados relacionais através de métodos nos seus repositórios. Essa abordagem, conhecida como **query methods**, permite que você defina consultas de forma declarativa, sem a necessidade de escrever JPQL diretamente.

### Como Funcionam as Query Methods?

O Spring Data JPA utiliza convenções de nomenclatura para gerar automaticamente as consultas JPQL a partir dos nomes dos métodos nos seus repositórios. 

**Exemplo:**

```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    List<Produto> findByNome(String nome);
    List<Produto> findByPrecoGreaterThan(Double preco);
}
```

* **findByNome(String nome):** Encontra todos os produtos com o nome igual ao passado como parâmetro.
* **findByPrecoGreaterThan(Double preco):** Encontra todos os produtos com o preço maior que o passado como parâmetro.

**Convenções de Nomenclatura:**

* **findBy:** Inicia o nome do método.
* **Propriedades:** Os nomes das propriedades da entidade são concatenados, iniciando com letra maiúscula após "by".
* **Operadores:** Podem ser usados operadores como `Equals`, `GreaterThan`, `LessThan`, `Containing`, etc.

### Consultas Mais Complexas com @Query

Para consultas mais complexas, podemos utilizar a anotação `@Query`:

```java
@Query("SELECT p FROM Produto p WHERE p.nome LIKE %?1%")
List<Produto> findByNomeContaining(String nome);
```

* **@Query:** Indica que o método possui uma consulta JPQL personalizada.
* **%?1%:** O parâmetro `?1` corresponde ao primeiro parâmetro do método.

### Outros Exemplos de Query Methods

* **Join:**
  ```java
  @Query("SELECT p FROM Pedido p JOIN p.cliente c WHERE c.nome = :nomeCliente")
  List<Pedido> findByClienteNome(@Param("nomeCliente") String nomeCliente);
  ```
* **Funções e Agrupamentos:**
  ```java
  @Query("SELECT COUNT(p) FROM Produto p")
  Long contarProdutos();
  ```
* **Ordenação:**
  ```java
  List<Produto> findByNomeOrderByPrecoDesc(String nome);
  ```

### Benefícios das Query Methods

* **Produtividade:** Reduz significativamente a quantidade de código necessário para realizar consultas.
* **Legibilidade:** As consultas são mais fáceis de entender e manter.
* **Tipo segurança:** Evita erros de compilação ao utilizar os métodos dos repositórios.
* **Reutilização:** Permite criar consultas reutilizáveis e personalizadas.

### Limitações e Considerações

* **Complexidade:** Para consultas muito complexas, a sintaxe dos query methods pode se tornar menos intuitiva.
* **Performance:** É importante considerar a performance das consultas, especialmente em grandes bases de dados.
* **Flexibilidade:** Embora as query methods sejam poderosas, em alguns casos pode ser necessário utilizar JPQL diretamente para obter maior flexibilidade.

### Quando Utilizar @Query?

* **Consultas complexas:** Quando as convenções de nomenclatura não são suficientes para expressar a lógica da consulta.
* **Funções específicas do banco de dados:** Para utilizar funções específicas do banco de dados que não são mapeadas pelas convenções.
* **Otimização de performance:** Para escrever consultas mais eficientes e otimizadas.
---
## Utilizando Keywords para Definir Critérios em Query Methods
As **query methods** no Spring Data JPA são uma forma poderosa e intuitiva de criar consultas em bancos de dados relacionais. Através de convenções de nomenclatura, podemos definir critérios de busca de forma declarativa, sem a necessidade de escrever JPQL diretamente.

### Palavras-chave Essenciais
As palavras-chave utilizadas nos nomes dos métodos definem os critérios de busca. As mais comuns são:

* **findBy:** Indica o início de uma consulta.
* **Propriedades da entidade:** Os nomes das propriedades da entidade são concatenados, iniciando com letra maiúscula após "by".
* **Operadores:**
  * **Equals:** Igualdade (ex: `findByNome`)
  * **Containing:** Contém (ex: `findByNomeContaining`)
  * **StartingWith:** Começa com (ex: `findByNomeStartingWith`)
  * **EndingWith:** Termina com (ex: `findByNomeEndingWith`)
  * **GreaterThan, GreaterThanEqual, LessThan, LessThanEqual:** Comparação numérica
  * **Between:** Entre um intervalo
  * **Is, IsNot:** Verificação de nulidade
* **And, Or:** Combinação de critérios

### Exemplos
```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    List<Produto> findByNome(String nome); // Encontra produtos com o nome exato
    List<Produto> findByPrecoGreaterThan(Double preco); // Encontra produtos com preço maior que
    List<Produto> findByNomeContaining(String parteDoNome); // Encontra produtos com o nome contendo a substring
    List<Produto> findByPrecoBetween(Double precoInicial, Double precoFinal); // Encontra produtos com preço entre um intervalo
    List<Produto> findByCategoriaAndPrecoGreaterThan(Categoria categoria, Double preco); // Combina dois critérios
}
```

### Ordenação
Para ordenar os resultados, utilize os métodos `OrderBy`:

```java
List<Produto> findByNomeOrderByPrecoDesc(String nome); // Ordena por preço em ordem decrescente
```

### Ignorando Case
Para realizar buscas ignorando o caso, utilize a anotação `@Query` com a função `UPPER` ou `LOWER`:

```java
@Query("SELECT p FROM Produto p WHERE UPPER(p.nome) = UPPER(?1)")
List<Produto> findByNomeIgnoreCase(String nome);
```

### Limitando Resultados
Para limitar o número de resultados, utilize os métodos `Pageable` e `Page`:

```java
Page<Produto> findByNome(String nome, Pageable pageable);
```

### Consultas Mais Complexas com @Query
Para consultas mais complexas, você pode utilizar a anotação `@Query` para escrever JPQL diretamente:

```java
@Query("SELECT p FROM Produto p JOIN p.categoria c WHERE c.nome = :nomeCategoria")
List<Produto> findByCategoriaNome(@Param("nomeCategoria") String nomeCategoria);
```

### Dicas Adicionais
* **Personalização:** Para personalizar ainda mais as suas consultas, você pode criar métodos customizados utilizando o `EntityManager`.
* **Performance:** Utilize índices nos seus bancos de dados para melhorar o desempenho das consultas.
* **Legibilidade:** Escreva métodos com nomes claros e expressivos para facilitar a manutenção do código.
* **Complexidade:** Para consultas muito complexas, considere utilizar a API Criteria para construir consultas de forma programática.
---
## Conhecendo os Prefixos de Query Methods
Os **prefixos de query methods** no Spring Data JPA são como palavras-chave mágicas que permitem criar consultas complexas de forma intuitiva e declarativa. Ao utilizar esses prefixos nos nomes dos métodos em seus repositórios, você instrui o framework a gerar as consultas JPQL (Java Persistence Query Language) correspondentes.

### Quais são os principais prefixos?

* **findBy:** O prefixo mais comum, utilizado para iniciar uma consulta.
* **Containing:** Indica que o valor do parâmetro deve estar contido em um campo.
* **StartingWith:** Indica que o valor do parâmetro deve ser o início de um campo.
* **EndingWith:** Indica que o valor do parâmetro deve ser o final de um campo.
* **Is, IsNot:** Verifica se um campo é nulo ou não nulo.
* **GreaterThan, GreaterThanEqual, LessThan, LessThanEqual:** Comparações numéricas.
* **Between:** Indica um intervalo de valores.
* **In:** Verifica se um valor está em uma lista.

### Como usar os prefixos?

```java
public interface ProdutoRepository extends JpaRepository<Produto, Long> {
    List<Produto> findByNomeContaining(String parteDoNome); // Encontra produtos com o nome contendo a substring
    List<Produto> findByPrecoGreaterThan(Double precoMinimo); // Encontra produtos com preço maior que
    List<Produto> findByDataFabricacaoBetween(LocalDate dataInicio, LocalDate dataFim); // Encontra produtos fabricados entre duas datas
}
```

### Combinando Prefixos e Propriedades

Você pode combinar vários prefixos e propriedades para criar consultas mais complexas:

```java
List<Produto> findByCategoriaAndPrecoGreaterThan(Categoria categoria, Double preco); // Encontra produtos de uma categoria específica com preço maior que
```

### Ordenando os Resultados

Para ordenar os resultados, utilize os métodos `OrderBy`:

```java
List<Produto> findByNomeOrderByPrecoDesc(String nome); // Ordena por preço em ordem decrescente
```

### Ignorando Case

Para realizar buscas ignorando o caso, utilize a anotação `@Query` com a função `UPPER` ou `LOWER`:

```java
@Query("SELECT p FROM Produto p WHERE UPPER(p.nome) = UPPER(?1)")
List<Produto> findByNomeIgnoreCase(String nome);
```

### Limitando Resultados

Para limitar o número de resultados, utilize os métodos `Pageable` e `Page`:

```java
Page<Produto> findByNome(String nome, Pageable pageable);
```

### Personalizando as Consultas

Para consultas mais complexas, você pode utilizar a anotação `@Query` para escrever JPQL diretamente:

```java
@Query("SELECT p FROM Produto p JOIN p.categoria c WHERE c.nome = :nomeCategoria")
List<Produto> findByCategoriaNome(@Param("nomeCategoria") String nomeCategoria);
```

### Dicas Adicionais

* **Leia a documentação:** A documentação oficial do Spring Data JPA contém uma lista completa de palavras-chave e exemplos.
* **Experimente:** A melhor forma de aprender é experimentando. Crie diferentes consultas e veja os resultados.
* **Utilize o debugger:** O debugger pode te ajudar a entender como as consultas são geradas e executadas.
* **Considere a performance:** Para consultas complexas, utilize índices nos seus bancos de dados para melhorar o desempenho.
---
## Usando Queries JPQL Customizadas com @Query

**O que é JPQL?**
JPQL (Java Persistence Query Language) é uma linguagem de consulta orientada a objetos, projetada para interagir com dados persistidos em um banco de dados relacional usando o JPA (Java Persistence API). Diferente do SQL, que opera em um nível mais baixo, o JPQL permite que você escreva consultas diretamente em termos dos seus objetos Java, abstraindo a complexidade da estrutura do banco de dados.

**A anotação @Query**
No Spring Data JPA, a anotação `@Query` permite que você escreva consultas JPQL personalizadas diretamente em seus métodos de repositório. Isso oferece uma grande flexibilidade para realizar consultas mais complexas que não podem ser expressas apenas pelos métodos de consulta por convenção (query methods).

**Como usar a @Query**
1. **Interface do repositório:**
   * Crie uma interface que estenda `JpaRepository` e declare seus métodos de consulta.
   * Utilize a anotação `@Query` acima do método, passando a sua consulta JPQL como um String.

2. **Sintaxe da consulta:**
   * A sintaxe do JPQL é semelhante ao SQL, mas opera em termos de entidades e atributos Java.
   * Você pode usar os nomes das propriedades das suas entidades diretamente na consulta.
   * Utilize os operadores de comparação, lógicos e funções disponíveis no JPQL.

**Exemplo:**
```java
@Repository
public interface ProdutoRepository extends JpaRepository<Produto, Long> {

    @Query("from Produto where nome like %:nome%")
    List<Produto> consultarPorNome(String nome);

    @Query("from Produto where preco between :precoMin and :precoMax")
    List<Produto> consultarPrecoEntre(@Param("precoMin") Double precoMin, @Param("precoMax") Double precoMax);
}
```

**Vantagens de usar @Query:**
* **Flexibilidade:** Permite escrever consultas complexas que não podem ser expressas por query methods.
* **Reutilização:** As consultas podem ser reutilizadas em diferentes partes da aplicação.
* **Melhora a legibilidade:** As consultas são escritas em termos dos objetos Java, tornando o código mais fácil de entender.
* **Integração com o Spring Data:** Se integra perfeitamente com outras funcionalidades do Spring Data, como paginação, ordenação e projeções.
---
## Externalizando Consultas JPQL para um Arquivo XML

**Por que externalizar consultas JPQL?**
* **Melhora na organização do código:** Separa a lógica de persistência da lógica de negócio, tornando o código mais limpo e fácil de manter.
* **Reutilização de consultas:** Uma mesma consulta pode ser utilizada em diferentes partes da aplicação, evitando duplicação de código.
* **Facilita a manutenção:** Alterações nas consultas podem ser feitas em um único lugar, reduzindo o risco de erros.
* **Suporte a diferentes dialetos SQL:** Permite que a mesma aplicação seja utilizada com diferentes bancos de dados, ajustando as consultas para cada um.

**Como fazer?**
1. **Criar o arquivo "orm.xml":**
   * Dentro do package  src.main.resources.META-INF do seu projeto, crie um arquivo com o nome "orm.xml".
   * O conteúdo desse arquivo deve seguir a especificação do JPA para arquivos ORM.xml.

2. **Definir as consultas:**
   * Dentro do arquivo "orm.xml", utilize as tags `<sql-query>` ou `<named-native-query>` para definir suas consultas JPQL.

**Exemplo de um arquivo "orm.xml":**

```xml title:orm
<?xml version="1.0" encoding="UTF-8"?>
<entity-mappings xmlns="http://xmlns.jcp.org/xml/ns/persistence/orm"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence/orm http://xmlns.jcp.org/xml/ns/persistence/orm_2_1.xsd"
                 version="2.2">
                 
    <named-query name="findAllProdutos">
        <query>SELECT p FROM Produto p</query>
    </named-query>

    <named-query name="findProdutosByNome">
        <query>SELECT p FROM Produto p WHERE p.nome LIKE :nome</query>
    </named-query>
</entity-mappings>
```

**Utilizando as consultas no código:**
```java
@Repository
public interface ProdutoRepository extends JpaRepository<Produto, Long> {

    // @Query(name = "findAllProdutos")
    List<Produto> findAllProdutos();

    // @Query(name = "findProdutosByNome")
    List<Produto> findProdutosByNome(@Param("nome") String nome);
}
```

**Observações importantes:**

* **Nome das consultas:** O atributo `name` da tag `<named-query>` define o nome da consulta, que será utilizado na anotação `@Query` do seu repositório.
* **Parâmetros:** Utilize a tag `<parameter>` para definir parâmetros na sua consulta. O nome do parâmetro deve corresponder ao nome do parâmetro utilizado na anotação `@Param`.
* **Consultas nativas:** Se você precisar executar uma consulta SQL nativa, utilize a tag `<named-native-query>`.
* **Prioridade:** As consultas definidas no arquivo "orm.xml" têm prioridade sobre as consultas definidas diretamente nas interfaces dos repositórios.

**Vantagens de usar o arquivo "orm.xml":**
* **Centralização:** Todas as consultas ficam em um único lugar, facilitando a gestão e a manutenção.
* **Reutilização:** As consultas podem ser reutilizadas em diferentes classes e métodos.
* **Testes:** É mais fácil testar as consultas de forma isolada.
* **Separação de responsabilidades:** A lógica de negócio fica separada da lógica de persistência.
---
## Implementando um Repositório SDJ Customizado

**Entendendo a Necessidade**
Um repositório Spring Data JPA (SDJ) customizado é útil quando as funcionalidades padrão não atendem às suas necessidades específicas. Isso pode incluir:
* **Consultas complexas:** Quando as consultas não podem ser expressas através dos métodos de consulta por convenção.
* **Lógica de negócio:** Ao precisar adicionar lógica de negócio diretamente no acesso aos dados.
* **Integrações com outros sistemas:** Ao precisar interagir com outras fontes de dados ou serviços.

**Criando um Repositório Customizado**
1. **Extender JpaRepository:**
   * Crie uma interface que estenda `JpaRepository` e especifique o tipo da entidade e do ID.

2. **Anotar com @Repository:**
   * Anote a interface com `@Repository` para que o Spring possa gerenciá-la como um bean.

3. **Definir métodos personalizados:**
   * Crie métodos com a lógica de acesso aos dados desejada.
   * Utilize a anotação `@Query` para definir consultas JPQL ou nativas.

**Exemplo:**
```java
@Repository
public interface ProdutoCustomRepository extends JpaRepository<Produto, Long> {

    @Query("SELECT p FROM Produto p WHERE p.nome LIKE %?1%")
    List<Produto> findByNomeContaining(String nome);

    // Método customizado com lógica adicional
    List<Produto> findProdutosEmEstoque();
}
```

**Injeção de Dependências**
* **Injetar outros serviços:** Se precisar de outros serviços em seus métodos customizados, utilize a injeção de dependências do Spring.

```java
@Repository
public class ProdutoCustomRepositoryImpl implements ProdutoCustomRepository {
    @Autowired
    private ProdutoRepository produtoRepository;

    @Override
    public List<Produto> findProdutosEmEstoque() {
        return produtoRepository.findAll().stream()
                .filter(p -> p.getQuantidadeEstoque() > 0)
                .collect(Collectors.toList());
    }
}
```

**Configuração do Spring**
* **Habilitar interfaces de repositório:** Certifique-se de que o Spring esteja configurado para procurar e gerenciar interfaces de repositório.
* **Registrar implementações customizadas:** Se você criou uma implementação customizada para um repositório, você pode registrá-la manualmente no contexto do Spring ou utilizar mecanismos de descoberta de componentes.

**Quando usar Repositórios Customizados?**
* **Consultas complexas:** Quando as consultas envolvem junções, subconsultas ou funções agregadas.
* **Lógica de negócio:** Quando a lógica de acesso aos dados envolve validações, transformações ou cálculos.
* **Integrações:** Quando você precisa integrar com outras fontes de dados ou serviços.
* **Performance:** Quando você precisa otimizar a performance de consultas específicas.

**Considerações Adicionais**
* **Testes:** É fundamental testar seus repositórios customizados para garantir que eles funcionam corretamente.
* **Performance:** Evite criar consultas complexas e ineficientes. Utilize índices e otimize suas consultas para melhorar o desempenho.
* **Manutenibilidade:** Mantenha seus repositórios customizados organizados e fáceis de entender.

**Benefícios dos Repositórios Customizados:**
* **Flexibilidade:** Permite criar soluções personalizadas para suas necessidades específicas.
* **Reusabilidade:** As consultas e a lógica de acesso aos dados podem ser reutilizadas em diferentes partes da aplicação.
* **Manutenibilidade:** Separa a lógica de acesso aos dados da lógica de negócio, facilitando a manutenção.
---
## Implementando Consultas Dinâmicas com JPQL

**O que são consultas dinâmicas?**
Consultas dinâmicas são aquelas que podem ser construídas em tempo de execução com base em critérios variáveis, permitindo uma maior flexibilidade na busca de dados. No contexto do Spring Data JPA, elas são especialmente úteis quando os critérios de busca podem mudar frequentemente ou quando o usuário precisa ter um controle mais granular sobre os resultados da consulta.

**Como implementar consultas dinâmicas com JPQL?**
Existem diversas abordagens para implementar consultas dinâmicas com JPQL no Spring Data JPA. As mais comuns são:

### 1. **Specifications:**
* **Criar uma interface Specification:** Esta interface define um método `toPredicate`, que recebe um `Root<T>` e um `CriteriaQuery<T>` e retorna um `Predicate`.
* **Construir o Predicate:** Dentro do método `toPredicate`, você pode construir o `Predicate` de forma dinâmica, adicionando as cláusulas WHERE, AND, OR, etc., de acordo com os critérios de busca.
* **Utilizar a Specification no repositório:** O método de busca do repositório receberá a Specification como parâmetro.

**Exemplo:**
```java
public interface ProdutoSpecification {
    Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb);
}

public class ProdutoSpecificationImpl implements ProdutoSpecification {
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        // Construir o Predicate com base nos critérios de busca
        List<Predicate> predicates = new ArrayList<>();
        // ... adicionar predicates

        return cb.and(predicates.toArray(new Predicate[0]));
    }
}
```

```java
public interface ProdutoRepository extends JpaRepository<Produto, Long>, JpaSpecificationExecutor<Produto> {
}
```

### 2. **@Query com parâmetros:**
* **Utilizar a anotação @Query:** Defina a consulta JPQL com parâmetros.
* **Passar os parâmetros no método do repositório:** Os valores dos parâmetros serão passados dinamicamente no momento da chamada do método.

**Exemplo:**
```java
@Query("SELECT p FROM Produto p WHERE p.nome LIKE :nome AND p.preco >= :precoMin")
List<Produto> findByNomeAndPreco(@Param("nome") String nome, @Param("precoMin") Double precoMin);
```

### 3. **JPQL dinâmico com StringBuilder:**
* **Construir a consulta em tempo de execução:** Utilize um `StringBuilder` para construir a string da consulta JPQL de forma dinâmica.
* **Injetar os parâmetros:** Utilize o `setParameter` do `TypedQuery` para adicionar os parâmetros à consulta.

**Exemplo:**
```java
StringBuilder sb = new StringBuilder("SELECT p FROM Produto p WHERE 1=1");
if (nome != null) {
    sb.append(" AND p.nome LIKE :nome");
}
if (precoMin != null) {
    sb.append(" AND p.preco >= :precoMin");
}

TypedQuery<Produto> query = entityManager.createQuery(sb.toString(), Produto.class);
if (nome != null) {
    query.setParameter("nome", "%" + nome + "%");
}
if (precoMin != null) {
    query.setParameter("precoMin", precoMin);
}

return query.getResultList();
```

**Qual abordagem escolher?**
* **Specifications:** Ideal para consultas complexas e dinâmicas, com múltiplos critérios de busca.
* **@Query com parâmetros:** Simples e eficaz para consultas com poucos parâmetros e critérios fixos.
* **JPQL dinâmico com StringBuilder:** Maior flexibilidade, mas pode ser mais propenso a erros se não for bem implementado.

**Considerações importantes:**
* **Segurança:** Evite a injeção de SQL utilizando parâmetros nomeados e validando os dados de entrada.
* **Performance:** Para consultas complexas, considere utilizar índices e otimizar as consultas.
* **Legibilidade:** Mantenha o código das consultas dinâmicas legível e fácil de entender.

**Exemplo completo com Specifications:**
```java
public class ProdutoController {
    @Autowired
    private ProdutoRepository produtoRepository;

    public List<Produto> buscarProdutos(String nome, Double precoMin) {
        ProdutoSpecification spec = new ProdutoSpecificationImpl(nome, precoMin);
        return produtoRepository.findAll(spec);
    }
}
```
---
## Implementando uma Consulta Simples com Criteria API
A Criteria API é uma ferramenta poderosa do JPA que permite construir consultas de forma programática, oferecendo uma grande flexibilidade para criar consultas dinâmicas. Vamos explorar um exemplo simples para entender como funciona:

**Cenário:**
Imagine que temos uma entidade `Produto` com os atributos `id`, `nome` e `preco`. Queremos buscar todos os produtos com o preço maior que 100.

**1. Criar a interface do repositório:**
```java
public interface ProdutoRepository extends JpaRepository<Produto, Long>, JpaSpecificationExecutor<Produto> {
}
```
* **JpaRepository:** Fornece métodos básicos de CRUD.
* **JpaSpecificationExecutor:** Permite utilizar a Criteria API para consultas mais complexas.

**2. Criar a especificação:**
```java
import javax.persistence.criteria.*;
import org.springframework.data.jpa.domain.Specification;

public class ProdutoSpecification implements Specification<Produto> {

    @Override
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        return cb.greaterThan(root.get("preco"), 100);
    }
}
```
* **Root:** Representa a entidade raiz da consulta (Produto).
* **CriteriaQuery:** Representa a consulta em si.
* **CriteriaBuilder:** Permite construir os critérios da consulta (igual a, maior que, etc.).
* **Predicate:** Representa uma condição lógica da consulta.

**3. Utilizar a especificação no serviço:**
```java
@Service
public class ProdutoService {

    @Autowired
    private ProdutoRepository produtoRepository;

    public List<Produto> buscarProdutosCaros() {
        ProdutoSpecification spec = new ProdutoSpecification();
        return produtoRepository.findAll(spec);
    }
}
```
**Explicação:**
* A classe `ProdutoSpecification` implementa a interface `Specification<Produto>`.
* O método `toPredicate` constrói o predicado `cb.greaterThan(root.get("preco"), 100)`, que significa "o preço do produto é maior que 100".
* A classe `ProdutoService` utiliza o método `findAll` do repositório, passando a especificação como parâmetro.

**Vantagens da Criteria API:**
* **Flexibilidade:** Permite construir consultas complexas de forma programática.
* **Tipo seguro:** Evita erros de sintaxe em tempo de compilação.
* **Reutilizável:** As especificações podem ser reutilizadas em diferentes partes da aplicação.
* **Integração com o Spring Data JPA:** Se integra perfeitamente com o Spring Data JPA.

**Exemplo mais complexo:**
```java
public class ProdutoSpecification implements Specification<Produto> {

    private String nome;
    private Double precoMin;

    public ProdutoSpecification(String nome, Double precoMin) {
        this.nome = nome;
        this.precoMin = precoMin;
    }

    @Override
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        List<Predicate> predicates = new ArrayList<>();
        if (nome != null) {
            predicates.add(cb.like(root.get("nome"), "%" + nome + "%"));
        }
        if (precoMin != null) {
            predicates.add(cb.greaterThanOrEqualTo(root.get("preco"), precoMin));
        }
        return cb.and(predicates.toArray(new Predicate[0]));
    }
}
```
Neste exemplo, a especificação permite buscar produtos por nome e preço mínimo, criando um predicado composto com base nos parâmetros fornecidos.

---
## Adicionando Restrições na Cláusula WHERE com Criteria API
A Criteria API oferece uma maneira flexível e tipo-segura de construir consultas dinâmicas no JPA. Uma das suas principais funcionalidades é a capacidade de adicionar restrições à cláusula WHERE, permitindo que você filtre os resultados de sua consulta de acordo com critérios específicos.

**Entendendo os Componentes:**
* **Root:** Representa a entidade raiz da sua consulta.
* **CriteriaBuilder:** Permite criar os critérios (igualdade, maior que, etc.) para a sua consulta.
* **Predicate:** Representa uma condição lógica da consulta.
* **CriteriaQuery:** Representa a consulta em si.

**Construindo Restrições:**
Para adicionar restrições à cláusula WHERE, você utiliza o método `where` do `CriteriaQuery` e passa um ou mais `Predicate`s. O `CriteriaBuilder` oferece diversos métodos para criar `Predicate`s, como:

* **Igualdade:** `cb.equal(root.get("campo"), valor)`
* **Maior que:** `cb.greaterThan(root.get("campo"), valor)`
* **Menor que:** `cb.lessThan(root.get("campo"), valor)`
* **Entre:** `cb.between(root.get("campo"), valorMinimo, valorMaximo)`
* **LIKE:** `cb.like(root.get("campo"), "%valor%")`
* **IN:** `cb.in(root.get("campo")).value(valor1).value(valor2)`
* **IsNull:** `cb.isNull(root.get("campo"))`
* **IsNotNull:** `cb.isNotNull(root.get("campo"))`

**Combinando Restrições:**
Para combinar múltiplas restrições, você pode utilizar os métodos `and` e `or` do `CriteriaBuilder`.

**Exemplo:**
```java
public class ProdutoSpecification implements Specification<Produto> {

    @Override
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        // Busca por produtos com preço maior que 100 e nome começando com "Produto"
        Predicate precoMaiorQueCem = cb.greaterThan(root.get("preco"), 100);
        Predicate nomeComecaComProduto = cb.like(root.get("nome"), "Produto%");
        return cb.and(precoMaiorQueCem, nomeComecaComProduto);
    }
}
```

**Exemplo com Múltiplos Parâmetros:**
```java
public class ProdutoSpecification implements Specification<Produto> {

    private String nome;
    private Double precoMin;

    public ProdutoSpecification(String nome, Double precoMin) {
        this.nome = nome;
        this.precoMin = precoMin;
    }

    @Override
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        List<Predicate> predicates = new ArrayList<>();
        if (nome != null) {
            predicates.add(cb.like(root.get("nome"), "%" + nome + "%"));
        }
        if (precoMin != null) {
            predicates.add(cb.greaterThanOrEqualTo(root.get("preco"), precoMin));
        }
        return cb.and(predicates.toArray(new Predicate[0]));
    }
}
```

**Utilizando a Especificação no Repositório:**
```java
public interface ProdutoRepository extends JpaRepository<Produto, Long>, JpaSpecificationExecutor<Produto> {
}
```

**Chamando a Consulta:**
```java
ProdutoSpecification spec = new ProdutoSpecification("Produto", 100.0);
List<Produto> produtos = produtoRepository.findAll(spec);
```

**Considerações Adicionais:**
* **Join:** Para realizar junções entre entidades, utilize o método `join` do `Root`.
* **Subqueries:** A Criteria API também suporta subqueries.
* **Grouping e Having:** Para realizar agrupamentos e aplicar condições sobre os grupos, utilize os métodos `groupBy` e `having` do `CriteriaQuery`.
* **Performance:** Para consultas complexas, é importante otimizar as consultas utilizando índices e evitando operações desnecessárias.
---
## Tornando a Consulta com Criteria API Dinâmica
A Criteria API oferece uma excelente flexibilidade para construir consultas dinâmicas, permitindo que você adapte a consulta de acordo com os critérios fornecidos pelo usuário ou outras variáveis da aplicação.

**Como tornar a consulta dinâmica:**
1. **Parametrizar a especificação:**
   * Crie um construtor na sua classe de especificação para receber os parâmetros de filtro.
   * Armazene esses parâmetros em atributos da classe.
   * Utilize esses atributos dentro do método `toPredicate` para construir a consulta de forma dinâmica.

2. **Construir a consulta condicionalmente:**
   * Dentro do método `toPredicate`, utilize estruturas condicionais (if, else) para adicionar ou remover partes da consulta com base nos valores dos parâmetros.

**Exemplo:**
```java
public class ProdutoSpecification implements Specification<Produto> {

    private String nome;
    private Double precoMin;
    private Double precoMax;

    public ProdutoSpecification(String nome, Double precoMin, Double precoMax) {
        this.nome = nome;
        this.precoMin = precoMin;
        this.precoMax = precoMax;
    }

    @Override
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        List<Predicate> predicates = new ArrayList<>();

        if (nome != null) {
            predicates.add(cb.like(root.get("nome"), "%" + nome + "%"));
        }

        if (precoMin != null) {
            predicates.add(cb.greaterThanOrEqualTo(root.get("preco"), precoMin));
        }

        if (precoMax != null) {
            predicates.add(cb.lessThanOrEqualTo(root.get("preco"), precoMax));
        }

        return cb.and(predicates.toArray(new Predicate[0]));
    }
}
```

**Explicação:**
* A especificação agora aceita três parâmetros: nome, preço mínimo e preço máximo.
* Dentro do método `toPredicate`, cada parâmetro é verificado e um predicado é adicionado à lista de predicados se o parâmetro não for nulo.
* Ao final, todos os predicados são combinados utilizando o `and` do `CriteriaBuilder`.

**Utilizando a especificação:**
```java
ProdutoSpecification spec = new ProdutoSpecification("Produto", 100.0, 200.0);
List<Produto> produtos = produtoRepository.findAll(spec);
```

**Flexibilidade e Personalização:**
* **Múltiplos filtros:** Você pode adicionar quantos parâmetros de filtro forem necessários à sua especificação.
* **Combinações de filtros:** Utilize os métodos `and`, `or` e `not` do `CriteriaBuilder` para criar combinações complexas de filtros.
* **Tipos de dados:** A Criteria API suporta diversos tipos de dados, permitindo criar filtros para diferentes campos da entidade.
* **Funções:** Utilize funções como `lower`, `upper`, `concat` para realizar operações mais complexas nos campos.
* **Subqueries:** Crie subconsultas para relacionar dados de diferentes entidades.

**Exemplo com subquery:**
```java
// Supondo que Produto tem uma relação com Categoria
Subquery<Long> subquery = query.subquery(Long.class);
Root<Categoria> categoria = subquery.from(Categoria.class);
subquery.select(categoria.get("id"));
subquery.where(cb.equal(categoria.get("nome"), "Eletrônicos"));
predicates.add(cb.in(root.get("categoria").get("id")).value(subquery));
```

**Considerações:**
* **Performance:** Para consultas complexas, é fundamental otimizar as consultas utilizando índices e evitando operações desnecessárias.
* **Legibilidade:** Mantenha o código da sua especificação organizado e comentado para facilitar a manutenção.
* **Segurança:** Evite a injeção de SQL utilizando parâmetros nomeados e validando os dados de entrada.
---
## O Padrão Specifications (DDD) com Spring Data JPA
O padrão Specifications, proveniente do Domain Driven Design (DDD), é uma ferramenta poderosa para construir consultas dinâmicas e flexíveis em aplicações Java utilizando o Spring Data JPA. Ele permite encapsular regras de negócio complexas em objetos, tornando o código mais legível, manutenível e testável.

### O que são Specifications?
No contexto do DDD, uma Specification representa uma regra de negócio que define um conjunto de critérios para filtrar um conjunto de entidades. No Spring Data JPA, uma Specification é uma interface que define um método `toPredicate`, responsável por construir um `Predicate` (condição lógica) a partir de um `Root` (entidade raiz), `CriteriaQuery` e `CriteriaBuilder`.

### Benefícios do uso de Specifications:
* **Reutilização de lógica:** Regras de negócio complexas podem ser encapsuladas em Specifications e reutilizadas em diferentes partes da aplicação.
* **Testes:** É mais fácil testar as Specifications isoladamente, garantindo a corretude das regras de negócio.
* **Leiturabilidade:** O código fica mais legível ao separar a lógica de negócio da implementação técnica da consulta.
* **Flexibilidade:** Permite construir consultas dinâmicas de forma declarativa, facilitando a adaptação a mudanças nos requisitos.
 ---
### Implementando Specifications
**1. Criar a interface Specification:**
```java
import javax.persistence.criteria.*;
import org.springframework.data.jpa.domain.Specification;

public interface ProdutoSpecification extends Specification<Produto> {
}
```

**2. Implementar a Specification:**
```java
public class ProdutoNomeSpecification implements ProdutoSpecification {

    private String nome;

    public ProdutoNomeSpecification(String nome) {
        this.nome = nome;
    }

    @Override
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        return cb.like(root.get("nome"), "%" + nome + "%");
    }
}
```

**3. Utilizar a Specification no repositório:**
```java
public interface ProdutoRepository extends JpaRepository<Produto, Long>, JpaSpecificationExecutor<Produto> {
}
```

**4. Chamar a consulta:**
```java
ProdutoSpecification spec = new ProdutoNomeSpecification("Notebook");
List<Produto> produtos = produtoRepository.findAll(spec);
```

### Combinando Múltiplas Specifications
Para combinar múltiplas Specifications, você pode utilizar os métodos `and`, `or` e `not` do `CriteriaBuilder`.

```java
ProdutoSpecification specNome = new ProdutoNomeSpecification("Notebook");
ProdutoSpecification specPreco = new ProdutoPrecoSpecification(1000.0);

Specification<Produto> combinedSpec = specNome.and(specPreco);
List<Produto> produtos = produtoRepository.findAll(combinedSpec);
```

### Criando Specifications Dinâmicas
Você pode criar Specifications dinâmicas passando parâmetros para o construtor da classe de especificação. Isso permite construir consultas personalizadas com base em diferentes critérios.

```java
public class ProdutoSpecification implements Specification<Produto> {
    // ...
    public Predicate toPredicate(Root<Produto> root, CriteriaQuery<?> query, CriteriaBuilder cb) {
        // Construir a consulta com base nos parâmetros
    }
}
```

### Vantagens Adicionais
* **Regras de negócio complexas:** As Specifications podem encapsular regras de negócio complexas, como validações, cálculos e combinações de critérios.
* **Testes unitários:** As Specifications podem ser testadas isoladamente, garantindo a corretude das regras de negócio.
* **Integração com outras ferramentas:** As Specifications podem ser integradas com outras ferramentas, como frameworks de busca e ferramentas de relatório.
---
## Criando uma Fábrica de Specifications
Uma fábrica de Specifications pode ser uma ferramenta poderosa para centralizar a criação de consultas dinâmicas e complexas em sua aplicação. Ela permite que você encapsule a lógica de construção de Specifications, tornando o código mais organizado e reutilizável.

**Por que usar uma fábrica de Specifications?**
* **Reutilização de código:** Crie Specifications genéricas que podem ser reutilizadas em diferentes partes da aplicação.
* **Facilidade de manutenção:** Centralize a lógica de construção de consultas em um único lugar.
* **Melhora na legibilidade:** Separe a lógica de negócio da implementação técnica da consulta.
* **Flexibilidade:** Permite criar consultas dinâmicas com base em diferentes critérios.

**Como criar uma fábrica de Specifications:**

1. **Definir a interface da fábrica:**
```java
public interface SpecificationFactory<T> {
    Specification<T> createSpecification(Map<String, Object> filters);
}
```

2. **Implementar a fábrica:**
```java
public class ProdutoSpecificationFactory implements SpecificationFactory<Produto> {

    @Override
    public Specification<Produto> createSpecification(Map<String, Object> filters) {
        CriteriaBuilder cb = entityManager.getCriteriaBuilder();
        CriteriaQuery<Produto> query = cb.createQuery(Produto.class);
        Root<Produto> root = query.from(Produto.class);

        List<Predicate> predicates = new ArrayList<>();

        filters.forEach((key, value) -> {
            switch (key) {
                case "nome":
                    predicates.add(cb.like(root.get("nome"), "%" + value + "%"));
                    break;
                case "preco":
                    predicates.add(cb.greaterThanOrEqualTo(root.get("preco"), (Double) value));
                    break;
                // ... outros filtros
            }
        });

        return cb.and(predicates.toArray(new Predicate[0]));
    }
}
```

3. **Utilizar a fábrica:**
```java
Map<String, Object> filters = new HashMap<>();
filters.put("nome", "Notebook");
filters.put("preco", 1000.0);

ProdutoSpecificationFactory factory = new ProdutoSpecificationFactory();
Specification<Produto> spec = factory.createSpecification(filters);
List<Produto> produtos = produtoRepository.findAll(spec);
```

**Explicação:**
* A interface `SpecificationFactory` define um método `createSpecification` que recebe um mapa de filtros e retorna uma Specification.
* A implementação da fábrica itera sobre o mapa de filtros e constrói os predicados de acordo com as chaves e valores.
* A consulta final é construída combinando todos os predicados.

**Vantagens desta abordagem:**
* **Flexibilidade:** Você pode adicionar novos filtros facilmente, apenas adicionando um novo case no switch.
* **Reutilização:** A fábrica pode ser reutilizada em diferentes partes da aplicação.
* **Extensibilidade:** Você pode criar fábricas mais complexas para lidar com filtros mais sofisticados.

**Considerações:**
* **Tipo seguro:** É recomendado utilizar tipos seguros para os valores dos filtros, como `Enum`s ou classes específicas.
* **Performance:** Para consultas complexas, é importante otimizar as consultas utilizando índices e evitando operações desnecessárias.
* **Segurança:** Evite a injeção de SQL utilizando parâmetros nomeados e validando os dados de entrada.

**Exemplo com Enum:**
```java
public enum FilterType {
    NOME, PRECO, CATEGORIA
}

public class ProdutoSpecificationFactory implements SpecificationFactory<Produto> {
    // ...
    switch (key) {
        case "NOME":
            predicates.add(cb.like(root.get("nome"), "%" + value + "%"));
            break;
        // ... outros casos
    }
}
```
---
## Injetando o Próprio Repositório na Implementação Customizada e a Anotação @Lazy

### Entendendo o Cenário
A injeção de um repositório dentro da própria implementação customizada pode parecer contraintuitiva à primeira vista, mas existem cenários específicos onde essa abordagem pode ser útil, especialmente quando se trabalha com consultas complexas ou quando é necessário realizar operações recursivas.

A anotação `@Lazy` é utilizada para controlar a inicialização de beans no Spring. Ao aplicar `@Lazy` a um bean, ele não será inicializado durante o startup do contexto do Spring, mas sim quando for injetado em outro bean pela primeira vez.

### Quando Utilizar essa Abordagem?
* **Consultas recursivas:** Em casos onde uma entidade precisa consultar a si mesma ou outras entidades relacionadas em uma hierarquia complexa, a injeção do repositório pode ajudar a simplificar a lógica.
* **Customizações complexas:** Quando a consulta envolve lógica de negócio complexa ou cálculos específicos, a injeção do repositório permite centralizar essa lógica em um único lugar.
* **Performance:** Em alguns casos, a injeção do repositório pode ajudar a otimizar a performance, evitando consultas desnecessárias.

### Exemplo Prático
```java
@Service
public class ProdutoService {

    @Autowired
    private ProdutoRepository produtoRepository;

    public List<Produto> buscarProdutosComRelacionamentos() {
        List<Produto> produtos = produtoRepository.findAll();
        produtos.forEach(produto -> {
            // Carregar os relacionamentos do produto de forma lazy
            produto.getRelacionamentos().forEach(relacionamento -> {
                // ... lógica para carregar os dados do relacionamento
            });
        });
        return produtos;
    }
}
```

**Problema:** Neste exemplo, estamos carregando todos os produtos e depois carregando os relacionamentos de cada produto. Se a tabela de relacionamentos for muito grande, isso pode impactar o desempenho.

**Solução com injeção do repositório:**
```java
@Service
public class ProdutoService {

    @Autowired
    private ProdutoRepository produtoRepository;

    @Autowired
    @Lazy
    private ProdutoService produtoService; // Injeção do próprio serviço

    public List<Produto> buscarProdutosComRelacionamentos() {
        List<Produto> produtos = produtoRepository.findAll();
        produtos.forEach(produto -> {
            // Carregar os relacionamentos do produto de forma lazy, utilizando o próprio serviço
            produto.setRelacionamentos(produtoService.buscarRelacionamentosPorProduto(produto.getId()));
        });
        return produtos;
    }

    public List<Relacionamento> buscarRelacionamentosPorProduto(Long produtoId) {
        // Lógica para buscar os relacionamentos do produto
        return relacionamentoRepository.findByProdutoId(produtoId);
    }
}
```

**Explicação:**
* **Injeção circular:** Ao injetar o `ProdutoService` dentro de si mesmo, criamos uma injeção circular. A anotação `@Lazy` garante que o `ProdutoService` seja inicializado apenas quando necessário, evitando um ciclo infinito.
* **Carga lazy dos relacionamentos:** Ao chamar o método `buscarRelacionamentosPorProduto` dentro do loop, estamos carregando os relacionamentos de cada produto de forma lazy, evitando carregar todos os relacionamentos de uma vez.

### Considerações Importantes
* **Ciclo de dependência:** A injeção circular deve ser utilizada com cuidado, pois pode levar a problemas de inicialização se não for configurada corretamente.
* **Performance:** Avalie o impacto da injeção do repositório na performance da sua aplicação. Em alguns casos, pode ser mais eficiente utilizar mecanismos de lazy loading do JPA.
* **Testes:** É fundamental escrever testes unitários para garantir que a lógica funcione corretamente.
* **Alternativas:** Considere utilizar outras abordagens, como projeções ou view objects, para resolver problemas de carga excessiva.
---
## Estendendo o JpaRepository para Customizar o Repositório Base

**Entendendo a necessidade:**

Ao trabalhar com Spring Data JPA, o `JpaRepository` oferece uma base sólida para operações CRUD em entidades. No entanto, em muitos cenários, é necessário adicionar funcionalidades personalizadas para atender a requisitos específicos do domínio. Estender o `JpaRepository` permite criar repositórios customizados com métodos e comportamentos únicos.

**Por que estender o JpaRepository?**

* **Métodos personalizados:** Criar métodos para consultas complexas que não são diretamente suportadas pela query method implementation.
* **Lógica de negócio específica:** Encapsular lógica de negócio relacionada ao domínio dentro do repositório.
* **Herança de comportamentos:** Herdar métodos e funcionalidades do `JpaRepository` e adicioná-las.

**Como estender o JpaRepository:**

1. **Criar uma interface:**
   ```java
   public interface CustomProdutoRepository extends JpaRepository<Produto, Long> {
       List<Produto> findByNomeContaining(String nome);
       // Outros métodos personalizados
   }
   ```
2. **Criar a implementação:**
   ```java
   @Repository
   public class CustomProdutoRepositoryImpl implements CustomProdutoRepository {
       @PersistenceContext
       private EntityManager entityManager;

       @Override
       public List<Produto> findByNomeContaining(String nome) {
           CriteriaBuilder cb = entityManager.getCriteriaBuilder();
           CriteriaQuery<Produto> query = cb.createQuery(Produto.class);
           Root<Produto> root = query.from(Produto.class);
           return entityManager.createQuery(query
                   .where(cb.like(root.get("nome"), "%" + nome + "%")))
                   .getResultList();
       }
   }
   ```
3. **Configurar a interface:**
   ```java
   @Repository
   public interface ProdutoRepository extends CustomProdutoRepository {
       // Outros métodos do JpaRepository
   }
   ```

**Explicando o código:**

* **Interface customizada:** A interface `CustomProdutoRepository` estende o `JpaRepository` e define o método personalizado `findByNomeContaining`.
* **Implementação customizada:** A classe `CustomProdutoRepositoryImpl` implementa a interface customizada e fornece a implementação do método personalizado utilizando o `EntityManager`.
* **Combinação:** A interface `ProdutoRepository` estende tanto o `JpaRepository` quanto a interface customizada, combinando os métodos de ambos.

**Vantagens:**

* **Reutilização:** O `JpaRepository` fornece métodos básicos de CRUD, que podem ser reutilizados.
* **Flexibilidade:** Permite criar métodos personalizados para atender a requisitos específicos.
* **Organização:** Separa a lógica de acesso aos dados da lógica de negócio.
* **Testes:** Facilita a criação de testes unitários para os métodos personalizados.

**Considerações:**

* **Performance:** Para consultas complexas, considere utilizar índices para melhorar o desempenho.
* **Legibilidade:** Escreva código claro e conciso, utilizando nomes de métodos significativos.
* **Testes:** Crie testes unitários para garantir a corretude dos métodos personalizados.
* **Convenções:** Siga as convenções de nomenclatura do Spring Data JPA para facilitar a compreensão do código.

**Cenários de uso:**

* **Consultas complexas:** Joins, agrupamentos, funções de agregação.
* **Lógica de negócios específica:** Validações, cálculos, transformações de dados.
* **Personalização do comportamento:** Sobrescrever métodos do `JpaRepository` para adicionar comportamento personalizado.

**Exemplo com Criteria API:**
O exemplo acima utiliza a Criteria API para construir a consulta. A Criteria API oferece uma forma mais flexível e poderosa de criar consultas dinâmicas.

**Outras opções:**

* **@Query:** Utilizar a anotação `@Query` para escrever consultas JPQL ou nativas.
* **Specifications:** Utilizar o padrão Specifications para criar consultas dinâmicas e complexas.
* **Projections:** Projetar os resultados da consulta em objetos personalizados.
---
