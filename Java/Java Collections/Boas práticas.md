# Encapsulamento com coleções não-modificáveis
O encapsulamento é um dos pilares da programação orientada a objetos, e quando falamos de coleções em Java, ele se torna ainda mais importante. Uma das melhores práticas para garantir a integridade e segurança de suas coleções é utilizar **coleções não-modificáveis**.

### O que são coleções não-modificáveis?
Coleções não-modificáveis são aquelas que não permitem a adição, remoção ou modificação de seus elementos após a criação. Isso significa que você pode apenas ler os elementos da coleção, mas não alterá-la.

### Por que usar coleções não-modificáveis?
- **Segurança:** Evita modificações acidentais na coleção, especialmente em código concorrente.
- **Impossibilidade de alterações:** Garante que a coleção permanecerá imutável após a criação.
- **Defensiva:** Ajuda a criar APIs mais defensivas, protegendo os dados internos da classe.
- **Facilita a razão:** Torna o código mais fácil de entender e raciocinar, pois o estado da coleção é mais previsível.

### Como criar coleções não-modificáveis?
Java oferece métodos para criar coleções não-modificáveis a partir de coleções existentes:
- **Collections.unmodifiableList():** Cria uma lista não-modificável a partir de uma lista existente.
- **Collections.unmodifiableSet():** Cria um conjunto não-modificável a partir de um conjunto existente.
- **Collections.unmodifiableMap():** Cria um mapa não-modificável a partir de um mapa existente.

##### Exemplo:
```java
import java.util.*;

public class ColecoesNaoModificaveis {
    public static void main(String[] args) {
        List<String> listaOriginal = List.of("Java", "Python", "JavaScript");
        List<String> listaNaoModificavel = Collections.unmodifiableList(listaOriginal);

        // Tentativa de adicionar um elemento (vai lançar UnsupportedOperationException)
        // listaNaoModificavel.add("C#");

        // Iterando sobre a lista
        for (String linguagem : listaNaoModificavel) {
            System.out.println(linguagem);
        }
    }
}
```

### Boas práticas adicionais
- **Retorne cópias não-modificáveis:** Ao expor coleções privadas de uma classe, retorne cópias não-modificáveis para evitar que o cliente modifique a coleção interna.
- **Use coleções imutáveis sempre que possível:** Para dados que nunca precisam ser alterados, use coleções imutáveis como `List.of()`, `Set.of()` e `Map.of()`.
- **Evite o casting:** Evite fazer casting de coleções não-modificáveis para tipos modificáveis. Isso pode levar a erros em tempo de execução.

### Benefícios do encapsulamento com coleções não-modificáveis
- **Código mais seguro:** Reduz o risco de erros causados por modificações acidentais.
- **Código mais limpo:** Torna o código mais fácil de entender e manter.
- **Melhora a concorrência:** Evita problemas de concorrência em ambientes multithread.
- **Facilita o teste:** Torna o código mais fácil de testar, pois o estado das coleções é mais previsível.
---
## Coleções Imutáveis
As coleções imutáveis são um conceito fundamental na programação funcional e cada vez mais valorizado em Java. **Uma coleção imutável é aquela que não pode ser alterada após sua criação.** Isso significa que você não pode adicionar, remover ou modificar elementos de uma coleção imutável.

### Por que usar coleções imutáveis?
- **Segurança:** Evita erros causados por modificações acidentais, especialmente em código concorrente.
- **Facilidade de raciocínio:** Torna o código mais previsível e fácil de entender, pois o estado da coleção é constante.
- **Melhora a performance:** Em alguns casos, coleções imutáveis podem oferecer melhor desempenho, especialmente em ambientes multithread.
- **Promove programação funcional:** Alimenta o paradigma de programação funcional, que enfatiza a imutabilidade e a pureza das funções.

### Como criar coleções imutáveis em Java?
Há várias maneiras de criar coleções imutáveis:
- **Métodos `of()`:** A partir do Java 9, as interfaces `List`, `Set` e `Map` possuem métodos estáticos `of()` para criar coleções imutáveis com um número fixo de elementos.
- **Métodos `copyOf()`:** Os métodos `copyOf()` em `Arrays` e `Collections` podem ser usados para criar arrays e coleções imutáveis a partir de coleções existentes.
- **Coleções não-modificáveis:** Como mencionado anteriormente, os métodos `unmodifiableList()`, `unmodifiableSet()` e `unmodifiableMap()` da classe `Collections` podem ser usados para criar vistas não-modificáveis de coleções existentes.

**Exemplo:**
```java
import java.util.*;

public class ColecoesImutaveis {
    public static void main(String[] args) {
        // Criando uma lista imutável
        List<String> linguagens = List.of("Java", "Python", "JavaScript");

        // Tentativa de adicionar um elemento (vai lançar UnsupportedOperationException)
        // linguagens.add("C#");

        // Criando um mapa imutável
        Map<String, Integer> idades = Map.of("João", 30, "Maria", 25);
    }
}
```

### Quando usar coleções imutáveis?
- **Dados de configuração:** Quando os dados não precisam ser alterados após a inicialização.
- **Resultados de cálculos:** Quando o resultado de um cálculo é uma coleção que não precisa ser modificada.
- **Parâmetros de métodos:** Ao passar coleções como parâmetros para métodos, usar coleções imutáveis ajuda a evitar efeitos colaterais.
- **Dados compartilhados:** Em ambientes multithread, as coleções imutáveis são mais seguras, pois não precisam de sincronização.

### Benefícios adicionais
- **Melhora a segurança de threads:** Coleções imutáveis são naturalmente thread-safe, pois não podem ser modificadas por múltiplas threads simultaneamente.
- **Facilita a depuração:** O estado imutável torna o código mais fácil de depurar, pois não há necessidade de rastrear mudanças inesperadas.
- **Promove um estilo de programação mais funcional:** O uso de coleções imutáveis incentiva um estilo de programação mais funcional, que é considerado mais conciso e elegante.
---