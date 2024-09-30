## Introdução às Classes Aninhadas em Java
Uma classe aninhada (ou _nested class_) é uma classe que é declarada dentro de outra classe. Essa estrutura oferece um alto grau de encapsulamento e permite organizar o código de forma mais lógica, especialmente quando classes possuem uma relação estreita.

**Tipos de Classes Aninhadas:**
Existem quatro tipos principais de classes aninhadas em Java:

1. **Classes Aninhadas Estáticas:**
       - Se comportam como classes normais, mas são membros da classe externa.
    - Não têm acesso a membros não estáticos da classe externa.
    - São criadas usando o modificador `static`.
    - **Exemplo:**
        ```java
        class Outer {
            static class Nested {
                // ...
            }
        }
        ```

2. **Classes Aninhadas Não Estáticas (Internas):**
       - Têm acesso a todos os membros da classe externa, incluindo os privados.
    - Cada instância da classe interna está associada a uma instância da classe externa.
    - **Exemplo:**
        ```java
        class Outer {
            class Inner {
                // ...
            }
        }
        ```

3. **Classes Locais:**
    - Declaradas dentro de um método ou bloco.
    - Têm acesso a variáveis finais e efetivamente finais do método ou bloco em que são declaradas.
    - **Exemplo:**
        ```java
        public void method() {
            class LocalClass {
                // ...
            }
        }
        ```

4. **Classes Anônimas:**
    - Não possuem nome e são declaradas diretamente no local onde são usadas, geralmente como implementação de uma interface ou extensão de uma classe.
    - **Exemplo:**
        ```java
        Button button = new Button("Click me");
        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e)    {
                // ...
            }
        });
        ```


**Quando Usar Classes Aninhadas?**
- **Encapsulamento:** Agrupar classes relacionadas em uma única classe externa.
- **Auxiliares:** Criar classes auxiliares que são específicas para uma classe externa.
- **Callbacks:** Implementar callbacks de forma concisa.
- **Adaptadores:** Criar adaptadores para diferentes interfaces.

**Vantagens:**
- **Organização:** Melhora a organização do código.
- **Reutilização:** Permite a reutilização de código dentro de uma classe.
- **Encapsulamento:** Aumenta o encapsulamento.
- **Leiturabilidade:** Em alguns casos, pode tornar o código mais legível.

**Desvantagens:**
- **Complexidade:** Pode tornar o código mais complexo de entender.
- **Performance:** Em alguns casos, pode ter um leve impacto na performance.

**Exemplo Prático:**
```java
class Outer {
    private int x = 10;

    class Inner {
        public void printX() {
            System.out.println(x); // Pode acessar x da classe externa
        }
    }
}
```
---
## Classes Aninhadas Estáticas
As classes aninhadas estáticas são um tipo especial de classe interna que reside dentro de outra classe, mas não têm associação direta com instâncias da classe externa. Isso significa que você pode criar objetos da classe aninhada estática sem precisar de uma instância da classe externa.

**Características Principais:**
- **Acesso a Membros Estáticos:** As classes aninhadas estáticas podem acessar diretamente os membros estáticos da classe externa, independentemente de sua visibilidade.
- **Sem Acesso a Membros Não Estáticos:** Não têm acesso a membros não estáticos da classe externa, pois não estão associadas a uma instância específica.
- **Criação:** Para criar uma instância de uma classe aninhada estática, você usa a sintaxe `NomeDaClasseExterna.NomeDaClasseAninhada`.
- **Utilização do Modificador `static`:** A palavra-chave `static` indica que a classe é estática e não está associada a uma instância da classe externa.

**Por que Usar Classes Aninhadas Estáticas?**
- **Organização:** Agrupar classes relacionadas logicamente dentro de uma classe externa.
- **Encapsulamento:** Esconder a implementação de classes auxiliares dentro da classe principal.
- **Auxiliares:** Criar classes auxiliares que são específicas para uma classe externa, mas não precisam de acesso a seus membros não estáticos.
- **Melhoria da Leiturabilidade:** Em alguns casos, pode tornar o código mais fácil de entender.

**Exemplo Prático:**
```java
class Outer {
    private int x = 10; // Membro não estático

    static class Nested {
        public static void printMessage() {
            // System.out.println(x); // Erro: x é não estático
            System.out.println("Mensagem da classe aninhada estática");
        }
    }
}
```

**Quando Usar Classes Aninhadas Estáticas?**

- **Classes Utilitárias:** Para criar classes que fornecem métodos utilitários relacionados à classe externa.
- **Constantes:** Para definir constantes relacionadas à classe externa.
- **Enumerações:** Para criar enumerações específicas para a classe externa.
- **Factory Methods:** Para implementar padrões de fábrica.

**Comparação com Classes Aninhadas Não Estáticas:**

|Característica|Classes Aninhadas Estáticas|Classes Aninhadas Não Estáticas|
|---|---|---|
|Acesso a membros da classe externa|Apenas membros estáticos|Todos os membros, incluindo privados|
|Criação de instâncias|Sem necessidade de instância da classe externa|Necessita de uma instância da classe externa|
|Associação com a classe externa|Não há associação direta|Cada instância está associada a uma instância da classe externa|

**Considerações Adicionais:**

- **Nomeação:** É comum usar nomes descritivos para as classes aninhadas estáticas, como `Outer.Inner`.
- **Performance:** O uso de classes aninhadas estáticas geralmente não tem um impacto significativo na performance.
- **Design:** Ao decidir se uma classe deve ser aninhada estática, considere o nível de acoplamento entre as classes e a necessidade de acesso aos membros da classe externa.
---
## Modificadores de Acesso em Classes Aninhadas em Java
**Os modificadores de acesso em classes aninhadas em Java funcionam de forma um pouco diferente das classes normais.** Isso se deve à relação especial entre a classe externa e a classe aninhada.

### Níveis de Acesso e Classes Aninhadas

| Modificador                   | Visibilidade                                                          | Observações                                                                                   |
| ----------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **public**                    | Visível em qualquer lugar.                                            | Pode ser acessada de qualquer parte do programa.                                              |
| **protected**                 | Visível dentro da mesma classe, subclasses e classes do mesmo pacote. | As subclasses da classe externa também podem acessar as classes aninhadas protegidas.         |
| **default** (sem modificador) | Visível dentro do mesmo pacote.                                       | As classes aninhadas default são visíveis apenas dentro do mesmo pacote que a classe externa. |
| **private**                   | Visível apenas dentro da classe externa.                              | Somente a classe externa pode acessar a classe aninhada privada.                              |
### Considerações Específicas
- **Classes Aninhadas Estáticas:**
    - Se comportam como classes normais em relação aos modificadores de acesso.
    - A visibilidade é determinada pelo modificador de acesso da classe aninhada estática.
- **Classes Aninhadas Não Estáticas:**
    - Mesmo sendo privadas, as classes aninhadas não estáticas têm acesso a todos os membros da classe externa, incluindo os privados.
    - A visibilidade da classe aninhada não estática para o mundo externo é determinada pelo seu modificador de acesso.

### Exemplo
```java
class Outer {
    private int x = 10;

    public class PublicInner {
        public void printX() {
            System.out.println(x);
        }
    }

    private class PrivateInner {
        private void printX() {
            System.out.println(x);
        }
    }
}
```

- **PublicInner:** Visível em qualquer lugar, pode ser acessada fora da classe `Outer`.
- **PrivateInner:** Visível apenas dentro da classe `Outer`.

### Quando Usar Qual Modificador?
- **public:** Quando a classe aninhada precisa ser acessada por outras classes fora do pacote.
- **protected:** Quando a classe aninhada precisa ser acessada por subclasses da classe externa ou por classes no mesmo pacote.
- **default:** Quando a classe aninhada é um detalhe de implementação e não precisa ser acessada de fora do pacote.
- **private:** Quando a classe aninhada é um helper para a classe externa e não precisa ser acessada de fora.

---
## Enums como Membros Estáticos de uma Classe em Java
Enums, ou enumerações, são tipos de dados que representam um conjunto fixo de constantes. Em Java, eles são implementados como classes e são frequentemente utilizados para representar valores que podem assumir apenas um conjunto limitado de opções.

**Por que Usar Enums como Membros Estáticos?**
- **Organização:** Agrupar constantes relacionadas a uma classe específica dentro de um enum, tornando o código mais organizado e legível.
- **Tipo Seguro:** Ao usar um enum, você garante que o valor atribuído a uma variável seja sempre um dos valores definidos no enum, evitando erros de digitação.
- **Reutilização:** Um enum pode ser reutilizado em diferentes partes do código, promovendo a consistência.

**Exemplo:**
```java
public class Planeta {
    public enum Tamanho { PEQUENO, MÉDIO, GRANDE }

    private Tamanho tamanho;

    // ... outros métodos e atributos
}
```

Neste exemplo, o enum `Tamanho` está aninhado dentro da classe `Planeta`. Ele define os possíveis tamanhos de um planeta. A classe `Planeta` possui um atributo `tamanho` do tipo `Tamanho`.

**Como Acessar os Valores de um Enum:**
```java
Planeta terra = new Planeta();
terra.tamanho = Planeta.Tamanho.MÉDIO;
```

**Vantagens:**
- **Clareza:** Torna o código mais claro e autodocumentado.
- **Segurança:** Evita erros de digitação ao trabalhar com valores fixos.
- **Extensibilidade:** É possível adicionar novos valores ao enum sem alterar as classes que o utilizam.
- **Facilidade de uso:** Os enums podem ser usados em switch-case, como valores de parâmetros de métodos, etc.

**Considerações Adicionais:**
- **Herança:** Enums não podem herdar de outras classes nem ser herdados.
- **Construtores:** Enums possuem construtores privados, que são utilizados para inicializar os valores das constantes.
- **Métodos:** Enums podem ter métodos, o que permite adicionar funcionalidades personalizadas aos seus valores.

**Quando Usar Enums?**
- **Dias da semana:** `enum DiaSemana { SEGUNDA, TERÇA, QUARTA, ... }`
- **Estados de um objeto:** `enum Estado { ATIVO, INATIVO, PAUSADO }`
- **Tipos de dados:** `enum TipoDado { INTEIRO, REAL, STRING }`
- **Direções:** `enum Direcao { NORTE, SUL, LESTE, OESTE }`
---
## Classes Aninhadas Não-Estáticas
As classes aninhadas não-estáticas, também conhecidas como classes internas, são classes declaradas dentro de outra classe. Ao contrário das classes aninhadas estáticas, elas possuem uma forte ligação com a classe externa, tendo acesso a todos os seus membros, inclusive os privados.

**Características Principais:**
- **Associação:** Cada instância de uma classe interna está associada a uma instância específica da classe externa.
- **Acesso a Membros:** As classes internas podem acessar diretamente todos os membros da classe externa, incluindo os membros privados.
- **Criação:** Para criar uma instância de uma classe interna, você precisa primeiro ter uma instância da classe externa.
- **Não são Independentes:** As classes internas não podem existir por si só, elas sempre estão associadas a uma classe externa.

**Exemplo:**
```java
class Outer {
    private int x = 10;

    class Inner {
        public void printX() {
            System.out.println(x); // Pode acessar x da classe externa
        }
    }
}
```

**Quando Usar Classes Aninhadas Não-Estáticas?**
- **Helper Classes:** Criar classes auxiliares que são específicas para uma classe externa e que precisam acessar seus membros privados.
- **Callbacks:** Implementar callbacks de forma concisa.
- **Adaptadores:** Criar adaptadores para diferentes interfaces.
- **Eventos:** Lidar com eventos de componentes gráficos.

**Tipos de Classes Aninhadas Não-Estáticas:**
- **Classes internas de instância:** As mais comuns, associadas a uma instância específica da classe externa.
- **Classes internas locais:** Declaradas dentro de um método ou bloco.
- **Classes internas anônimas:** Não possuem nome e são criadas diretamente no local onde são usadas.

**Vantagens:**
- **Encapsulamento:** Permite encapsular classes relacionadas dentro de uma classe externa.
- **Reutilização:** Pode ser reutilizada dentro da classe externa.
- **Acesso a membros privados:** Permite acessar membros privados da classe externa.
- **Flexibilidade:** Oferece maior flexibilidade na organização do código.

**Desvantagens:**
- **Complexidade:** Pode tornar o código mais complexo de entender.
- **Acoplamento:** Aumenta o acoplamento entre a classe interna e a classe externa.

**Comparação com Classes Aninhadas Estáticas:**

|Característica|Classes Aninhadas Não-Estáticas|Classes Aninhadas Estáticas|
|---|---|---|
|Associação com a classe externa|Fortemente associada|Não há associação direta|
|Acesso a membros|Todos os membros, incluindo privados|Apenas membros estáticos|
|Criação de instâncias|Necessita de uma instância da classe externa|Não precisa de uma instância da classe externa|

---
## Shadowing em Classes Aninhadas
Shadowing ocorre quando uma variável com o mesmo nome é declarada em um escopo interno, ocultando a variável com o mesmo nome em um escopo externo.

**Shadowing em Classes Aninhadas:**
Em classes aninhadas, o shadowing pode ocorrer entre variáveis da classe externa e da classe aninhada, ou entre variáveis de diferentes classes aninhadas.

**Exemplo:**
```java
class Outer {
    int x = 10;

    class Inner {
        int x = 20;

        void printX() {
            System.out.println(x); // Imprime 20 (shadowing)
        }
    }
}
```

Neste exemplo, a variável `x` da classe `Inner` oculta (ou "shadowa") a variável `x` da classe `Outer`. Quando o método `printX` é chamado, ele imprime o valor de `x` da classe `Inner`.

**Regras para Shadowing em Classes Aninhadas:**
- **Visibilidade:** A variável que está sendo ocultada deve ser visível no escopo interno.
- **Tipo:** A variável que está sendo ocultada e a variável que a oculta devem ter o mesmo tipo ou um tipo compatível.
- **Acesso:** Se a variável externa é privada, a classe aninhada não pode acessá-la diretamente. No entanto, pode acessá-la através de métodos públicos ou protegidos da classe externa.

**Quando Evitar Shadowing:**
- **Confusão:** Shadowing pode tornar o código mais difícil de entender, especialmente se as variáveis têm nomes semelhantes.
- **Erros:** Se não for cuidadoso, o shadowing pode levar a erros.

**Quando Usar Shadowing:**
- **Encapsulamento:** Em alguns casos, o shadowing pode ser útil para encapsular variáveis locais dentro de uma classe aninhada, tornando-as mais privadas e menos propensas a erros.
- **Claridade:** Em alguns casos, o shadowing pode tornar o código mais claro, especialmente se as variáveis têm nomes diferentes e seus significados são distintos.
---
## Classes Locais
Classes locais são classes que são declaradas dentro de um método, construtor ou bloco de inicialização. Elas possuem algumas características e restrições específicas:

- **Escopo:** Uma classe local só é visível dentro do bloco em que foi declarada.
- **Acesso a Variáveis:** As classes locais podem acessar as variáveis finais (ou efetivamente finais) do método ou bloco em que foram declaradas.
- **Modificadores de Acesso:** Classes locais não podem ter modificadores de acesso (public, private, protected).

### Quando Usar Classes Locais?
- **Classes Auxiliares:** Criar classes auxiliares que são específicas para uma determinada operação dentro de um método.
- **Callbacks:** Implementar callbacks de forma concisa.
- **Adaptadores:** Criar adaptadores para diferentes interfaces dentro de um método.

#### Exemplo:
```java
public class Exemplo {
    public void meuMetodo() {
        class ClasseLocal {
            public void imprimirMensagem() {
                System.out.println("Esta é uma classe local");
            }
        }

        ClasseLocal objetoLocal = new ClasseLocal();
        objetoLocal.imprimirMensagem();
    }
}
```

### Restrições e Considerações:
- **Variáveis Finais:** As classes locais só podem acessar variáveis finais ou efetivamente finais do método ou bloco em que foram declaradas. Isso significa que o valor dessas variáveis não pode ser alterado após a declaração da classe local.
- **Modificadores de Acesso:** Como mencionado, classes locais não podem ter modificadores de acesso, o que limita sua visibilidade ao bloco em que foram declaradas.
- **Uso Moderado:** Embora sejam úteis em algumas situações, o uso excessivo de classes locais pode tornar o código mais difícil de entender e manter.

### Comparação com Outras Classes Aninhadas:

|Tipo de Classe|Local de Declaração|Acesso a Membros Externos|Modificadores de Acesso|
|---|---|---|---|
|**Estática**|Dentro de uma classe|Apenas membros estáticos|Possíveis|
|**Não Estática**|Dentro de uma classe|Todos os membros|Possíveis|
|**Local**|Dentro de um método/bloco|Variáveis finais/efetivamente finais|Não permitidos|
### Por que Usar Classes Locais?
- **Encapsulamento:** Ajudam a encapsular a lógica dentro de um método.
- **Reutilização:** Podem ser reutilizadas dentro do método em que foram declaradas.
- **Flexibilidade:** Oferecem flexibilidade para criar classes auxiliares específicas para uma determinada tarefa.
---
## Classes Anônimas
As classes anônimas são um tipo especial de classes internas que não possuem um nome explícito. Elas são declaradas e instanciadas em uma única linha de código, geralmente como um argumento para um método ou como uma expressão.

**Sintaxe Básica:**
```java
novo Tipo() {
    // Corpo da classe anônima
};
```

**Quando Usar Classes Anônimas?**
- **Implementando Interfaces:** Quando você precisa criar um objeto que implementa uma interface e você só precisa usar essa implementação em um único lugar.
- **Extendendo Classes Abstratas:** Quando você precisa criar um objeto que estende uma classe abstrata e você só precisa usar essa implementação em um único lugar.
- **Callbacks:** Para passar um objeto que implementa uma interface como um callback para outro método.

**Exemplo:**
```java
// Criando um objeto Runnable de forma anônima
Runnable tarefa = new Runnable() {
    @Override
    public void run() {
        System.out.println("Tarefa sendo executada");
    }
};

// Passando o objeto Runnable para um método
new Thread(tarefa).start();
```

**Vantagens:**
- **Concisão:** Permitem escrever código mais conciso, especialmente quando a classe é usada apenas uma vez.
- **Flexibilidade:** Podem ser usadas para implementar interfaces e estender classes abstratas.
- **Callbacks:** São ideais para implementar callbacks de forma concisa.

**Desvantagens:**
- **Legibilidade:** O código pode se tornar menos legível, especialmente se a classe anônima for muito grande ou complexa.
- **Reutilização:** Como não possuem um nome, não podem ser reutilizadas em outros lugares do código.
- **Depuração:** Podem dificultar a depuração, pois não possuem um nome para serem referenciadas.

**Comparação com Classes Locais:**

|Característica|Classe Local|Classe Anônima|
|---|---|---|
|Nome|Possui nome|Não possui nome|
|Escopo|Dentro de um método/bloco|Dentro de uma expressão|
|Reutilização|Pode ser reutilizada dentro do método|Não pode ser reutilizada|
**Quando Escolher Classes Anônimas?**
- **Callbacks simples:** Quando você precisa passar um objeto que implementa uma interface simples como um callback.
- **Inicializadores:** Para inicializar coleções com objetos personalizados.
- **Eventos:** Para lidar com eventos de componentes gráficos.

**Exemplo com Interface:**
```java
List<String> nomes = Arrays.asList("Ana", "Pedro", "João");
Collections.sort(nomes, new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return s1.compareToIgnoreCase(s2);   
    }
});
```

**Considerações:**
- **Lambdas:** A partir do Java 8, as expressões lambda oferecem uma sintaxe mais concisa para criar classes anônimas em muitos casos.
- **Interfaces Funcionais:** As interfaces funcionais são interfaces com apenas um método abstrato e são ideais para serem usadas com lambdas e classes anônimas.
---