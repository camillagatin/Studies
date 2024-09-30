## Como Evitar NullPointerException em Java: Abordagens Tradicionais

O **NullPointerException (NPE)** é um dos erros mais comuns em Java e ocorre quando tentamos acessar um método ou atributo de um objeto que é nulo. Embora existam técnicas mais modernas para lidar com esse problema, as abordagens tradicionais ainda são amplamente utilizadas e compreendê-las é fundamental para escrever código mais robusto.

#### 1. Verificações Explícitas:
- **Antes de cada acesso:** A forma mais básica é verificar explicitamente se um objeto é nulo antes de utilizá-lo:
    ```java
    if (objeto != null) {
        // Use o objeto aqui
        String nome = objeto.getNome();
    } else {
        // Lidar com o caso em que o objeto é nulo
        System.out.println("Objeto é nulo");
    }
    ```

- **Operador ternário:** Uma sintaxe mais concisa para a mesma verificação:
    `{java}String nome = objeto != null ? objeto.getNome() : "Nome não disponível";`


#### 2. Inicialização com Valores Defaul:
- **Atributos:** Inicialize os atributos de uma classe com valores padrão (por exemplo, uma string vazia, um número zero) para evitar que sejam nulos por padrão.
- **Coleções:** Utilize coleções que não permitem elementos nulos (como `HashSet<String>`) ou inicialize-as com um valor padrão (uma lista vazia).

#### 3. Métodos de Utilidades:
- **Objects.requireNonNull:** Verifica se um objeto é nulo e lança uma `NullPointerException` caso seja:
    `{java}Objects.requireNonNull(objeto, "Objeto não pode ser nulo");`
- **Métodos personalizados:** Crie métodos auxiliares para realizar verificações comuns e encapsular a lógica.

#### 4. Design Defensivo:
- **Validação de parâmetros:** Verifique os parâmetros de métodos para garantir que não sejam nulos antes de usá-los.
- **Tratamento de exceções:** Use `try-catch` para capturar `NullPointerExceptions` e tomar ações adequadas, como registrar um erro ou retornar um valor padrão.

### Desvantagens das Abordagens Tradicionais:
- **Código verboso:** Muitas verificações explícitas podem tornar o código mais prolixo e difícil de ler.
- **Propensão a erros:** É fácil esquecer de verificar um objeto em algum ponto do código.
- **Não escalável:** À medida que o código cresce, o número de verificações aumenta, tornando a manutenção mais complexa.

### Alternativas Modernas:
- **Optional:** Introduzido no Java 8, o `Optional` oferece uma maneira mais elegante de representar valores que podem estar presentes ou ausentes.
- **Null Safety:** Linguagens como Kotlin oferecem suporte nativo a null safety, tornando mais difícil introduzir `NullPointerExceptions`.
---
## Evoluindo seu código com Optional: Uma abordagem mais elegante para lidar com nulidade em Java
- **Encapsula um valor opcional:** Representa um valor que pode estar presente ou não.
- **Evita verificações explícitas de nulidade:** O Optional oferece métodos para trabalhar com valores de forma segura, reduzindo o risco de `NullPointerExceptions`.
- **Melhora a legibilidade:** Torna o código mais conciso e expressivo, facilitando a compreensão da intenção do programador.

#### Como usar Optional?
```java
import java.util.Optional;

Optional<String> nomeOptional = Optional.ofNullable(pessoa.getNome());

// Verificando se o valor está presente:
if (nomeOptional.isPresent()) {
    String nome = nomeOptional.get();
    System.out.println("O nome é: " + nome);
} else {
    System.out.println("Nome não informado");
}
```

**Métodos úteis do Optional:**
- **isPresent():** Retorna `true` se um valor estiver presente.
- **get():** Retorna o valor se estiver presente, caso contrário, lança uma `NoSuchElementException`.
- **orElse(T other):** Retorna o valor se estiver presente, caso contrário, retorna o valor fornecido como argumento.
`- **orElseGet(Supplier<? extends T> other):** Retorna o valor se estiver presente, caso contrário, retorna o valor fornecido por um `Supplier`.
`- **map(Function<? super T, ? extends U> mapper):** Aplica uma função ao valor presente e retorna um novo Optional.
`- **flatMap(Function<? super T, Optional<U>> mapper):** Similar ao `map`, mas a função retorna um Optional.
- `**ifPresent(Consumer<? super T> consumer):** Executa uma ação se o valor estiver presente.`

### Exemplos práticos
**1. Retornando um valor padrão:**
`{java}String nome = nomeOptional.orElse("Anônimo");`

**2. Executando uma ação se o valor estiver presente:**
`{java}nomeOptional.ifPresent(nome -> System.out.println("O nome é: " + nome));`

**3. Mapeando o valor:**
`{java}Optional<Integer> tamanhoNome = nomeOptional.map(String::length);`

**4. Encadeando operações:**
```java
Optional<String> primeiroCaractere = nomeOptional
    .filter(nome -> nome.length() > 0)
    .map(nome -> nome.charAt(0) + "");
```

#### Quando usar Optional?
- **Retornos de métodos:** Quando um método pode não ter um valor a retornar.
- **Campos de objetos:** Para representar valores que podem ser nulos.
- **Coleções:** Para representar elementos que podem estar ausentes.

### Considerações importantes
- **Não abuse do Optional:** O Optional não é uma panaceia. Use-o com moderação e apenas quando fizer sentido.
- **Combine com outras técnicas:** O Optional pode ser combinado com outras técnicas, como a validação de parâmetros e o tratamento de exceções.
- **Considere o contexto:** A escolha de usar Optional depende do contexto e dos requisitos do seu projeto.
---
## Testando o valor do Optional com isPresent()
O método `isPresent()` do `Optional` é fundamental para verificar se um valor está presente dentro de um objeto Optional. Ele retorna um booleano: `true` se um valor estiver presente e `false` caso contrário.

**Por que usar isPresent()?**
- **Prevenção de NullPointerExceptions:** Ao verificar a presença do valor antes de acessá-lo, você evita o erro comum de tentar acessar um valor nulo.
- **Código mais seguro e robusto:** Ao garantir que o valor exista antes de realizar operações, você torna seu código mais confiável.
- **Leiturabilidade:** O método `isPresent()` torna o código mais claro e expressivo, facilitando a compreensão da lógica.

**Exemplo:**
```java
import java.util.Optional;

Optional<String> nomeOptional = Optional.ofNullable("João");

if (nomeOptional.isPresent()) {
    String nome = nomeOptional.get();
    System.out.println("O nome é: " + nome);
} else {
    System.out.println("Nome não informado");
}
```
**Explicando o código:**
1. **Criando um Optional:** O código cria um Optional de String e inicializa com o valor "João".
2. **Verificando a presença:** O `if (nomeOptional.isPresent())` verifica se há um valor dentro do Optional.
3. **Acessando o valor:** Se o valor estiver presente, o `nomeOptional.get()` retorna o valor e o imprime.
4. **Caso contrário:** Se o valor não estiver presente, a mensagem "Nome não informado" é exibida.

**Outras formas de utilizar isPresent():**
- **Com lambda expressions:**
    `{java}nomeOptional.ifPresent(nome -> System.out.println("O nome é: " + nome));`
    
- **Retornando um valor padrão:**
    `{java}String nome = nomeOptional.orElse("Anônimo");`
    
- **Executando uma ação caso não esteja presente:**
    ```java
    nomeOptional.ifPresentOrElse(
        nome -> System.out.println("O nome é: " + nome),
        () -> System.out.println("Nome não informado")
    );
    ```

**Boas práticas ao usar isPresent():**
- **Evite usar get() diretamente:** Sempre verifique se o valor está presente antes de usar `get()`, para evitar `NoSuchElementException`.
- **Utilize métodos como orElse(), orElseGet() e map()** para manipular o valor de forma mais segura e concisa.
- **Considere o contexto:** Avalie se o uso de Optional realmente agrega valor ao seu código.
---
## Obtendo Valor e Lançando Exceção com orElseThrow() em Java
O método `orElseThrow()` do `Optional` em Java é uma ferramenta poderosa para obter o valor de um `Optional` caso ele esteja presente, ou lançar uma exceção personalizada caso contrário. Essa abordagem é especialmente útil quando você deseja garantir que um valor esteja presente e que o programa não continue a execução com um valor nulo.

#### Como funciona o orElseThrow()?
- **Valor presente:** Se o `Optional` contiver um valor, esse valor será retornado.
- **Valor ausente:** Se o `Optional` estiver vazio, a exceção fornecida como argumento será lançada.

#### Sintaxe:
`{java}T orElseThrow(Supplier<? extends X> exceptionSupplier)`

- **T:** O tipo do valor contido no `Optional`.
- **X:** O tipo da exceção a ser lançada.
- **exceptionSupplier:** Um `Supplier` que fornece a exceção a ser lançada caso o valor esteja ausente.

#### Exemplo prático:
```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<String> nomeOptional = Optional.ofNullable(null); // Simulando um nome nulo

        try {
            String nome = nomeOptional.orElseThrow(() -> new IllegalArgumentException("Nome não pode ser nulo"));
            System.out.println("O nome é: " + nome);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }
}
```
**Explicação:**
1. **Criando um Optional:** Criamos um `Optional` de `String` e o inicializamos com `null`.
2. **Usando orElseThrow():** Chamamos `orElseThrow()` e fornecemos um `Supplier` que cria uma nova instância de `IllegalArgumentException` com a mensagem "Nome não pode ser nulo".
3. **Tratamento da exceção:** Se o nome for nulo, a exceção será lançada e capturada pelo bloco `catch`, imprimindo a mensagem de erro.

#### Vantagens de usar orElseThrow():
- **Clareza:** O código fica mais conciso e expressa claramente a intenção de lançar uma exceção se o valor estiver ausente.
- **Tratamento de erros:** Permite tratar a ausência de um valor de forma personalizada, lançando a exceção mais adequada para o contexto.
- **Prevenção de NullPointerExceptions:** Garante que o código não continue a execução com um valor nulo, evitando erros em tempo de execução.

#### Quando usar orElseThrow():
- **Cenários críticos:** Quando a ausência de um valor é considerada uma condição de erro e a aplicação deve ser interrompida.
- **Validação de dados:** Para validar a presença de valores obrigatórios antes de realizar operações.
- **Tratamento de exceções personalizadas:** Para lançar exceções específicas que forneçam informações mais detalhadas sobre o erro.

#### Outros métodos semelhantes:
- `orElse(T other)`: Retorna um valor padrão se o `Optional` estiver vazio.
- `orElseGet(Supplier<? extends T> other)`: Retorna um valor calculado por um `Supplier` se o `Optional` estiver vazio.
---
## Obtendo Valor Alternativo com orElse e orElseGet
Quando trabalhamos com `Optional` em Java, muitas vezes precisamos fornecer um valor alternativo caso o valor principal não esteja presente. Os métodos `orElse` e `orElseGet` são utilizados para essa finalidade, mas com nuances importantes.

#### orElse()
- **Retorna um valor:** Se o `Optional` contiver um valor, ele é retornado; caso contrário, o valor fornecido como argumento é retornado.
- **Avaliação imediata:** O valor fornecido é calculado imediatamente, independentemente de o `Optional` estar vazio ou não.

**Exemplo:**
```java
Optional<String> nomeOptional = Optional.ofNullable(null);
String nome = nomeOptional.orElse("Anônimo");
```
Neste exemplo, se `nomeOptional` estiver vazio, o valor "Anônimo" será atribuído à variável `nome`.

#### orElseGet()
- **Retorna um valor calculado por um Supplier:** Se o `Optional` estiver vazio, o `Supplier` fornecido como argumento é executado para calcular o valor a ser retornado.
- **Avaliação diferida:** O valor só é calculado se o `Optional` estiver vazio.

**Exemplo:**
```java
Optional<String> nomeOptional = Optional.ofNullable(null);
String nome = nomeOptional.orElseGet(() -> {
    System.out.println("Calculando nome padrão...");
    return "Padrão";
});
```
Neste exemplo, se `nomeOptional` estiver vazio, a mensagem "Calculando nome padrão..." será impressa e o valor "Padrão" será retornado.

### Quando usar cada um?
- **orElse:**
    - Quando o valor alternativo é simples de calcular ou obter.
    - Quando o valor alternativo não depende de nenhum estado externo.
- **orElseGet:**
    - Quando o cálculo do valor alternativo é caro ou envolve operações complexas.
    - Quando o valor alternativo depende de algum estado externo (por exemplo, uma chamada a um banco de dados).

### Comparação resumida

|Método|Descrição|Quando usar|
|---|---|---|
|orElse|Retorna um valor fixo|Valor alternativo simples|
|orElseGet|Retorna um valor calculado por um Supplier|Valor alternativo complexo ou dependente de estado|
#### Exemplo prático:
```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<Integer> idadeOptional = Optional.ofNullable(null);

        // Usando orElse para um valor simples
        int idade = idadeOptional.orElse(30);
        System.out.println("Idade: " + idade);

        // Usando orElseGet para um valor calculado
        int idadeCalculada = idadeOptional.orElseGet(() -> {
            // Simulação de cálculo complexo
            System.out.println("Calculando idade padrão...");
            return calcularIdadePadrao();
        });
        System.out.println("Idade calculada: " + idadeCalculada);
    }

    private static int calcularIdadePadrao() {
        // Lógica para calcular a idade padrão
        return 25;
    }
}
```
---
## Obtendo e Testando Valor com ifPresent e ifPresentOrElse
Os métodos `ifPresent` e `ifPresentOrElse` são ferramentas poderosas para trabalhar com `Optional` em Java, permitindo executar ações específicas dependendo da presença ou ausência de um valor.

#### ifPresent()
O método `ifPresent()` executa uma ação fornecida como um `Consumer` se um valor estiver presente no `Optional`.

**Sintaxe:**
`{java}optional.ifPresent(consumer);`

**Exemplo:**
```java
Optional<String> nomeOptional = Optional.of("João");
nomeOptional.ifPresent(nome -> System.out.println("O nome é: " + nome));
```
**Explicação:**
- Se `nomeOptional` contiver um valor (no caso, "João"), a ação dentro do `Consumer` será executada, imprimindo o nome na tela.
- Se `nomeOptional` estiver vazio, a ação não será executada.

#### ifPresentOrElse()
O método `ifPresentOrElse()` oferece uma forma mais concisa de executar ações diferentes dependendo da presença ou ausência de um valor.

**Sintaxe:**
`{java}optional.ifPresentOrElse(consumerIfPresent, emptyAction);`

**Exemplo:**
```java
Optional<String> nomeOptional = Optional.empty();
nomeOptional.ifPresentOrElse(
    nome -> System.out.println("O nome é: " + nome),
    () -> System.out.println("Nome não informado")
);
```
**Explicação:**
- Se `nomeOptional` contiver um valor, a primeira ação (dentro do `consumerIfPresent`) será executada.
- Se `nomeOptional` estiver vazio, a segunda ação (dentro do `emptyAction`) será executada.

### Comparação entre ifPresent() e ifPresentOrElse()

|Método|Descrição|
|---|---|
|ifPresent()|Executa uma ação se o valor estiver presente.|
|ifPresentOrElse()|Executa uma ação se o valor estiver presente e outra se estiver ausente.|
#### Quando usar cada um?
- **ifPresent():** Quando você precisa executar uma única ação caso o valor esteja presente.
- **ifPresentOrElse():** Quando você precisa executar ações diferentes dependendo da presença ou ausência do valor.

#### Exemplo mais completo:
```java
Optional<Integer> idadeOptional = Optional.of(25);

idadeOptional.ifPresentOrElse(
    idade -> {
        System.out.println("A idade é: " + idade);
        if (idade >= 18) {
            System.out.println("É maior de idade.");
        } else {
            System.out.println("É menor de idade.");
        }
    },
    () -> System.out.println("Idade não informada")
);
```

#### Vantagens de usar ifPresent e ifPresentOrElse:
- **Legibilidade:** Torna o código mais conciso e fácil de entender.
- **Prevenção de NullPointerExceptions:** Garante que você não tente acessar um valor nulo.
- **Flexibilidade:** Permite executar diferentes ações dependendo do estado do Optional.
---
## Testando e Filtrando Valores com Predicate em Java
O `Predicate` é uma interface funcional em Java que representa um predicado (uma função booleana de um único argumento) e é amplamente utilizado para filtrar coleções, testar condições e realizar outras operações. Quando combinado com o `Optional`, o `Predicate` se torna uma ferramenta poderosa para testar e filtrar valores de forma concisa e elegante.

#### O que é um Predicate?
Um `Predicate<T>` representa uma função que aceita um argumento de tipo `T` e retorna um booleano. É comumente usado para definir condições que devem ser satisfeitas por um elemento.

#### Como usar Predicate com Optional?
**1. Criando um Predicate:**
`{java}Predicate<Integer> isEven = number -> number % 2 == 0;`
Este Predicate verifica se um número é par.

**2. Aplicando o Predicate a um Optional:**
```java
Optional<Integer> numberOptional = Optional.of(4);
boolean isEvenNumber = numberOptional.filter(isEven).isPresent();
```
- `filter()` aplica o Predicate ao valor dentro do Optional. Se o Predicate retornar `true`, o Optional permanece com o valor. Caso contrário, o Optional fica vazio.
- `isPresent()` verifica se o Optional ainda contém um valor após a filtragem.

#### Exemplo Completo:
```java
import java.util.Optional;
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        Optional<Integer> numberOptional = Optional.of(3);

        Predicate<Integer> isEven = number -> number % 2 == 0;
        Predicate<Integer> isPositive = number -> number > 0;

        // Verificando se o número é par e positivo
        boolean isEvenAndPositive = numberOptional
            .filter(isEven)
            .filter(isPositive)
            .isPresent();

        if (isEvenAndPositive) {
            System.out.println("O número é par e positivo.");
        } else {
            System.out.println("O número não é par e positivo.");
        }
    }
}
```

#### Combinando Predicates
Você pode combinar Predicates usando métodos como `and`, `or` e `negate`:

- **and:** Retorna um Predicate que é a conjunção de dois Predicates.
- **or:** Retorna um Predicate que é a disjunção de dois Predicates.
- **negate:** Retorna um Predicate que nega o Predicate original.
`{java}Predicate<Integer> isEvenAndPositive = isEven.and(isPositive);`

#### Vantagens de usar Predicate com Optional:
- **Legibilidade:** Código mais conciso e expressivo.
- **Reutilização:** Predicates podem ser reutilizados em diferentes partes do código.
- **Flexibilidade:** Permite criar combinações complexas de condições.
- **Funcional:** Se encaixa bem no paradigma de programação funcional.

#### Outros Usos
- **Filtrando coleções:** `Predicate` é amplamente utilizado com `Stream` para filtrar elementos de uma coleção.
- **Validando dados:** Pode ser usado para validar dados de entrada.
- **Customizando comportamentos:** Permite criar lógica personalizada para testar condições.
---
## Aplicando Transformações com map()
O método `map()` é uma ferramenta poderosa em Java 8 e versões posteriores, especialmente quando se trabalha com coleções e `Optional`. Ele permite aplicar uma função a cada elemento de uma coleção ou a um valor dentro de um `Optional`, transformando-o em um novo valor.

#### Como funciona o map()?
- **Coleções:** Quando aplicado a uma `Stream`, o `map()` transforma cada elemento da Stream aplicando a função fornecida.
- **Optional:** Quando aplicado a um `Optional`, o `map()` transforma o valor dentro do Optional, se ele estiver presente. Se o Optional estiver vazio, o resultado será um Optional vazio.

#### Sintaxe:
```java
// Para Streams:
Stream<T> stream = ...;
Stream<R> mappedStream = stream.map(element -> function(element));

// Para Optional:
Optional<T> optional = ...;
Optional<R> mappedOptional = optional.map(element -> function(element));
```

#### Exemplos:
**Transformando uma lista de números em uma lista de seus quadrados:**
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer>    squaredNumbers = numbers.stream()
                                      .map(n -> n * n)
                                      .collect(Collectors.toList());   
```

##### Transformando um `Optional<String>` em um `Optional<Integer>` representando o comprimento da string:
```java
import java.util.Optional;

Optional<String> nameOptional = Optional.of("Alice");
Optional<Integer> nameLengthOptional = nameOptional.map(String::length);
```

#### Usos comuns de map():
- **Transformando dados:** Convertendo um tipo de dado em outro.
- **Criando novas coleções:** Transformando uma coleção em outra com elementos transformados.
- **Manipulando Optional:** Transformando o valor dentro de um Optional.

#### Exemplo mais complexo:
```java
import java.util.List;
import java.util.stream.Collectors;

class Person {
    private String name;
    private int age;
    // ... getters e setters
}

// ...

List<Person> people = ...; // Uma lista de pessoas

List<String> names = people.stream()
                           .map(Person::getName)
                           .collect(Collectors.toList());
```
Neste exemplo, estamos extraindo os nomes de uma lista de pessoas e criando uma nova lista com apenas os nomes.

#### Vantagens de usar map():
- **Funcional:** Se encaixa bem no paradigma de programação funcional.
- **Conciso:** Permite escrever código mais conciso e expressivo.
- **Reutilizável:** Funções podem ser reutilizadas em diferentes contextos.
- **Flexível:** Permite realizar transformações complexas em dados.
---
## Aplicando Transformações com flatMap() em Java
O método `flatMap()` é uma ferramenta poderosa em Java 8 e versões posteriores, especialmente quando se trabalha com coleções aninhadas ou estruturas de dados mais complexas. Ele permite "achatá" uma estrutura de dados, aplicando uma função a cada elemento e combinando os resultados em um único Stream.

#### Como funciona o flatMap()?
- **Coleções aninhadas:** Ao invés de apenas transformar cada elemento, o `flatMap()` aplica uma função que retorna um Stream para cada elemento. Em seguida, todos esses Streams são "achatados" em um único Stream.
- **Optional:** Embora menos comum, o `flatMap()` também pode ser usado com Optional para realizar transformações mais complexas.

#### Sintaxe:
```java
// Para Streams:
Stream<T> stream = ...;
Stream<R> flatMappedStream = stream.flatMap(element -> function(element));
```

#### Exemplos:
**Achatando uma lista de listas:**
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

List<List<Integer>> nestedLists = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4, 5));
List<Integer> flattenedList = nestedLists.stream()
                                        .flatMap(List::stream)
                                        .collect(Collectors.toList());
```

#### Transformando uma lista de pessoas em uma lista de seus hobbies:
```java
class Person {
    private String name;
    private List<String> hobbies;
    // ... getters e setters
}

// ...

List<Person> people = ...; // Uma lista de pessoas

List<String> hobbies = people.stream()
                             .flatMap(person -> person.getHobbies().stream())
                             .collect(Collectors.toList());
```

#### Quando usar flatMap()?
- **Achatando estruturas:** Quando você precisa transformar uma estrutura aninhada em uma estrutura plana.
- **Combinando resultados:** Quando uma operação retorna múltiplos valores para cada elemento.
- **Simplificando código:** Ao lidar com estruturas complexas, o `flatMap()` pode tornar o código mais conciso e legível.

#### Comparação entre map() e flatMap()

| Método    | Descrição                                                                                   |
| --------- | ------------------------------------------------------------------------------------------- |
| map()     | Transforma cada elemento em um novo elemento.                                               |
| flatMap() | Transforma cada elemento em um Stream e então "achata" todos os Streams em um único Stream. |
#### Vantagens de usar flatMap():
- **Flexibilidade:** Permite transformar estruturas complexas de forma mais fácil.
- **Concisão:** Torna o código mais conciso e expressivo.
- **Funcional:** Se encaixa bem no paradigma de programação funcional.

#### Outros Usos
- **Processando dados hierárquicos:** Árvore de diretórios, estruturas JSON, etc.
- **Criando novas coleções:** A partir de estruturas aninhadas.
- **Resolvendo problemas complexos:** Combinando com outros métodos como `filter`, `map`, `reduce`, etc.
---
## Tipos Especiais de Optional para Tipos Primitivos

**O que são Optional e seus tipos primitivos?**
O `Optional` em Java é uma classe introduzida no Java 8 que representa um valor que pode estar presente ou não. Ele é usado para evitar `NullPointerExceptions` e tornar o código mais seguro e expressivo.

Por padrão, o `Optional` trabalha com tipos de referência. No entanto, para acomodar os tipos primitivos (int, double, boolean, etc.), o Java oferece classes wrapper específicas dentro do pacote `java.util`:
- **OptionalInt:** Representa um valor inteiro opcional.
- **OptionalDouble:** Representa um valor double opcional.
- **OptionalLong:** Representa um valor long opcional.
- **OptionalBoolean:** Representa um valor booleano opcional.

**Por que usar Optional para tipos primitivos?**
- **Consistência:** Mantém a consistência ao trabalhar com valores que podem estar ausentes, tanto para tipos de referência quanto para tipos primitivos.
- **Segurança:** Evita `NullPointerExceptions` ao lidar com valores primitivos que podem ser nulos em determinados contextos.
- **Expressividade:** Torna o código mais expressivo e claro, indicando explicitamente se um valor está presente ou não.

**Como utilizar os Optional para tipos primitivos:**
```java
import java.util.OptionalInt;

public class OptionalPrimitiveExample {
    public static void main(String[] args) {
        OptionalInt age = OptionalInt.of(25);
        OptionalInt emptyAge = OptionalInt.empty();

        // Verificando se o valor está presente
        if (age.isPresent()) {
            System.out.println("A idade é: " + age.getAsInt());
        }

        // Obtendo um valor padrão se não estiver presente
        int defaultAge = emptyAge.orElse(30);
        System.out.println("Idade padrão: " + defaultAge);
    }
}
```

**Métodos comuns:**
Os métodos disponíveis para os Optional de tipos primitivos são semelhantes aos do Optional padrão, com algumas adaptações para os tipos primitivos:
- **isPresent():** Verifica se um valor está presente.
- **getAsInt(), getAsDouble(), getAsLong(), getAsBoolean():** Obtém o valor presente, lançando uma exceção se o valor estiver ausente.
- **orElse(T other):** Retorna o valor presente se estiver presente, caso contrário, retorna o valor fornecido.
- **`orElseGet(Supplier<? extends T> other)`:** Retorna o valor presente se estiver presente, caso contrário, calcula o valor usando o Supplier fornecido.
- **ifPresent(IntConsumer action):** Executa uma ação se o valor estiver presente.
- **ifPresentOrElse(IntConsumer action, Runnable emptyAction):** Executa uma ação se o valor estiver presente, caso contrário, executa outra ação. // ... e outros métodos semelhantes

**Quando usar Optional para tipos primitivos?**
- **Valores opcionais em cálculos:** Quando um cálculo pode resultar em um valor ausente (por exemplo, divisão por zero).
- **Dados de entrada:** Ao lidar com dados de entrada que podem estar ausentes ou inválidos.
- **Retorno de métodos:** Quando um método pode não ter um valor válido a retornar em determinadas situações.

**Exemplo prático:**
```java
OptionalDouble average = numbers.stream()
                                .mapToInt(Integer::intValue)
                                .average();

if (average.isPresent()) {
    System.out.println("A média é: " + average.getAsDouble());
} else {
    System.out.println("Não há números para calcular a média.");
}
```
---
## Boas Práticas ao Usar Optional
O Optional é uma ferramenta poderosa para lidar com valores que podem estar ausentes em Java, mas seu uso inadequado pode levar a código menos legível e mais propenso a erros. Para aproveitar ao máximo os benefícios do Optional, siga estas boas práticas:

#### 1. Retorne Optional quando o valor puder estar ausente:
- **Métodos de acesso:** Ao retornar um valor que pode ser nulo de um método, considere retornar um Optional. Isso força o chamador a verificar se o valor está presente antes de usá-lo.
- **Resultados de operações:** Se uma operação puder falhar ou não produzir um resultado, retorne um Optional.

#### 2. Evite aninhar excessivamente Optional:
- **Chamadas encadeadas:** Evite encadear muitos métodos `map` ou `flatMap` em um Optional, pois pode tornar o código difícil de ler e entender.
- **Condições complexas:** Se precisar de muitas condições para verificar a presença de um valor, considere refatorar o código.

#### 3. Use `{java}orElse`, `{java}orElseGet` e `{java}orElseThrow` de forma adequada:
- **orElse:** Use para fornecer um valor padrão quando o valor estiver ausente.
- **orElseGet:** Use quando o valor padrão é caro de calcular.
- **orElseThrow:** Use para lançar uma exceção específica quando o valor estiver ausente.

#### 4. Não use `{java}get()` diretamente:
- **Risco de NullPointerException:** O método `get()` lança uma `NoSuchElementException` se o valor estiver ausente. Prefira usar `isPresent()` para verificar a presença antes de obter o valor.
- **Alternativas:** Use `orElse`, `orElseGet` ou `orElseThrow` para lidar com a ausência de valor de forma mais segura.

#### 5. Evite `{java}Optional.ofNullable(null)`:
- **Redundante:** Criar um Optional de um valor nulo é redundante e pode levar a confusão.
- **Use Optional.empty()** para representar um valor ausente explicitamente.

#### 6. Considere as alternativas:
- **Nullable annotations:** Para tipos que podem ser nulos, considere usar anotações como `@Nullable` e `@NonNull` para documentar essa possibilidade e permitir que a ferramenta de análise de código verifique o uso correto.
- **Tipos específicos:** Em alguns casos, tipos específicos como `Maybe` ou `Either` podem oferecer funcionalidades adicionais e uma semântica mais clara.

#### 7. Seja consistente:
- **Estilo de codificação:** Adote um estilo consistente para usar Optional em todo o seu código.
- **Convenções:** Siga as convenções de sua equipe ou empresa para o uso de Optional.

#### Exemplo de código bem escrito:
```java
Optional<String> name = Optional.ofNullable(person.getName());

String formattedName = name
        .map(String::toUpperCase)
        .orElse("Anônimo");
```

**Quando não usar Optional:**
- **Valores sempre presentes:** Se um valor sempre estiver presente, não há necessidade de usar Optional.
- **Coleções:** Para representar coleções que podem estar vazias, use coleções vazias diretamente.
- **Exceções:** Se a ausência de um valor indica uma condição de erro, lance uma exceção apropriada em vez de usar Optional.
---