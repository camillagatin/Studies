## Operadores de Comparação Básicos

- **:** Verifica se dois valores são iguais.
- **!=:** Verifica se dois valores são diferentes.
- **<:** Verifica se o valor à esquerda é menor que o valor à direita.
- **>:** Verifica se o valor à esquerda é maior que o valor à direita.
- **<=:** Verifica se o valor à esquerda é menor ou igual ao valor à direita.
- **>=:** Verifica se o valor à esquerda é maior ou igual ao valor à direita.

**Exemplo:**
```java
int num1 = 10;
int num2 = 20;

if (num1 == num2) {
    System.out.println("Os números são iguais.");
} else if (num1 < num2) {
    System.out.println("O primeiro número é menor.");
} else {
    System.out.println("O primeiro número é maior.");
}
```

### Comparando Números de Ponto Flutuante
Ao comparar números de ponto flutuante, é preciso ter cuidado com a precisão. Devido à forma como os computadores representam esses números, pequenas diferenças podem ocorrer. Por isso, em vez de usar `{java}==`, é recomendado usar uma pequena margem de erro:
```java
double num1 = 0.1;
double num2 = 0.3 - 0.2;

double epsilon = 0.00001; // Margem de erro

if (Math.abs(num1 - num2) < epsilon) {
    System.out.println("Os números são aproximadamente iguais.");
}
```

### Comparando Objetos
Ao comparar objetos, o operador `{java}==` verifica se as referências aos objetos são iguais, ou seja, se ambos os objetos são a mesma instância. Para comparar o conteúdo dos objetos, é necessário implementar o método `{java}equals()` na classe.

```java
class Ponto {
    int x, y;

    // Método equals() personalizado
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        Ponto other = (Ponto) obj;
        return    x == other.x && y == other.y;
    }
}
```


##### Em resumo:
- **Tipos primitivos:** Use os operadores de comparação básicos.
- **Números de ponto flutuante:** Use uma margem de erro para evitar problemas de precisão.
- **Objetos:** Implemente o método `equals()` para comparar o conteúdo dos objetos.
- **Arrays:** Percorra cada elemento e compare os valores individualmente.
- **Strings:** Use o método `equals()`.

##### Observações:
- **Autoboxing:** Java permite a conversão automática entre tipos primitivos e seus wrappers (Integer, Double, etc.). Ao comparar um tipo primitivo com um objeto wrapper, o autoboxing ocorre.
- **Operador ternário:** O operador ternário `? :` pode ser usado para expressões condicionais mais concisas.
- **Interfaces comparáveis:** A interface `Comparable` permite definir uma ordem natural para objetos de uma determinada classe.
---
## Operações Matemáticas com java.lang.Math
A classe `java.lang.Math` oferece uma ampla gama de métodos estáticos para realizar diversas operações matemáticas em Java.

**Por que usar a classe Math?**
- **Eficiência:** Os métodos da classe Math são altamente otimizados, garantindo um desempenho superior.
- **Conveniência:** Fornece um conjunto abrangente de funções matemáticas prontas para uso.
- **Padronização:** Assegura a consistência nas operações matemáticas em suas aplicações.

##### Principais Métodos:
- **Trigonometria:**
    - `sin(double a)`: Retorna o seno de um ângulo em radianos.
    - `cos(double a)`: Retorna o cosseno de um ângulo em radianos.
    - `tan(double a)`: Retorna a tangente de um ângulo em radianos.
    - E muitos outros métodos para funções trigonométricas inversas, hiperbólicas, etc.
- **Exponenciais e Logaritmos:**
    - `exp(double a)`: Retorna e elevado à potência a.
    - `log(double a)`: Retorna o logaritmo natural de a.
    - `log10(double a)`: Retorna o logaritmo em base 10 de a.
    - `pow(double a, double b)`: Retorna a elevado à potência b.
- **Arredondamento:**
    - `ceil(double a)`: Retorna o menor inteiro maior ou igual a a.
    - `floor(double a)`: Retorna o maior inteiro menor ou igual a a.
    - `round(double a)`: Arredonda a para o inteiro mais próximo.
- **Valores Absolutos e Máximos/Mínimos:**
    - `abs(int a)`: Retorna o valor absoluto de a.
    - `max(int a, int b)`: Retorna o maior valor entre a e b.
    - `min(int a, int b)`: Retorna o menor valor entre a e b.
- **Números Aleatórios:**
    - `random()`: Retorna um número aleatório entre 0.0 (inclusive) e 1.0 (exclusivo).

**Exemplo:**
```java
public class ExemploMath {
    public static void main(String[] args) {
        double angulo = Math.PI / 4; // 45 graus em radianos
        double seno = Math.sin(angulo);
        double raizQuadrada = Math.sqrt(16);

        System.out.println("Seno de 45 graus: " + seno);
        System.out.println("Raiz quadrada de 16: " + raizQuadrada);

        int numeroAleatorio = (int) (Math.random() * 100); // Número aleatório entre 0 e 99
        System.out.println("Número aleatório: " + numeroAleatorio);
    }
}
```

**Outras Funcionalidades:**
- **Constantes:** A classe Math fornece constantes como `PI`, `E`, etc.
- **Conversão de graus para radianos e vice-versa:** Utilize as fórmulas adequadas.

**Quando usar:**
- **Cálculos trigonométricos:** Seno, cosseno, tangente, etc.
- **Operações exponenciais e logarítmicas:** Potências, raízes, logaritmos.
- **Arredondamento de números:** Para obter valores inteiros a partir de números de ponto flutuante.
- **Geração de números aleatórios:** Para simular eventos aleatórios.
- **Cálculos diversos:** A classe Math oferece uma variedade de outras funções úteis.
---
## Boas Práticas: Evite float e double quando a precisão é crucial

#### Por que evitar float e double em cálculos que exigem alta precisão?
A representação de números de ponto flutuante em computadores, seja em formato float ou double, é baseada em uma aproximação. Isso significa que nem todos os números reais podem ser representados com precisão exata. Pequenos erros de arredondamento podem se acumular em cálculos complexos, levando a resultados imprecisos.

#### Quando a imprecisão pode ser um problema:
- **Cálculos financeiros:** Onde até mesmo pequenas diferenças podem resultar em grandes perdas ou ganhos.
- **Simulações científicas:** Onde a precisão é fundamental para obter resultados confiáveis.
- **Jogos:** Onde a física precisa ser simulada de forma realista.
- **Qualquer aplicação que exija cálculos numéricos precisos.**

#### Alternativas para float e double:
- **BigDecimal:** Essa classe permite representar números com precisão arbitrária, ideal para cálculos financeiros e outras aplicações que exigem alta precisão.
- **Tipos inteiros:** Se você estiver trabalhando com números inteiros, utilizar tipos como int ou long pode garantir a precisão exata.
- **Bibliotecas especializadas:** Existem bibliotecas que oferecem suporte a aritmética de alta precisão, como a MPFR (Multiple-Precision Floating-Point Reliable).
---
## Precisão nos Cálculos com BigDecimal

### Como funciona?
- **Representação interna:** Os números `BigDecimal` são armazenados internamente como um par de inteiros: um significando e uma escala. Isso permite representar números com um número arbitrário de casas decimais.
- **Operações:** As operações matemáticas com `BigDecimal` são definidas de forma precisa para garantir a exatidão. Por exemplo, a adição é realizada alinhando as vírgulas decimais dos operandos e somando os dígitos correspondentes.
- **Arredondamento:** Quando uma operação resulta em um número com mais casas decimais do que o desejado, o `BigDecimal` oferece diversos modos de arredondamento, como `ROUND_UP`, `ROUND_DOWN`, `ROUND_HALF_UP`, etc.

### Motivos para usar BigDecimal:
- **Cálculos financeiros:** Onde a precisão é essencial para evitar perdas financeiras.
- **Aplicações científicas:** Onde os erros de arredondamento podem comprometer a validade dos resultados.
- **Qualquer situação em que a precisão de ponto flutuante padrão não seja suficiente.**

### Exemplo Prático:
```java
import java.math.BigDecimal;

public class ExemploBigDecimal {
    public static void main(String[] args) {
        BigDecimal valor1 = new BigDecimal("0.1");
        BigDecimal valor2 = new BigDecimal("0.2");
        BigDecimal resultado = valor1.add(valor2);
        System.out.println(resultado); // Imprime 0.3, com int imprimiria 0.2999999998
    }
}
```

### Considerações Importantes:
- **Construtores:** Ao criar um `BigDecimal`, evite usar `new BigDecimal(double)` pois pode introduzir erros de arredondamento. Prefira usar `new BigDecimal(String)`.
- **Operações:** Todas as operações aritméticas básicas estão disponíveis, assim como funções como `sqrt`, `pow`, etc.
- **Comparação:** Utilize o método `compareTo()` para comparar `BigDecimal`s, pois o operador `{java}==` compara apenas as referências.
- **Arredondamento:** Escolha o modo de arredondamento adequado para a sua aplicação.
- **Desempenho:** As operações com `BigDecimal` são geralmente mais lentas do que com tipos primitivos. Utilize-o apenas quando a precisão for crítica.

### Quando usar BigDecimal?
- **Cálculos com muitas casas decimais:** Quando a precisão de ponto flutuante padrão não é suficiente.
- **Operações monetárias:** Onde a exatidão é fundamental.
- **Cálculos científicos que exigem alta precisão.**

### Alternativas ao BigDecimal:
- **Tipos inteiros:** Para cálculos com números inteiros, tipos como `int` e `long` oferecem precisão exata.
- **Bibliotecas especializadas:** Para aplicações que exigem um desempenho ainda maior, existem bibliotecas como MPFR (Multiple-Precision Floating-Point Reliable).
---
## Divisão de BigDecimal e Formas de Arredondamento
A divisão com `BigDecimal` em Java oferece um alto grau de controle sobre o resultado, permitindo que você especifique o número de casas decimais e o método de arredondamento. Isso é especialmente útil em cálculos financeiros e outras aplicações que exigem precisão.

### O Método `divide()`
O método principal para realizar divisões com `BigDecimal` é o `divide()`. Ele possui duas variantes principais:

- **`divide(BigDecimal divisor)`:** Lança uma ArithmeticException se a divisão resultar em um número com um número infinito de casas decimais.
- **`divide(BigDecimal divisor, int scale, int roundingMode)`:** Permite especificar o número de casas decimais (scale) e o modo de arredondamento.

### Modos de Arredondamento
O Java oferece diversos modos de arredondamento para o método `divide()`, cada um com seu comportamento específico:

- **ROUND_UP:** Arredonda para cima, em direção a +infinito.
- **ROUND_DOWN:** Arredonda para baixo, em direção a -infinito.
- **ROUND_CEILING:** Arredonda para cima se positivo, para baixo se negativo.
- **ROUND_FLOOR:** Arredonda para baixo se positivo, para cima se negativo.
- **ROUND_HALF_UP:** Arredonda para o número par mais próximo, se o número a ser arredondado estiver exatamente no meio entre dois números arredondados.
- **ROUND_HALF_DOWN:** Arredonda para o número par mais próximo, se o número a ser arredondado estiver exatamente no meio entre dois números arredondados.
- **ROUND_HALF_EVEN:** Semelhante a `ROUND_HALF_UP`, mas arredonda para o número par mais próximo.
- **ROUND_UNNECESSARY:** Lança uma ArithmeticException se o arredondamento for necessário.

### Exemplo Prático
```java
import java.math.BigDecimal;
import java.math.RoundingMode;

public class DivisaoBigDecimal {
    public static void main(String[] args) {
        BigDecimal dividendo = new BigDecimal("10");
        BigDecimal divisor = new BigDecimal("3");

        // Divisão com duas casas decimais, arredondando para cima
        BigDecimal resultado = dividendo.divide(divisor, 2, RoundingMode.UP);
        System.out.println(resultado); // Imprime 3.34

        // Divisão com três casas decimais, arredondando para o número par mais próximo
        resultado = dividendo.divide(divisor, 3, RoundingMode.HALF_EVEN);
        System.out.println(resultado); // Imprime 3.333
    }
}
```

### Considerações Importantes
- **Escolha do modo de arredondamento:** A escolha do modo de arredondamento depende da sua aplicação e das suas necessidades de precisão.
- **Exceções:** Se a divisão resultar em um número com um número infinito de casas decimais e você não especificar um modo de arredondamento, será lançada uma `ArithmeticException`.
- **Desempenho:** As operações com `BigDecimal` são geralmente mais lentas do que com tipos primitivos. Utilize-o apenas quando a precisão for crítica.

### Quando usar a divisão com BigDecimal?
- **Cálculos financeiros:** Onde a precisão é essencial para evitar erros de arredondamento que podem resultar em perdas financeiras.
- **Aplicações científicas:** Onde a precisão é fundamental para obter resultados confiáveis.
- **Qualquer situação em que a precisão de ponto flutuante padrão não seja suficiente.**
---
## Formatação Decimal com DecimalFormat
A classe `DecimalFormat` em Java é uma ferramenta poderosa para formatar números decimais de acordo com padrões específicos, como separadores de milhar, número de casas decimais e símbolos de moeda. Ela é ideal para apresentar dados numéricos de forma clara e concisa para o usuário.

### Como funciona o DecimalFormat?
- **Padrões de formatação:** O `DecimalFormat` utiliza padrões de formato baseados em caracteres especiais para definir a aparência do número formatado.
- **Customização:** Você pode personalizar praticamente todos os aspectos da formatação, desde o número de casas decimais até o símbolo da moeda.
- **Localização:** É possível adaptar a formatação para diferentes localidades, utilizando os padrões de formatação específicos de cada região.

### Exemplo básico
```java
import java.text.DecimalFormat;

public class ExemploDecimalFormat {
    public static void main(String[] args) {
        double valor = 12345.6789;

        // Formatando com duas casas decimais e separador de milhar
        DecimalFormat df = new DecimalFormat("#,##0.00");
        String valorFormatado = df.format(valor);
        System.out.println(valorFormatado); // Imprime: 12.345,68
    }
}
```

### Caracteres especiais nos padrões de formatação
- **0:** Dígito obrigatório. Se o número não tiver um dígito nessa posição, um zero será exibido.
- **#:** Dígito opcional. Se o número não tiver um dígito nessa posição, nada será exibido.
- **,:** Separa grupos de milhar.
- **.:** Separa a parte inteira da parte decimal.
- **;:** Separa o formato para números positivos e negativos.
- **-:** Sinal negativo.
- **E:** Notação científica.

### Exemplos mais complexos

- **Moeda:**
	```java
	DecimalFormat df = new DecimalFormat("¤ #,##0.00");
	df.setCurrency(Currency.getInstance(Locale.US));
	System.out.println(df.format(valor)); // Imprime: $12,345.68
	```
    
- **Porcentagem:**
	```java
    DecimalFormat df = new DecimalFormat("##0.00%");
    System.out.println(df.format(0.25)); // Imprime: 25.00%
    ```
    
- **Número científico:** 
    ```java
    DecimalFormat df = new DecimalFormat("0.###E0");
    System.out.println(df.format(123456789)); // Imprime: 1.235E8
    ```
    

### Personalizando o formato
- **Grupos de milhar:** Utilize vírgulas (,) para separar grupos de milhar.
- **Casas decimais:** Especifique o número de casas decimais após o ponto decimal.
- **Símbolos:** Use símbolos de moeda, porcentagem ou outros caracteres especiais para personalizar o formato.
- **Padrões negativos:** Utilize o ponto e vírgula (;) para definir formatos diferentes para números positivos e negativos.

### Considerações adicionais
- **Localização:** Para adaptar a formatação a diferentes localidades, utilize a classe `NumberFormat` e os métodos `getCurrencyInstance()`, `getNumberInstance()` e `getPercentInstance()`.
- **Personalização:** Você pode criar padrões de formatação personalizados para atender às suas necessidades específicas.
- **Performance:** Embora o `DecimalFormat` seja uma ferramenta poderosa, é importante utilizá-la com moderação, pois a formatação de números pode ter um impacto no desempenho, especialmente em aplicações com alto volume de dados.
---
## Localizando a Formatação de Números com Locale
A classe `DecimalFormat` oferece uma flexibilidade incrível para formatar números, mas para garantir que a formatação esteja de acordo com as convenções de diferentes regiões, é fundamental utilizar a classe `Locale`.

**O que é Locale?**
- Representa uma região geográfica, cultural ou política.
- Define padrões para idioma, data, hora, moeda e, é claro, números.

**Como usar Locale com DecimalFormat?**

1. **Obter uma instância de NumberFormat:**
    - `{java}NumberFormat.getInstance(Locale locale)`: Retorna um objeto `{java}NumberFormat` configurado para a localidade especificada.
2. **Personalizar o formato (opcional):**
    - Se necessário, você pode personalizar o formato usando os métodos da classe `DecimalFormat`, como `setMinimumFractionDigits`, `setMaximumFractionDigits`, etc.
3. **Formatar o número:**
    - Utilize o método `format()` do objeto `NumberFormat` para obter a representação em string do número formatado.

**Exemplo prático: Formatando um valor monetário para diferentes localidades**
```java
import java.text.NumberFormat;
import java.util.Locale;

public class FormatacaoComLocale {
    public static void main(String[] args) {
        double valor = 12345.6789;

        // Formatando para os EUA
        NumberFormat usFormat = NumberFormat.getCurrencyInstance(Locale.US);
        String valorUS = usFormat.format(valor);
        System.out.println("Valor em US: " + valorUS); // Saída: $12,345.68

        // Formatando para o Brasil
        NumberFormat brFormat = NumberFormat.getCurrencyInstance(Locale.forLanguageTag("pt-BR"));
        String valorBR = brFormat.format(valor);
        System.out.println("Valor no Brasil: " + valorBR); // Saída: R$ 12.345,68
    }
}
```

**Outros exemplos de uso de Locale:**
- **Formatação de datas:** `DateFormat.getDateInstance(Locale locale)`
- **Formatação de horas:** `DateFormat.getTimeInstance(Locale locale)`
- **Formatação de números:** `NumberFormat.getNumberInstance(Locale locale)`

**Por que usar Locale?**
- **Globalização:** Garante que seus aplicativos exibam dados numéricos de forma correta para usuários em diferentes regiões.
- **Convenções culturais:** Respeita as convenções de cada localidade, como o separador decimal, o símbolo da moeda e a ordem dos componentes da data.
- **Melhor experiência do usuário:** Evita confusão e facilita a compreensão dos dados.

**Locais comuns:**
- `Locale.US`: Estados Unidos
- `Locale.UK`: Reino Unido
- `Locale.FRANCE`: França
- `Locale.JAPAN`: Japão
- `Locale.CHINA`: China
- `Locale.forLanguageTag("pt-BR")`: Português do Brasil

```java
public class
	psvm {
		Locale.setDefault(new Locale("pt", "BR"));
	}
}
```

**Considerações adicionais:**
- **Personalização:** Você pode criar seus próprios padrões de formatação personalizados usando `DecimalFormatSymbols` para definir símbolos como o separador decimal e o símbolo de agrupamento de milhares.
- **Desempenho:** A criação de objetos `NumberFormat` pode ter um pequeno impacto no desempenho. Se você precisar formatar muitos números, considere reutilizar o mesmo objeto.

```java
DecimalFormatSymbols symbols = new DecimalFormatSymbols(new Locale("pt", "BR"));

NumberFormat formatador = new DecimalFormat("¤ #,##0.00;(¤ #,##0.00)", symbols);

NumberFormat formatador = NumberFormat.getCurrencyInstance(new Locale("pt", "BR"));
```
---
## Formatação Numérica Compacta

**Formatando números de forma concisa e clara**
Ao trabalhar com grandes quantidades de dados numéricos, especialmente em aplicações onde o espaço é limitado (como telas pequenas ou relatórios), a formatação compacta se torna essencial. Java oferece diversas ferramentas para formatar números de forma concisa, preservando a legibilidade e a precisão.

### DecimalFormat e seus padrões
A classe `DecimalFormat` é a principal ferramenta para formatar números em Java. Ela permite definir padrões personalizados para controlar o número de casas decimais, separadores de milhar e outros aspectos da formatação.

**Padrões básicos:**
- **#:** Dígito opcional.
- **0:** Dígito obrigatório.
- **,:** Separa grupos de milhar.
- **.:** Separa a parte inteira da parte decimal.

**Exemplo:**
```java
import java.text.DecimalFormat;

public class FormatacaoCompacta {
    public static void main(String[] args) {
        double valor = 1234567.89;

        // Formatando com duas casas decimais e separador de milhar
        DecimalFormat df = new DecimalFormat("#,##0.00");
        String valorFormatado = df.format(valor);
        System.out.println(valorFormatado); // Saída: 1,234,567.89
    }
}
```

### Formatação científica

Para números muito grandes ou muito pequenos, a notação científica é ideal. O padrão `E` indica a notação científica.

Java

```
DecimalFormat df = new DecimalFormat("0.###E0");
System.out.println(df.format(123456789)); // Saída: 1.235E8
```

### Formatação personalizada
Você pode criar padrões personalizados para atender a necessidades específicas. Por exemplo:

- **Sem casas decimais:** `#,##0`
- **Uma casa decimal:** `#,##0.0`
- **Número mínimo de dígitos:** `0000`

### Outras opções de formatação
- **NumberFormat:** Fornece métodos estáticos para obter instâncias de `NumberFormat` configuradas para diferentes tipos de formatação (moeda, porcentagem, número).
- **Locale:** Permite personalizar a formatação de acordo com as convenções de diferentes localidades.

#### Exemplo prático: Formatação de valores monetários
```java
import java.text.NumberFormat;
import java.util.Locale;

public class FormatacaoMonetaria {
    public static void main(String[] args) {
        double valor = 1234567.89;

        // Formatando para os EUA com duas casas decimais
        NumberFormat usFormat = NumberFormat.getCurrencyInstance(Locale.US);
        String valorUS = usFormat.format(valor);
        System.out.println("Valor em US: " + valorUS); // Saída: $1,234,567.89
    }
}
```

**Em resumo:**
A formatação numérica compacta em Java é uma ferramenta poderosa para apresentar dados de forma clara e concisa. Ao utilizar a classe `DecimalFormat` e os padrões de formatação adequados, você pode personalizar a aparência dos números de acordo com suas necessidades.

---
## Transformando Strings em Números com DecimalFormat

**Entendendo o Problema**
Frequentemente, em aplicações Java, nos deparamos com a necessidade de converter strings que representam números em valores numéricos para realizar cálculos ou outras operações. A classe `DecimalFormat` oferece uma ferramenta poderosa para formatar números, mas também pode ser utilizada para **parsear** strings em números, considerando diferentes formatos regionais e padrões numéricos.

**O Processo de Parsing**
Para converter uma string em um número utilizando `DecimalFormat`, seguimos estes passos:

1. **Criar um objeto DecimalFormat:**
    - Definimos o padrão de formato esperado para a string.
    - **Exemplo:** `{java}DecimalFormat df = new DecimalFormat("#,##0.00");`
2. **Utilizar o método parse():**
    - Passamos a string a ser parseada como argumento para o método `parse()`.
    - **Exemplo:** `{java}Number number = df.parse("1,234.56");`
3. **Converter o resultado para o tipo numérico desejado:**
    - O método `parse()` retorna um objeto `Number`. Podemos convertê-lo para `double`, `float`, `int` ou outros tipos numéricos, dependendo da necessidade.

**Exemplo Completo:**
```java
import java.text.DecimalFormat;
import java.text.ParseException;

public class ParseStringParaNumero {
    public static void main(String[] args) {
        String valorString = "1.234,56"; // String com formato brasileiro
        DecimalFormat df = new DecimalFormat("#,##0.00"); // Padrão brasileiro

        try {
            Number numero = df.parse(valorString);
            double valorDouble = numero.doubleValue();
            System.out.println("Valor em double: " + valorDouble);
        } catch (ParseException e) {
            System.out.println("Erro ao parsear: " + e.getMessage());
        }
    }
}
```

```java
 public static void main(String[] args) throws ParseException {
	String texto = "1.000,43";
	DecimalFormat formatador = new DecimalFormat("#,##0.00");
	formatador.setParseBigDecimal(true);

	BigDecimal valor = (BigDecimal) formatador.parse(texto);
	BigDecimal total = valor.add(new BigDecimal("1000"));

	System.out.println(total);
}
```

#### Considerações Importantes:
- **Padrão de formato:** O padrão de formato definido no `DecimalFormat` deve corresponder exatamente ao formato da string que você está tentando parsear.
- **Exceção ParseException:** Se a string não corresponder ao padrão, será lançada uma `ParseException`. É fundamental tratar essa exceção para evitar erros em tempo de execução.
- **Locale:** Para lidar com diferentes formatos regionais, utilize o construtor `DecimalFormat(String pattern, Locale locale)`.
- **Tipos numéricos:** O método `parse()` retorna um objeto `Number`. Você pode converter esse objeto para o tipo numérico desejado utilizando os métodos `doubleValue()`, `floatValue()`, `intValue()`, etc.

**Cenários Comuns:**
- **Lendo dados de arquivos:** Ao ler dados de arquivos CSV ou planilhas, os valores numéricos são frequentemente armazenados como strings.
- **Validando entrada do usuário:** Ao receber valores numéricos do usuário em um formulário, é importante validar se a entrada está no formato esperado.
- **Calculando valores:** Após converter as strings para números, você pode realizar cálculos matemáticos.

**Exemplo com Locale:**
```java
import java.text.NumberFormat;
import java.util.Locale;

public class ParseComLocale {
    public static void main(String[] args) {
        String valorString = "1.234,56"; // String com formato brasileiro
        NumberFormat df = NumberFormat.getInstance(Locale.FRANCE); // Formato francês

        try {
            Number numero = df.parse(valorString);
            System.out.println("Valor parseado: " + numero);
        } catch (ParseException e) {
            System.out.println("Erro ao parsear: " + e.getMessage());
        }
    }
}
```
---
