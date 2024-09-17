Toda a estrutura de código, na linguagem Java é distribuído em arquivos, com extensão **.java** denominados de **classe**.

As classes existentes em nosso projeto, serão composta por:

**Identificador**, **Características** e **Comportamentos**.

- **Classe** _(class)_: A estrutura e/ou representação que direciona a criação dos objetos de mesmo tipo.
- **Identificador** (identity): Propósito existencial aos objetos que serão criados.
- **Características** _(states)_**:** Também conhecido como **atributos** ou **propriedades**, é toda informação que representa o estado do objeto.
- **Comportamentos** _(behavior)_**:** Também conhecido como **ações** ou **métodos**, é toda parte comportamental que um objeto dispõe.
- **Instanciar** _(new)_**:** É o ato de criar um objeto a partir de estrutura, definida em uma classe.

![[Pasted image 20240626203218.png|500]]
Exmplo da imagem acima:
```java
// Criando a classe Student
// Com todas as características e compartamentos aplicados

public class Student {
    String name;
    int age;
    Color color;
    Sex sex;

    void eating(Lunch lunch){
      //NOSSO CÓDIGO AQUI
    }
    void drinking(Juice juice){
      //NOSSO CÓDIGO AQUI
    }
    void running(){
      //NOSSO CÓDIGO AQUI
    }
}

```

```java
// Criando objetos a partir da classe Student

public class School {
    public static void main(String[] args) throws Exception {
      Student student1 = new Student();
      student1.name= "John";
      student1.age= 12;
      student1.color= Color.FAIR;
      student1.sex= Sex.MALE;

      Student student2 = new Student();
      student2.name= "Sophia";
      student2.age= 10;
      student2.color= Color.FAIR;
      student2.sex= Sex.FEMALE;

      Student student3 = new Student();
      student3.name= "Lily";
      student3.age= 11;
      student3.color= Color.DARK;
      student3.sex= Sex.FEMALE;
    }
}
j
```

---
Seguindo algumas convenções, as nossas classes são classificadas como:
- **Classe de modelo (model)**: classes que representam estrutura de domínio da aplicação, exemplo: Cliente, Pedido, Nota Fiscal e etc.
- **Classe de serviço (service)**: classes que contém regras de negócio e validação de nosso sistema.
- **Classe de repositório (repository)**: classes que contém uma integração com banco de dados.
- **Classe de controle (controller)**: classes que possuem a finalidade de disponibilizar alguma comunicação externa, à nossa aplicação, como http web ou webservices.
- **Classe utilitária (util)**: classe que contém recursos comuns, à toda nossa aplicação.

![[Pasted image 20240626205833.png|400]]

---
## Múltiplas classes não-públicas em um único arquivo
```java
package com.algaworks.erp.estoque;

import java.util.Objects;
import java.util.UUID;

public class Produto {

    static final int QUANTIDADE_ESTOQUE_INICIAL = 100;

    private final String codigo;
    private String nome;
    private int quantidadeEstoque;
    private Fornecedor fornecedor;
    private Categoria categoria;

    public Produto() {
        this("Sem nome");
    }

    public Produto(String nome) {
        this(nome, QUANTIDADE_ESTOQUE_INICIAL);
    }

    private Produto(String nome, int estoqueInicial) {
        Objects.requireNonNull(nome, "Nome é obrigatório");

        if (estoqueInicial < 0) {
            throw new IllegalArgumentException("Estoque inicial não pode ser negativo");
        }

        this.nome = nome;
        this.quantidadeEstoque = estoqueInicial;
        this.codigo = gerarCodigo();
    }

    private String gerarCodigo() {
        return UUID.randomUUID().toString();
    }

    public void imprimir() {
        System.out.printf("%s x %d itens", nome, quantidadeEstoque);
    }

}
// só é possível ter outras classes dentro de uma se elas não forem públicas
// classes públicas precisam do seu arquivo .java
class Fornecedor {
}

class Categoria {
}

class Principal {

    public static void main(String[] args) {
        Produto produto = new Produto("Suco de uva");
        produto.imprimir();
    }

}
```