## Padrão Decorator em Java: Adicionando funcionalidades dinamicamente

O **padrão Decorator** é um dos padrões de projeto estruturais mais utilizados em Java. Ele permite adicionar novas funcionalidades a um objeto em tempo de execução, sem a necessidade de modificar a classe original. Essa flexibilidade é alcançada através da criação de objetos wrapper, chamados de decoradores, que encapsulam o objeto original e adicionam seu próprio comportamento.

**Quando usar o Decorator:**
- **Adicionar responsabilidades a objetos de forma dinâmica:** Quando você precisa adicionar comportamentos específicos a objetos em tempo de execução, sem alterar a sua classe base.
- **Customizar objetos de forma flexível:** O Decorator permite criar diversas combinações de decoradores para personalizar um objeto de acordo com as necessidades do momento.
- **Evitar a explosão de subclasses:** Se você precisasse criar subclasses para cada combinação de funcionalidades, a hierarquia de classes se tornaria complexa e difícil de manter. O Decorator permite adicionar novas funcionalidades sem criar novas subclasses.

**Como funciona:**
1. **Interface Comum:** Tanto o objeto a ser decorado quanto os decoradores implementam uma mesma interface.
2. **Encapsulamento:** Um decorador possui uma referência ao objeto que ele está decorando.
3. **Delegação:** Quando um método é chamado em um decorador, ele geralmente delega a chamada para o objeto que está decorando e pode adicionar seu próprio comportamento antes ou depois.

**Exemplo prático:**
Imagine que você está desenvolvendo um sistema de bebidas. Você tem uma classe `Bebida` e deseja adicionar funcionalidades como `adicionarAçúcar`, `adicionarGelo` e `adicionarCanudo`. Em vez de criar subclasses para cada combinação possível, você pode usar o Decorator:
```java
interface Bebida {
    String getDescricao();
    double getCusto();
}

class Espresso implements Bebida {
    @Override
    public String getDescricao() {
        return "Espresso";
    }

    @Override
    public double getCusto() {
        return 1.99;
    }
}

abstract class Decorator implements Bebida {
    protected Bebida bebida;

    public Decorator(Bebida bebida) {
        this.bebida = bebida;
    }

    @Override
    public String getDescricao() {
        return bebida.getDescricao();
    }

    @Override
    public    double getCusto() {
        return bebida.getCusto();
    }
}

class AdicionarAcucar extends Decorator {
    public AdicionarAcucar(Bebida bebida) {
        super(bebida);
    }

    @Override
    public String getDescricao() {
        return bebida.getDescricao() + ", com açúcar";
    }

    @Override
    public double getCusto() {
        return bebida.getCusto() + 0.20;
    }
}

// ... outros decoradores como AdicionarGelo, AdicionarCanudo

public class ExemploDecorator {
    public static void main(String[] args) {
        Bebida espresso = new Espresso();
        Bebida espressoComAcucar = new AdicionarAcucar(espresso);
        System.out.println(espressoComAcucar.getDescricao()); // Imprime: Espresso, com açúcar
        System.out.println(espressoComAcucar.getCusto()); // Imprime: 2.19
    }
}
```

**Vantagens do Decorator:**
- **Flexibilidade:** Permite adicionar funcionalidades de forma dinâmica e em tempo de execução.
- **Reutilização:** Os decoradores podem ser reutilizados em diferentes contextos.
- **Extensibilidade:** É fácil adicionar novos decoradores sem modificar o código existente.
- **Melhora a coesão:** Cada classe tem uma única responsabilidade.

**Desvantagens do Decorator:**
- **Complexidade:** Pode tornar o código mais complexo, especialmente com muitos decoradores aninhados.
- **Desempenho:** A criação de múltiplos objetos pode ter um impacto no desempenho.