### Terminal
Nem sempre executamos nosso programa Java pela IDE, já pensou, nossos clientes tendo que instalar o Eclipse ou VsCode para rodar o sistema em sua empresa ?

Com a JVM devidamente configurada, nós podemos criar um executável do nosso programa e disponibilizar o instalador para qualquer sistema operacional.

No nosso caso, iremos aprender como executar um programa Java via terminal, como MS - DOS ou terminal do VsCode.

Vamos criar uma classe chamada MinhaClasse.java com o código abaixo:
```java
public class MinhaClasse {
    public static void main(String[] args) {
        System.out.println("Oi, fui executado pelo Terminal");
    }
}
```

> [!info]
> Observe que nosso projeto Java criado por uma IDE, terá uma pasta chamada bin. É nesta pasta que ficarão os arquivos .class, o nosso bytecode.

Mesmo usando uma IDE, nós sempre precisaremos identificar aonde se encontram as classes do nosso projeto
1. Encontre a pasta do projeto e copie o endereço na pasta bin;
2. Abra o CMD (Terminal);
3. ``cd diretório pasta bin do projeto``;
4. ``java MinhaClasse`` (nome da sua classe sem a extensão .class).
   
> [!danger]
> Se o diretório não estiver no C:\ e sim no A:\ 
> Entre na pasta bin no explorer e segure shift e aperte o botão direito do mouse
> Ou digite cmd na barra de endereços e aperte ↵ Enter
> Ou digite A: no CMD

---
### Argumentos
Quando executamos uma classe, que contenha o método main, o mesmo permite que passemos um array [] de argumentos, do tipo String. Logo, podemos após a definição da classe a ser executada, informar estes parâmetros, exemplo:
``java MinhaClasse agumentoUm argumentoDois``
~~ver exemplo no vscode (dio-bootcamp-java)~~

---
### Scanner
A classe **Scanner**, permite que o usuário tenha, uma interação mais assertiva com o nosso programa, veja como vamos mudar o nosso programa `AboutMe` para deixar mais intuitivo aos usuários:
```java
import java.util.Locale;
import java.util.Scanner;
```
~~ver exemplo no vscode (dio-bootcamp-java)~~
