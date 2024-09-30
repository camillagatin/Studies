Uma string é uma sequência imutável de caracteres. Isso significa que, uma vez criada, o conteúdo de uma string não pode ser alterado. As strings são objetos da classe `java.lang.String` e são muito utilizadas para armazenar e manipular texto.

**Criando Strings:**

Existem duas formas principais de criar uma string:

- **Literais:**    

	`{java} String nome = "João da Silva";`
    
- **Usando o construtor:**
    
	`{java} String sobrenome = new String("Santos");`
    

#### Métodos importantes para manipulação de strings:
- **length():** Retorna o número de caracteres em uma string.
- **charAt(index):** Retorna o caractere em uma determinada posição.
- **indexOf(str):** Retorna o índice da primeira ocorrência de uma substring.
- **lastIndexOf(str):** Retorna o índice da última ocorrência de uma substring.
- **substring(beginIndex, endIndex):** Extrai uma substring entre os índices especificados.
- **concat(str):** Concatena duas strings.
- **toLowerCase():** Converte todos os caracteres para minúsculas.
- **toUpperCase():** Converte todos os caracteres para maiúsculas.
- **trim():** Remove espaços em branco no início e no final da string.
- **replace(oldChar, newChar):** Substitui todas as ocorrências de um caractere por outro.
- **split(regex):** Divide uma string em um array de substrings com base em um padrão.

**Exemplo:**
```java
String frase = "Olá, mundo!";

// Imprimindo o tamanho da string
System.out.println(frase.length());

// Obtendo o primeiro caractere
char primeiroCaractere = frase.charAt(0);
System.out.println(primeiroCaractere);

// Convertendo para maiúsculas
String fraseMaiuscula = frase.toUpperCase();
System.out.println(fraseMaiuscula);

// Dividindo a frase em palavras
String[] palavras = frase.split(" ");
for (String palavra : palavras) {
    System.out.println(palavra);
}
```

#### Por que as strings são imutáveis?
- **Segurança:** Evita modificações acidentais em dados sensíveis.
- **Eficiência:** Permite a otimização de memória e processamento, pois strings podem ser compartilhadas.
- **Concorrência:** Facilita a programação concorrente, pois strings não precisam ser sincronizadas.

##### Quando usar StringBuilder ou StringBuffer?
Se você precisa realizar muitas modificações em uma string, é mais eficiente utilizar `StringBuilder` ou `StringBuffer`. Essas classes são mutáveis e oferecem métodos para construir strings de forma mais eficiente. A principal diferença entre elas é que `StringBuilder` não é sincronizada, enquanto `StringBuffer` é sincronizada e adequada para ambientes multi-thread.

---
## Extraindo Trechos de Strings com indexOf e substring

**Entendendo os Métodos**
Ao trabalhar com strings em Java, os métodos `indexOf` e `substring` são ferramentas poderosas para manipular e extrair partes específicas de uma sequência de caracteres.

- **indexOf(String str):** Retorna o índice da primeira ocorrência da string `str` dentro da string original. Se a string não for encontrada, retorna -1.
- **substring(int beginIndex):** Retorna uma nova string que é uma subsequência da string original, começando no índice `beginIndex` e indo até o final da string.
- **substring(int beginIndex, int endIndex):** Retorna uma nova string que é uma subsequência da string original, começando no índice `beginIndex` e terminando antes do índice `endIndex`.

**Exemplo Prático**
```java
public class ExtrairTrechos {
    public static void main(String[] args) {
        String texto = "Este é um exemplo de string para extrair trechos.";
        
        // Encontrar a posição da palavra "exemplo"
        int posicaoExemplo = texto.indexOf("exemplo");
        
        // Extrair a substring a partir da palavra "exemplo" até o final
        String trecho = texto.substring(posicaoExemplo);
        System.out.println(trecho); // Imprime: "exemplo de string para extrair trechos."
        
        // Extrair apenas a palavra "exemplo"
        String palavraExemplo = texto.substring(posicaoExemplo, posicaoExemplo + 7);
        System.out.println(palavraExemplo); // Imprime: "exemplo"
    }
}
```

**Explicação do Código:**
1. **Declaração da String:** Uma string de exemplo é criada para demonstrar o uso dos métodos.
2. **Encontrando a Posição:** O método `indexOf` é usado para encontrar a posição da palavra "exemplo".
3. **Extraindo o Trecho:**
    - A partir da posição encontrada, o método `substring` extrai a parte restante da string.
    - Para extrair apenas a palavra "exemplo", é utilizado o `substring` com um intervalo específico.
4. **Imprimindo os Resultados:** Os resultados são impressos no console para visualização.

**Aplicações Comuns:**
- **Parse de Strings:** Extrair informações específicas de strings formatadas, como datas, nomes, IDs, etc.
- **Validação de Dados:** Verificar se uma string contém determinados padrões ou palavras-chave.
- **Manipulação de Textos:** Remover partes indesejadas de uma string, substituir caracteres, etc.
- **Processamento de Arquivos:** Ler e analisar o conteúdo de arquivos texto.

**Considerações Adicionais:**
- **Índices em Java:** Os índices em Java começam em 0.
- **Case Sensitivity:** O método `indexOf` é sensível a maiúsculas e minúsculas. Para realizar buscas independentes de caso, você pode converter a string para um formato comum antes de usar `indexOf`.
- **Múltiplas Ocorrências:** Para encontrar todas as ocorrências de uma substring, você pode utilizar um loop e o método `indexOf` repetidamente, ajustando o índice inicial a cada iteração.
- **Expressões Regulares:** Para padrões de busca mais complexos, as expressões regulares oferecem uma ferramenta mais poderosa.

**Exemplo com Expressões Regulares (Pattern e Matcher):**
```java
import java.util.regex.*;

// ... (código anterior)

// Encontrar todas as palavras que começam com "e"
Pattern pattern = Pattern.compile("\\bex\\w+");
Matcher matcher = pattern.matcher(texto);
while (matcher.find()) {
    System.out.println(matcher.group());
}
```
---
## Extraindo Trechos de Strings com lastIndexOf e substring

**Uma Ferramenta Complementar para suas Extrações**
Além do `indexOf`, o método `lastIndexOf` é outro aliado poderoso na hora de manipular strings em Java. Enquanto o `indexOf` busca a primeira ocorrência de uma substring, o `lastIndexOf` procura pela última.

**Entendendo o lastIndexOf**
- **lastIndexOf(String str):** Retorna o índice da **última** ocorrência da string `str` dentro da string original. Se a string não for encontrada, retorna -1.

**Combinando lastIndexOf e substring**
A combinação de `lastIndexOf` e `substring` é especialmente útil quando você precisa extrair partes de uma string a partir do final ou quando há múltiplas ocorrências de uma mesma substring e você está interessado na última.

**Exemplo Prático**
```java
public class ExtrairTrechos {
    public static void main(String[] args) {
        String texto = "Este é um exemplo de string que contém a palavra exemplo duas vezes.";

        // Encontrar a última posição da palavra "exemplo"
        int ultimaPosicaoExemplo = texto.lastIndexOf("exemplo");

        // Extrair a substring a partir da última ocorrência de "exemplo"
        String trechoFinal = texto.substring(ultimaPosicaoExemplo);
        System.out.println(trechoFinal); // Imprime: "exemplo duas vezes."

        // Extrair apenas a última palavra
        String ultimaPalavra = texto.substring(texto.lastIndexOf(" ") + 1);
        System.out.println(ultimaPalavra); // Imprime: "vezes."
    }
}
```

**Explicação do Código:**
1. **Encontrando a Última Posição:** O `lastIndexOf` localiza a última ocorrência de "exemplo".
2. **Extraindo o Trecho Final:** A partir dessa posição, o `substring` extrai o restante da string.
3. **Extraindo a Última Palavra:** Para extrair a última palavra, encontramos a posição do último espaço e utilizamos `substring` a partir dessa posição.

**Cenários de Uso**
- **Extraindo Extensões de Arquivos:** Ao trabalhar com nomes de arquivos, `lastIndexOf` pode ser usado para encontrar o ponto (`.`) e extrair a extensão.
- **Processando Logs:** Ao analisar logs, você pode extrair informações específicas, como datas ou IDs, que geralmente aparecem no final das linhas.
- **Manipulando URLs:** Extrair parâmetros de URLs, como query strings.

**Considerações Adicionais**
- **Múltiplos Delimitadores:** Para extrair partes de uma string delimitada por diferentes caracteres, você pode combinar `lastIndexOf` com `indexOf` e outros métodos de string.
- **Expressões Regulares:** Em casos mais complexos, as expressões regulares oferecem uma flexibilidade ainda maior para extrair padrões específicos.

**Exemplo com Expressões Regulares (Pattern e Matcher):**
```java
// ... (código anterior)

// Encontrar todas as palavras que terminam com "es"
Pattern pattern = Pattern.compile("\\b\\w+es\\b");
Matcher matcher = pattern.matcher(texto);
while (matcher.find()) {
    System.out.println(matcher.group());
}
```
---
## Transformando strings

- **Converter para Maiúsculas e Minúsculas:**
    - **toUpperCase():** Converte todos os caracteres para maiúsculas.
    - **toLowerCase():** Converte todos os caracteres para minúsculas.
	```java
	String texto = "Exemplo de Texto";
	String maiusculo = texto.toUpperCase();
	String minusculo = texto.toLowerCase();
	```
        
- **Substituir Caracteres:**
    - **replace(char oldChar, char newChar):** Substitui todas as ocorrências de um caractere por outro.
    - **replaceAll(String regex, String replacement):** Substitui todas as correspondências de uma expressão regular.
    ```java
    String texto = "Olá, mundo!";
    String novoTexto = texto.replace('o', 'a'); // Olá, munda!
    ```
        
- **Recortar Strings:**
    - **substring(int beginIndex):** Retorna uma substring a partir de um determinado índice.
    - **substring(int beginIndex, int endIndex):** Retorna uma substring entre dois índices.
    ```java
    String texto = "Java é divertido";
    String palavra = texto.substring(5, 9); // é di
    ```
        
- **Quebrar Strings:**
    - **split(String regex):** Divide uma string em um array de substrings com base em uma expressão regular.
    ```java
    String texto = "Maçã,Banana,Laranja";
    String[] frutas = texto.split(",");
    ```
        
- **Remover Espaços em Branco:**
    - **trim():** Remove espaços em branco no início e no final da string.
    ```java
    String texto = "   Java   ";
    String textoSemEspacos = texto.trim();
    ```
        
- **Formatar Strings:**
    - **String.format():** Formata strings usando placeholders.
	```java
    String nome = "Ana";
    int idade = 25;
    String frase = String.format("Olá, %s! Você tem %d anos.", nome, idade);
    ```  

#### Exemplo Completo: Formatação de Data
```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class FormatacaoData {
    public static void main(String[] args) {
        LocalDate hoje = LocalDate.now();
        DateTimeFormatter formatador = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        String    dataFormatada = hoje.format(formatador);
        System.out.println(dataFormatada);   
    }
}
```

#### Quando Usar Cada Método
- **Concatenar:** Para juntar strings simples.
- **Converter:** Para alterar o caso das letras.
- **Substituir:** Para modificar o conteúdo de uma string.
- **Recortar:** Para extrair partes específicas de uma string.
- **Quebrar:** Para dividir uma string em várias partes.
- **Remover Espaços:** Para limpar strings com espaços extras.
- **Formatar:** Para criar strings com um formato específico.

##### Considerações Adicionais
- **Imutável:** Strings em Java são imutáveis. Ao modificar uma string, você cria uma nova string.
- **StringBuilder:** Para operações de concatenação frequente, use `StringBuilder` para melhor desempenho.
- **Expressões Regulares:** Para padrões de busca e substituição mais complexos, utilize expressões regulares.
---
## Implementando Algoritmos com os Métodos da Classe String

A classe `String` em Java oferece um conjunto robusto de métodos que nos permitem manipular e transformar texto de diversas formas. Ao combinar esses métodos de maneira criativa, podemos implementar algoritmos para resolver uma variedade de problemas.

### Exemplos de Algoritmos

**1. Verificando Palíndromos:**
Um palíndromo é uma palavra ou frase que se lê da mesma forma de trás para frente, como "radar" ou "A cara rajada da Lara".
```java
public static boolean isPalindrome(String str) {
    str = str.replaceAll("\\s+", "").toLowerCase(); // Remove espaços e converte para minúsculas
    int length = str.length();
    for (int i = 0; i < length / 2; i++) {
        if (str.charAt(i) != str.charAt(length - i - 1)) {
            return false;
        }
    }
    return true;
}
```

**2. Contando a Ocorrência de um Caractere:**
```java
public static int countOccurrences(String str, char c) {
    int count = 0;
    for (int i = 0; i < str.length(); i++) {
        if (str.charAt(i) == c) {
            count++;
        }
    }
    return count;   
}
```

**3. Invertendo uma String:**
```java
public static String reverseString(String str) {
    return new StringBuilder(str).reverse().toString();
}
```

**4. Verificando Anagramas:**
Dois anagramas são palavras formadas pelas mesmas letras, porém em ordem diferente.
```java
public static boolean areAnagrams(String str1, String str2) {
    if (str1.length() != str2.length()) {
        return false;
    }
    char[] charArray1 = str1.toCharArray();
    char[] charArray2    = str2.toCharArray();
    Arrays.sort(charArray1);
    Arrays.sort(charArray2);
    return Arrays.equals(charArray1, charArray2);   
}
```

**5. Rotando uma String:**
```java
public static String rotateString(String str, int shift) {
    shift %= str.length();
    return str.substring(shift) + str.substring(0, shift);
}
```

### Outros Algoritmos Possíveis
- **Criptografia:** Cifras simples como a cifra de César podem ser implementadas usando operações de rotação e substituição de caracteres.
- **Validadores de Senhas:** Criar algoritmos para verificar se uma senha atende a critérios de complexidade, como ter letras maiúsculas, minúsculas, números e caracteres especiais.
- **Formatação de Textos:** Alinhar texto, justificar, criar tabelas simples, etc.
- **Análise de Texto:** Contar palavras, encontrar a palavra mais longa, calcular a frequência de letras, etc.
---
## Testando Correspondências de Strings com Expressões Regulares

**Expressões regulares** são ferramentas poderosas para encontrar padrões em texto. Em Java, elas são amplamente utilizadas para validar dados de entrada, extrair informações de strings e realizar diversas outras tarefas de manipulação de texto.

**Como funcionam as expressões regulares em Java?**
1. **Criação do padrão:** Você define um padrão usando uma string especial que segue a sintaxe das expressões regulares.
2. **Compilação do padrão:** O padrão é compilado em um objeto `Pattern`.
3. **Criação do matcher:** Um objeto `Matcher` é criado para aplicar o padrão a uma determinada string.
4. **Busca por correspondências:** O método `find()` do `Matcher` é usado para encontrar a próxima correspondência do padrão na string.

**Exemplo básico:**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexExample {
    public static void main(String[] args) {
        String    texto = "Meu email é exemplo@email.com";
        String regex = "\\w+@\\w+\\.\\w+"; // Padrão para endereços de email

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(texto);

        if (matcher.find()) {
            System.out.println("Endereço de email encontrado: " + matcher.group());
        } else {
            System.out.println("Endereço de email não encontrado");
        }
    }
}
```

**Quebrando o código:**
- `"\\w+@\\w+\\.\\w+"`: Essa é a expressão regular que representa um endereço de email básico.
    - `\w`: Corresponde a um caractere alfanumérico ou underscore.
    - `+`: Quantificador que indica uma ou mais ocorrências do caractere anterior.
    - `@`: Corresponde ao caractere literal @.
    - `.`: Corresponde ao caractere literal ponto.
- `Pattern.compile(regex)`: Cria um objeto `Pattern` a partir da expressão regular.
- `matcher.find()`: Busca pela primeira ocorrência do padrão na string.
- `matcher.group()`: Retorna a substring que corresponde ao padrão.

**Outros métodos úteis do Matcher:**
- **lookingAt()**: Verifica se o início da string corresponde ao padrão.
- **matches()**: Verifica se a string inteira corresponde ao padrão.
- **groupCount()**: Retorna o número de grupos de captura no padrão.
- **start(), end()**: Retorna o índice inicial e final da última correspondência encontrada.

**Exemplos de expressões regulares:**
- **Números:** `\\d+`
- **Datas:** `\\d{4}-\\d{2}-\\d{2}`
- **Palavras que começam com maiúscula:** `\\b[A-Z]\\w+`
- **Endereço de IP:** `\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}`

### Exemplos:
##### 1. Validando um CPF
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class ValidacaoCPF {
    public static void main(String[] args) {
        String cpf = "123.456.789-10";
        String regex = "\\d{3}\\.\\d{3}\\.\\d{3}-\\d{2}";

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(cpf);

        if (matcher.matches())    {
            System.out.println("CPF válido.");
        } else {
            System.out.println("CPF inválido.");   
        }
    }
}
```
**Explicação:**
- A expressão regular `\d{3}\.\d{3}\.\d{3}-\d{2}` verifica se a string possui exatamente 11 dígitos, separados por pontos e um hífen.

##### 2. Extraindo todas as palavras de uma string
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class ExtrairPalavras {
    public static void main(String[] args) {
        String texto = "Esta é uma frase com várias palavras.";
        String regex = "\\w+";

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(texto);

        while (matcher.find()) {
            System.out.println(matcher.group());   
        }
    }
}
```
**Explicação:**
- A expressão regular `\w+` encontra todas as sequências de um ou mais caracteres alfanuméricos ou underscores.

##### 3. Validando uma URL
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class ValidacaoURL {
    public static void main(String[] args) {
        String url = "https://www.example.com";
        String regex = "^(https?://)(www\\.)?[-a-z0-9]+(\\.[a-z]{2,}){1,3}$";

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(url);

        if (matcher.matches()) {
            System.out.println("URL válida.");
        } else {
            System.out.println("URL inválida.");
        }
    }
}
```
**Explicação:**
- A expressão regular é mais complexa e verifica o protocolo (http ou https), o subdomínio opcional (www.), o nome do domínio e a extensão.

##### 4. Encontrando todas as ocorrências de um tag HTML
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class EncontrarTagsHTML {
    public static void main(String[] args) {
        String html = "<p>Este é um parágrafo.</p><span>Este é um span.</span>";
        String regex = "<\\/?[a-z][^>]*>";

        Pattern pattern = Pattern.compile(regex, Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(html);

        while (matcher.find()) {
            System.out.println(matcher.group());   
        }
    }
}
```
**Explicação:**
- A expressão regular encontra tags HTML tanto de abertura quanto de fechamento. A flag `Pattern.CASE_INSENSITIVE` permite que a busca seja feita ignorando maiúsculas e minúsculas.
---
## A importância do StringBuilder para manipulação de strings

**Por que usar StringBuilder?**
Quando se trata de manipular strings em Java, o **StringBuilder** é uma ferramenta indispensável para garantir performance e eficiência. Ao contrário da classe `String` que é imutável, o `StringBuilder` permite a modificação direta de seus caracteres, evitando a criação de novos objetos a cada alteração.

**Quando usar StringBuilder?**
- **Concatenções frequentes:** Se você precisa concatenar muitas strings em um loop, o `StringBuilder` é a melhor opção. A cada concatenação com `String`, um novo objeto String é criado, o que pode levar a um consumo excessivo de memória e afetar o desempenho.
- **Modificações constantes:** Se você precisa inserir, remover ou substituir caracteres em uma string repetidamente, o `StringBuilder` oferece métodos eficientes para essas operações.
- **Construção de strings grandes:** Para construir strings muito grandes, o `StringBuilder` é mais eficiente do que concatenar strings com o operador `+`.

**Exemplo:**
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        // Usando StringBuilder
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 100000; i++) {
            sb.append("Olá, mundo! ");
        }
        String resultado = sb.toString();

        // Usando String (menos eficiente)
        String resultado2 = "";
        for (int i = 0; i < 100000; i++) {
            resultado2 += "Olá, mundo! ";
        }
    }
}
```

**Por que o StringBuilder é mais rápido?**
- **Mutabilidade:** O `StringBuilder` permite modificar a sequência de caracteres diretamente, sem criar novos objetos a cada alteração.
- **Alocação de memória:** O `StringBuilder` aloca um buffer de caracteres que pode ser redimensionado conforme necessário, evitando a realocação frequente de memória.

**Métodos importantes do StringBuilder:**
- **append(String str):** Adiciona uma string ao final do StringBuilder.
- **insert(int offset, String str):** Insere uma string em uma posição específica.  
- **delete(int start, int end):** Remove caracteres entre os índices start e end (exclusivo).
- **replace(int start, int end, String str):** Substitui caracteres entre os índices start e end por uma nova string.
- **toString():** Converte o StringBuilder em uma String.

**Quando usar StringBuffer?**
O `StringBuffer` é semelhante ao `StringBuilder`, mas é sincronizado, o que o torna seguro para uso em ambientes multithread. No entanto, a sincronização adiciona sobrecarga, tornando-o mais lento que o `StringBuilder`. Portanto, use `StringBuffer` apenas quando a sincronização for realmente necessária.

---
## Text Blocks: Uma nova forma de lidar com strings
Os **Text Blocks** foram introduzidos no Java 15 como uma forma mais concisa e legível de definir strings multilinha. Eles eliminam a necessidade de utilizar caracteres de escape para quebras de linha e aspas duplas dentro de strings, tornando o código mais limpo e fácil de entender.

**Como funcionam os Text Blocks?**
- **Delimitadores:** Um Text Block é delimitado por três aspas duplas (""").
- **Quebras de linha:** As quebras de linha dentro de um Text Block são preservadas como quebras de linha no valor da string.
- **Aspas duplas:** Não é necessário escapar aspas duplas dentro de um Text Block.
- **Indentação:** A indentação inicial do Text Block é removida automaticamente.

**Exemplo:**
```java
String multilineString = """
        Este é um exemplo de um Text Block.
        Podemos escrever texto em múltiplas linhas
        sem a necessidade de usar caracteres de escape.
        """;
```

**Comparando com a forma tradicional:**
```java
String multilineString = "Este é um exemplo de um Text Block.\n" +
        "Podemos escrever texto em múltiplas linhas\n" +
        "sem a necessidade de usar caracteres de escape.";
```

**Benefícios dos Text Blocks:**
- **Melhora a legibilidade:** O código fica mais limpo e fácil de entender, especialmente para strings grandes e complexas.
- **Reduz o número de caracteres:** Elimina a necessidade de caracteres de escape, tornando o código mais conciso.
- **Facilita a formatação:** Permite formatar o texto de forma mais natural, sem a necessidade de utilizar caracteres de escape para quebras de linha e tabulações.
- **Ideal para JSON, XML e SQL:** Os Text Blocks são perfeitos para representar esses tipos de dados, pois preservam a formatação original.

**Exemplo com JSON:**
```java
String json = """
        {
            "nome": "João",
            "idade": 30,
            "cidade": "São Paulo"
        }
        """;
```

**Outras funcionalidades:**
- **Interpolação de variáveis:** É possível inserir o valor de variáveis dentro de um Text Block usando a sintaxe ${variável}.
- **Escape de caracteres especiais:** Se necessário, você pode escapar caracteres especiais usando uma barra invertida ().

**Exemplo com interpolação:**
```java
String nome = "Maria";
String saudação = """
        Olá, ${nome}!
        Seja bem-vinda!
        """;
```

**Quando usar Text Blocks:**
- **Strings multilinha:** Sempre que você precisar definir strings com múltiplas linhas.
- **Formatação de texto:** Para formatar texto de forma mais natural e legível.
- **Representação de dados estruturados:** Para representar dados JSON, XML e SQL de forma concisa.
- **Documentação:** Para gerar documentação dentro do código.
---
