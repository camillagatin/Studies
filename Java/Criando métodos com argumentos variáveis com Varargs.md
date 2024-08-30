```java
public class Fatura {

    int numero;
    double valorTotal;

}
```

```java
import java.util.Arrays;

public class ServicoDeCobranca {

    void pagar(Fatura fatura, String... emailsCobranca) {
//        System.out.println(Arrays.toString(emailsCobranca));

        System.out.printf("Fatura %d, no valor total de R$%.2f, foi paga!%n",
                fatura.numero, fatura.valorTotal);

        for (String email : emailsCobranca) {
            System.out.printf("Fatura %d enviada para %s%n", fatura.numero, email);
        }
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Fatura fatura = new Fatura();
        fatura.numero = 123;
        fatura.valorTotal = 1_293.55;

        ServicoDeCobranca servicoDeCobranca = new ServicoDeCobranca();

//        String[] emailsCobranca = {"joao@algaworks.com", "maria@algaworks.com"};
//        servicoDeCobranca.pagar(fatura, emailsCobranca);

//        servicoDeCobranca.pagar(fatura,
//                new String[]{"joao@algaworks.com", "maria@algaworks.com"});

//        servicoDeCobranca.pagar(fatura, new String[0]);
//        servicoDeCobranca.pagar(fatura, new String[]{});

        servicoDeCobranca.pagar(fatura, "joao@algaworks.com", "maria@algaworks.com");
//        servicoDeCobranca.pagar(fatura);
    }

}
```

---
## Boas práticas: Use varargs com cuidado
Fatura.java

```java
import java.util.Objects;

public class ServicoDeCobranca {

    void pagar(Fatura fatura, String emailCobranca, String... emailsAdicionais) {
        Objects.requireNonNull(fatura, "Informe a fatura");
        Objects.requireNonNull(emailCobranca, "Informe o e-mail cobrança");

        System.out.printf("Fatura %d, no valor total de R$%.2f, foi paga!%n",
                fatura.numero, fatura.valorTotal);

        enviarNotificacao(fatura, emailCobranca);

        for (String email : emailsAdicionais) {
            enviarNotificacao(fatura, email);
        }
    }

    private void enviarNotificacao(Fatura fatura, String email) {
        System.out.printf("Fatura %d enviada para %s%n", fatura.numero, email);
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Fatura fatura = new Fatura();
        fatura.numero = 123;
        fatura.valorTotal = 1_293.55;

        ServicoDeCobranca servicoDeCobranca = new ServicoDeCobranca();

        // Não compila
        // servicoDeCobranca.pagar(fatura);

        // Compila
        // servicoDeCobranca.pagar(fatura, "joao@algaworks.com");

        // Compila
        servicoDeCobranca.pagar(fatura, "joao@algaworks.com",
                "maria@algaworks.com", "jose@algaworks.com");
    }

}
```