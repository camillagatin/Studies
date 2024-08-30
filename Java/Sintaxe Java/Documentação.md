Um requisito imprescindível é adquirir a habilidade de compreender, a documentação oficial da linguagem e dos frameworks que são incorporados nos projetos atuais.
Aqui, temos o link da documentação de uma das principais classes da linguagem Java: [Oracle](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html)
### Tags
Java Documentation é composto por tags que, representam dados relevantes para a compreensão da proposta de uma classe e os conjuntos de seus métodos e atributos conforme tabela abaixo:

| Tag      | Descrição                                              |
| -------- | ------------------------------------------------------ |
| @autor   | Autor / Criador                                        |
| @version | Versão do recurso disponibilizado                      |
| @since   | Versão / Data de início da disponibilização do recurso |
| @param   | Descrição dos parâmetros dos métodos criados           |
| @return  | Definição do tipo de retorno de um método              |
| @throws  | Se o método lança alguma exceção                       |

Exemplo de documentação, destacando as **tags** mais utilizadas:
```java
/**
* <h1>Calculadora</h1>
* A Calculadora realiza operações matemáticas entre números inteiros
* <p>
* <b>Note:</b> Leia atentamente a documentação desta classes
* para desfrutar dos recursos oferecidos pelo autor
*
* @author  Gleyson Sampaio
* @version 1.0
* @since   01/01/2022
*/
public class Calculadora {
    /**
   * Este método é utilizado para somar dois números inteiros
   * @param numeroUm este é o primeiro parâmetro do método
   * @param numeroDois este é o segundo parâmetro do método
   * @return int o resultado deste método é a soma dos dois números.
   */
    public int somar(int numeroUm, int numeroDois) {
        return  numeroUm + numeroDois;
    }
}

```
## Javadoc

[Javadoc](https://pt.wikipedia.org/wiki/Javadoc) é um gerador de documentação criado pela [Sun Microsystems](https://pt.wikipedia.org/wiki/Sun_Microsystems) , para documentar a [API](https://pt.wikipedia.org/wiki/API) dos programas em [Java](https://pt.wikipedia.org/wiki/Linguagem_de_programa%C3%A7%C3%A3o_Java), a partir do [código-fonte](https://pt.wikipedia.org/wiki/C%C3%B3digo-fonte). O resultado é expresso em [HTML](https://pt.wikipedia.org/wiki/HTML). É constituído, basicamente, por algumas marcações muitos simples, inseridas nos comentários do programa.

Este sistema, é o padrão de documentação de classes em Java, onde muitas das [IDEs](https://pt.wikipedia.org/wiki/Ambiente_de_desenvolvimento_integrado) desta linguagem irão automaticamente gerar um Javadoc em [HTML](https://pt.wikipedia.org/wiki/HTML).

Criando nossa documentação no formato html, para disponibilizar via web.
No terminal execute o comando abaixo:
`javadoc -encoding UTF-8 -docencoding ISO-8859-1  -d ../docs  src/*.java`
