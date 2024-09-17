```java
public class Cliente {

    byte[] x = new byte[500 * 1024 * 1024];
    Endereco endereco;

}
```

```java
public class Endereco {

    byte[] x = new byte[500 * 1024 * 1024];
    Cliente cliente;

}
```

```java
public class Teste1 {

    public static void main(String[] args) {
        imprimirUsoMemoria();

        byte[] x = new byte[500 * 1024 * 1024];
        imprimirUsoMemoria();
        x = null;

        System.gc();

        imprimirUsoMemoria();
    }

    static void imprimirUsoMemoria() {
        System.out.printf("Máxima: %s%n",
                emMegabytes(Runtime.getRuntime().maxMemory()));

        System.out.printf("Total empenhada: %s%n",
                emMegabytes(Runtime.getRuntime().totalMemory()));

        System.out.printf("Disponível: %s%n",
                emMegabytes(Runtime.getRuntime().freeMemory()));

        long memoriaUsada = Runtime.getRuntime().totalMemory()
                - Runtime.getRuntime().freeMemory();
        System.out.printf("Usada: %s%n", emMegabytes(memoriaUsada));

        System.out.println("---");
    }

    static String emMegabytes(long bytes) {
        return String.format("%.2fMB", bytes / 1024d / 1024d);
    }

}
```

```java
public class Teste2 {

    public static void main(String[] args) {
        imprimirUsoMemoria();

        byte[] x = new byte[500 * 1024 * 1024];
        byte[] y = new byte[500 * 1024 * 1024];

        imprimirUsoMemoria();

        x = y;

        System.gc();

        imprimirUsoMemoria();
    }

    static void imprimirUsoMemoria() {
        System.out.printf("Máxima: %s%n",
                emMegabytes(Runtime.getRuntime().maxMemory()));

        System.out.printf("Total empenhada: %s%n",
                emMegabytes(Runtime.getRuntime().totalMemory()));

        System.out.printf("Disponível: %s%n",
                emMegabytes(Runtime.getRuntime().freeMemory()));

        long memoriaUsada = Runtime.getRuntime().totalMemory()
                - Runtime.getRuntime().freeMemory();
        System.out.printf("Usada: %s%n", emMegabytes(memoriaUsada));

        System.out.println("---");
    }

    static String emMegabytes(long bytes) {
        return String.format("%.2fMB", bytes / 1024d / 1024d);
    }

}
```

```java
public class Teste3 {

    public static void main(String[] args) {
        imprimirUsoMemoria();

        criarObjeto();

        imprimirUsoMemoria();

        System.gc();

        imprimirUsoMemoria();
    }

    static void criarObjeto() {
        byte[] x = new byte[500 * 1024 * 1024];
    }

    static void imprimirUsoMemoria() {
        System.out.printf("Máxima: %s%n",
                emMegabytes(Runtime.getRuntime().maxMemory()));

        System.out.printf("Total empenhada: %s%n",
                emMegabytes(Runtime.getRuntime().totalMemory()));

        System.out.printf("Disponível: %s%n",
                emMegabytes(Runtime.getRuntime().freeMemory()));

        long memoriaUsada = Runtime.getRuntime().totalMemory()
                - Runtime.getRuntime().freeMemory();
        System.out.printf("Usada: %s%n", emMegabytes(memoriaUsada));

        System.out.println("---");
    }

    static String emMegabytes(long bytes) {
        return String.format("%.2fMB", bytes / 1024d / 1024d);
    }

}
```

```java
public class Teste4 {

    public static void main(String[] args) {
        imprimirUsoMemoria();

        new Cliente();

        imprimirUsoMemoria();

        System.gc();

        imprimirUsoMemoria();
    }

    static void imprimirUsoMemoria() {
        System.out.printf("Máxima: %s%n",
                emMegabytes(Runtime.getRuntime().maxMemory()));

        System.out.printf("Total empenhada: %s%n",
                emMegabytes(Runtime.getRuntime().totalMemory()));

        System.out.printf("Disponível: %s%n",
                emMegabytes(Runtime.getRuntime().freeMemory()));

        long memoriaUsada = Runtime.getRuntime().totalMemory()
                - Runtime.getRuntime().freeMemory();
        System.out.printf("Usada: %s%n", emMegabytes(memoriaUsada));

        System.out.println("---");
    }

    static String emMegabytes(long bytes) {
        return String.format("%.2fMB", bytes / 1024d / 1024d);
    }

}
```

```java
public class Teste5 {

    public static void main(String[] args) {
        imprimirUsoMemoria();

        Cliente cliente = new Cliente();
        Endereco endereco = new Endereco();

        cliente.endereco = endereco;
        endereco.cliente = cliente;

        cliente = null;
        endereco = null;

        imprimirUsoMemoria();

        System.gc();

        imprimirUsoMemoria();
    }

    static void imprimirUsoMemoria() {
        System.out.printf("Máxima: %s%n",
                emMegabytes(Runtime.getRuntime().maxMemory()));

        System.out.printf("Total empenhada: %s%n",
                emMegabytes(Runtime.getRuntime().totalMemory()));

        System.out.printf("Disponível: %s%n",
                emMegabytes(Runtime.getRuntime().freeMemory()));

        long memoriaUsada = Runtime.getRuntime().totalMemory()
                - Runtime.getRuntime().freeMemory();
        System.out.printf("Usada: %s%n", emMegabytes(memoriaUsada));

        System.out.println("---");
    }

    static String emMegabytes(long bytes) {
        return String.format("%.2fMB", bytes / 1024d / 1024d);
    }

}
```

