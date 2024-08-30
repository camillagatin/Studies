CarrinhdeCompra.java
```java
import java.util.Objects;

public class CarrinhoDeCompra {

    Produto produto;
    int quantidadeItens;

    void adicionarItem(Produto produto, int quantidade) {
        Objects.requireNonNull(produto, "Produto deve ser informado");

        if (quantidade <= 0) {
            throw new IllegalArgumentException("Quantidade deve ser maior que 0");
        }

        System.out.printf("Produto: %s%n", produto.nome);

        // TODO implementar
    }

    void gerarPedido(Endereco enderecoEntrega) {
        Objects.requireNonNull(enderecoEntrega, "Endereço de entrega deve ser informado");

        criarNovoPedido(enderecoEntrega);
    }

    void gerarPedido() {
        criarNovoPedido(null);
    }

    // método interno (vamos estudar sobre private em breve)
    private void criarNovoPedido(Endereco enderecoEntrega) {
        // TODO implementar
    }

}
```

Endereco.java
```java
public class Endereco {

    String logradouro;
    String numero;
    String bairro;

}
```

Produto.java
```java
public class Produto {

    String nome;
    double precoUnitario;

}
```

Principal.java
```java
public class Principal {

    public static void main(String[] args) {
        CarrinhoDeCompra carrinho = new CarrinhoDeCompra();

        Produto produto = new Produto();
        produto.nome = "Água";
        produto.precoUnitario = 5;

        carrinho.adicionarItem(produto, 4);

        Endereco endereco = new Endereco();
        endereco.logradouro = "Rua das Amoras";
        endereco.numero = "1000";
        endereco.bairro = "Centro";

        carrinho.gerarPedido();

        System.out.println("Pedido gerado");
    }

}
```