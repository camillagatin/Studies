Enbrulham o tipo primitivo dentro delas para poderem ser tratados como objeto

Podem atribuir o null (que fica como padrão) , enquanto os primitivos (int, double...) não podem

| primitivo | classe wrapper |
| --------- | -------------- |
| int       | Integer        |
| double    | Double         |
| float     | Float          |
| long      | Long           |
| short     | Short          |
| char      | Character      |
| boolean   | Boolean        |

Cliente.java
```java
String nome;
Integer idade;
Double rendaMensal;
```

Principal1.java
```java
public static void main(String[] args) {
    // tipos primitivos
    int diasParaEntrega;
    long codigoEntrega;
    float valorFrete;
    double valorTotal;
    char tipoCliente;
    boolean compraPaga;

    // String é uma classe
    String nomeCliente;
}
```

Principal2.java
```java
public static void main(String[] args) {
	Cliente cliente = new Cliente();
    cliente.idade = Integer.valueOf(20);
    //cliente.idade = Integer.valueOf("25"); → consegue converter
	//cliente.idade = Integer.valueOf("vinte"); → lança uma exceção (erro de conversão)

    System.out.printf("Idade: %d%n", cliente.idade);
}

```

---
## Métodos de Conversão

```java
int idade = 20;
short idadeShort = (short) idade; // → cast

Integer diasEntrega = Integer.valueOf(30);

Short diasEntregaShort = Short.valueOf(diasEntrega.shortValue());

Long diasEntregaLong = Long.valueOf(diasEntrega.longValue());

Double valorTotal = Double.valueOf(1500.2);
int valorTotalInt = valorTotal.intValue();
System.out.println(valorTotalInt);
```

---
## Autoboxing e Unboxing
Quando for atribuir um valor tipo wrapper não é preciso utilizar desta maneira "`Integer diasEntrega = Integer.valueOf(30);`" pois a linguagem já faz um "autoboxing".

```java
// autoboxing
Integer diasEntrega = 30;
// unboxing
int diasEntregaInt = diasEntrega;
```

---
## Comparando Wrappers

compara o valor da variável
```java
int numero1 = 128;
int numero2 = 128;
System.out.println(numero1 == numero2);
```
...........................................................................
nos wrappers as variáveis referenciam objetos em memória
quando a comparação (`numero1 == numero2`) é feita, não é o valor da variável que é comparado e sim o endereço da memória
```java
Integer numero1 = 128;
Integer numero2 = 128;
Short numero3 = 128;

//comparação dos valores
System.out.println(numero1.equals(numero2));
System.out.println(numero1.intValue() == numero3.intValue());
```

