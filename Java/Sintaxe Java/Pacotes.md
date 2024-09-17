Os pacotes são subdiretórios, a partir da pasta src do nosso projeto, onde estão localizadas, as classes da linguagem e novas que forem criadas para o projeto. Existem algumas convenções para criação de pacotes já utilizadas no mercado.

![[Pasted image 20240626211855.png|400]]
### Nomenclatura

Vamos imaginar, que sua empresa se chama **Power Soft** e ela está desenvolvendo software comercial, governamental e um software livre ou de código aberto. Abaixo teríamos os pacotes sugeridos conforme tabela abaixo:

- **Comercial** : com.powersoft;
- **Governamental** : gov.powersoft;
- **Código aberto**: org.powersoft.

Oraganizar as classes mediante a proposta de sua existência:
- **model** : Classes que representam a camada e modelo da aplicação : Cliente, Pedido, NotaFiscal, Usuario;
- **repository**: Classes ou interfaces que possuem a finalidade de interagir com tabelas no banco de dados: ClienteRepository;
- **service**: Classes que contém regras de negócio do sistema : ClienteService possui o método validar o CPF, do cliente cadastrado;
- **controller**: Classes que possuem a finalidade de, disponibilizar os nossos recursos da aplicação, para outras aplicações via padrão HTTP;
- **view**: Classes que possuem alguma interação, com a interface gráfica acessada pelo usuário;
- **util**: Pacote que contém, classes utilitárias do sistema: FormatadorNumeroUtil, ValidadorUtil.
### Identificação

Uma das características de uma classe é a sua identificação: Cliente, NotaFiscal, TituloPagar. Porém quando esta classe é organizada por pacotes, ela passa a ter duas identificações. O nome simples (**próprio nome**) e agora o nome qualificado (**endereçamento do pacote + nome**), exemplo: Considere a classe `Usuario`, que está endereçada no pacote `com.controle.acesso.model`, o nome qualificado desta classe é `com.controle.acesso.model.Usuario`.

---
## Visibilidade dos recursos
Em Java, utilizamos três palavras reservadas e um conceito default para definir os quatro tipo de visibilidade de atributos, métodos e até mesmo classes.
### Modificador public
Como o próprio nome representa, quando nossa classe, método e atributo é definido como public, qualquer outra classe em qualquer outro pacote, poderá visualizar tais recursos.
![[Pasted image 20240626213827.png|400]]
~~exemplo da imagem no vscode (dio-bootcamp-java)~~

> **Acredite!** Nem tudo precisa ser visto por todos.
### Modificador default

O modificador `default`, está fortemente associado a organização das classes por pacotes, algumas implementações, não precisam estar disponíveis por todo o projeto, e este modificador de acesso, restringe a visibilidade por pacotes.

Dentro do pacote `lanchonete`, iremos criar dois sub-pacotes para representar a divisão do estabelecimento.

- **lanchonete.atendimento.cozinha**: Pacote que contém classes, da parte da cozinha da lanchonete e atendimentos.
- **lanchonete.area.cliente**: Pacote que contém classes, relacionadas ao espaço do cliente.

![[image.avif|450]]
### Modificador private

Depois de reestruturar nosso estabelecimento (projeto), onde temos as divisões (pacotes), espaço do cliente e atendimento, chegou a hora de uma reflexão sobre visibilidade ou modificadores de acesso.

Conhecemos as ações disponíveis nas classes `Cozinheiro, Almoxarife, Atendente e Cliente`, mesmo com a organização da visibilidade por pacote, será que realmente estas classes precisam ser tão explícitas?

- Será que o `Cozinheiro` precisa saber que\como o `Almoxarife` controla as entradas e saídas ?
- Que o `Cliente` precisa saber como o `Atendente` recebe o pedido, para servir sua mesa ?
- Que o `Atendente` precisa saber que antes de pagar, o `Cliente` consulta o saldo no App ?

Diante destes questionamentos, é que nossas classes precisam continuar mantendo suas ações (métodos), mas nem todas precisam ser vistas por ninguém.

A visibilidade de recursos da linguagem não está associada a **interface gráfica**, mas sim, o que as classes conseguem **acessar,** umas das outras.

### Modificador protected
ver em [[Polimorfismo]]


---
## Organizando as classes em pacotes

src/erp.estoque
src/erp.comercial
```java
package erp.estoque
public class Produto {}
```

```java
package erp.comercial
public class Pedido {}
```

- usar sempre o dominio
src/com.sitelegal.erp.estoque
src/com.sitelegal.erp.comercial
```java
package com.sitelegal.erp.estoque;
public class Produto {}
```

```java
package com.sitelegal.erp.comercial;
public class Pedido {}
```

---
## Importando Classes de Pacotes

```java
package com.sitelegal.erp;

import com.sitelegal.erp.comercial.Pedido;
import com.sitelegal.erp.estoque.Produto;

public class Principal {}
```

---
##  Importando membros estáticos (static import) 
```java
import com.algaworks.matematica.CalculadoraArea;

public class Principal {
	public static void main(String[] args) {

		double areaQuadrado = CalculadoraArea.calcularAreaQuadrado(5.2);
        double areaCirculo = CalculadoraArea.calcularAreaCirculo(10.5);

        System.out.printf("PI: %.2f%n", Calculadora.PI);
        System.out.printf("Área do quadrado: %.2f%n", areaQuadrado);
        System.out.printf("Área do círculo: %.2f%n", areaCirculo);
	}
}
```

```java
// import static com.algaworks.matematica.CalculadoraArea.calcularAreaQuadrado; importando o método static
import static com.algaworks.matematica.CalculadoraArea.*;

public class Principal {
    public static void main(String[] args) {
    
        double areaQuadrado = calcularAreaQuadrado(5.2);
        double areaCirculo = calcularAreaCirculo(10.5);

        System.out.printf("PI: %.2f%n", PI);
        System.out.printf("Área do quadrado: %.2f%n", areaQuadrado);
        System.out.printf("Área do círculo: %.2f%n", areaCirculo);
    }

}
```