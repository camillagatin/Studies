## Streams API: Uma Introdução às Correntes de Dados

**O que são Streams?**
Em Java 8, a API de Streams foi introduzida como uma forma elegante e funcional de processar coleções de dados. Imagine uma corrente de dados fluindo, onde cada elemento é processado de forma sequencial ou paralela. Essa é a essência das Streams.

**Por que usar Streams?**
* **Código mais conciso e expressivo:** As operações em Streams são declarativas, o que torna o código mais fácil de ler e entender.
* **Processamento paralelo:** Muitas operações em Streams podem ser realizadas em paralelo, aproveitando múltiplos núcleos de processador.
* **Laziness:** As operações em Streams são geralmente *lazy*, ou seja, são executadas apenas quando o resultado final é necessário. Isso permite otimizações e evita cálculos desnecessários.

**Operações básicas em Streams**
As operações em Streams podem ser divididas em dois grupos:
1. **Intermediárias:** Retornam uma nova Stream, permitindo encadear múltiplas operações.
   * **map:** Aplica uma função a cada elemento da Stream, retornando uma nova Stream com os resultados.
   * **filter:** Filtra os elementos da Stream com base em um predicado.
   * **flatMap:** Mapeia cada elemento para uma Stream e depois achata todas as Streams em uma única.
   * **sorted:** Ordena os elementos da Stream.
   * **distinct:** Remove elementos duplicados.
   * **limit:** Limita o número de elementos da Stream.
   * **skip:** Pula os primeiros n elementos da Stream.

2. **Terminais:** Consomem a Stream e produzem um resultado.
   * **forEach:** Executa uma ação para cada elemento da Stream.
   * **collect:** Coleta os elementos da Stream em uma coleção.
   * **reduce:** Reduz os elementos da Stream a um único valor.
   * **anyMatch, allMatch, noneMatch:** Verifica se algum, todos ou nenhum elemento satisfaz uma condição.
   * **findFirst, findAny:** Retorna o primeiro ou qualquer elemento da Stream.

**Exemplo:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Encontrar os números pares e somá-los
int sumOfEvenNumbers = numbers.stream()
                              .filter(n -> n % 2 == 0)
                              .map(n -> n * n) // Elevar ao quadrado
                              .reduce(0, Integer::sum);
```

**Quando usar Streams?**
* **Processamento de coleções:** Para realizar operações como filtragem, mapeamento, ordenação e redução.
* **Processamento paralelo:** Para aproveitar a capacidade de processamento de múltiplos núcleos.
* **Expressões funcionais:** Para escrever código mais conciso e declarativo.

**Considerações importantes:**
* **Immutable:** As Streams são imutáveis. As operações em Streams não modificam a coleção original.
* **Lazy evaluation:** As operações em Streams são geralmente *lazy*, o que significa que são executadas apenas quando o resultado final é necessário.
* **Performance:** A performance das Streams pode variar dependendo da implementação e dos dados. É importante entender como as operações são otimizadas.
---
## Stream.filter(): Filtrando elementos em uma Stream
A operação `filter` é uma das mais comuns e versáteis da API de Streams em Java. Ela permite que você crie uma nova Stream, contendo apenas os elementos que satisfazem um determinado critério.

#### Sintaxe:
```java
Stream<T> filteredStream = stream.filter(predicate);
```
* **stream:** A Stream original que você deseja filtrar.
* **predicate:** Um objeto funcional que representa a condição de filtragem. Deve retornar um booleano indicando se o elemento deve ser incluído na nova Stream.

#### Como funciona:
1. **Iteração:** O `filter` itera sobre cada elemento da Stream original.
2. **Avaliação:** Para cada elemento, o predicado é aplicado.
3. **Inclusão:** Se o predicado retorna `true`, o elemento é incluído na nova Stream. Caso contrário, ele é descartado.

#### Exemplo:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);

// Filtrar os números pares
List<Integer> evenNumbers = numbers.stream()
                                    .filter(n -> n % 2 == 0)
                                    .collect(Collectors.toList());
```
Neste exemplo:
* Criamos uma lista de números inteiros.
* Transformamos a lista em uma Stream.
* Aplicamos o `filter` para selecionar apenas os números pares (aqueles divisíveis por 2).
* Coletamos os resultados em uma nova lista.

#### Usos comuns:
* **Selecionar elementos:** Filtrar elementos com base em propriedades específicas (por exemplo, idade, nome, status).
* **Remover elementos:** Excluir elementos que não atendem a um determinado critério.
* **Criar subconjuntos:** Dividir uma Stream em subconjuntos com base em diferentes condições.

#### Exemplos mais complexos:
```java
// Filtrar pessoas com idade maior que 30 e nome começando com "A"
List<Person> people = ...; // Suponha que você tenha uma lista de objetos Person
List<Person> filteredPeople = people.stream()
                                    .filter(p -> p.getAge() > 30)
                                    .filter(p -> p.getName().startsWith("A"))
                                    .collect(Collectors.toList());
```
**Observações:**
* **Encadeamento de filtros:** Você pode encadear múltiplos `filter` para criar filtros mais complexos.
* **Lazy evaluation:** O `filter` é uma operação *lazy*. Isso significa que os elementos são filtrados apenas quando são necessários, como ao coletar os resultados em uma lista ou ao aplicar outra operação terminal.
* **Parallel streams:** O `filter` pode ser usado com streams paralelas, permitindo que a filtragem seja realizada em paralelo em múltiplos núcleos de processador.
---
## Stream.forEach(): Iterando sobre cada elemento de uma Stream

A operação `forEach` é uma operação terminal da API de Streams em Java que permite percorrer cada elemento de uma Stream e executar uma ação específica para cada um deles. É como um `for` tradicional, mas com uma sintaxe mais concisa e funcional.

### Sintaxe:
`{java}stream.forEach(action);`
* **stream:** A Stream que você deseja percorrer.
* **action:** Uma expressão lambda que representa a ação a ser executada para cada elemento. A expressão lambda recebe um parâmetro que representa o elemento atual da Stream.

### Como funciona:
1. **Iteração:** O `forEach` itera sobre cada elemento da Stream.
2. **Execução:** Para cada elemento, a ação especificada na expressão lambda é executada.

### Exemplo:
```java
List<String> names = Arrays.asList("Ana", "Bruno", "Carla");

// Imprimir cada nome
names.stream()
     .forEach(name -> System.out.println(name));
```
Neste exemplo:
* Criamos uma lista de nomes.
* Transformamos a lista em uma Stream.
* Usamos `forEach` para imprimir cada nome na console.

### Usos comuns:
* **Imprimir elementos:** Exibir os elementos da Stream em um console ou em um arquivo.
* **Atualizar elementos:** Modificar os elementos da Stream (embora seja mais comum criar uma nova Stream com os elementos modificados).
* **Realizar ações secundárias:** Executar outras ações para cada elemento, como enviar uma notificação, salvar um registro em um banco de dados, etc.

### Exemplos mais complexos:
```java
// Multiplicar cada número por 2 e imprimir o resultado
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .map(n -> n * 2)
       .forEach(n -> System.out.println(n));
```

### Observações:
* **Operação terminal:** `forEach` é uma operação terminal, o que significa que ela consome a Stream e não retorna outra Stream.
* **Sem retorno:** `forEach` não retorna nenhum valor. Seu propósito é simplesmente executar uma ação para cada elemento.
* **Lado a lado:** A ação executada dentro do `forEach` não pode modificar a Stream original. Se você precisar modificar os elementos, use `map` para criar uma nova Stream com os elementos modificados.
* **Parallel streams:** `forEach` pode ser usado com streams paralelas, mas cuidado: se a ação não for thread-safe, você pode ter resultados inesperados.
---
## Criando Pipelines com Encadeamento de Operações em Streams

**O que é um pipeline de Streams?**
Um pipeline de Streams é uma sequência de operações intermediárias e terminais aplicadas a uma Stream. Cada operação transforma a Stream de alguma forma, criando um novo Stream como resultado. Essa abordagem permite um processamento de dados declarativo e eficiente.

**Como criar um pipeline:**
1. **Obter uma Stream:** A primeira etapa é obter uma Stream a partir de uma coleção (List, Set, etc.), um array ou um gerador de valores.
2. **Aplicar operações intermediárias:** Encadeie as operações intermediárias para filtrar, mapear, ordenar ou transformar os elementos da Stream.
3. **Aplicar uma operação terminal:** A última operação do pipeline deve ser uma operação terminal que consome a Stream e produz um resultado final.

**Exemplo:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);

// Encontrar a soma dos quadrados dos números pares
int sumOfEvenSquares = numbers.stream()
                              .filter(n -> n % 2 == 0) // Filtrar os números pares
                              .map(n -> n * n)     // Elevar ao quadrado
                              .reduce(0, Integer::sum); // Somar os resultados
```
**Explicação do código:**
* **Obter a Stream:** A lista de números é convertida em uma Stream.
* **Operação intermediária 1: filter:** Filtra os números pares.
* **Operação intermediária 2: map:** Eleva ao quadrado cada número.
* **Operação terminal: reduce:** Soma todos os números resultantes.

**Encadeamento de operações:**
A beleza da API de Streams está na capacidade de encadear várias operações intermediárias. Cada operação retorna uma nova Stream, permitindo que você construa pipelines complexos para processar seus dados de forma declarativa.

**Exemplo mais complexo:**
```java
List<Person> people = ...; // Uma lista de objetos Person com atributos name e age

// Encontrar a pessoa mais velha com nome começando com "A"
Optional<Person> oldestPersonStartingWithA = people.stream()
                                                 .filter(p -> p.getName().startsWith("A"))
                                                 .max(Comparator.comparing(Person::getAge));
```

**Vantagens de usar pipelines:**
* **Código mais conciso e legível:** O código fica mais expressivo e fácil de entender.
* **Reutilização de código:** As operações intermediárias podem ser reutilizadas em diferentes pipelines.
* **Paralelização:** Muitas operações podem ser paralelizadas, aproveitando múltiplos núcleos de processador.
* **Lazy evaluation:** As operações são executadas apenas quando a operação terminal é alcançada, o que pode levar a otimizações de desempenho.

**Considerações importantes:**
* **Operações intermediárias:** Retornam uma nova Stream e são executadas de forma lazy.
* **Operação terminal:** Consome a Stream e produz um resultado final.
* **Immutable:** As Streams são imutáveis. As operações não modificam a Stream original.
* **Parallel streams:** É possível paralelizar as operações, mas é preciso ter cuidado com a thread safety.
---
## Stream.peek(): Uma Visão Geral
O método `peek()` em Streams do Java é uma operação intermediária que permite você "espiar" os elementos de uma Stream à medida que eles passam por um pipeline. É como colocar um ponto de verificação em um fluxo de dados para inspecionar os elementos sem alterá-los.

**Sintaxe:**
`{java}Stream<T> peekedStream = stream.peek(action);`
* **stream:** A Stream original.
* **action:** Uma ação a ser executada em cada elemento. Essa ação é geralmente uma expressão lambda que imprime o elemento, o loga ou executa alguma outra operação de "lado de efeito".

**Por que usar peek()?**
* **Depuração:** É extremamente útil para depurar pipelines complexos, permitindo que você veja os elementos em cada etapa do processo.
* **Logging:** Pode ser usado para registrar informações sobre os elementos que estão sendo processados.
* **Side effects:** Embora não seja recomendado para modificar o estado de objetos, `peek()` pode ser usado para executar ações que têm efeitos colaterais, como atualizar um contador ou adicionar elementos a uma coleção externa.

**Exemplo:**
```java
List<String> names = Arrays.asList("Ana", "Bruno", "Carla");

names.stream()
     .filter(name -> name.length() > 4)
     .peek(name -> System.out.println("Nome filtrado: " + name))
     .map(String::toUpperCase)
     .forEach(System.out::println);
```
Neste exemplo:
* Filtramos os nomes com mais de 4 caracteres.
* Usamos `peek()` para imprimir os nomes que passaram pelo filtro.
* Convertemos os nomes para maiúsculas.
* Imprimimos os nomes finais.

**Importante:**
* **Não modifica a Stream:** `peek()` retorna uma nova Stream com os mesmos elementos, apenas executando a ação fornecida em cada elemento.
* **Side effects:** Evite usar `peek()` para modificar o estado de objetos dentro da Stream, pois isso pode levar a comportamentos inesperados e tornar o código mais difícil de entender e manter.
* **Operação intermediária:** `peek()` é uma operação intermediária, o que significa que pode ser encadeada com outras operações.

**Quando usar peek()?**
* **Depuração:** Para entender o fluxo de dados em um pipeline.
* **Logging:** Para registrar informações sobre o processamento dos dados.
* **Ações secundárias:** Para executar ações simples que não alteram a estrutura da Stream.

**Exemplo mais complexo:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

int count = 0;
numbers.stream()
       .filter(n -> n % 2 == 0)
       .peek(n -> count++)
       .map(n -> n * 2)
       .forEach(System.out::println);

System.out.println("Número de pares: " + count);
```
---
## Operações Terminais de Curto-Circuito: findFirst e findAny
As operações terminais `findFirst` e `findAny` são ferramentas poderosas na API de Streams do Java, especialmente quando você precisa encontrar um único elemento que satisfaça uma determinada condição. Elas são chamadas de operações de **curto-circuito** porque, assim que encontram o primeiro elemento que satisfaz o critério, elas interrompem a avaliação da Stream, evitando iterações desnecessárias e otimizando o desempenho.

### findFirst()
* **Retorna:** O primeiro elemento da Stream que satisfaz o predicado fornecido.
* **Ordem:** Respeita a ordem original dos elementos na Stream.
* **Paralelismo:** Em Streams paralelas, a garantia de que o primeiro elemento será retornado não é absoluta, mas é provável.

**Exemplo:**
```java
List<String> names = Arrays.asList("Ana", "Bruno", "Carla");

Optional<String> firstStartingWithA = names.stream()
                                           .filter(name -> name.startsWith("A"))
                                           .findFirst();
```

### findAny()
* **Retorna:** Qualquer elemento da Stream que satisfaça o predicado fornecido.
* **Ordem:** Não há garantia de que o elemento retornado seja o primeiro.
* **Paralelismo:** Em Streams paralelas, `findAny` pode ser mais eficiente do que `findFirst`, pois não precisa garantir a ordem.

**Exemplo:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

Optional<Integer> anyEvenNumber = numbers.stream()
                                         .filter(n -> n % 2 == 0)
                                         .findAny();
```

### Quando usar cada uma?
* **findFirst:**
  * Quando a ordem dos elementos é importante e você precisa do primeiro elemento que satisfaz a condição.
  * Em Streams sequenciais, é garantido que o primeiro elemento será retornado.
* **findAny:**
  * Quando a ordem dos elementos não é importante e você precisa de qualquer elemento que satisfaça a condição.
  * Em Streams paralelas, pode ser mais eficiente, pois não precisa garantir a ordem.
  * Quando a probabilidade de encontrar um elemento que satisfaça a condição é alta, `findAny` pode ser mais rápido.

### Retorno Optional
Tanto `findFirst` quanto `findAny` retornam um `Optional`. Isso é importante porque:
* **Elemento não encontrado:** Se nenhum elemento satisfizer o predicado, o `Optional` estará vazio.
* **NullPointerException:** Evita `NullPointerExceptions` ao tentar acessar um elemento que pode não existir.

**Exemplo com Optional:**
```java
if (firstStartingWithA.isPresent()) {
    System.out.println("O primeiro nome começando com A é: " + firstStartingWithA.get());
} else {
    System.out.println("Nenhum nome começa com A.");
}
```
---
## Testando Predicados com Stream.anyMatch, Stream.allMatch e Stream.noneMatch
As operações terminais `anyMatch`, `allMatch` e `noneMatch` são úteis para verificar se algum, todos ou nenhum elemento de uma Stream satisfaz um determinado predicado. Elas são operações de curto-circuito, o que significa que podem interromper a avaliação da Stream assim que o resultado final é determinado.

### Stream.anyMatch()
* Retorna `true` se pelo menos um elemento da Stream satisfaz o predicado.
* Interrompe a avaliação da Stream assim que encontra um elemento que satisfaz o predicado.

**Exemplo:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

boolean anyEvenNumber = numbers.stream()
                                .anyMatch(n -> n % 2 == 0);
```

### Stream.allMatch()

* Retorna `true` se todos os elementos da Stream satisfazem o predicado.
* Interrompe a avaliação da Stream assim que encontra um elemento que não satisfaz o predicado.

**Exemplo:**
```java
List<String> names = Arrays.asList("Ana", "Bruno", "Carla");

boolean allNamesStartWithA = names.stream()
                                  .allMatch(name -> name.startsWith("A"));
```

### Stream.noneMatch()
* Retorna `true` se nenhum elemento da Stream satisfaz o predicado.
* Interrompe a avaliação da Stream assim que encontra um elemento que satisfaz o predicado.

**Exemplo:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

boolean noneIsNegative = numbers.stream()
                                .noneMatch(n -> n < 0);
```

### Quando usar cada uma?
* **anyMatch:** Quando você precisa verificar se pelo menos um elemento satisfaz uma condição.
* **allMatch:** Quando você precisa verificar se todos os elementos satisfazem uma condição.
* **noneMatch:** Quando você precisa verificar se nenhum elemento satisfaz uma condição.

#### Exemplo mais complexo:
```java
List<Person> people = ...; // Uma lista de objetos Person com atributos name e age

boolean someoneIsOver30 = people.stream()
                                .anyMatch(p -> p.getAge() > 30);

boolean everyoneIsOver18 = people.stream()
                                .allMatch(p -> p.getAge() >= 18);

boolean noOneIsUnder10 = people.stream()
                                .noneMatch(p -> p.getAge() < 10);
```
---
## Ordenando Elementos de Streams
A API de Streams do Java oferece uma forma elegante e concisa de ordenar coleções de dados. O método `sorted()` é o principal responsável por essa funcionalidade, permitindo que você ordene os elementos de uma Stream de acordo com um critério específico.

### Como funciona o sorted()
O método `sorted()` aceita um `Comparator` opcional. Se nenhum `Comparator` for fornecido, os elementos serão ordenados de acordo com a ordem natural dos elementos (implementada pela interface `Comparable`). 

**Sem Comparator:**
```java
List<Integer> numbers = Arrays.asList(3, 1, 4, 1, 5, 9);
List<Integer> sortedNumbers = numbers.stream()
                                    .sorted()
                                    .collect(Collectors.toList());
```

**Com Comparator:**
```java
class Person {
    String name;
    int age;
    // ... construtores, getters e setters
}

List<Person> people = ...; // Uma lista de pessoas

List<Person> sortedByAge = people.stream()
                               .sorted(Comparator.comparing(Person::getAge))
                               .collect(Collectors.toList());
```

### Customizando a Ordenação com Comparator
* **Comparator.comparing():** Cria um `Comparator` com base em um método extraído.
* **Comparator.thenComparing():** Encadeia múltiplos comparadores para ordenação multi-nível.
* **Comparator.reversed():** Inverte a ordem de comparação.

**Exemplo de ordenação multi-nível:**
```java
List<Person> sortedByAgeAndName = people.stream()
                                      .sorted(Comparator.comparing(Person::getAge)
                                                      .thenComparing(Person::getName))
                                      .collect(Collectors.toList());
```

### Ordenação Paralela
A operação `sorted()` pode ser aplicada em Streams paralelas, mas é importante lembrar que a ordem dos elementos não é garantida em todas as posições da Stream resultante. A garantia é que todos os elementos menores virão antes dos maiores.

### Outros Pontos a Considerar
* **Estabilidade:** A ordenação é estável, o que significa que elementos iguais manterão sua ordem relativa na Stream original.
* **Lazy Evaluation:** `sorted()` é uma operação intermediária, ou seja, a ordenação só ocorre quando uma operação terminal é aplicada.
* **Tipos Primitivos:** Para tipos primitivos, existem métodos específicos como `IntStream.sorted()`, `DoubleStream.sorted()`, etc.

### Exemplos Adicionais
* **Ordenando Strings por comprimento:**
```java
List<String> words = Arrays.asList("banana", "apple", "orange");
List<String> sortedByLength = words.stream()
                                   .sorted(Comparator.comparingInt(String::length))
                                   .collect(Collectors.toList());
```

* **Ordenando um conjunto de objetos personalizados:**
```java
class Produto {
    String nome;
    double preco;
    // ...
}

List<Produto> produtos = ...;
List<Produto> sortedByPreco = produtos.stream()
                                     .sorted(Comparator.comparingDouble(Produto::getPreco))
                                     .collect(Collectors.toList());
```
---
## Operações Intermediárias com Estado em Streams

### O que são operações intermediárias com estado?
Em um pipeline de Streams, as operações intermediárias são responsáveis por transformar a Stream, gerando uma nova Stream a partir da anterior. Normalmente, essas operações são **sem estado** (stateless), ou seja, o resultado de uma operação depende apenas dos elementos da Stream atual e não de qualquer estado externo ou de processamentos anteriores.

**Operações intermediárias com estado** são aquelas que **mantêm algum tipo de estado** durante a execução do pipeline. Esse estado pode ser usado para influenciar o resultado das operações subsequentes. Um exemplo clássico é o `reduce` quando usado para concatenar strings, onde um acumulador mantém a string construída até então.

### Por que usar operações intermediárias com estado?
* **Agrupamento:** Agrupar elementos com base em um critério, como em um agrupamento por chave.
* **Contagem:** Contar o número de elementos que satisfazem uma determinada condição.
* **Acumulação:** Calcular somas, produtos, máximos, mínimos, etc.
* **Construção de estruturas de dados:** Criar listas, mapas, ou outras estruturas de dados a partir dos elementos da Stream.

### Exemplos comuns
* **`reduce` para concatenar strings:**
  ```java
  List<String> words = Arrays.asList("Hello", "world", "!");
  String joined = words.stream()
                       .reduce("", (acc, word) -> acc + " " + word);
  ```
  O acumulador `acc` mantém a string construída até o momento.
* **`collect` para agrupar elementos:**
  ```java
  Map<Integer, List<Person>> peopleByAge = people.stream()
                                                .collect(Collectors.groupingBy(Person::getAge));
  ```
  O `Collector` mantém um mapa para agrupar as pessoas por idade.

### Cuidados ao usar operações intermediárias com estado
* **Thread safety:** Se a Stream for paralela, é crucial garantir que o estado seja acessado de forma thread-safe para evitar problemas de concorrência.
* **Complexidade:** Operações com estado podem tornar o código mais complexo e menos fácil de entender.
* **Eficiência:** O uso excessivo de operações com estado pode impactar o desempenho, especialmente em pipelines longos.

### Quando usar e quando evitar
* **Use:** Quando a operação não puder ser expressa de forma puramente funcional ou quando a eficiência for um fator importante.
* **Evite:** Se possível, prefira operações sem estado para manter o código mais simples e fácil de entender.

### Alternativas às operações com estado
* **Dividir o pipeline:** Em alguns casos, pode ser mais eficiente dividir o pipeline em várias etapas, usando operações intermediárias sem estado e combinando os resultados posteriormente.
* **Utilizar bibliotecas funcionais:** Bibliotecas como Vavr ou Lombok oferecem funcionalidades adicionais para trabalhar com dados imutáveis e funções puras, o que pode ajudar a reduzir a necessidade de operações com estado.
___
## Transformando elementos com Stream.map()
O método `map()` é uma das ferramentas mais poderosas da API de Streams do Java. Ele permite que você aplique uma função a cada elemento de uma Stream, transformando-o em um novo elemento. Essa transformação pode ser simples, como converter um tipo de dado para outro, ou mais complexa, como aplicar cálculos ou criar novos objetos.

**Sintaxe:**
`{java}Stream<T> mappedStream = stream.map(function);`
* **stream:** A Stream original.
* **function:** Uma função que recebe um elemento do tipo `T` da Stream original e retorna um elemento do novo tipo. Essa função é geralmente uma expressão lambda.
* **mappedStream:** Uma nova Stream com os elementos transformados.

**Exemplo:**
```java
List<String> names = Arrays.asList("Ana", "Bruno", "Carla");

List<Integer> lengths = names.stream()
                             .map(String::length)
                             .collect(Collectors.toList());
```
Neste exemplo:
* Criamos uma lista de nomes.
* Usamos `map` para obter o comprimento de cada nome, transformando a Stream de `String` em uma Stream de `Integer`.
* Coletamos os resultados em uma nova lista.

**Casos de uso comuns:**
* **Convertendo tipos:** Converter um `List<Integer>` em um `List<String>`.
* **Aplicando cálculos:** Calcular o quadrado de cada número em uma lista.
* **Criando novos objetos:** Transformar uma lista de nomes em uma lista de objetos `Person`.
* **Extraindo informações:** Extrair um campo específico de uma lista de objetos.

**Exemplo mais complexo:**
```java
class Person {
    String name;
    int age;
    // ... construtores, getters e setters
}

List<Person> people = ...; // Uma lista de pessoas

List<String> upperCaseNames = people.stream()
                                   .map(Person::getName)
                                   .map(String::toUpperCase)
                                   .collect(Collectors.toList());
```
Neste exemplo, primeiro extraímos o nome de cada pessoa usando `map(Person::getName)`, depois convertemos os nomes para maiúsculas usando outro `map(String::toUpperCase)`.

**Encadeando operações:**
`map()` pode ser encadeado com outras operações intermediárias para criar pipelines complexos. Por exemplo:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<String> evenNumbersAsString = numbers.stream()
                                          .filter(n -> n % 2 == 0)
                                          .map(n -> "O número " + n + " é par")
                                          .collect(Collectors.toList());
```

**Considerações importantes:**
* **Lazy evaluation:** `map()` é uma operação intermediária, ou seja, a transformação só ocorre quando uma operação terminal é aplicada.
* **Funções puras:** A função passada para `map()` deve ser uma função pura, ou seja, ela não deve ter efeitos colaterais e o resultado deve depender apenas dos argumentos.
* **Performance:** Para grandes conjuntos de dados, é importante considerar o desempenho das operações dentro de `map()`.
---
## Obtendo um Stream de Elementos Distintos com Stream.distinct()
O método `distinct()` é uma ferramenta poderosa na API de Streams do Java, permitindo que você remova elementos duplicados de uma Stream, retornando apenas os elementos únicos.

### Como funciona o distinct()?
* **Comparação:** O método `distinct()` utiliza os métodos `equals()` e `hashCode()` para determinar se dois elementos são iguais. Se dois elementos forem considerados iguais de acordo com esses métodos, apenas um deles será incluído na Stream resultante.
* **Ordem:** A ordem dos elementos na Stream resultante não é necessariamente a mesma que a ordem na Stream original.
* **Estado interno:** `distinct()` é uma operação intermediária com estado, o que significa que ele mantém um conjunto interno para rastrear os elementos já vistos.

**Sintaxe:**
`{java}Stream<T> distinctStream = stream.distinct();`

#### Exemplo básico:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 2, 1, 4);

List<Integer> distinctNumbers = numbers.stream()
                                       .distinct()
                                       .collect(Collectors.toList());
```

### Personalizando a comparação:
Para personalizar a comparação de elementos, você pode fornecer um `Comparator` personalizado para o método `sorted()`, antes de aplicar o `distinct()`. Isso é útil quando você deseja considerar apenas certos atributos de um objeto para determinar a distinção.
```java
class Person {
    String name;
    int age;
    // ... construtores, getters e setters
}

List<Person> people = ...; // Uma lista de pessoas

List<Person> distinctByAge = people.stream()
                                  .sorted(Comparator.comparing(Person::getAge))
                                  .distinct()
                                  .collect(Collectors.toList());
```
Neste exemplo, os objetos `Person` serão considerados distintos apenas se suas idades forem diferentes.

### Considerações importantes:
* **Implementação de equals() e hashCode():** É fundamental que os objetos na sua Stream tenham implementações corretas de `equals()` e `hashCode()`. Caso contrário, o comportamento de `distinct()` pode ser imprevisível.
* **Performance:** Para grandes conjuntos de dados, o desempenho de `distinct()` pode ser afetado pela complexidade da implementação de `equals()` e `hashCode()`.
* **Ordem:** Se a ordem dos elementos distintos for importante, você pode combinar `distinct()` com `sorted()`.

### Quando usar distinct()?
* **Remover duplicatas:** Obter uma lista de elementos únicos a partir de uma lista com duplicatas.
* **Agrupamento:** Antes de agrupar elementos, você pode usar `distinct()` para garantir que cada grupo contenha apenas elementos distintos.
* **Otimização:** Em alguns casos, remover duplicatas antes de realizar outras operações pode melhorar o desempenho.
---
## Achatando um Stream com Stream.flatMap()
O método `flatMap()` é uma ferramenta poderosa na API de Streams do Java, especialmente quando você precisa lidar com estruturas de dados aninhadas. Ele permite que você "achate" um Stream de Streams em um único Stream. Imagine que você tem uma lista de listas e deseja obter uma única lista contendo todos os elementos dessas listas internas. O `flatMap()` é perfeito para essa tarefa.

**Como funciona o flatMap()?**
* **Transformação:** Ao invés de simplesmente aplicar uma função a cada elemento da Stream (como o `map()` faz), o `flatMap()` aplica uma função que retorna um Stream. 
* **Achatar:** Os Streams retornados por essa função são então "achatados" em um único Stream.

**Sintaxe:**
`{java}Stream<T> flatMappedStream = stream.flatMap(function);
* **stream:** A Stream original.
* **function:** Uma função que recebe um elemento do tipo `T` da Stream original e retorna um Stream.

**Exemplo:**
```java
List<List<String>> nestedLists = Arrays.asList(
        Arrays.asList("apple", "banana"),
        Arrays.asList("orange", "grape")
);

List<String> flattenedList = nestedLists.stream()
                                        .flatMap(List::stream)
                                        .collect(Collectors.toList());
```
Neste exemplo:
* Temos uma lista de listas de strings.
* Usamos `flatMap()` para transformar cada lista interna em um Stream e depois achatá-los em um único Stream.
* Coletamos os resultados em uma nova lista.

**Casos de uso comuns:**
* **Achatando listas aninhadas:** Transformar uma lista de listas em uma lista única.
* **Processando elementos de coleções dentro de objetos:** Extrair elementos de coleções dentro de objetos e processá-los individualmente.
* **Criando combinações:** Combinar elementos de diferentes Streams.

**Exemplo mais complexo:**
```java
class Person {
    String name;
    List<String> hobbies;
    // ... construtores, getters e setters
}

List<Person> people = ...; // Uma lista de pessoas

List<String> allHobbies = people.stream()
                               .flatMap(person -> person.getHobbies().stream())
                               .collect(Collectors.toList());
```
Neste exemplo, extraímos todos os hobbies de todas as pessoas e os colocamos em uma única lista.

**Comparando map() e flatMap():**
* **map():** Transforma cada elemento em outro elemento, mantendo a mesma estrutura.
* **flatMap():** Transforma cada elemento em um Stream e depois "achata" todos esses Streams em um único Stream.
---
## Especializações de Stream para Tipos Primitivos: Um Guia Completo
A API de Streams do Java oferece especializações para os tipos primitivos `int`, `long` e `double`, proporcionando otimizações e conveniências para trabalhar com grandes volumes de dados numéricos. Essas especializações são: `IntStream`, `LongStream` e `DoubleStream`, respectivamente.

### Por que usar as especializações?
* **Otimização de desempenho:** As operações sobre tipos primitivos são geralmente mais rápidas do que as operações sobre objetos wrappers (Integer, Long, Double).
* **Sintaxe mais concisa:** As especializações oferecem métodos específicos para operações comuns com números, como `sum()`, `average()`, `max()`, `min()`, etc.
* **Boxing/unboxing:** Evita a conversão constante entre tipos primitivos e seus wrappers.

### Criando Streams Especializadas
**A partir de coleções:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
IntStream intStream = numbers.stream().mapToInt(Integer::intValue);
```

**A partir de arrays:**
```java
int[] numbers = {1, 2, 3, 4, 5};
IntStream intStream = Arrays.stream(numbers);
```

**Gerando sequências:**
```java
IntStream intStream = IntStream.range(1, 10); // Valores de 1 a 9
IntStream intStream = IntStream.rangeClosed(1, 10); // Valores de 1 a 10
```

### Operações Comuns
* **Redução:** `sum()`, `average()`, `max()`, `min()`.
* **Mapeamento:** `mapToInt()`, `mapToLong()`, `mapToDouble()`.
* **Filtragem:** `filter()`.
* **Ordenação:** `sorted()`.

**Exemplo:**
```java
double average = numbers.stream()
                        .mapToInt(i -> i * i) // Elevar ao quadrado
                        .average()
                        .orElse(0.0);
```

### Quando Usar?
* **Grandes volumes de dados numéricos:** As especializações oferecem um desempenho significativamente melhor.
* **Operações matemáticas:** As especializações possuem métodos específicos para operações matemáticas.
* **Quando a precisão é crítica:** Evitar boxing/unboxing pode prevenir perda de precisão em cálculos.

### Comparando com Streams de Objetos

| Característica | Streams de Objetos | Streams Especializadas |
|---|---|---|
| Tipo de dados | Objetos | Tipos primitivos |
| Desempenho | Geralmente mais lento devido ao boxing/unboxing | Geralmente mais rápido |
| Sintaxe | Mais genérica | Mais específica para operações numéricas |
### Exemplo Completo: Calculando a média de números pares em um array
```java
int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8};

double averageOfEvenNumbers = Arrays.stream(numbers)
                                   .filter(n -> n % 2 == 0)
                                   .average()
                                   .orElse(0.0);
```
---
## Operações de Redução com Stream.reduce()
O método `reduce()` é uma das ferramentas mais poderosas na API de Streams do Java, permitindo que você reduza uma Stream a um único valor. Ele é essencial para realizar operações como somatório, produto, encontrar o máximo ou mínimo, e muitas outras.

### Como funciona o reduce()?
O `reduce()` funciona aplicando repetidamente uma operação binária a cada elemento da Stream, combinando-os gradualmente em um único resultado. Ele recebe dois argumentos:

* **Valor inicial:** O valor inicial do acumulador.
* **Operação binária:** Uma função que combina o valor atual do acumulador com o próximo elemento da Stream.

**Sintaxe:**
`{java}T result = stream.reduce(identity, accumulator);`
* `T`: O tipo do resultado.
* `identity`: O valor inicial do acumulador.
* `accumulator`: A função que combina o valor atual do acumulador com o próximo elemento.

### Exemplos
**Somando todos os elementos:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream().reduce(0, Integer::sum);
```

**Encontrando o maior valor:**
```java
Integer max = numbers.stream().reduce(Integer::max).orElse(null);
```

**Concatenando strings:**
```java
List<String> words = Arrays.asList("Hello", "world", "!");
String joined = words.stream().reduce("", (acc, word) -> acc + " " + word);
```

### Entendendo a operação binária
A operação binária é fundamental para o funcionamento do `reduce()`. Ela recebe dois argumentos:

* **Acumulador:** O valor atual do resultado parcial.
* **Próximo elemento:** O próximo elemento da Stream a ser processado.

A função deve retornar o novo valor do acumulador após combinar os dois argumentos.

### Usando o reduce() com um valor inicial opcional
O `reduce()` também pode ser usado sem um valor inicial. Nesse caso, o primeiro elemento da Stream será usado como valor inicial e a operação binária será aplicada a partir do segundo elemento. No entanto, se a Stream estiver vazia, uma `NoSuchElementException` será lançada.

`{java}Optional<Integer> max = numbers.stream().reduce(Integer::max);`

### Considerações importantes
* **Curto-circuito:** O `reduce()` pode ser otimizado para realizar um curto-circuito quando o resultado final já estiver determinado, evitando iterar sobre todos os elementos da Stream.
* **Paralelização:** O `reduce()` pode ser usado em Streams paralelas, mas é importante garantir que a operação binária seja associativa e não tenha efeitos colaterais.
* **Complexidade:** Operações complexas no `reduce()` podem afetar o desempenho.
---
## Reduzindo Streams de BigDecimal com reduce() e Funções de Combinação
O método `reduce()` é uma ferramenta versátil para realizar operações de redução em Streams. Quando trabalhamos com valores monetários ou números com alta precisão, o tipo `BigDecimal` é ideal para garantir a exatidão dos cálculos. Neste contexto, o `reduce()` permite realizar operações como somatório, produto e outras, preservando a precisão do `BigDecimal`.

### Entendendo a Função de Combinação
A função de combinação passada para o `reduce()` define como os elementos da Stream serão combinados para formar o resultado final. No caso do `BigDecimal`, a função de combinação geralmente envolve operações aritméticas como soma, subtração, multiplicação e divisão.

#### Exemplos
**Somando valores BigDecimal:**
```java
List<BigDecimal> valores = Arrays.asList(new BigDecimal("10.50"), new BigDecimal("25.30"), new BigDecimal("18.20"));
BigDecimal soma = valores.stream()
                         .reduce(BigDecimal.ZERO, BigDecimal::add);
```

**Multiplicando todos os valores:**
```java
BigDecimal produto = valores.stream()
                           .reduce(BigDecimal.ONE, BigDecimal::multiply);
```

**Encontrando o maior valor:**
```java
BigDecimal maiorValor = valores.stream()
                              .reduce(BigDecimal::max)
                              .orElse(BigDecimal.ZERO);
```

**Criando uma função de combinação personalizada:**
```java
BigDecimal aplicarDesconto(BigDecimal valor, BigDecimal desconto) {
    return valor.multiply(BigDecimal.ONE.subtract(desconto));
}

BigDecimal totalComDesconto = valores.stream()
                                    .reduce(BigDecimal.ZERO, (acc, valor) -> aplicarDesconto(valor, new BigDecimal("0.10")));
```

### Considerações Importantes
* **Precisão:** O `BigDecimal` garante uma precisão arbitrária, evitando os problemas de arredondamento que podem ocorrer com tipos como `double`.
* **Imutável:** O `BigDecimal` é imutável, o que significa que as operações de aritmética retornam novos objetos em vez de modificar os existentes. Isso garante a segurança e previsibilidade dos cálculos.
* **Performance:** Para grandes conjuntos de dados, é importante considerar a performance das operações com `BigDecimal`. Em alguns casos, pode ser necessário otimizar o código ou utilizar bibliotecas especializadas para cálculos com alta performance.

### Usos Práticos
* **Cálculos financeiros:** Cálculo de juros, impostos, valores totais de compras, etc.
* **Processamento de dados científicos:** Cálculos envolvendo números com alta precisão.
* **Qualquer situação que exija precisão numérica:** Sempre que a precisão for crítica, o `BigDecimal` é a melhor escolha.
---
## Operações de Redução que Retornam Optional
`Optional` é uma classe introduzida no Java 8 para representar um valor que pode estar presente ou não. É uma forma elegante de lidar com valores nulos, evitando o famoso `NullPointerException`. Quando usamos `reduce` em uma Stream que pode estar vazia, o resultado será um `Optional`. Isso nos permite verificar se um valor foi encontrado antes de tentar usá-lo.

**Por que usar Optional com reduce()?**
* **Prevenção de NullPointerExceptions:** Ao retornar um `Optional`, garantimos que não haverá erros de nulo se a Stream estiver vazia.
* **Tratamento de casos de borda:** Podemos definir comportamentos diferentes para quando um valor é encontrado ou não.
* **Código mais limpo e seguro:** O uso de `Optional` torna o código mais expressivo e menos propenso a erros.

**Exemplos:**
**Encontrando o maior valor em uma Stream:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
Optional<Integer> max = numbers.stream().reduce(Integer::max);

if (max.isPresent()) {
    System.out.println("O maior valor é: " + max.get());
} else {
    System.out.println("A lista está vazia.");
}
```

**Concatenando strings com um separador:**
```java
List<String> words = Arrays.asList("Hello", "world", "!");
String joined = words.stream()
                    .reduce((word1, word2) -> word1 + " " + word2)
                    .orElse("");
```

**Encontrando o primeiro elemento que satisfaz uma condição:**
```java
List<String> words = Arrays.asList("apple", "banana", "orange");
Optional<String> firstStartWithA = words.stream()
                                      .filter(word -> word.startsWith("a"))
                                      .findFirst();
```

**Métodos úteis de Optional:**
* **isPresent():** Retorna `true` se um valor estiver presente.
* **get():** Retorna o valor, lançando `NoSuchElementException` se não estiver presente.
* **orElse(T other):** Retorna o valor se estiver presente, caso contrário, retorna o valor fornecido.
* `orElseGet(Supplier<? extends T> other)`: Retorna o valor se estiver presente, caso contrário, retorna o resultado de um fornecedor.
* `ifPresent(Consumer<? super T> consumer)`: Executa uma ação se um valor estiver presente.
* `orElseThrow(Supplier<? extends X> exceptionSupplier)`: Lança uma exceção se um valor não estiver presente.

**Quando usar Optional:**
* **Métodos que podem retornar nenhum valor:** Como `findFirst()`, `findAny()`, `reduce()` sem valor inicial.
* **Valores opcionais em objetos:** Para representar campos que podem não ter um valor definido.
* **Retornando valores de métodos que podem falhar:** Em vez de lançar exceções para valores nulos.

**Boas práticas:**
* **Evite aninhar chamadas a `get()`:** Isso pode levar a `NullPointerExceptions` se o valor não estiver presente.
* **Use `orElse` ou `orElseGet` para fornecer valores padrão.**
* **Considere `ifPresent` para executar ações com o valor.**
* **Utilize `orElseThrow` para lançar exceções personalizadas.
* **Não abuse de `Optional`.** Use-o quando fizer sentido para representar a ausência de um valor.
---
## Operações de Redução Especiais: sum, average e count
Além do método `reduce()` genérico, a API de Streams do Java oferece métodos especializados para realizar operações comuns de redução, como `sum`, `average` e `count`. Esses métodos simplificam o código e, em alguns casos, podem oferecer um desempenho melhor.

**sum()**
* **Objetivo:** Calcular a soma de todos os elementos numéricos de uma Stream.
* **Retorno:** Um valor numérico do mesmo tipo dos elementos da Stream (int, long ou double).
* **Exemplo:**
  ```java
  List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
  int sum = numbers.stream().mapToInt(Integer::intValue).sum();
  ```

**average()**
* **Objetivo:** Calcular a média dos elementos numéricos de uma Stream.
* **Retorno:** Um valor opcional do tipo `OptionalDouble`.
  * `isPresent()`: Indica se a Stream não está vazia.
  * `getAsDouble()`: Retorna o valor da média.
* **Exemplo:**
  ```java
  double average = numbers.stream().mapToDouble(Integer::doubleValue).average().orElse(0.0);
  ```

**count()**
* **Objetivo:** Contar o número de elementos em uma Stream.
* **Retorno:** Um valor longo (long).
* **Exemplo:**
  `{java}long count = numbers.stream().count();`

**Por que usar métodos especializados?**
* **Simplicidade:** O código fica mais conciso e legível.
* **Desempenho:** Em alguns casos, os métodos especializados podem ser otimizados para um melhor desempenho.
* **Conveniência:** Métodos como `average()` e `count()` encapsulam cálculos comuns.

**Quando usar reduce()?**
* **Operações personalizadas:** Quando você precisa realizar uma operação de redução mais complexa que não está disponível como um método especializado.
* **Flexibilidade:** O `reduce()` permite definir a lógica de redução de forma arbitrária.

**Comparação entre reduce() e métodos especializados:**

| Característica | reduce() | sum(), average(), count() |
|---|---|---|
| Flexibilidade | Alta | Baixa |
| Desempenho | Pode variar | Geralmente otimizado |
| Facilidade de uso | Mais complexo | Mais simples |
**Exemplo completo: Calculando estatísticas de uma lista de números**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

IntSummaryStatistics stats = numbers.stream()
                                   .mapToInt(Integer::intValue)
                                   .summaryStatistics();

System.out.println("Count: " + stats.getCount());
System.out.println("Sum: " + stats.getSum());
System.out.println("Min: " + stats.getMin());
System.out.println("Max: " + stats.getMax());
System.out.println("Average: " + stats.getAverage());
```
---
## Operações de Redução Especiais: min e max
Além das operações de redução que vimos anteriormente, como `sum`, `average` e `count`, a API de Streams do Java oferece métodos específicos para encontrar o menor e o maior valor em uma Stream: `min` e `max`.

**min()**
* **Objetivo:** Encontrar o menor elemento em uma Stream, de acordo com uma determinada ordem natural ou um comparador personalizado.
* **Retorno:** Um `Optional` do tipo do elemento da Stream. Isso ocorre porque a Stream pode estar vazia.
* **Exemplo:**
```java
List<Integer> numbers = Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5);
Optional<Integer> min = numbers.stream().min(Integer::compareTo);

if (min.isPresent()) {
    System.out.println("O menor valor é: " + min.get());
} else {
    System.out.println("A lista está vazia.");
}
```

**max()**
* **Objetivo:** Encontrar o maior elemento em uma Stream, de acordo com uma determinada ordem natural ou um comparador personalizado.
* **Retorno:** Um `Optional` do tipo do elemento da Stream.
* **Exemplo:**
```java
String[] words = {"apple", "banana", "cherry", "date"};
Optional<String> max = Arrays.stream(words).max(Comparator.naturalOrder());

if (max.isPresent()) {
    System.out.println("A maior palavra é: " + max.get());
}
```

### Personalizando a comparação
Você pode personalizar a comparação usando um `Comparator`. Isso é útil quando você precisa encontrar o mínimo ou o máximo com base em um critério específico.
```java
class Pessoa {
    String nome;
    int idade;
    // ... construtores, getters e setters
}

// Comparando pessoas pela idade
Comparator<Pessoa> porIdade = Comparator.comparingInt(Pessoa::getIdade);

List<Pessoa> pessoas = ...;
Optional<Pessoa> pessoaMaisNova = pessoas.stream().min(porIdade);
```

### Por que usar min() e max()?
* **Simplicidade:** Esses métodos fornecem uma maneira concisa de encontrar o mínimo e o máximo.
* **Clareza:** O código fica mais legível ao usar métodos com nomes específicos.
* **Performance:** Em alguns casos, esses métodos podem ser otimizados para um melhor desempenho.

### Quando usar reduce()?
* **Operações mais complexas:** Se você precisar combinar o mínimo ou o máximo com outras operações, `reduce()` pode ser mais flexível.
* **Customizações avançadas:** Para personalizar completamente a lógica de comparação.
---
## Coletando Elementos do Stream em Lista com Stream.collect
O método `collect` é uma ferramenta poderosa na API de Streams do Java, permitindo que você transforme um Stream em uma coleção, como uma lista, conjunto ou mapa. Essa operação é conhecida como terminal, pois consome o Stream e produz um resultado final.

### Entendendo o Collectors
O `collect` funciona em conjunto com os `Collectors`, que são classes auxiliares que definem como os elementos do Stream devem ser agrupados. Os `Collectors` fornecem diversas formas de coletar os elementos, como:

* **toList():** Coleta os elementos em uma nova lista.
* **toSet():** Coleta os elementos em um novo conjunto, eliminando duplicatas.
* **toMap():** Coleta os elementos em um mapa, utilizando funções para mapear chaves e valores.
* **groupingBy():** Agrupa os elementos com base em uma função de classificação.
* **joining():** Concatena os elementos em uma única string, com um separador opcional.

#### Exemplos
#### Coletando em uma Lista
```java
List<String> palavras = Arrays.asList("java", "stream", "api");
List<String> listaMaiuscula = palavras.stream()
                                      .map(String::toUpperCase)
                                      .collect(Collectors.toList());
```

#### Coletando em um Conjunto
```java
Set<Integer> numeros = Arrays.asList(1, 2, 3, 2, 1).stream()
                                          .collect(Collectors.toSet());
```

#### Coletando em um Mapa
```java
List<Pessoa> pessoas = ...; // Uma lista de objetos Pessoa com nome e idade

Map<String, Integer> pessoasPorIdade = pessoas.stream()
                                              .collect(Collectors.toMap(
                                                  Pessoa::getNome,
                                                  Pessoa::getIdade
                                              ));
```

#### Agrupando Elementos
```java
List<Produto> produtos = ...; // Uma lista de objetos Produto com categoria

Map<String, List<Produto>> produtosPorCategoria = produtos.stream()
                                                        .collect(Collectors.groupingBy(Produto::getCategoria));
```

#### Concatenando Strings
```java
String joined = palavras.stream()
                        .collect(Collectors.joining(", "));
```

### Personalizando a Coleta
Você pode criar `Collectors` personalizados para realizar operações mais complexas. Para isso, use o método `of()` da classe `Collector`.

### Quando Usar collect()
* **Transformar Streams em coleções:** Quando você precisa armazenar os resultados de uma operação em uma estrutura de dados.
* **Agrupar elementos:** Para agrupar elementos com base em um critério específico.
* **Realizar operações de redução mais complexas:** Quando `reduce()` não é suficiente.

### Considerações
* **Performance:** A escolha do `Collector` pode afetar o desempenho. Para grandes conjuntos de dados, considere a complexidade das operações envolvidas.
* **Immutable:** A maioria dos `Collectors` retorna novas coleções imutáveis.
* **Flexibilidade:** Os `Collectors` são extremamente flexíveis e permitem realizar diversas transformações nos dados.
---
## Usando Coletores Padrão da Classe Collectors
A classe `Collectors` oferece uma variedade de coletores pré-construídos para realizar tarefas comuns de agregação e transformação em Streams. Esses coletores simplificam significativamente o processo de coleta de dados e a criação de novas coleções.

### Coletores mais comuns e suas funcionalidades:
* **toList():** Coleta os elementos do Stream em uma nova lista.
  ```java
  List<String> palavras = List.of("java", "stream", "api");
  List<String> listaMaiuscula = palavras.stream()
                                      .map(String::toUpperCase)
                                      .collect(Collectors.toList());
  ```

* **toSet():** Coleta os elementos em um novo conjunto, eliminando duplicatas.
  ```java
  Set<Integer> numeros = List.of(1, 2, 3, 2, 1).stream()
                                          .collect(Collectors.toSet());
  ```

* **toMap():** Coleta os elementos em um mapa, utilizando funções para mapear chaves e valores.
  ```java
  Map<String, Integer> pessoasPorIdade = pessoas.stream()
                                              .collect(Collectors.toMap(
                                                  Pessoa::getNome,
                                                  Pessoa::getIdade
                                              ));
  ```

* **groupingBy():** Agrupa os elementos com base em uma função de classificação.
  ```java
  Map<String, List<Produto>> produtosPorCategoria = produtos.stream()
                                                        .collect(Collectors.groupingBy(Produto::getCategoria));
  ```

* **joining():** Concatena os elementos em uma única string, com um separador opcional.
  ```java
  String joined = palavras.stream()
                        .collect(Collectors.joining(", "));
  ```

* **counting():** Conta o número de elementos no Stream.
  ```java
  long totalProdutos = produtos.stream().collect(Collectors.counting());
  ```
* **summingInt(), summingLong(), summingDouble():** Calcula a soma dos valores numéricos.
* **averagingInt(), averagingLong(), averagingDouble():** Calcula a média dos valores numéricos.
* **minBy(), maxBy():** Encontra o elemento mínimo ou máximo de acordo com um comparador.

### Personalizando Coletores
Para operações mais complexas, você pode criar coletores personalizados usando o método `of()` da classe `Collector`. Isso envolve definir:
* **Supplier:** Um fornecedor da coleção de saída.
* **Accumulator:** Uma função para acumular elementos na coleção.
* **Combiner:** Uma função para combinar duas coleções parciais (utilizado em operações paralelas).
* **Finisher:** Uma função opcional para realizar operações finais na coleção.

### Quando usar coletores padrão?
* **Operações comuns:** Para tarefas como coletar em listas, conjuntos, mapas, agrupar elementos, contar, somar, etc.
* **Código conciso:** Os coletores padrão tornam o código mais legível e conciso.
* **Desempenho:** Os coletores padrão são geralmente otimizados para um bom desempenho.

**Exemplo prático: Analisando dados de vendas**
```java
class Venda {
    String produto;
    double valor;
    // ... outros atributos
}

// Agrupando vendas por produto e calculando o valor total de cada grupo
Map<String, Double> valorTotalPorProduto = vendas.stream()
                                                .collect(Collectors.groupingBy(
                                                    Venda::getProduto,
                                                    Collectors.summingDouble(Venda::getValor)
                                                ));
```
---
## Usando Coletores de Listas Não-Modificáveis
Em muitas situações, é desejável criar listas imutáveis, ou seja, listas que não podem ser modificadas após sua criação. Isso promove uma programação mais segura e evita erros comuns causados por modificações acidentais. A API de Streams do Java oferece coletores específicos para criar listas imutáveis, garantindo a imutabilidade dos resultados.

**Collectors para Listas Imutáveis**
* **Collectors.toUnmodifiableList():**
  * Coleta os elementos do Stream em uma nova lista imutável.
  * Qualquer tentativa de modificar a lista resultante resultará em uma `UnsupportedOperationException`.

**Exemplo:**
```java
List<String> palavras = List.of("java", "stream", "api");
List<String> listaImutavel = palavras.stream()
                                      .map(String::toUpperCase)
                                      .collect(Collectors.toUnmodifiableList());

// Tentativa de adicionar um elemento (resultará em UnsupportedOperationException)
listaImutavel.add("novoElemento");
```

**Por que usar listas imutáveis?**
* **Segurança:** Evita modificações acidentais que podem levar a bugs difíceis de rastrear.
* **Concorrência:** Em ambientes multithread, listas imutáveis são mais seguras, pois não precisam de sincronização.
* **Clareza:** O código fica mais claro ao indicar explicitamente que uma lista não pode ser modificada.
* **Funcionalidade:** Listas imutáveis são um pilar da programação funcional, promovendo um estilo de programação mais declarativo.

**Quando usar Collectors.toUnmodifiableList()?**
* **Quando a imutabilidade é importante:** Em bibliotecas, frameworks ou partes do código onde a imutabilidade é um requisito fundamental.
* **Ao compartilhar dados entre threads:** Listas imutáveis podem ser compartilhadas entre threads sem a necessidade de sincronização.
* **Ao retornar resultados de métodos:** Retornar listas imutáveis evita que o chamador modifique o estado interno do objeto.

**Exemplo mais complexo: Agrupando elementos em listas imutáveis**
```java
Map<String, List<String>> palavrasPorTamanho = palavras.stream()
                                                      .collect(Collectors.groupingBy(
                                                          String::length,
                                                          Collectors.toUnmodifiableList()
                                                      ));
```

**Considerações:**
* **Performance:** Criar listas imutáveis pode ter um pequeno impacto no desempenho, especialmente para listas grandes, devido à criação de cópias defensivas.
* **Flexibilidade:** Se você precisar modificar a lista posteriormente, precisará criar uma nova lista mutável.
* **Compatibilidade:** Nem todas as APIs trabalham bem com listas imutáveis. Certifique-se de que a API que você está usando suporta listas imutáveis.
---
## Coletando Elementos do Stream em Mapas
O método `collect` da API de Streams do Java, em conjunto com o coletor `Collectors.toMap()`, permite transformar um Stream em um Map. Essa operação é extremamente útil quando você precisa agrupar elementos com base em uma chave e um valor, criando estruturas de dados mais complexas e significativas.

### Sintaxe básica do Collectors.toMap()
```java
Map<K, V> result = stream.collect(
    Collectors.toMap(keyMapper, valueMapper)
);
```
* **keyMapper:** Uma função que extrai a chave de cada elemento do Stream.
* **valueMapper:** Uma função que extrai o valor de cada elemento do Stream.

### Exemplo prático: Agrupando pessoas por idade
```java
class Pessoa {
    String nome;
    int idade;
    // ... outros atributos
}

Map<Integer, List<Pessoa>> pessoasPorIdade = pessoas.stream()
                                                  .collect(Collectors.groupingBy(
                                                      Pessoa::getIdade
                                                  ));
```
No exemplo acima, estamos agrupando uma lista de pessoas por idade, criando um mapa onde a chave é a idade e o valor é uma lista de pessoas com aquela idade.

### Personalizando o Mapa
Você pode personalizar ainda mais o mapa resultante usando a sobrecarga do `Collectors.toMap()` que aceita um terceiro argumento, uma função de merge. Essa função é utilizada para resolver colisões de chaves, ou seja, quando dois elementos do Stream geram a mesma chave.
```java
Map<String, Pessoa> primeiraPessoaPorNome = pessoas.stream()
                                                  .collect(Collectors.toMap(
                                                      Pessoa::getNome,
                                                      Function.identity(),
                                                      (p1, p2) -> p1 // Mantém a primeira pessoa encontrada
                                                  ));
```

### Outros Coletores Relacionados
* **groupingByConcurrent():** Similar ao `groupingBy()`, mas projeta para um resultado concorrente.
* **partitioningBy():** Particiona o Stream em dois grupos com base em um predicado.

### Usos comuns do Collectors.toMap()
* **Indexação:** Criar mapas onde a chave é um identificador único e o valor é o objeto completo.
* **Agrupamento:** Agrupar elementos por categorias ou atributos comuns.
* **Contagem:** Contar a frequência de elementos únicos.
* **Transformação:** Transformar um Stream em uma representação mais conveniente para outras operações.

### Considerações importantes
* **Chaves duplicadas:** Se dois elementos do Stream gerarem a mesma chave, o comportamento padrão é lançar uma `IllegalStateException`. Use a função de merge para definir como lidar com essas situações.
* **Performance:** A escolha da implementação do Map (HashMap, TreeMap, etc.) pode afetar o desempenho.
* **Imutabilidade:** Se você precisar de um mapa imutável, combine `Collectors.toMap()` com `Collectors.toUnmodifiableMap()`.

### Exemplo com mapa imutável e agrupamento por categoria
```java
Map<String, List<Produto>> produtosPorCategoriaImutavel = produtos.stream()
                                                                .collect(Collectors.groupingBy(
                                                                    Produto::getCategoria,
                                                                    Collectors.toUnmodifiableList()
                                                                ));
```
---
## Gerando Mapas Agrupados com Collectors.groupingBy
O coletor `Collectors.groupingBy()` é uma ferramenta poderosa na API de Streams do Java, permitindo agrupar elementos de um Stream com base em uma função de classificação, resultando em um mapa onde as chaves representam os grupos e os valores são coleções dos elementos que pertencem a cada grupo.

### Sintaxe básica
```java
Map<K, List<T>> result = stream.collect(
    Collectors.groupingBy(classifier)
);
```
* **classifier:** Uma função que extrai a chave de classificação (ou seja, o critério de agrupamento) de cada elemento.
* **result:** Um mapa onde as chaves são os valores retornados pela função `classifier` e os valores são listas dos elementos originais que mapearam para aquela chave.

### Exemplo: Agrupando pessoas por idade
```java
class Pessoa {
    String nome;
    int idade;
    // ... outros atributos
}

Map<Integer, List<Pessoa>> pessoasPorIdade = pessoas.stream()
                                                  .collect(Collectors.groupingBy(
                                                      Pessoa::getIdade
                                                  ));
```
Neste exemplo, o método `groupingBy()` agrupa a lista de pessoas por idade, criando um mapa onde as chaves são as idades e os valores são listas de pessoas com aquela idade.

### Personalizando o agrupamento
**1. Downstream collector:**
   Você pode aplicar outro coletor aos valores de cada grupo. Por exemplo, para calcular a média de idade em cada grupo:
   ```java
   Map<Integer, Double> mediaIdadePorGrupo = pessoas.stream()
                                                    .collect(Collectors.groupingBy(
                                                        Pessoa::getIdade,
                                                        Collectors.averagingInt(Pessoa::getIdade)
                                                    ));
   ```

**2. Função de merge:**
   Para lidar com chaves duplicadas, você pode fornecer uma função de merge:
   ```java
   Map<String, Pessoa> primeiraPessoaPorNome = pessoas.stream()
                                                      .collect(Collectors.toMap(
                                                          Pessoa::getNome,
                                                          Function.identity(),
                                                          (p1, p2) -> p1 // Mantém a primeira pessoa encontrada
                                                      ));
   ```

### Agrupamentos em múltiplos níveis
Você pode realizar agrupamentos em múltiplos níveis usando coletor `groupingBy` dentro de outro:
```java
Map<String, Map<Integer, List<Pessoa>>> pessoasPorCidadeEIdade = pessoas.stream()
                                                                     .collect(Collectors.groupingBy(
                                                                         Pessoa::getCidade,
                                                                         Collectors.groupingBy(Pessoa::getIdade)
                                                                     ));
```

### Outros coletores relacionados
* **partitioningBy():** Cria um mapa com duas chaves: true e false, dependendo do resultado de um predicado.
* **groupingByConcurrent():** Versão paralela do `groupingBy`, ideal para grandes conjuntos de dados.

### Quando usar groupingBy?
* **Análise de dados:** Agrupar dados para calcular estatísticas, criar relatórios ou visualizar informações.
* **Indexação:** Criar índices para facilitar a busca de elementos.
* **Organização:** Organizar dados em estruturas hierárquicas.

### Considerações
* **Performance:** A escolha da implementação do Map (HashMap, TreeMap, etc.) pode afetar o desempenho.
* **Imutabilidade:** Para criar mapas imutáveis, combine `groupingBy()` com `Collectors.toUnmodifiableMap()`.
* **Complexidade:** Agrupamentos complexos podem tornar o código menos legível. Use comentários e nomes de variáveis claros para melhorar a compreensão.
---
## Gerando Mapas Agrupados com Valores Agregados
O coletor `Collectors.groupingBy()` é extremamente poderoso quando combinado com outros coletores para realizar agregações nos grupos formados. Isso permite que você não apenas agrupe os dados, mas também calcule estatísticas, somas, médias e outras informações relevantes para cada grupo.

### Exemplo: Calculando a soma das vendas por produto
```java
class Venda {
    String produto;
    double valor;
}

Map<String, Double> valorTotalPorProduto = vendas.stream()
                                                .collect(Collectors.groupingBy(
                                                    Venda::getProduto,
                                                    Collectors.summingDouble(Venda::getValor)
                                                ));
```
Neste exemplo, estamos agrupando as vendas por produto e calculando o valor total de cada produto, utilizando o coletor `Collectors.summingDouble` para realizar a soma dos valores.

### Outros coletores para agregações
* **Collectors.averagingInt(), Collectors.averagingLong(), Collectors.averagingDouble():** Calculam a média dos valores numéricos.
* **Collectors.counting():** Conta o número de elementos em cada grupo.
* **Collectors.minBy(), Collectors.maxBy():** Encontram o elemento mínimo ou máximo em cada grupo, de acordo com um comparador.
* **Collectors.reducing():** Realiza uma redução mais genérica, permitindo aplicar funções personalizadas aos elementos de cada grupo.

### Agrupamentos em múltiplos níveis com agregações
```java
Map<String, Map<Integer, Double>> valorMedioPorCidadeEIdade = pessoas.stream()
                                                                     .collect(Collectors.groupingBy(
                                                                         Pessoa::getCidade,
                                                                         Collectors.groupingBy(Pessoa::getIdade,
                                                                                             Collectors.averagingDouble(Pessoa::getSalario)
                                                                         )
                                                                     ));
```
Neste exemplo, estamos agrupando as pessoas por cidade e idade, calculando a média salarial para cada grupo de idade em cada cidade.

### Personalizando as agregações
Você pode criar suas próprias funções de agregação usando o coletor `Collectors.reducing`. Por exemplo, para encontrar o produto com o maior valor em cada categoria:
```java
Map<String, Optional<Venda>> produtoMaisCaroPorCategoria = vendas.stream()
                                                               .collect(Collectors.groupingBy(
                                                                   Venda::getCategoria,
                                                                   Collectors.reducing(BinaryOperator.maxBy(Comparator.comparingDouble(Venda::getValor)))
                                                               ));
```

### Considerações importantes
* **Performance:** A escolha dos coletores e a complexidade das agregações podem afetar o desempenho.
* **Imutabilidade:** Os resultados são geralmente imutáveis, o que é desejável em muitos casos.
* **Clareza:** Use nomes de variáveis e comentários claros para tornar o código mais legível, especialmente em agrupamentos complexos.

### Quando usar agrupamentos com agregações?
* **Análise de dados:** Calcular estatísticas como soma, média, mínimo, máximo, contagem.
* **Relatórios:** Gerar relatórios resumidos com informações agregadas.
* **Otimização:** Identificar gargalos e oportunidades de melhoria.
---
## Gerando Mapas Particionados com Collectors.partitioningBy
O coletor `Collectors.partitioningBy()` é uma ferramenta poderosa na API de Streams do Java que permite particionar um Stream em dois grupos distintos com base em um predicado. O resultado é um mapa onde uma chave representa um grupo e a outra chave representa o outro grupo.

### Sintaxe básica
```java
Map<Boolean, List<T>> result = stream.collect(
    Collectors.partitioningBy(predicate)
);
```
* **predicate:** Um predicado que retorna `true` para os elementos que devem ser incluídos em um grupo e `false` para os outros.
* **result:** Um mapa onde a chave `true` contém os elementos que satisfazem o predicado e a chave `false` contém os demais.

### Exemplo: Separando números pares e ímpares
```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
Map<Boolean, List<Integer>> paresEImpares = numeros.stream()
                                                  .collect(Collectors.partitioningBy(n -> n % 2 == 0));
```
Neste exemplo, o predicado `n -> n % 2 == 0` verifica se um número é par. O mapa resultante terá duas chaves: `true` para os números pares e `false` para os números ímpares.

### Personalizando a partição
Você pode personalizar a partição utilizando um coletor downstream para cada grupo:
```java
Map<Boolean, Double> mediaParesEImpares = numeros.stream()
                                               .collect(Collectors.partitioningBy(
                                                   n -> n % 2 == 0,
                                                   Collectors.averagingInt(Integer::intValue)
                                               ));
```
Neste exemplo, estamos calculando a média dos números pares e ímpares.

### Usos comuns do Collectors.partitioningBy
* **Filtragem:** Separar elementos que satisfazem um determinado critério dos demais.
* **Validação:** Verificar se todos os elementos satisfazem uma condição.
* **Divisão em grupos:** Dividir dados em grupos distintos com base em um critério binário.

### Considerações importantes
* **Predicado:** A escolha do predicado é fundamental para determinar como os elementos serão particionados.
* **Coletores downstream:** Você pode aplicar diferentes coletores a cada grupo para realizar diversas operações.
* **Imutabilidade:** O mapa resultante é imutável.

### Quando usar partitioningBy?
* Quando você precisa dividir um Stream em dois grupos distintos com base em um critério simples.
* Quando você precisa realizar operações diferentes em cada grupo.
* Quando você precisa validar dados e verificar se todos os elementos satisfazem uma condição.

### Comparando partitioningBy com groupingBy
* **partitioningBy:** Cria exatamente dois grupos, baseados em um predicado booleano.
* **groupingBy:** Cria um número arbitrário de grupos, baseados em uma função de classificação.
---
## Outras Formas de Obter Instâncias de Stream
Além das coleções como `List`, `Set` e `Map`, existem diversas outras formas de obter instâncias de `Stream` em Java. Cada uma dessas formas se adapta a diferentes cenários e tipos de dados.

#### 1. Arrays:
* **Arrays.stream(array):** Converte um array em um Stream.
  ```java
  int[] numbers = {1, 2, 3};
  IntStream stream = Arrays.stream(numbers);
  ```

#### 2. Valores primitivos:
* **IntStream.range(start, end):** Cria um Stream de inteiros em um intervalo.
  ```java
  IntStream stream = IntStream.range(1, 10); // 1, 2, 3, ..., 9
  ```
* **DoubleStream.of(values):** Cria um Stream de valores double.
  ```java
  DoubleStream stream = DoubleStream.of(1.0, 2.5, 3.14);
  ```

#### 3. Arquivos:
* **Files.lines(path):** Lê as linhas de um arquivo em um Stream de Strings.
  ```java
  Path path = Paths.get("meu_arquivo.txt");
  Stream<String> lines = Files.lines(path);
  ```

#### 4. Geradores de números aleatórios:
* **Random.ints():** Gera um Stream de números inteiros aleatórios.
  ```java
  Random random = new Random();
  IntStream randomNumbers = random.ints(10, 1, 100); // 10 números entre 1 e 100
  ```

#### 5. Iteradores:
* **StreamSupport.stream(Spliterator, boolean):** Cria um Stream a partir de um Spliterator.
  ```java
  List<String> list = List.of("a", "b", "c");
  Spliterator<String> spliterator = list.spliterator();
  Stream<String> stream = StreamSupport.stream(spliterator, false);
  ```

#### 6. Funções geradoras:
* **Stream.generate():** Gera um Stream infinito de elementos a partir de uma função.
  ```java
  Stream<String> infiniteStream = Stream.generate(() -> "hello");
  ```
* **Stream.iterate():** Gera um Stream infinito de elementos aplicando uma função repetidamente a um valor inicial.
  ```java
  Stream<Integer> fibonacci = Stream.iterate(new int[]{0, 1}, t -> new int[]{t[1], t[0] + t[1]})
                                      .map(t -> t[0]);
  ```

#### 7. Outras fontes:
* **Bibliotecas externas:** Muitas bibliotecas oferecem funcionalidades específicas para criar Streams, como bibliotecas de parsing, bancos de dados e frameworks web.

### Quando usar cada forma?
* **Arrays:** Quando você já tem os dados em um array.
* **Valores primitivos:** Para gerar sequências numéricas ou trabalhar com valores numéricos aleatórios.
* **Arquivos:** Para processar dados de arquivos texto.
* **Geradores:** Para criar Streams infinitos ou gerar dados de forma dinâmica.
* **Iteradores:** Para trabalhar com estruturas de dados personalizadas que implementam a interface `Iterable`.
---
## Métodos `Objects.isNull` e `Objects.nonNull` com Streams
Os métodos `Objects.isNull` e `Objects.nonNull` são utilitários estáticos da classe `java.util.Objects` que servem para verificar se um objeto é nulo ou não nulo, respectivamente. Eles são especialmente úteis quando se trabalha com streams em Java 8 e versões posteriores.

**Por que usá-los com streams?**
* **Prevenção de NullPointerException:** Ao verificar a nulidade antes de realizar operações em um objeto, você evita a temida `NullPointerException`.
* **Código mais limpo:** Esses métodos tornam o código mais legível e conciso em comparação com verificações de nulidade manuais.
* **Integração com outras operações de stream:** Eles se encaixam perfeitamente em pipelines de streams, permitindo filtrar elementos com base em sua nulidade.

**Como utilizá-los?**
**1. Filtrando elementos nulos:**
```java
List<String> strings = Arrays.asList("maçã", null, "banana", null, "laranja");

List<String> stringsNulas = strings.stream()
                                  .filter(Objects::isNull)
                                  .collect(Collectors.toList());

System.out.println(stringsNulas); // Saída: [null, null]
```

**2. Filtrando elementos não nulos:**
```java
List<String> stringsNaoNulas = strings.stream()
                                    .filter(Objects::nonNull)
                                    .collect(Collectors.toList());

System.out.println(stringsNaoNulas); // Saída: [maçã, banana, laranja]
```

**3. Combinando com outras operações:**
```java
List<String> stringsNaoNulasENaoVazias = strings.stream()
                                              .filter(Objects::nonNull)
                                              .filter(s -> !s.isEmpty())
                                              .collect(Collectors.toList());

System.out.println(stringsNaoNulasENaoVazias); // Saída: [maçã, banana, laranja]
```

**Exemplo prático:**
Imagine que você tem uma lista de usuários e deseja filtrar aqueles que possuem um nome válido (não nulo e não vazio). Você poderia fazer isso da seguinte forma:
```java
List<Usuario> usuariosValidos = usuarios.stream()
                                       .filter(usuario -> Objects.nonNull(usuario.getNome()))
                                       .filter(usuario -> !usuario.getNome().isEmpty())
                                       .collect(Collectors.toList());
```
---
## Boas Práticas: Funções em Streams sem Efeito Colateral

**O que são efeitos colaterais em streams?**
Um efeito colateral em uma função dentro de um pipeline de stream ocorre quando a função modifica um estado externo à própria função. Isso pode incluir:

* **Modificação de variáveis externas:** Alterar o valor de uma variável fora do escopo da função.
* **Interação com recursos externos:** Acessar ou modificar bancos de dados, arquivos, redes, etc.
* **Chamadas a métodos que causam efeitos colaterais:** Usar métodos que não são puramente funcionais.

**Por que evitar efeitos colaterais em streams?**
* **Dificultam o raciocínio:** Efeitos colaterais tornam o código mais difícil de entender e depurar, pois o estado da aplicação pode mudar de forma inesperada.
* **Reduzem a testabilidade:** Funções com efeitos colaterais são mais difíceis de testar isoladamente, pois o resultado pode depender do estado externo.
* **Violam o paradigma funcional:** Streams são uma característica funcional do Java e, ao introduzir efeitos colaterais, você se afasta desse paradigma.

**Boas práticas para evitar efeitos colaterais:**
* **Funções puras:** As funções dentro de um pipeline de stream devem ser puras, ou seja, dado um mesmo input, sempre devem retornar o mesmo output e não devem modificar nenhum estado externo.
* **Imutar dados:** Evite modificar objetos existentes dentro do stream. Crie novos objetos com os valores desejados.
* **Usar métodos intermediários:** Utilize métodos como `map`, `filter`, `reduce`, etc., para transformar e filtrar dados de forma imutável.
* **Evitar side-effects em lambdas:** As expressões lambda dentro de um stream devem ser funções puras.
* **Preferir coletores:** Utilize coletores como `Collectors.toList()`, `Collectors.toMap()`, etc., para coletar os resultados do stream em novas coleções.

**Exemplo:**
```java
List<String> nomes = Arrays.asList("Ana", "Pedro", "Maria");

// Correto: função pura, cria uma nova lista com os nomes em maiúsculo
List<String> nomesMaiusculos = nomes.stream()
                                   .map(String::toUpperCase)
                                   .collect(Collectors.toList());

// Incorreto: efeito colateral, modifica a lista original
for (int i = 0; i < nomes.size(); i++) {
    nomes.set(i, nomes.get(i).toUpperCase());
}
```

**Benefícios de seguir essas práticas:**
* **Código mais limpo e conciso:** Funções puras são mais fáceis de entender e manter.
* **Maior confiabilidade:** A ausência de efeitos colaterais reduz a possibilidade de bugs.
* **Código mais testável:** Funções puras são mais fáceis de testar em isolamento.
* **Melhora a performance:** Em alguns casos, o uso de streams e funções puras pode levar a ganhos de performance.
---
