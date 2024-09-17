## Exceções
Ao executar o código Java, diferentes erros podem acontecer: erros de codificação feitos pelo programador, erros devido a entrada errada ou outros imprevistos.

Quando ocorre um erro, o Java normalmente para e gera uma mensagem de erro. O termo técnico para isso é: Java lançará uma exceção (jogará um erro).

Uma responsabilidade do desenvolvedor é prever situações e realizar o que denominamos de **[[#Tratamento de Exceções]]**.

```java
if (quantidade < 0) {
	throw new IllegalArgumentException ("Quantidade não pode ser negativa");
}
```

```java
if (!isActive()) {
	throw new IllegalStateException ("Ação não pode ser realizada por método inativo")
}
```


##### Exemplos de exceções:

| Entrada               | Valor            | Exceção                          | Causa                                                                                    |
| --------------------- | ---------------- | -------------------------------- | ---------------------------------------------------------------------------------------- |
| Digite seu nome:      | **Camilla**      |                                  |                                                                                          |
| Digite seu sobrenome: | **Gatin**        |                                  |                                                                                          |
| Digite sua idade:     | **vinte e dois** | java.util.InputMismatchException | O programa esperava o valor do tipo numérico inteiro.                                    |
| Digite sua altura:    | **1,65**         | java.util.InputMismatchException | O programa esperava o valor do tipo numérico decimal no formato americano, exemplo: 1.65 |


> [!quote] Lei de Murphy
> A melhor forma de prever, que pode ocorrer uma exceção, é pensar que ela pode ocorrer.

#### Exceções comuns:

| Nome                           | Causa                                                                 |
| ------------------------------ | --------------------------------------------------------------------- |
| java.lang.NullPointerException | Quando tentamos obter alguma informação de uma variável nula.         |
| java.lang.ArithmeticException  | Quando tentamos dividir um valor por zero.                            |
| java.sql.SQLException          | Quando existe algum erro, relacionado a interação com banco de dados. |
| java.io.FileNotFoundException  | Quando tentamos ler ou escrever, em um arquivo que não existe.

---
## Tratamento de Exceções
A instrução `try`, permite que você defina um bloco de código, para ser testado quanto a erros enquanto está sendo executado.

A instrução `catch`, permite definir um bloco de código a ser executado, caso ocorra um erro no bloco try.

A instrução [[#Usando a cláusula finally|finally]], permite definir um bloco de código a ser executado, independente de ocorrer um erro ou não. As palavras-chave `try` e `catch` vem em pares:
```java
// estrutura de um bloco com try e catch

try {
  //  Block of code to try
}
catch(Exception e) { // qual exceção
  //  Block of code to handle errors
}
```

> [!warning]
> O bloco `try` / `catch` pode conter um conjunto de **catchs,** correspondentes a cada exceção **prevista** em uma funcionalidade do programa.

### Blocos múltiplos de catch
Produto.java
```java
 if (quantidade < 0) {
    throw new IllegalArgumentException("Quantidade não pode ser negativa para retirada no estoque");
}

if (isInativo()) {
    throw new IllegalStateException("Retirada no estoque não pode ser realizada em produto inativo");
}

if (this.quantidadeEstoque - quantidade < 0) {
    throw new IllegalArgumentException("Quantidade inválida porque estoque ficaria negativo");
}

```

Principal.java
```java
 do {
    try {
	    efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
	} catch (IllegalArgumentException iae) {
        System.out.println("Erro na compra: " + iae.getMessage());
    } catch (IllegalStateException ise) {
        System.out.println("Erro na compra: " + ise.getMessage());
    }
} while (true);
```
---
## Hierarquia das exceções
A linguagem Java, dispõe de uma variedade de classes, que representam exceções e estas classes, são organizadas em uma hierarquia denominadas **Checked and Unchecked Exceptions**.
![[Pasted image 20240623165711.png|350]] ![[hierarquia-excecoes.png|500]]

 **Checked**
- Exceções que obrigatoriamente é preciso tratar (try/catch)
- Não passam pela *RuntimeException* e *Error*

**Unchecked**
- Tratamento opcional
### Capturando checked exceptions
```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

public class Principal {

    public static void main(String[] args) {
        try {
            Path arquivo = Path.of("/Users/thiago/Desktop/abc/teste.txt");
            Files.createFile(arquivo);
        } catch (IOException e) {
            System.out.println("Erro ao criar arquivo: " + e.getMessage());
            e.printStackTrace();
        }
    }

}
```

---
## Exceções customizadas (unchecked)
Nós podemos criar nossas próprias exceções, baseadas em regras de negócio e assim melhor direcionar quem for utilizar os recursos desenvolvidos no projeto, exemplo:

~~ver exemplo no vscode (bootcamp java santander)~~
 Imagina que como regra de negócio, para formatar um cep, necessita sempre de ter 8 dígitos, caso contrário, lançará uma exceção que denominamos de **CepInvalidoException**.
- Primeiro criamos nossa exceção: `` public class CepInvalidoException extends Exception {}``
- Em seguida, criamos nosso método de formatação de cep: 
```java title:CepInvalidoException
static String formatarCep(String cep) throws CepInvalidoException{
        if(cep.length() != 8)
          throw new CepInvalidoException();
        
          //simulando um cep formatado
          return "23.765-064";
    }
```
<mark class="hltr-purple">ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ</mark>

==outro exemplo:==

```java title:Produto.java
if (isInativo()) {
            throw new ProdutoInativoException("Retirada no estoque não pode ser realizada em produto inativo");
}

if (this.quantidadeEstoque - quantidade < 0) {
            throw new ProdutoSemEstoqueException("Quantidade inválida porque estoque ficaria negativo");
}
```

```java title:ProdutoSemEstoqueException.java
public class ProdutoSemEstoqueException extends RuntimeException {

    public ProdutoSemEstoqueException(String message) {
        super(message);
    }
}
```

```java title:ProdutoInativoException.java
public class ProdutoInativoException extends RuntimeException {

    public ProdutoInativoException(String message) {
        super(message);
    }
}
```

```java title:Principal.java
 do {
    try {
	    efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
	} catch (IllegalArgumentException iae) {
        System.out.println("Erro na compra: " + iae.getMessage());
    } catch (ProdutoSemEstoqueException e) {
        System.out.println("Erro na compra: " + e.getMessage());
    } catch (ProdutoInativoException e) {
	    System.out.println("Erro na compra: " + e.getMessage());
    }
} while (true);
```
#### Variáveis de Instância
```java title:ProdutoSemEstoqueException.java
public class ProdutoSemEstoqueException extends RuntimeException {

	private final int estoqueDisponivel;
	private final int estoqueNecessario;

    public ProdutoSemEstoqueException(String message, int estoqueDisponivel, int estoqueNecessario) {
        super(message);
        this.estoqueDisponivel = estoqueDisponivel;
        this.estoqueNecessario = estoqueNecessario;
    }
    
	public int getEstoqueDisponivel() {
		return estoqueDisponivel;
	}

	public int getEstoqueNecessario() {
		return estoqueNecessario;
	}
}
```

```java title:Produto.java
if (quantidade < 0) {
	throw new IllegalArgumentException("Quantidade não pode ser negativa para retirada no estoque");
}

if (isInativo()) {
    throw new ProdutoInativoException("Retirada no estoque não pode ser realizada em produto inativo");
}

if (this.quantidadeEstoque - quantidade < 0) {
    throw new ProdutoSemEstoqueException("Estoque insuficiente", this.quantidadeEstoque, quantidade);
}
```

```java title:Principal.java
do {
    try {
        efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
    } catch (IllegalArgumentException iae) {
        System.out.println("Erro na compra: " + iae.getMessage());
    } catch (ProdutoSemEstoqueException e) {
        System.out.printf("Erro na compra: %s. Estoque disponível: %d. Estoque necessário: %d%n",e.getMessage(), e.getEstoqueDisponivel(), e.getEstoqueNecessario());
    } catch (ProdutoInativoException e) {
        System.out.println("Erro na compra: " + e.getMessage());

	    System.out.print("Deseja ativar o produto? ");

        if (scanner.nextBoolean()) {
	        produto.ativar();
	        System.out.println("Ok. Produto já foi ativado");
        } else {
	        System.out.println("Ok. Compra não pode ser realizada");
	        break;
        }
    }
} while (true);
```
#### Lançando e propagando checked exceptions
![[Pasted image 20240912083228.png|500]]
```java title:ProdutoInativoException.java

public class ProdutoInativoException extends Exception {

    public ProdutoInativoException(String message) {
        super(message);
    }

}
```

```java title:ProdutoSemEstoqueException.java
public class ProdutoSemEstoqueException extends Exception {

    private final int estoqueDisponivel;
    private final int estoqueNecessario;

    public ProdutoSemEstoqueException(String message, int estoqueDisponivel, int estoqueNecessario) {
        super(message);
        this.estoqueDisponivel = estoqueDisponivel;
        this.estoqueNecessario = estoqueNecessario;
    }

    public int getEstoqueDisponivel() {
        return estoqueDisponivel;
    }

    public int getEstoqueNecessario() {
        return estoqueNecessario;
    }

}
```

```java title:Principal.java
 do{try{}catch{if}}while;
 
private static void efetuarBaixaEstoque(Produto produto, int quantidade) throws ProdutoSemEstoqueException, ProdutoInativoException {
    produto.retirarEstoque(quantidade);
    System.out.printf("%d unidades retiradas do estoque. Estoque atual: %d%n", quantidade, produto.getQuantidadeEstoque());
}
```
### Capturando exceções menos específicas (upcasting)
![[Pasted image 20240912085007.png|500]]

```java title:ProdutoException.java
public class ProdutoException extends Exception {

    public ProdutoException(String message) {
        super(message);
    }
}
```


```java title:ProdutoInativoException.java
public class ProdutoInativoException extends ProdutoException {

    public ProdutoInativoException(String message) {
        super(message);
    }

}
```

```java title:ProdutoSemEstoqueException.java
public class ProdutoSemEstoqueException extends ProdutoException {

    private final int estoqueDisponivel;
    private final int estoqueNecessario;

    public ProdutoSemEstoqueException(String message, int estoqueDisponivel, int estoqueNecessario) {
        super(message);
        this.estoqueDisponivel = estoqueDisponivel;
        this.estoqueNecessario = estoqueNecessario;
    }

    public int getEstoqueDisponivel() {
        return estoqueDisponivel;
    }

    public int getEstoqueNecessario() {
        return estoqueNecessario;
    }
}
```

```java title:Principal.java
do {
    try {
        efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
    } catch (IllegalArgumentException iae) {
	    System.out.println("Erro na compra: " + iae.getMessage());
//  } catch (ProdutoSemEstoqueException e) {
//      System.out.printf("Erro na compra: %s. Estoque disponível: %d. Estoque necessário: %d%n", e.getMessage(), e.getEstoqueDisponivel(), e.getEstoqueNecessario());
    } catch (ProdutoInativoException e) {
        System.out.println("Erro na compra: " + e.getMessage());

        System.out.print("Deseja ativar o produto? ");

        if (scanner.nextBoolean()) {
            produto.ativar();
            System.out.println("Ok. Produto já foi ativado");
        } else {
            System.out.println("Ok. Compra não pode ser realizada");
            break;
        }
    } catch (ProdutoException e) {
//      System.out.println(e.getClass().getName());
	    System.out.println("Erro na compra: " + e.getMessage());
    }
} while (true);

    private static void efetuarBaixaEstoque(Produto produto, int quantidade) throws ProdutoSemEstoqueException, ProdutoInativoException {
        produto.retirarEstoque(quantidade);
        System.out.printf("%d unidades retiradas do estoque. Estoque atual: %d%n", quantidade, produto.getQuantidadeEstoque());
    }
```
### Capturando e lançando nova exceção
```java title:BaixaEstoqueException.java

public class BaixaEstoqueException extends Exception {

    public BaixaEstoqueException(String message) {
        super(message);
    }
}
```

ProdutoException.java
ProdutoInativoException.java
ProdutoSemEstoqueException.java

```java title:Produto.java
public void retirarEstoque(int quantidade) throws ProdutoSemEstoqueException, ProdutoInativoException {
    if (quantidade < 0) {
	    throw new IllegalArgumentException("Quantidade não pode ser negativa para retirada no estoque");
    }

    if (isInativo()) {
		throw new ProdutoInativoException("Retirada no estoque não pode ser realizada em produto inativo");
    }

    if (this.quantidadeEstoque - quantidade < 0) {
        throw new ProdutoSemEstoqueException("Estoque insuficiente", this.quantidadeEstoque, quantidade);
    }
```


```java title:Principal.java
do {
    try {
        efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
    } catch (BaixaEstoqueException e) {
        System.out.println("Erro na compra: " + e.getMessage());
        e.printStackTrace();
    }
} while (true);

private static void efetuarBaixaEstoque(Produto produto, int quantidade) throws BaixaEstoqueException {
    try {
		produto.retirarEstoque(quantidade);
        System.out.printf("%d unidades retiradas do estoque. Estoque atual: %d%n", quantidade, produto.getQuantidadeEstoque());
    } catch (IllegalArgumentException e) {
        throw new BaixaEstoqueException("Erro ao realizar baixa no estoque");
    } catch (ProdutoException e) {
        throw new BaixaEstoqueException("Erro ao realizar baixa no estoque");
    }
}
```
#### Embrulhando a causa raiz do problema
ProdutoException.java
ProdutoInativoException.java
ProdutoSemEstoqueException.java
Produto.java

```java title:BaixaEstoqueException.java
public class BaixaEstoqueException extends Exception {

    public BaixaEstoqueException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

```java title:Principal.java
do {
    try {
	    System.out.print("Quantidade: ");
        int quantidade = scanner.nextInt();

        efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
    } catch (BaixaEstoqueException e) {
        System.out.println("Erro na compra: " + e.getCause().getMessage());
//      e.printStackTrace();
	}
} while (true);

private static void efetuarBaixaEstoque(Produto produto, int quantidade) throws BaixaEstoqueException {
    try {
	    produto.retirarEstoque(quantidade);
        System.out.printf("%d unidades retiradas do estoque. Estoque atual: %d%n", quantidade, produto.getQuantidadeEstoque());
    } catch (IllegalArgumentException e) {
	    throw new BaixaEstoqueException("Erro ao realizar baixa no estoque", e);
	} catch (ProdutoException e) {
        throw new BaixaEstoqueException("Erro ao realizar baixa no estoque", e);
    }
}
```

### Capturando exceções com multi-catch

```java title:Principal.java
do {
    try {
	    System.out.print("Quantidade: ");
        int quantidade = scanner.nextInt();

        efetuarBaixaEstoque(produto, quantidade);
        System.out.println("Compra realizada");

        break;
    } catch (BaixaEstoqueException e) {
	    System.out.println("Erro na compra: " + e.getCause().getMessage());
    }
} while (true);

private static void efetuarBaixaEstoque(Produto produto, int quantidade) throws BaixaEstoqueException {
	try {
        produto.retirarEstoque(quantidade);
        System.out.printf("%d unidades retiradas do estoque. Estoque atual: %d%n", quantidade, produto.getQuantidadeEstoque());
    } catch (IllegalArgumentException | ProdutoException e) {
	    throw new BaixaEstoqueException("Erro ao realizar baixa no estoque", e);
    }
}
```

### Usando a cláusula finally
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

public class Principal {

    public static void main(String[] args) {
        Path arquivo = Path.of("/Users/thiago/Desktop/teste2.txt");
        BufferedReader reader = null;

        try {
            reader = Files.newBufferedReader(arquivo);
            System.out.println(reader.readLine());

            reader.close();
        } catch (IOException e) {
            System.out.println("Erro ao ler arquivo: " + e.getMessage());
        } finally {
            try {
                reader.close();
            } catch (IOException ex) {
                System.out.println("Erro fechando leitor de arquivo");
            }
        }
    }

}
```

