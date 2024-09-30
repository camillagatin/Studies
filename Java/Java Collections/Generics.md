## O que são Generics?
Generics, introduzidos no Java 5, são uma ferramenta poderosa para escrever código mais seguro, flexível e reutilizável. Eles permitem que você crie classes e métodos que podem trabalhar com diferentes tipos de dados, sem a necessidade de fazer casting manualmente.

**Por que usar Generics?**
- **Tipo segurança:** Evita erros de tempo de execução causados por tipos incompatíveis.
- **Reutilização de código:** Permite criar classes e métodos genéricos que podem ser usados com diversos tipos.
- **Melhora a legibilidade do código:** Torna o código mais claro e conciso.

## Sintaxe Básica
A sintaxe dos generics envolve o uso de símbolos angulares `<>` para especificar o tipo genérico.
```java
// Classe genérica
public class Caixa<T> {
    private T objeto;

    public void set(T objeto) {
        this.objeto = objeto;
    }

    public T get() {
        return objeto;
    }
}
```
No exemplo acima, `T` é um tipo genérico que pode ser substituído por qualquer tipo de dado quando a classe `Caixa` for instanciada.

## Usando Generics
```java
Caixa<String> caixaDeString = new Caixa<>();
caixaDeString.set("Olá, mundo!");
String mensagem = caixaDeString.get();

Caixa<Integer> caixaDeInteiro = new Caixa<>();
caixaDeInteiro.set(42);
int numero = caixaDeInteiro.get();
```

## Limitações de Tipos
É possível limitar os tipos que podem ser usados com um genérico utilizando:
- **Bounds:** Especifica um limite superior ou inferior para o tipo genérico.
- **Wildcards:** Permite usar tipos mais genéricos sem especificar o tipo exato.

```java
// Bound superior
public class Numero<T extends Number> {
    // ...
}

// Wildcard com bound inferior
public void imprimirLista(List<? extends Number> lista) {
    // ...
}
```

## Generics e Coleções
Generics são amplamente utilizados com as coleções do Java, como `List`, `Set` e `Map`.
```java
List<String> nomes = new ArrayList<>();
nomes.add("João");
nomes.add("Maria");
```

## Generics e Métodos
Métodos também podem ser genéricos:
```java
public static <T> void imprimirArray(T[] array) {
    for (T elemento : array) {
        System.out.println(elemento);
    }
}
```

## Considerações Adicionais
- **Type Erasure:** O compilador Java remove a informação de tipo genérico em tempo de execução.
- **Boxing e Unboxing:** Ao usar generics com tipos primitivos, ocorre o processo de boxing e unboxing.
- **Generics e Herança:** A herança com generics pode ser complexa e requer um cuidado especial.