## Remova referências de objetos não usados

```java
public class Cliente {

    String nome;
//    byte[] x = new byte[500 * 1024 * 1024];

}
```

```java
import java.util.Arrays;

public class Pilha {

    static final int CAPACIDADE_INICIAL_PADRAO = 4;

    Cliente[] elementos = new Cliente[CAPACIDADE_INICIAL_PADRAO];
    int tamanho = 0;

    void adicionar(Cliente elemento) {
        garantirCapacidade();
        elementos[tamanho++] = elemento;
    }

    Cliente retirar() {
        if (tamanho == 0) {
            // seria melhor lançar exception (mas ainda não aprendemos isso)
            return null;
        }

        Cliente elemento = elementos[--tamanho];
        elementos[tamanho] = null;
        return elemento;

//        return elementos[--tamanho];
    }

    void imprimirEstatisticas() {
        System.out.printf("Tamanho atual: %d%n", tamanho);
        System.out.printf("Capacidade: %d%n%n", elementos.length);
    }

    private void garantirCapacidade() {
        if (elementos.length == tamanho) {
            elementos = Arrays.copyOf(elementos, tamanho + 10);
        }
    }

}
```

```java
public class Teste1 {

    public static void main(String[] args) {
        Cliente cliente1 = new Cliente();
        Cliente cliente2 = new Cliente();
        cliente1.nome = "João";
        cliente2.nome = "Maria";

        Pilha pilha = new Pilha();
        pilha.adicionar(cliente1);
        pilha.adicionar(cliente2);

        pilha.imprimirEstatisticas();

        Cliente clienteRetirado = pilha.retirar();
        System.out.println(clienteRetirado.nome);

        clienteRetirado = pilha.retirar();
        System.out.println(clienteRetirado.nome);

        clienteRetirado = pilha.retirar();
        System.out.println(clienteRetirado.nome);

        pilha.imprimirEstatisticas();
    }

}
```

```java
public class Teste2 {

    public static void main(String[] args) {
        Pilha pilha = new Pilha();
        pilha.imprimirEstatisticas();

        pilha.adicionar(new Cliente());
        pilha.adicionar(new Cliente());
        pilha.adicionar(new Cliente());
        pilha.adicionar(new Cliente());
        pilha.adicionar(new Cliente());
        pilha.adicionar(new Cliente());

        Cliente clienteRetirado = null;

        do {
            clienteRetirado = pilha.retirar();
            pilha.imprimirEstatisticas();
        } while (clienteRetirado != null);

        Cliente c1 = new Cliente();
        Cliente c2 = new Cliente();
        Cliente c3 = new Cliente();
    }

}
```
