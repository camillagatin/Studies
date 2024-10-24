https://github.com/camillagatin/ganhando_produtividade_com_Stream_API_Java
## Implementando Expressões Lambda

**O que são Expressões Lambda?**
Em Java, expressões lambda são uma forma concisa de representar uma interface funcional. Uma interface funcional é uma interface que contém exatamente um método abstrato. As lambdas permitem você tratar código como um dado, tornando o código mais legível e conciso, especialmente quando se trabalha com coleções e streams.

**Sintaxe Básica**
Uma expressão lambda geralmente tem a seguinte forma:
`{java}(parâmetros) -> { corpo }`

- **Parâmetros:** A lista de parâmetros da função lambda.
- **->:** A seta lambda, separando os parâmetros do corpo.
- **Corpo:** O bloco de código que implementa a funcionalidade da lambda.

**Exemplo Simples:**
```java
(int x) -> {
    System.out.println("O valor de x é: " + x);
}
```

**Interfaces Funcionais**
Para utilizar lambdas, você precisa de uma interface funcional. Algumas interfaces funcionais comuns em Java são:
- **Runnable:** Representa uma tarefa que pode ser executada por uma thread.
- **Comparator:** Compara dois objetos.
- **Predicate:** Representa um predicado (uma função booleana).
- **Function:** Representa uma função que mapeia um valor para outro.

**Exemplo com Runnable:**
```java
Runnable r = () -> {
    System.out.println("Hello, world!");
};
new Thread(r).start();
```

**Exemplo com Listas e Lambdas:**
```java
List<String> nomes = Arrays.asList("Ana", "Pedro", "Carlos");
nomes.forEach(nome -> System.out.println(nome));
```

**Características Importantes:**
- **Inferência de Tipos:** O compilador geralmente consegue inferir os tipos dos parâmetros e do valor de retorno da lambda.
- **Corpo Curto:** Se o corpo da lambda tiver apenas uma expressão, as chaves e a palavra-chave `return` podem ser omitidas.
- **Referência a Métodos:** Você pode usar referências a métodos estáticos, de instância ou construtores para criar lambdas.

**Usos Comuns:**
- **Coleções:** Iterar sobre elementos, filtrar, mapear e reduzir.
- **Streams:** Processar dados de forma declarativa.
- **Eventos:** Lidar com eventos de interfaces gráficas e outros sistemas.
- **Threads:** Criar e gerenciar threads de forma mais concisa.

**Benefícios:**
- **Código mais conciso e legível:** As lambdas reduzem a quantidade de código boilerplate.
- **Programação funcional:** Permitem um estilo de programação mais funcional e declarativo.
- **Melhora a expressividade:** Facilitam a expressão de ideias complexas de forma mais clara.

**Quando Usar Lambdas:**
- **Expressões curtas:** Quando a lógica da função é simples e cabe em uma linha.
- **Interfaces funcionais:** Quando você está trabalhando com interfaces funcionais.
- **Coleções e streams:** Ao processar coleções de dados.
- **Eventos:** Ao lidar com eventos.
---
## Interfaces Funcionais

**O que são Interfaces Funcionais?**
Recapitulando, uma interface funcional em Java é aquela que possui **exatamente um método abstrato**. Essa característica específica a torna o candidato perfeito para ser implementada por expressões lambda, tornando o código mais conciso e expressivo.

**Por que Interfaces Funcionais são Importantes?**
- **Base para Lambdas:** Como já mencionado, são o pilar para a utilização de expressões lambda.
- **Padronização:** Fornecem um padrão para operações comuns, como filtrar, mapear, reduzir, etc.
- **Reutilização:** Podem ser reutilizadas em diversos contextos, promovendo a modularidade do código.
- **Integração com Streams:** São essenciais para trabalhar com streams em Java 8 e versões posteriores.

**Interfaces Funcionais Predefinidas:**
O Java oferece várias interfaces funcionais predefinidas no pacote `java.util.function`, como:
- **Predicate:** Representa um predicado (uma função booleana). Usado para filtrar elementos.
    `{java}Predicate<Integer> isEven = x -> x % 2 == 0;`
    
- **Function:** Representa uma função que mapeia um valor para outro. Usado para transformar elementos.
    `{java}Function<String, Integer> toLength = s -> s.length();`
    
- **Consumer:** Representa uma operação a ser realizada em um valor. Usado para consumir elementos.
    `{java}Consumer<String> print = System.out::println;`
    
- **Supplier:** Fornece um valor de um determinado tipo. Usado para gerar valores.
    `{java}Supplier<String> hello = () -> "Hello";`
    
- **Comparator:** Compara dois objetos. Usado para ordenar coleções.
    `{java}Comparator<Integer> compareAsc = Integer::compareTo;`
    

**Criando Interfaces Funcionais Personalizadas:**
Você também pode criar suas próprias interfaces funcionais para atender às suas necessidades específicas:
```java
@FunctionalInterface
interface MyFunction<T, R> {
    R apply(T t);
}
```

**Exemplo Prático: Filtrando e Somando Números Pares**
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class LambdaExample {
    public static void main(String[] args)    {
        List<Integer> numbers = Arrays.asList(1, 2,    3, 4, 5, 6, 7, 8);

        int sumOfEven = numbers.stream()
                .filter(n -> n % 2 == 0) // Filtra os números pares
                .mapToInt(Integer::intValue) // Converte para int
                .sum();

        System.out.println("Soma dos números pares: " + sumOfEven);
    }
}
```
---
## A Anotação @FunctionalInterface em Java
A anotação `@FunctionalInterface` em Java serve para indicar explicitamente que uma interface é funcional. **Uma interface funcional, como já vimos, é aquela que possui exatamente um método abstrato.**

**Por que usar a anotação @FunctionalInterface?**
- **Clareza e Autodocumentação:** Ao adicionar essa anotação, você comunica claramente aos outros desenvolvedores e ao compilador que a intenção é criar uma interface funcional.
- **Verificação do Compilador:** O compilador verifica se a interface realmente possui apenas um método abstrato. Caso haja mais de um ou nenhum, o compilador gerará um erro de compilação, evitando problemas em tempo de execução.
- **Suporte a Lambdas:** Garante que a interface possa ser usada com expressões lambda, facilitando a escrita de código conciso e funcional.

**Exemplo:**
```java
@FunctionalInterface
interface MyFunction<T, R> {
    R apply(T t);
}
```

**Quando usar a anotação @FunctionalInterface?**
- **Interfaces criadas para serem usadas com lambdas:** Sempre que você criar uma nova interface com a intenção de usá-la com expressões lambda, é altamente recomendado adicionar essa anotação.
- **Interfaces existentes:** Se uma interface já existente possui apenas um método abstrato, você pode adicionar a anotação para documentar essa característica e garantir que não sejam adicionados novos métodos abstratos no futuro.

**Importante:**
- **Não é obrigatória:** A anotação `@FunctionalInterface` não é obrigatória para que uma interface seja considerada funcional. O compilador pode inferir isso automaticamente. No entanto, é uma boa prática adicioná-la para maior clareza e segurança.
- **Métodos default e static:** Uma interface funcional pode ter métodos default e static, além do único método abstrato. Esses métodos não violam a regra de ter apenas um método abstrato, pois não são considerados métodos para implementação.

**Exemplo de uso:**
```java
@FunctionalInterface
interface Greeting {
    String greet(String name);

    // Método default
    default String farewell(String name) {
        return "Goodbye, " + name + "!";
    }
}

public class Main {
    public static void main(String[] args) {
        Greeting greeting = (name) -> "Hello, " + name + "!";
        System.out.println(greeting.greet("World"));
        System.out.println(greeting.farewell("World"));
    }
}
```
---
## Lambdas vs. Classes Anônimas: Por que Preferir Lambdas?
#### 1. Concisão:
- **Menos código:** Lambdas eliminam a necessidade de declarar uma classe inteira apenas para implementar um único método, reduzindo o ruído visual no código.
- **Sintaxe mais limpa:** A sintaxe das lambdas é mais direta e intuitiva, facilitando a leitura e escrita do código.

#### 2. Legibilidade:
- **Foco no comportamento:** Lambdas permitem focar diretamente no comportamento desejado, sem se preocupar com detalhes de implementação como construtores ou nomes de classes.
- **Alinhamento com estilo funcional:** A sintaxe das lambdas se alinha melhor com o estilo de programação funcional, que busca expressar intenções de forma clara e concisa.

#### 3. Integração com Streams:
- **Fluxo natural de dados:** Lambdas se encaixam perfeitamente com a API de Streams, permitindo criar pipelines de processamento de dados de forma fluente e expressiva.
- **Operações de alta ordem:** Lambdas são essenciais para aplicar operações de alta ordem como `map`, `filter`, `reduce`, etc., sobre streams.

#### 4. Inferência de tipos:

- **Menos código repetitivo:** O compilador geralmente consegue inferir os tipos dos parâmetros e do valor de retorno da lambda, eliminando a necessidade de especificá-los explicitamente.

##### Exemplo Comparativo:
```java
// Usando classe anônima
List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return s1.compareTo(s2);
    }
});

// Usando lambda
List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
names.sort((s1, s2) -> s1.compareTo(s2));
```

**Como você pode ver, a versão com lambda é mais concisa e legível.**

### Quando usar lambdas?
- **Interfaces funcionais:** Sempre que você tiver uma interface funcional, uma lambda é a escolha ideal.
- **Operações curtas:** Para expressões simples e concisas.
- **Com streams:** Ao trabalhar com a API de Streams.
- **Ao priorizar concisão e legibilidade:** Quando a clareza do código é fundamental.

### Limitações das lambdas
- **Complexidade:** Para lógica mais complexa, uma classe anônima ou uma classe separada pode ser mais adequada para manter a organização do código.
- **Estado:** Lambdas não têm estado próprio, o que pode limitar sua aplicabilidade em alguns cenários.
---
## Tornando Lambdas Mais Concisas
As lambdas são uma ferramenta poderosa para tornar o código Java mais expressivo e conciso. No entanto, para tirar o máximo proveito delas, é importante seguir algumas boas práticas que ajudem a manter o código limpo e legível.

#### 1. Inferência de Tipos:
- **Aproveite ao máximo:** O compilador Java é muito bom em inferir tipos. Evite declarar tipos explicitamente quando o compilador já consegue deduzi-los.
- **Exemplo:**
    ```java
    List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
    names.forEach(name -> System.out.println(name)); // O tipo de 'name' é inferido como String
    ```

#### 2. Expressões em Linha:
- **Seja conciso:** Quando o corpo da lambda consiste em uma única expressão, você pode omitir as chaves `{}` e a palavra-chave `return`.
- **Exemplo:**
    `{java}Function<Integer, Integer> square = x -> x * x;`

#### 3. Referência a Métodos:
- **Simplifique:** Utilize referências a métodos para representar lambdas que invocam um método existente.
- **Exemplo:**
    ```java
    List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
    names.sort(String::compareToIgnoreCase); // Em vez de: (s1, s2) -> s1.compareToIgnoreCase(s2)
    ```

#### 4. Métodos Default:
- **Reutilize:** Utilize métodos default em interfaces funcionais para encapsular lógica comum e evitar a repetição de código em lambdas.
- **Exemplo:**
    ```java
    @FunctionalInterface
    interface Greeting {
        String greet(String name);
    
        default String farewell(String name) {
            return "Goodbye, " + name + "!";
        }
    }
    ```

#### 5. Métodos Estáticos:
- **Compartilhamento:** Utilize métodos estáticos para encapsular lógica comum que pode ser compartilhada entre várias lambdas.
- **Exemplo:**
    ```java
    class Utils {
        public static int square(int x) {
            return x * x;
        }
    }
    // ...
    Function<Integer, Integer> square = Utils::square;
    ```

#### 6. Evite Código Duplicado:
- **Extraia para métodos:** Se uma parte do código de uma lambda é repetida em várias lambdas, extraia-a para um método separado.
- **Exemplo:**
    ```java
    private boolean isEven(int x) {
        return x % 2 == 0;
    }
    // ...
    List<Integer> evenNumbers = numbers.stream().filter(this::isEven).collect(Collectors.toList());
    ```

#### 7. Considere a Legibilidade:
- **Equilíbrio:** Embora a concisão seja importante, não sacrifique a legibilidade em prol dela. Se uma lambda se torna muito complexa, considere extrair a lógica para um método separado.

**Exemplo Completo:**
```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Function;

public class LambdaExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Filtrar números pares e elevar ao quadrado
        List<Integer> squaredEvenNumbers = numbers.stream()
                                                 .filter(n -> n % 2 == 0)
                                                 .map(n -> n * n)
                                                 .collect(Collectors.toList());

        // Imprimir cada número com uma mensagem personalizada
        numbers.forEach(n -> System.out.println("O número é: " + n));
    }
}
```

**Dicas Adicionais:**
- **Use nomes de variáveis significativos:** Mesmo em lambdas curtas, use nomes de variáveis que reflitam o propósito delas.
- **Formatação:** Utilize uma formatação consistente para melhorar a legibilidade do código.
- **Comentários:** Adicione comentários apenas quando necessário para explicar a lógica complexa.
---
## Implementando Comparator com Lambdas
Um `Comparator` é uma interface funcional que define uma ordem de comparação entre dois objetos. É frequentemente usado para ordenar coleções como listas ou conjuntos.

**Como usar Lambdas com Comparator**
A sintaxe básica para criar um `Comparator` usando uma lambda é:
```java
Comparator<Tipo> comparator = (objeto1, objeto2) -> {
    // Lógica de comparação
};
```

**Exemplo Prático: Ordenando uma Lista de Strings**
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class ComparatorExample    {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");   

        // Ordenando em ordem alfabética crescente
        Collections.sort(names, (s1, s2) -> s1.compareTo(s2));

        System.out.println(names);
    }
}
```
**Explicação:**
1. **Criamos uma lista de strings.**
2. **Usamos `Collections.sort`** para ordenar a lista.
3. **Passamos um `Comparator` como segundo argumento.**
4. **O `Comparator` é uma lambda** que compara dois strings usando o método `compareTo`.

**Ordenando em ordem alfabética decrescente:**
`{java}Collections.sort(names, (s1, s2) -> s2.compareTo(s1));`

**Ordenando por tamanho da string:**
`{java}Collections.sort(names, (s1, s2) -> s1.length() - s2.length());`

**Ordenando por critérios personalizados:**
Você pode criar `Comparators` mais complexos para ordenar objetos com base em critérios personalizados. Por exemplo, para ordenar uma lista de pessoas por idade e depois pelo nome:
```java
class Person {
    String name;
    int age;

    // ... getters e setters
}

// ...

Collections.sort(people, (p1, p2) -> {
    int ageComparison = p1.getAge() - p2.getAge();
    if (ageComparison != 0) {
        return ageComparison;
    } else {
        return p1.getName().compareTo(p2.getName());
    }
});
```

**Vantagens de usar Lambdas com Comparator:**
- **Mais conciso:** Lambdas permitem escrever `Comparators` de forma mais concisa.
- **Mais legível:** A sintaxe das lambdas é geralmente mais fácil de entender do que a de classes anônimas.
- **Integração com Streams:** Lambdas são essenciais para trabalhar com streams e operações como `sorted`.
---
## Prefira Interfaces Funcionais Padrão
São aquelas que possuem exatamente um método abstrato e podem ser usadas com expressões lambda. O pacote `java.util.function` fornece uma série dessas interfaces, como `Predicate`, `Function`, `Consumer`, `Supplier`, `Comparator`, entre outras.

**Por que preferi-las?**
1. **Reutilização:** Ao utilizar interfaces funcionais padrão, você se beneficia de uma API amplamente utilizada e bem testada, evitando a reimplementação de funcionalidades comuns.
2. **Legibilidade:** O uso de interfaces com nomes claros e intuitivos, como `Predicate` para representar um predicado ou `Function` para representar uma função, torna o código mais fácil de entender.
3. **Interoperabilidade:** Ao adotar interfaces padrão, você facilita a integração com outras bibliotecas e frameworks que também utilizam essas interfaces.
4. **Convenção:** O uso de interfaces padrão estabelece uma convenção comum na comunidade Java, tornando o código mais consistente e familiar para outros desenvolvedores.

**Quando criar interfaces funcionais personalizadas?**
Apesar dos benefícios das interfaces padrão, existem situações em que criar uma interface funcional personalizada pode ser necessário:

- **Especificidade:** Quando a funcionalidade requerida não se encaixa perfeitamente em nenhuma das interfaces padrão.
- **Domínio específico:** Ao modelar conceitos específicos de um domínio, uma interface personalizada pode fornecer um nível de abstração mais adequado.
- **Métodos default:** Se você precisar adicionar métodos default específicos à interface.

**Exemplo:**
```java
import java.util.function.Function;

public class Example {
    public static void main(String[] args) {
        Function<String, Integer> toLength = s -> s.length();
        int length = toLength.apply("Hello");
        System.out.println(length);
    }
}
```
Neste exemplo, a interface `Function` é utilizada para representar uma função que transforma uma string em um inteiro (seu comprimento).

**Outras considerações:**
- **Métodos default:** As interfaces funcionais padrão podem ter métodos default, que fornecem implementações padrão para métodos comuns. Isso pode ser útil para adicionar funcionalidades adicionais sem quebrar a compatibilidade com implementações existentes.
- **Sobrecargas:** Evite criar muitas sobrecargas de métodos que aceitam diferentes interfaces funcionais na mesma posição de argumento, pois isso pode levar a ambiguidades.
---
## As 4 Principais Interfaces Funcionais em Java
As interfaces funcionais são um dos pilares da programação funcional, permitindo a criação de código mais conciso e expressivo. Entre as diversas interfaces funcionais disponíveis no pacote `java.util.function`, destacam-se as seguintes:

#### 1. `Predicate<T>`
- **Propósito:** Representa um predicado (uma função booleana).
- **Método principal:** `boolean test(T t)`
- **Uso:** Utilizado para filtrar elementos em uma coleção com base em uma condição.
- **Exemplo:**
```java
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    List<Integer> evenNumbers = numbers.stream()
                                       .filter(n -> n % 2 == 0)
                                       .collect(Collectors.toList());
```

#### 2. `Function<T, R>`
- **Propósito:** Representa uma função que mapeia um valor de um tipo para outro.
- **Método principal:** `R apply(T t)`
- **Uso:** Utilizado para transformar elementos em uma coleção.
- **Exemplo:**
    ```java
    List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
    List<Integer> lengths = names.stream()
                                  .map(String::length)
                                  .collect(Collectors.toList());
    ```

#### 3. `Consumer<T>`
- **Propósito:** Representa uma operação a ser realizada em um valor.
- **Método principal:** `void accept(T t)`
- **Uso:** Utilizado para consumir elementos de uma coleção, como imprimir na tela ou salvar em um arquivo.
- **Exemplo:**
    ```java
    List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
    names.forEach(System.out::println);
    ```

#### 4. `Supplier<T>`
- **Propósito:** Fornece um valor de um determinado tipo.
- **Método principal:** `T get()`
- **Uso:** Utilizado para gerar valores, como números aleatórios ou objetos.
- **Exemplo:**
    ```java
    Supplier<String> helloSupplier = () -> "Hello";
    String greeting = helloSupplier.get();
    ```

**Resumo das principais interfaces funcionais:**

|Interface|Método principal|Descrição|
|---|---|---|
|Predicate<T>|boolean test(T t)|Verifica se um elemento satisfaz uma condição.|
|Function<T, R>|R apply(T t)|Mapeia um valor de um tipo para outro.|
|Consumer<T>|void accept(T t)|Consome um valor, realizando uma ação.|
|Supplier<T>|T get()|Fornece um valor.|
**Por que essas interfaces são importantes?**
- **Concisão:** Permitem escrever código mais conciso e expressivo.
- **Flexibilidade:** Podem ser combinadas de diversas formas para criar comportamentos complexos.
- **Integração com Streams:** São fundamentais para trabalhar com a API de Streams em Java 8 e versões posteriores.

**Outras interfaces importantes:**
Além dessas quatro, existem outras interfaces funcionais úteis, como:

- **`Comparator<T>`:** Compara dois objetos.
- **`BinaryOperator<T>`:** Combina dois valores do mesmo tipo.
- **`UnaryOperator<T>`:** Aplica uma operação a um único valor.
---
## A Interface Funcional Predicate e a Remoção de Elementos em Coleções
A interface funcional `Predicate` é uma ferramenta poderosa em Java 8 e versões posteriores, especialmente quando se trata de manipular coleções. Ela permite definir uma condição que será utilizada para filtrar elementos de uma coleção. Em conjunto com o método `removeIf` das coleções, o `Predicate` se torna uma ferramenta essencial para remover elementos que não satisfazem um determinado critério.

### O que é um Predicate?
Um `Predicate` representa uma função booleana que recebe um argumento e retorna um valor booleano. Em outras palavras, ele define uma condição que pode ser verdadeira ou falsa para um determinado elemento.

### Como usar Predicate para remover elementos?
O método `removeIf` das coleções (como `List` e `Set`) recebe um `Predicate` como argumento. Ele itera sobre todos os elementos da coleção e remove aqueles para os quais o `Predicate` retorna `true`.

**Exemplo:**
```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class PredicateExample {
    public static    void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);
        numbers.add(4);
        numbers.add(5);   

        // Remover todos os números pares
        Predicate<Integer> isEven = number -> number % 2 == 0;
        numbers.removeIf(isEven);

        System.out.println(numbers); // Imprime: [1, 3, 5]
    }
}
```
**Explicação:**
1. **Criamos uma lista de números.**
2. **Definimos um Predicate `isEven`:** Ele retorna `true` se o número for par.
3. **Usamos `removeIf`:** O método itera sobre a lista e remove todos os elementos para os quais `isEven` retorna `true`.

### Mais exemplos de uso
- **Remover elementos nulos:**
```java
List<String> names = Arrays.asList("Ana", null, "Carlos");
names.removeIf(Objects::isNull);
```

- **Remover elementos com base em um atributo:**
```java
class Person {
    String name;
    int age;
    // ...
}

List<Person> people = ...;
people.removeIf(person -> person.getAge() < 18);
```

### Vantagens de usar Predicate
- **Concisão:** A sintaxe das lambdas torna o código mais conciso e legível.
- **Flexibilidade:** Permite criar condições complexas de filtragem.
- **Integração com Streams:** `Predicate` é amplamente utilizado em operações de streams para filtrar elementos.

### Considerações importantes
- **Modificação da coleção:** O método `removeIf` modifica a coleção original. Se você precisar manter a coleção original, crie uma cópia antes de aplicar a remoção.
- **Performance:** Para grandes coleções, o uso de `removeIf` pode ser mais eficiente do que iterar manualmente e remover elementos.
- **Concorrência:** Se a coleção está sendo modificada por múltiplas threads, a remoção de elementos pode levar a problemas de concorrência. Utilize mecanismos de sincronização adequados.
---
## Interface Funcional Consumer: Iterando em Coleções com forEach
A interface funcional `Consumer` em Java 8 e versões posteriores é ideal para realizar ações em cada elemento de uma coleção. Em conjunto com o método `forEach`, ela oferece uma forma concisa e elegante de iterar e processar elementos.

### O que é um Consumer?
Um `Consumer` representa uma operação a ser realizada em um valor. Em outras palavras, ele "consome" um elemento. O método principal de um `Consumer` é `accept(T t)`, onde `T` é o tipo do elemento que será consumido.

### Como usar Consumer com forEach?
O método `forEach` de uma coleção recebe um `Consumer` como argumento. Para cada elemento da coleção, o `Consumer` é chamado com esse elemento como parâmetro, permitindo que você execute qualquer ação desejada.

**Exemplo:**
```java
import java.util.List;
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        List<String>    names = List.of("Ana", "Pedro", "Carlos");

        // Imprimindo cada nome
        Consumer<String> printName = name -> System.out.println(name);
        names.forEach(printName);
    }
}
```
**Explicação:**
1. **Criamos uma lista de nomes.**
2. **Definimos um Consumer `printName`:** Ele imprime o nome recebido.
3. **Usamos `forEach`:** Para cada nome na lista, o `Consumer` `printName` é chamado.

### Mais exemplos de uso
- **Modificando elementos:**
```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5);
Consumer<Integer> increment = number -> number++; // Não modifica a lista original, pois Integer é imutável
```

- **Operações mais complexas:**
```java
List<Person> people = ...;
Consumer<Person> printInfo = person -> System.out.println("Nome: " + person.getName() + ", Idade: " + person.getAge());
```

### Vantagens de usar Consumer
- **Concisão:** A sintaxe das lambdas torna o código mais conciso e legível.
- **Flexibilidade:** Permite realizar diversas ações em cada elemento, como imprimir, modificar, salvar em um arquivo, etc.
- **Integração com Streams:** `Consumer` pode ser usado em operações de streams como `forEach`, `peek`, etc.

### Considerações importantes
- **Impossibilidade de remover elementos:** O `Consumer` é projetado para consumir elementos, não para removê-los. Para remover elementos, utilize `removeIf` com um `Predicate`.
- **Efeito colateral:** O `Consumer` pode ter efeitos colaterais, como modificar variáveis externas ou realizar operações de entrada/saída. Use com cuidado para evitar efeitos indesejados.

### Comparação com for tradicional
```java
// Usando for tradicional
for (String name : names) {
    System.out.println(name);
}

// Usando forEach e Consumer
names.forEach(name -> System.out.println(name));
```
Ambas as formas fazem a mesma coisa, mas o `forEach` com `Consumer` é geralmente considerado mais conciso e elegante, especialmente quando combinado com outras features funcionais do Java.

---
## Interface Funcional Function: Ordenando Listas com Comparator.comparing
A interface funcional `Function` é uma ferramenta versátil em Java 8 e versões posteriores, permitindo mapear um valor de um tipo para outro. Em conjunto com o método `Comparator.comparing`, ela pode ser usada para ordenar listas de objetos com base em um atributo específico.

### O que é um Function?
Um `Function` representa uma função que recebe um argumento de um tipo e retorna um resultado de outro tipo. O método principal de um `Function` é `apply(T t)`, onde `T` é o tipo do argumento e `R` é o tipo do resultado.

### Como usar Function com Comparator.comparing?
O método `Comparator.comparing` recebe um `Function` como argumento. Ele cria um `Comparator` que compara dois objetos com base no resultado da função aplicada a cada objeto.

**Exemplo:**
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.function.Function;

class Person {
    String name;
    int age;

    // ... getters e setters
}

public class FunctionExample {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
            new Person("Alice", 25),
            new Person("Bob", 30),
            new Person("Charlie", 20)   
        );

        // Ordenando por idade crescente
        Function<Person, Integer> getAge = Person::getAge;
        people.sort(Comparator.comparing(getAge));

        System.out.println(people);
    }
}
```
**Explicação:**
1. **Criamos uma lista de pessoas.**
2. **Definimos uma Function `getAge`:** Ela extrai a idade de uma pessoa.
3. **Usamos `Comparator.comparing`:** Ele cria um `Comparator` que compara pessoas com base na idade.
4. **Ordenamos a lista:** O método `sort` ordena a lista usando o `Comparator` criado.

### Mais exemplos de uso
- **Ordenando por nome:**
```java
Function<Person, String> getName = Person::getName;
people.sort(Comparator.comparing(getName));
```

- **Ordenando por múltiplos atributos:**
`{java}people.sort(Comparator.comparing(Person::getAge).thenComparing(Person::getName));`

### Vantagens de usar Function com Comparator.comparing
- **Concisão:** A sintaxe das lambdas torna o código mais conciso e legível.
- **Flexibilidade:** Permite ordenar por qualquer atributo de um objeto.
- **Integração com Streams:** Pode ser usado em operações de streams como `sorted`.

### Considerações importantes
- **Ordem de comparação:** O `Comparator` criado por `Comparator.comparing` compara os resultados da função em ordem natural. Para alterar a ordem, use `Comparator.comparing(Function, Comparator)`.
- **NullPointerException:** Se a função aplicada a um objeto retornar `null`, uma `NullPointerException` será lançada. Certifique-se de tratar casos de `null` adequadamente.
---
## Usando Referências de Método
Referências de método são uma forma concisa de representar uma referência a um método existente. Elas são uma sintaxe especial que permite passar um método como um argumento para outro método, sem a necessidade de escrever uma expressão lambda completa.

**Quando usar Referências de Método?**
- **Quando a lambda é simplesmente uma chamada a um método existente:** Em vez de criar uma lambda para chamar um método, você pode usar uma referência de método diretamente.
- **Para melhorar a legibilidade do código:** Referências de método podem tornar o código mais conciso e fácil de entender.
- **Ao trabalhar com interfaces funcionais:** Referências de método são frequentemente usadas com interfaces funcionais como `Function`, `Consumer`, `Predicate` e `Comparator`.

**Sintaxe:**
- **Método de instância:** `Objeto::método`
- **Método estático:** `Classe::método`
- **Construtor:** `Classe::new`

**Exemplo:**
```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Function;

class Person {
    String name;
    int age;

    // ... getters e setters
}

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
            new Person("Alice", 25),
            new Person("Bob", 30),
            new Person("Charlie", 20)   
        );

        // Ordenando por nome usando referência de método
        people.sort(Comparator.comparing(Person::getName));
    }
}
```
Neste exemplo:
- `Person::getName` é uma referência de método que aponta para o método `getName` da classe `Person`.
- `Comparator.comparing` recebe essa referência como argumento, criando um `Comparator` que ordena os objetos `Person` com base no resultado do método `getName`.

**Outros exemplos:**
- **Imprimindo uma lista usando `forEach` e uma referência de método:**
    ```java
    List<String> names = Arrays.asList("Ana", "Pedro", "Carlos");
    names.forEach(System.out::println); // System.out::println é uma referência de método estático
    ```

- **Criando uma lista de números a partir de uma lista de strings usando `map` e uma referência de método:**
    ```java
    List<String> numbersAsString = Arrays.asList("1", "2", "3");
    List<Integer> numbers = numbersAsString.stream()
                                          .map(Integer::parseInt)
                                          .collect(Collectors.toList());
    ```    

**Benefícios de usar Referências de Método:**
- **Melhora a legibilidade:** O código fica mais conciso e fácil de entender.
- **Evita código repetitivo:** Elimina a necessidade de escrever lambdas simples.
- **Aumenta a reutilização de código:** Permite reutilizar métodos existentes de forma mais flexível.

**Quando não usar Referências de Método:**
- **Quando a lógica da lambda é muito complexa:** Para lógica mais complexa, uma lambda completa pode ser mais clara.
- **Quando a lambda captura variáveis externas:** Referências de método não podem capturar variáveis externas.
---
## Referenciando Métodos de uma Instância Particular
As referências de método oferecem uma forma concisa de representar um método como um argumento. Isso é particularmente útil quando trabalhamos com interfaces funcionais e queremos passar um comportamento como um parâmetro. Um dos tipos de referências de método é a referência a um método de uma instância particular.

**Sintaxe:**
`{java}objeto::método`

**Exemplo:**
Imagine que temos uma classe `Pessoa` com um método `getNome()`:
```java
class Pessoa {
    private String nome;

    // ... construtores e outros métodos

    public String getNome() {
        return nome;
    }
}
```
E queremos criar uma lista de nomes a partir de uma lista de pessoas:
```java
List<Pessoa> pessoas = ...;
List<String> nomes = pessoas.stream()
                            .map(Pessoa::getNome)
                            .collect(Collectors.toList());
```
Nesse exemplo, `Pessoa::getNome` é uma referência ao método `getNome` de uma instância da classe `Pessoa`. O `map` aplica essa função a cada elemento da lista, extraindo o nome de cada pessoa e colocando-o na nova lista.

**Como funciona:**
- **Objeto:** O objeto à esquerda do `::` é a instância específica cujo método será chamado.
- **Método:** À direita do `::` está o nome do método.
- **Contexto:** O contexto em que a referência de método é usada determina o tipo do objeto e os parâmetros do método.

**Outro exemplo, usando `Consumer`:**
```java
Pessoa pessoa = new Pessoa("João");
Consumer<Pessoa> imprimirNome = pessoa::imprimirNome;
imprimirNome.accept(pessoa);
```

Neste caso, `pessoa::imprimirNome` é uma referência ao método `imprimirNome` da instância específica `pessoa`.

**Vantagens de usar referências de método:**
- **Código mais conciso e legível:** Elimina a necessidade de escrever lambdas simples.
- **Melhora a reutilização de código:** Permite reutilizar métodos existentes de forma mais flexível.
- **Aumenta a expressividade do código:** Torna o código mais declarativo e fácil de entender.

**Quando usar referências de método de instância:**
- Quando a lógica da lambda é simplesmente uma chamada a um método existente de um objeto específico.
- Quando você quer passar um comportamento como um parâmetro para outro método.
- Para melhorar a legibilidade do código, especialmente quando o método é curto e simples.
---
## Referenciando Métodos Estáticos
Assim como podemos referenciar métodos de instâncias, também podemos referenciar métodos estáticos em Java. Uma referência a um método estático é uma forma concisa de representar um método que não pertence a uma instância específica, mas sim à classe como um todo.

**Sintaxe:**
`{java}Classe::método`

**Exemplo:**
Considere uma classe `Util` com um método estático `somar`:
```java
class Util {
    public static int somar(int a, int b) {
        return a + b;
    }
}
```
Podemos criar uma referência a esse método da seguinte forma:
`{java}Function<Integer, Function<Integer, Integer>> somar = Util::somar;`

Aqui, criamos uma função de alta ordem `somar` que recebe um inteiro e retorna outra função que também recebe um inteiro e retorna um inteiro. Essa função interna é a implementação do método `somar` da classe `Util`.

**Quando usar referências de métodos estáticos?**
- **Métodos utilitários:** Quando temos métodos estáticos que realizam operações gerais e não dependem de um estado específico de um objeto.
- **Funções puras:** Para funções que sempre retornam o mesmo resultado para os mesmos argumentos, sem efeitos colaterais.
- **Métodos de fábrica:** Para criar objetos de uma classe sem a necessidade de um construtor.

**Exemplo prático:**
```java
List<String> nomes = List.of("Ana", "Pedro", "Carlos");
nomes.forEach(System.out::println);
```
Neste exemplo, `System.out::println` é uma referência ao método estático `println` da classe `System`.

**Vantagens de usar referências de métodos estáticos:**
- **Código mais conciso:** Evita a necessidade de escrever lambdas simples.
- **Melhora a legibilidade:** Torna o código mais declarativo e fácil de entender.
- **Aumenta a reutilização de código:** Permite reutilizar métodos estáticos de forma mais flexível.

**Comparando com referências de métodos de instância:**

|Característica|Referência de método de instância|Referência de método estático|
|---|---|---|
|Objeto|Necessário|Não necessário|
|Contexto|Método pertence a uma instância específica|Método pertence à classe|
|Sintaxe|objeto::método|Classe::método|

---
## Referenciando Construtores
Uma referência a um construtor é uma forma concisa de representar a criação de um novo objeto. Em outras palavras, é uma maneira de indicar que queremos criar uma nova instância de uma classe.

**Sintaxe:**
`{java}Classe::new`

**Exemplo:**
Imagine que temos uma classe `Pessoa` com um construtor que recebe um nome:
```java
class Pessoa {
    private String nome;

    public Pessoa(String nome) {
        this.nome = nome;
    }
}
```
Podemos criar uma lista de pessoas usando uma referência ao construtor:
```java
List<Pessoa> pessoas = List.of("Ana", "Pedro", "Carlos")
                            .stream()
                            .map(Pessoa::new)
                            .collect(Collectors.toList());
```
Nesse exemplo, `Pessoa::new` é uma referência ao construtor da classe `Pessoa`. O `map` aplica essa referência a cada elemento da lista de nomes, criando uma nova instância de `Pessoa` para cada nome.

**Quando usar referências a construtores?**
- **Criando objetos de forma dinâmica:** Quando a classe de um objeto a ser criado é determinada em tempo de execução.
- **Passando construtores como parâmetros:** Quando um método espera um objeto como parâmetro e você quer que o objeto seja criado no momento da chamada.
- **Simplificando o código:** Quando a criação de objetos é uma parte comum do seu código, as referências a construtores podem tornar o código mais conciso.

**Exemplo prático:**
```java
Function<String, Pessoa> criarPessoa = Pessoa::new;
Pessoa pessoa = criarPessoa.apply("João");
```
Neste exemplo, `criarPessoa` é uma função que recebe uma string e retorna uma instância de `Pessoa`.

**Vantagens de usar referências a construtores:**
- **Código mais conciso:** Evita a necessidade de escrever lambdas simples.
- **Melhora a legibilidade:** Torna o código mais declarativo e fácil de entender.
- **Aumenta a reutilização de código:** Permite reutilizar construtores de forma mais flexível.
---