https://github.com/camillagatin/collections-java-api-2023
## Introdução aos Conjuntos e o Tipo Set
Em matemática, um conjunto é uma coleção de elementos distintos. Em Java, essa mesma ideia é representada pela interface `Set`. Um `Set` não permite elementos duplicados, ou seja, cada elemento só pode aparecer uma vez no conjunto.

**Características principais:**
- **Elementos únicos:** Cada elemento só pode estar presente uma vez.
- **Desordenado:** Não há uma ordem específica para os elementos em um conjunto.
- **Baseado em hash:** A maioria das implementações de `Set` usa uma função hash para garantir a unicidade dos elementos e um acesso rápido.

### O tipo Set em Java Collections
A interface `Set` em Java oferece métodos para adicionar, remover e verificar a existência de elementos. Algumas das implementações mais comuns de `Set` incluem:

- **HashSet:**
    - Baseado em uma tabela hash.
    - Oferece um desempenho excelente para operações de adição, remoção e verificação de existência.
    - Não garante nenhuma ordem específica dos elementos.
- **TreeSet:**
    - Baseado em uma árvore rubro-negra.
    - Mantém os elementos ordenados de acordo com a ordem natural ou um `Comparator` especificado.
    - Mais lento que `HashSet` para operações básicas, mas oferece ordenação natural.
- **LinkedHashSet:**
    - Combina as características de `HashSet` e `LinkedHashSet`.
    - Mantém a ordem de inserção dos elementos.
    - Geralmente mais lento que `HashSet`, mas oferece a ordem de inserção.

### Quando usar Set?
- **Elementos únicos:** Quando você precisa garantir que cada elemento apareça apenas uma vez em uma coleção.
- **Remoção de duplicados:** Para remover duplicados de uma lista.
- **Operações de conjunto:** Para realizar operações como união, interseção e diferença entre conjuntos.

##### Exemplo de uso:
```java
import java.util.HashSet;
import java.util.Set;

public class ExemploSet {
    public static void main(String[] args) {
        Set<String> frutas = new HashSet<>();
        frutas.add("maçã");
        frutas.add("banana");
        frutas.add("laranja");
        frutas.add("maçã"); // Tentativa de adicionar um elemento duplicado (ignorada)

        System.out.println(frutas); // Imprime: [laranja, banana, maçã] (a ordem pode variar)
    }
}
```

### Comparando Set com List

|Característica|Set|List|
|---|---|---|
|Elementos duplicados|Não permite|Permite|
|Ordem|Não garantida|Garantida (indexada)|
|Operações comuns|Adicionar, remover, verificar existência|Adicionar, remover, obter por índice, iterar|

### Conclusão
O `Set` é uma estrutura de dados fundamental em Java, ideal para representar coleções de elementos únicos. Sua escolha entre as diferentes implementações (HashSet, TreeSet, LinkedHashSet) dependerá das suas necessidades específicas, como a necessidade de ordenação e o desempenho das operações.

---
## Utilizando Conjuntos do Tipo HashSet
Um `HashSet` em Java é uma implementação da interface `Set` baseada em uma tabela hash. Ele armazena elementos de forma desordenada e não permite duplicados. A principal vantagem do `HashSet` é o alto desempenho para operações de adição, remoção e verificação de existência de elementos.

### Quando usar HashSet?
- **Elementos únicos:** Quando você precisa garantir que cada elemento apareça apenas uma vez em uma coleção.
- **Desempenho:** Quando a ordem dos elementos não é importante e você precisa de um acesso rápido aos elementos.
- **Remoção de duplicados:** Para remover elementos duplicados de uma lista.

### Como criar e usar um HashSet?
```java
import java.util.HashSet;
import java.util.Set;

public class ExemploHashSet {
    public static void main(String[] args) {
        // Criando um HashSet    de Strings
        Set<String> frutas = new HashSet<>();

        // Adicionando elementos
        frutas.add("maçã");
        frutas.add("banana");
        frutas.add("laranja");
        // Tentativa de adicionar um elemento duplicado (ignorada)
        frutas.add("maçã");

        // Verificando se um elemento existe
        if (frutas.contains("banana")) {
            System.out.println("A fruta banana está presente.");
        }

        // Iterando sobre os elementos (a ordem não é garantida)
        for (String fruta : frutas) {
            System.out.println(fruta);
        }
    }
}
```

### Operações comuns em HashSet
- **add(E e):** Adiciona um elemento ao conjunto. Retorna `true` se o elemento foi adicionado com sucesso (ou seja, se o elemento não existia anteriormente).
- **remove(Object o):** Remove o elemento especificado do conjunto. Retorna `true` se o elemento foi removido.
- **contains(Object o):** Verifica se o conjunto contém o elemento especificado.
- **clear():** Remove todos os elementos do conjunto.
- **size():** Retorna o número de elementos no conjunto.
- **isEmpty():** Verifica se o conjunto está vazio.

### Operações de conjunto
- `addAll(Collection<?> c)` : Adiciona todos os elementos de outra coleção ao conjunto.
- `removeAll(Collections<?>c)` : Remove todos os elementos que estão presentes em outra coleção.
- `retainAll(Collection<?> c)` : Retorna apenas os elementos que estão presentes em ambas as coleções.

### Considerações importantes
- **Hashcode e equals:** Para garantir que elementos sejam considerados iguais em um HashSet, é crucial que as classes dos elementos sobrescrevam os métodos `hashCode()` e `equals()` de forma consistente.
- **Ordem não garantida:** A ordem dos elementos em um HashSet não é definida e pode variar entre diferentes execuções.
- **Null:** Um HashSet pode conter no máximo um elemento null.

### Quando usar HashSet vs TreeSet vs LinkedHashSet?
- **HashSet:** Ideal para quando a ordem não importa e você precisa de um acesso rápido aos elementos.
- **TreeSet:** Ideal quando você precisa manter os elementos ordenados de acordo com uma determinada ordem natural ou um `Comparator`.
- **LinkedHashSet:** Ideal quando você precisa manter a ordem de inserção dos elementos e também garantir a unicidade.

### Exemplo de uso prático:
```java
// Remover duplicados de uma lista
List<String> listaComDuplicados = Arrays.asList("a", "b", "a", "c");
Set<String> conjuntoSemDuplicados = new HashSet<>(listaComDuplicados);
```

**Em resumo:**
O HashSet é uma ferramenta poderosa em Java para trabalhar com coleções de elementos únicos. Sua simplicidade e alto desempenho o tornam ideal para uma variedade de cenários. Ao entender suas características e as diferenças entre ele e outras implementações de Set, você poderá escolher a estrutura de dados mais adequada para suas necessidades.

---
## Tabelas de Espalhamento (Hash Tables)
Uma tabela de espalhamento, ou hash table em inglês, é uma estrutura de dados que permite um acesso rápido a elementos através de uma função de hash. Em Java, essa estrutura é a base para diversas coleções, como `HashSet`, `HashMap` e `Hashtable`.

##### Como funcionam?
1. **Função de Hash:** Cada elemento tem um código hash calculado através de uma função de hash. Esse código hash é um número inteiro que representa o elemento de forma única (na maioria das vezes).
2. **Array:** A tabela de espalhamento é implementada como um array, onde cada índice representa um possível valor de hash.
3. **Colisões:** Quando dois elementos diferentes geram o mesmo código hash, ocorre uma colisão. Para resolver esse problema, são utilizadas diferentes técnicas, como listas encadeadas ou sondagem linear.

##### Vantagens:
- **Acesso rápido:** A busca, inserção e remoção de elementos são operações com tempo constante em média (O(1)), desde que a função de hash seja bem projetada.
- **Flexibilidade:** Podem ser usadas para armazenar qualquer tipo de objeto.

##### Desvantagens:
- **Colisões:** A performance pode ser afetada por um grande número de colisões.
- **Ordem não garantida:** A ordem dos elementos não é definida e pode variar.

##### HashSet: Um exemplo de implementação
O `HashSet` em Java é uma implementação de `Set` baseada em uma tabela de hash. Ele garante que cada elemento seja único e oferece um desempenho excelente para operações de adição, remoção e verificação de existência.

##### Como o HashSet funciona:
- **Adição:** Ao adicionar um elemento, o HashSet calcula o código hash do elemento e o coloca na posição correspondente da tabela. Se houver uma colisão, o elemento é adicionado a uma lista encadeada nessa posição.
- **Busca:** Para buscar um elemento, o HashSet calcula o código hash e busca o elemento na posição correspondente da tabela.
- **Remoção:** A remoção é semelhante à busca, mas após encontrar o elemento, ele é removido da lista encadeada.

**Código de exemplo:**
```java
import java.util.HashSet;
import java.util.Set;

public class ExemploHashSet {
    public static void main(String[] args) {
        Set<String>    frutas = new HashSet<>();
        frutas.add("maçã");
        frutas.add("banana");
        frutas.add("laranja");
        // ...
    }
}
```

**Considerações importantes:**
- **Função de hash:** A qualidade da função de hash influencia diretamente o desempenho da tabela de espalhamento. Uma boa função de hash distribui os elementos de forma uniforme pela tabela, minimizando o número de colisões.
- **Fator de carga:** O fator de carga é a razão entre o número de elementos e o tamanho da tabela. Um fator de carga alto pode aumentar o número de colisões e degradar o desempenho.
- **Implementações:** Além do `HashSet`, outras classes como `HashMap` e `Hashtable` também utilizam tabelas de espalhamento.

---
## O Método hashCode( )
O método `hashCode()` em Java é uma função que retorna um número inteiro, conhecido como código hash, associado a um objeto. Esse número é utilizado por diversas estruturas de dados, como `HashSet`, `HashMap` e `Hashtable`, para indexar e comparar objetos de forma eficiente.

**Por que é importante?**
- **Eficiência:** Em estruturas de dados baseadas em hash, o `hashCode()` permite um acesso rápido aos elementos, reduzindo o tempo de busca.
- **Unicidade:** Embora não garanta a unicidade absoluta, um bom `hashCode()` ajuda a minimizar colisões, ou seja, situações em que objetos diferentes possuem o mesmo código hash.
- **Consistência:** O valor retornado por `hashCode()` deve ser consistente para um mesmo objeto, a menos que seus atributos que afetam a igualdade sejam modificados.

### Como funciona?
O método `hashCode()` geralmente combina os valores hash dos atributos que definem a igualdade de um objeto. A combinação é feita usando uma fórmula matemática que envolve um número primo (comumente 31) para dispersar os valores de forma mais uniforme.

**Exemplo:**
```java
class Pessoa {
    private String nome;
    private int idade;

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result   1. github.com github.com + ((nome == null) ? 0 : nome.hashCode());
        result = prime   1. pt.stackoverflow.com pt.stackoverflow.com * result + idade;
        return result;
    }
}
```

**Explicação do código:**
- **Número primo:** O número 31 é frequentemente utilizado por ser primo e auxiliar na distribuição dos valores hash.
- **Combinação dos atributos:** O código hash é calculado combinando os códigos hash dos atributos `nome` e `idade`.
- **Tratamento de null:** Se o atributo `nome` for nulo, o valor 0 é adicionado para evitar `NullPointerException`.

### Dicas e Melhores Práticas
- **Consistência com equals():** Se dois objetos são considerados iguais por `equals()`, seus códigos hash devem ser iguais.
- **Evitar operações complexas:** O cálculo do `hashCode()` deve ser rápido, evitando operações caras.
- **Utilizar todos os atributos relevantes:** Inclua todos os atributos que afetam a igualdade do objeto no cálculo do hash.
- **Considerar a distribuição:** Uma boa função `hashCode()` distribui os valores de forma uniforme para minimizar colisões.
- **Bibliotecas:** Algumas bibliotecas oferecem implementações de `hashCode()` mais robustas e eficientes.

#### Por que é importante implementar corretamente?
- **Desempenho:** Um `hashCode()` bem implementado garante um bom desempenho em estruturas de dados baseadas em hash.
- **Corretude:** Um `hashCode()` mal implementado pode levar a comportamentos inesperados, como objetos iguais não sendo encontrados em um `HashSet`.

### Método hashCode( ) e as Coleções Java

O `hashCode()` desempenha um papel crucial nas seguintes coleções:

- **HashSet:** Utiliza o `hashCode()` para determinar a posição de um elemento na tabela hash, garantindo a unicidade dos elementos.
- **HashMap:** Utiliza o `hashCode()` da chave para determinar a posição do par chave-valor na tabela hash.
- **Hashtable:** Funciona de forma semelhante ao `HashMap`, mas é sincronizada.
##### Implementação de hashCode com hashSet
```java title:Contato.java
package com.algaworks.crm;
import java.util.Objects;

public class Contato {

    private String nome;
    private String email;
    private int idade;

    public Contato(String nome, String email, int idade) {
        Objects.requireNonNull(nome);
        Objects.requireNonNull(email);
        this.nome = nome;
        this.email = email;
        this.idade = idade;
    }

    // ... getters e setters

    @Override
    public String toString() {
        return "Contato{" +
                "nome='" + nome + '\'' +
                ", email='" + email + '\'' +
                ", idade=" + idade +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        System.out.printf("%s = %s%n", getEmail(), ((Contato) o).getEmail());
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Contato contato = (Contato) o;
        return email.equals(contato.email);
    }

    @Override
    public int hashCode() {
        return email.charAt(0);
    }

}
```
```java title:Principal.java
import com.algaworks.crm.Contato;

import java.util.HashSet;
import java.util.Set;

public class Principal {
    public static void main(String[] args) {
        Set<Contato> contatos = new HashSet<>();

        System.out.println("---");
        contatos.add(new Contato("Maria", "maria@algaworks.com", 40));
        contatos.add(new Contato("Ana", "ana@algaworks.com", 30));
        contatos.add(new Contato("José", "jose@algaworks.com", 25));
        contatos.add(new Contato("Rosa", "rosa@algaworks.com", 50));
        contatos.add(new Contato("João", "joao@algaworks.com", 70));
        System.out.println("--");
        contatos.add(new Contato("Josefina", "josefina@algaworks.com", 70));
        System.out.println("--");
        contatos.add(new Contato("Josefina", "josefina@algaworks.com", 70));
        contatos.add(null);
        System.out.println("--");

//        System.out.println(contatos);

        boolean resultado = contatos.contains(
                new Contato("Alaor", "alaor@algaworks.com", 30));
        System.out.println(resultado);
    }

}
```
---
## Usando conjuntos do tipo TreeSet
É uma implementação da interface `Set` que armazena elementos em uma ordem **natural** ou **específica**. Essa ordem é determinada por um critério de comparação, que pode ser:

- **Natural:** Os elementos são ordenados de acordo com a implementação do método `compareTo` da classe que representa esses elementos.
- **Customizado:** Um `Comparator` é fornecido para definir a ordem de comparação.

#### Características principais:
- **Elementos únicos:** Assim como todos os `Set`, um `TreeSet` não permite elementos duplicados.
- **Ordenado:** Os elementos são sempre mantidos em ordem, o que facilita operações como busca e ordenação.
- **Baseado em árvore:** Internamente, um `TreeSet` utiliza uma estrutura de dados em árvore para armazenar os elementos de forma eficiente.

### Quando usar TreeSet?
- **Quando a ordem é importante:** Se você precisa iterar sobre os elementos em uma ordem específica, o `TreeSet` é uma excelente escolha.
- **Quando a busca por elementos é frequente:** A estrutura em árvore do `TreeSet` permite buscas eficientes, mesmo em conjuntos grandes.
- **Quando você precisa manter elementos únicos e ordenados:** O `TreeSet` combina essas duas características de forma elegante.

### Exemplo básico:
```java
import java.util.TreeSet;

public class TreeSetExemplo {
    public static void main(String[] args) {
        TreeSet<String> frutas = new TreeSet<>();
        frutas.add("Banana");
        frutas.add("Maçã");
        frutas.add("Pera");

        for (String fruta : frutas) {
            System.out.println(fruta);
        }
    }
}
```
Neste exemplo, as frutas serão impressas na ordem alfabética, pois a classe `String` implementa o método `compareTo` para realizar a comparação lexicográfica.

#### Ordenação personalizada:
```java
import java.util.Comparator;
import java.util.TreeSet;

class Pessoa implements Comparable<Pessoa> {
    private String nome;
    private int idade;

    // ... construtores e getters

    @Override
    public int compareTo(Pessoa outraPessoa) {
        return Integer.compare(this.idade, outraPessoa.idade);
    }
}

public class TreeSetExemplo {
    public static void main(String[] args) {
        TreeSet<Pessoa> pessoas = new TreeSet<>(Comparator.comparing(Pessoa::getNome));
        // ... adicionar pessoas
    }
}
```

Neste exemplo, as pessoas serão ordenadas pelo nome, mesmo que a classe `Pessoa` implemente o método `compareTo` para ordenar por idade. Isso ocorre porque passamos um `Comparator` personalizado para o construtor do `TreeSet`.

#### Usos comuns:
- **Ordenação de objetos:** Ordenar listas de objetos com base em diferentes critérios.
- **Implementação de conjuntos ordenados:** Criar conjuntos que mantenham os elementos em uma ordem específica.
- **Implementação de estruturas de dados mais complexas:** Servir como base para estruturas de dados mais sofisticadas, como árvores balanceadas e heaps.

#### Considerações:
- **Custo de inserção:** A inserção de elementos em um `TreeSet` pode ser mais lenta do que em um `HashSet`, especialmente para conjuntos grandes.
- **Implementação do `compareTo`:** A correta implementação do método `compareTo` é crucial para garantir a ordenação correta dos elementos.
- **Uso de `Comparator`:** O `Comparator` permite personalizar a ordem de comparação de forma flexível.

---
## Usando conjuntos do tipo LinkedHashSet
O `LinkedHashSet` é uma implementação da interface `Set` em Java que combina as melhores características de `HashSet` e `LinkedHashSet`. Ele garante a **unicidade** dos elementos (como em um `HashSet`) e mantém a **ordem de inserção** dos elementos (como em uma `LinkedList`).

#### Características principais:
- **Elementos únicos:** Não permite elementos duplicados.
- **Ordem de inserção:** Os elementos são armazenados na ordem em que foram adicionados ao conjunto.
- **Baseado em hash e lista:** Internamente, utiliza uma tabela hash para garantir acesso rápido aos elementos e uma lista duplamente encadeada para manter a ordem de inserção.

#### Quando usar LinkedHashSet?
- **Quando a ordem de inserção é importante:** Se você precisa iterar sobre os elementos na mesma ordem em que foram adicionados, o `LinkedHashSet` é a escolha ideal.
- **Quando você precisa de um conjunto único e ordenado:** Ele combina a eficiência de um `HashSet` com a ordem de um `LinkedList`.
- **Quando a ordem natural dos elementos não é relevante:** Se a ordem natural (como em um `TreeSet`) não é importante, mas você precisa manter uma ordem específica, o `LinkedHashSet` é uma boa opção.

**Exemplo:**
```java
import java.util.LinkedHashSet;

public class LinkedHashSetExemplo {
    public static void main(String[] args) {
        LinkedHashSet<String>    cores = new LinkedHashSet<>();
        cores.add("Vermelho");
        cores.add("Azul");
        cores.add("Verde");
        cores.add("Amarelo");
        cores.add("Azul"); // Duplicado, será ignorado

        for (String cor : cores) {
            System.out.println(cor);
        }
    }
}
```

Neste exemplo, as cores serão impressas na mesma ordem em que foram adicionadas, mesmo que a tentativa de adicionar "Azul" novamente seja ignorada.

**Comparação com HashSet e TreeSet:**

|Característica|HashSet|TreeSet|LinkedHashSet|
|---|---|---|---|
|Ordem|Não ordenada|Ordenada naturalmente|Ordem de inserção|
|Duplicados|Não permite|Não permite|Não permite|
|Performance|Geralmente mais rápido para inserção e busca|Mais lento para inserção, mas eficiente para buscas ordenadas|Desempenho intermediário|

##### Usos comuns:
- **Cache:** Armazenar elementos em um cache, mantendo a ordem em que foram adicionados.
- **Histórico de ações:** Manter um histórico de ações em uma determinada ordem.
- **Implementação de LRU cache:** Criar um cache que remove os elementos menos recentemente usados.

##### Considerações:
- **Consumo de memória:** O `LinkedHashSet` pode consumir mais memória do que um `HashSet` devido à lista duplamente encadeada.
- **Performance:** A performance do `LinkedHashSet` é geralmente boa, mas pode ser um pouco mais lenta do que um `HashSet` para operações de inserção e remoção.
---