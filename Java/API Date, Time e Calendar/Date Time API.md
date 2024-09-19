## Introdução à Date and Time API e ao Padrão ISO-8601

### Por que a nova API?
Antes do Java 8, a manipulação de datas e horas em Java era considerada uma tarefa complexa e propensa a erros. As classes `Date` e `Calendar`, embora presentes, apresentavam uma série de limitações e comportamentos inconsistentes. A nova API de datas e horas, introduzida no Java 8, trouxe uma abordagem mais intuitiva e robusta para lidar com esses conceitos.

### O que é a ISO-8601?
O padrão ISO-8601 é uma norma internacional que define a representação de datas e horas de forma clara e concisa, evitando ambiguidades. Ele é amplamente utilizado em sistemas de informação e troca de dados, garantindo a interoperabilidade entre diferentes plataformas e aplicações.

### Principais classes da nova API
- **LocalDate:** Representa uma data sem informações de hora, como 2023-11-28.
- **LocalTime:** Representa um tempo sem informações de data, como 10:15:30.
- **LocalDateTime:** Combina data e hora, como 2023-11-28T10:15:30.
- **Instant:** Representa um ponto no tempo na linha do tempo, geralmente em relação ao UTC (Tempo Universal Coordenado).
- **ZonedDateTime:** Representa um instante em tempo, incluindo zona horária.

### Formatando datas e horas com ISO-8601
A nova API oferece uma forma simples de formatar datas e horas de acordo com o padrão ISO-8601 utilizando a classe `DateTimeFormatter`:
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class ExemploISO8601 {
    public static void main(String[] args) {
        LocalDateTime agora = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;   
        String dataHoraISO = agora.format(formatter);
        System.out.println(dataHoraISO); // Saída: 2023-11-28T14:30:00 (por exemplo)
    }
}
```

### Manipulando datas e horas
A API oferece diversos métodos para manipular datas e horas, como:

- **Adicionar ou subtrair:** `plusDays`, `minusHours`, `plusYears`, etc.
- **Comparar:** `isAfter`, `isBefore`, `isEqual`.
- **Extrair componentes:** `getYear`, `getMonth`, `getDayOfMonth`.

### Exemplo prático: Calculando a diferença entre duas datas
```java
import java.time.LocalDate;
import java.time.Period;

public class DiferencaEntreDatas {
    public static void main(String[] args) {
        LocalDate dataNascimento = LocalDate.of(1990, 1, 1);
        LocalDate hoje = LocalDate.now();
        Period periodo = Period.between(dataNascimento, hoje);
        System.out.println("Idade: " + periodo.getYears()    + " anos");
    }
}
```

### Benefícios da nova API
- **Facilidade de uso:** Sintaxe intuitiva e métodos concisos.
- **Imutável:** Objetos de data e hora são imutáveis, evitando modificações acidentais.
- **Orientada a objetos:** Modelagem clara dos conceitos de data e hora.
- **Suporte a zonas horárias:** Manipulação precisa de datas e horas em diferentes zonas horárias.
---
## Instant: Representando um Momento na Linha do Tempo

**O que é um Instant?**
Representa um ponto específico no tempo em relação ao Tempo Universal Coordenado (UTC). É como um carimbo de data e hora que marca um instante exato na linha do tempo.

**Por que usar Instant?**
- **Precisão:** O `Instant` oferece uma precisão de nanossegundos, ideal para aplicações que exigem alta precisão temporal, como sistemas de log, monitoramento de desempenho e transações financeiras.
- **Comparação:** Você pode comparar dois `Instant`s para determinar qual ocorreu primeiro ou se são iguais.
- **Conversão:** É possível converter um `Instant` para outras classes de data e hora, como `LocalDateTime` ou `ZonedDateTime`, para obter informações mais detalhadas ou adaptá-lo a diferentes zonas horárias.

**Criando um Instant:**
- **Agora:** Para obter o instante atual:
    `{java}Instant agora = Instant.now();`
    
- **A partir de uma época:** Para criar um `Instant` a partir de uma época específica (por exemplo, o Unix epoch, que começa em 1º de janeiro de 1970):
    `{java}Instant epoch = Instant.ofEpochMilli(0); // Instante inicial do Unix epoch`
    
- **A partir de um LocalDateTime:** Para criar um `Instant` a partir de um `LocalDateTime` em uma zona horária específica:
    ```java
    LocalDateTime dataHora = LocalDateTime.of(2023, 11, 28, 10, 15, 30);
    Instant instant = dataHora.atZone(ZoneId.of("America/Sao_Paulo")).toInstant();
    ```

**Manipulando Instants:**
- **Comparação:**
    ```java
    boolean ehIgual = instant1.equals(instant2);
    boolean ehAntes = instant1.isBefore(instant2);
    boolean ehDepois = instant1.isAfter(instant2);
    ```
    
- **Duração:**
    `{java}Duration duracao = Duration.between(instant1, instant2);`
    
- **Conversão:**
    ```java
	LocalDateTime localDateTime = instant.atZone(ZoneId.systemDefault()).toLocalDateTime();
    ZonedDateTime zonedDateTime = instant.atZone(ZoneId.of("UTC"));
    ```
	```java
	Calendar calendar = Calendar.getInstance();
	Instant instante = calendar.toInstant();

	System.out.println(calendar.getTime());
	System.out.println(instante);
	```
	```java
	Instant instante = Instant.now();
	Date data = Date.from(instante);

	System.out.println(instante);
	System.out.println(data);
	```
	```java
	Date data = new Date();
	Instant instante = data.toInstant();

	System.out.println(data);
	System.out.println(instante);
	```

#### Exemplo prático: Medindo a duração de uma operação:
```java
import java.time.Duration;
import java.time.Instant;

public class MedindoDuracao {
    public static void main(String[] args) {
        Instant inicio = Instant.now();

        // Código que você deseja medir a duração

        Instant fim = Instant.now();

        Duration duracao = Duration.between(inicio, fim);
        System.out.println("Duração: " + duracao.toMillis() + " milissegundos");
    }
}
```

```java
Instant instante = Instant.now();
System.out.println(instante);

System.out.println(instante.toEpochMilli());
System.out.println(System.currentTimeMillis());
```
---
## LocalDate: Representando Apenas as Datas

O **LocalDate** é uma classe da nova API de datas e horas do Java 8 que representa uma data sem informações de hora. É ideal para representar datas como aniversários, datas de vencimento ou qualquer outra data que não exija a especificação de um horário.

**Por que usar LocalDate?**
- **Simplicidade:** Ao trabalhar apenas com datas, o LocalDate torna o código mais limpo e fácil de entender.
- **Imutável:** Objetos LocalDate são imutáveis, o que significa que você não pode modificá-los após a criação, garantindo a consistência dos dados.
- **Operações:** Permite realizar uma variedade de operações com datas, como adição e subtração de dias, meses e anos, além de comparação entre datas.

**Criando um LocalDate:**
- **Data atual:**
    `{java}LocalDate hoje = LocalDate.now();`
    
- **Data específica:**
    `{java}LocalDate dataNascimento = LocalDate.of(1990, 1, 1);`


**Manipulando LocalDate:**
- **Adicionar ou subtrair:**
    ```java
    LocalDate dataFutura = hoje.plusDays(30);
    LocalDate dataPassada = hoje.minusMonths(2);
    ```
    
- **Extrair componentes:**
    ```java
    int ano = hoje.getYear();
    int mes = hoje.getMonthValue();
    int dia = hoje.getDayOfMonth();
    ```
    
- **Comparar:**
    ```java
    boolean ehAntes = dataNascimento.isBefore(hoje);
    boolean ehDepois = dataNascimento.isAfter(hoje);
    ```
    

**Exemplo prático: Calculando a idade:**
```java
import java.time.LocalDate;
import java.time.Period;

public class CalculandoIdade {
    public static void main(String[] args) {
        LocalDate dataNascimento = LocalDate.of(1990, 1, 1);
        LocalDate hoje = LocalDate.now();

        Period periodo = Period.between(dataNascimento, hoje);
        System.out.println("Idade: " + periodo.getYears()    + " anos");
    }
}
```

```java
LocalDate diaDoProgramador = LocalDate.ofYearDay(2022, 256);
System.out.println(diaDoProgramador);
```

**Comparação com a classe Date:**

|Característica|Date|LocalDate|
|---|---|---|
|Mutabilidade|Mutável|Imutável|
|Zona horária|Sensível a zona horária|Insensível a zona horária|
|Facilidade de uso|Menos intuitiva|Mais intuitiva e fácil de usar|

**Quando usar LocalDate:**
- **Datas sem hora:** Aniversários, datas de vencimento, feriados.
- **Cálculos simples:** Adição, subtração e comparação de datas.
- **Formatação:** Usando DateTimeFormatter para formatar a data de acordo com suas necessidades.
---
## LocalTime: Representando Horários sem Data

O **LocalTime** é uma classe da nova API de datas e horas do Java 8 que representa um horário específico sem informações de data. É ideal para representar horários de eventos, horários de abertura e fechamento, ou qualquer outro horário que não esteja vinculado a uma data específica.

**Por que usar LocalTime?**
- **Simplicidade:** Ao trabalhar apenas com horários, o LocalTime torna o código mais limpo e fácil de entender.
- **Imutável:** Objetos LocalTime são imutáveis, o que significa que você não pode modificá-los após a criação, garantindo a consistência dos dados.
- **Operações:** Permite realizar uma variedade de operações com horários, como adição e subtração de horas, minutos e segundos, além de comparação entre horários.

**Criando um LocalTime:**
- **Horário atual:**
    `{java}LocalTime agora = LocalTime.now();`
    
- **Horário específico:**
    `{java}LocalTime horarioReuniao = LocalTime.of(10, 15); // 10h15`
    

**Manipulando LocalTime:**
- **Adicionar ou subtrair:**
  ```java
    LocalTime horarioFinal = horarioReuniao.plusHours(2);
    LocalTime horarioInicio = horarioFinal.minusMinutes(30);
    ```
    
- **Extrair componentes:**
    ```java
    int hora = horarioReuniao.getHour();
    int minuto = horarioReuniao.getMinute();
    int segundo = horarioReuniao.getSecond();
    ```
    
- **Comparar:**
    ```java
    boolean ehAntes = horarioReuniao.isBefore(agora);
    boolean ehDepois = horarioReuniao.isAfter(agora);
    ```
    

**Exemplo prático: Calculando a duração de uma reunião:**
```java
import java.time.Duration;
import java.time.LocalTime;

public class CalculandoDuracaoReuniao {
    public static void main(String[] args) {
        LocalTime inicioReuniao = LocalTime.of(10, 0);
        LocalTime fimReuniao = LocalTime.of(12, 30);

        Duration duracao = Duration.between(inicioReuniao, fimReuniao);
        System.out.println("Duração da reunião: " + duracao.toMinutes() + " minutos");
    }
}
```

**Comparação com a classe Date:**

|Característica|Date|LocalTime|
|---|---|---|
|Mutabilidade|Mutável|Imutável|
|Zona horária|Sensível a zona horária|Insensível a zona horária|
|Facilidade de uso|Menos intuitiva|Mais intuitiva e fácil de usar|
**Quando usar LocalTime:**
- **Horários sem data:** Horários de eventos, horários de abertura e fechamento, horários de voos.
- **Cálculos simples:** Adição, subtração e comparação de horários.
- **Formatação:** Usando DateTimeFormatter para formatar o horário de acordo com suas necessidades.
---
## LocalDateTime: Representando Data e Hora

O **LocalDateTime** é uma classe da nova API de datas e horas do Java 8 que combina as funcionalidades de **LocalDate** e **LocalTime**, representando um instante específico no tempo, incluindo tanto a data quanto a hora. É ideal para representar eventos que ocorrem em um momento preciso, como reuniões, compromissos ou registros de log.

### Por que usar LocalDateTime?
- **Completude:** Ao representar tanto a data quanto a hora, o LocalDateTime oferece uma visão mais completa de um ponto no tempo.
- **Imutável:** Assim como LocalDate e LocalTime, os objetos LocalDateTime são imutáveis, garantindo a consistência dos dados.
- **Operações:** Permite realizar uma ampla variedade de operações com datas e horas, como adição e subtração de dias, horas, minutos e segundos, além de comparação entre instantes.

### Criando um LocalDateTime:
- **Data e hora atuais:**
    `{java}LocalDateTime agora = LocalDateTime.now();`
    
- **Data e hora específicas:**
    `{java}LocalDateTime reuniao = LocalDateTime.of(2023, 11, 28, 10, 15); // 28/11/2023 10:15`
    

### Manipulando LocalDateTime:
- **Adicionar ou subtrair:**
   ```java
    LocalDateTime reuniaoFinal = reuniao.plusHours(2);
    LocalDateTime reuniaoInicio = reuniaoFinal.minusMinutes(30);
    ```
    
- **Extrair componentes:**
    ```java
    int ano = reuniao.getYear();
    int mes = reuniao.getMonthValue();
    int dia = reuniao.getDayOfMonth();
    int hora = reuniao.getHour();
    int minuto = reuniao.getMinute();
    int segundo = reuniao.getSecond();
    ```
    
- **Comparar:**
    ```java
    boolean ehAntes = reuniao.isBefore(agora);
    boolean ehDepois = reuniao.isAfter(agora);
    ```

### Exemplo prático: Calculando a duração de um evento:
```java
import java.time.Duration;
import java.time.LocalDateTime;

public class CalculandoDuracaoEvento {
    public static void main(String[] args) {
        LocalDateTime inicioEvento = LocalDateTime.of(2023, 11, 28, 10, 0);
        LocalDateTime fimEvento = LocalDateTime.of(2023, 11, 28, 12, 30);

        Duration duracao = Duration.between(inicioEvento, fimEvento);
        System.out.println("Duração do evento: " + duracao.toMinutes() + " minutos");
    }
}
```

### Comparação com as classes Date e Calendar:

|Característica|Date|Calendar|LocalDateTime|
|---|---|---|---|
|Mutabilidade|Mutável|Mutável|Imutável|
|Zona horária|Sensível a zona horária|Sensível a zona horária|Insensível a zona horária (mas pode ser convertida para ZonedDateTime para lidar com zonas horárias)|
|Facilidade de uso|Menos intuitiva|Complexa|Mais intuitiva e fácil de usar|
### Quando usar LocalDateTime:
- **Eventos com data e hora:** Reuniões, compromissos, registros de log.
- **Cálculos complexos:** Adição, subtração e comparação de datas e horas.
- **Formatação:** Usando DateTimeFormatter para formatar a data e hora de acordo com suas necessidades.
---
## Outras Formas de Obter Instâncias de LocalDate, LocalTime e LocalDateTime
Além dos métodos `now()` e `of()` que já vimos, a nova API de datas e horas do Java 8 oferece diversas outras formas de criar instâncias de `LocalDate`, `LocalTime` e `LocalDateTime`. Vamos explorar algumas delas:

### **A partir de Strings:**
- **Usando o método `parse()`:**
    ```java
    LocalDate dataNascimento = LocalDate.parse("1990-01-01");
    LocalTime horaReuniao = LocalTime.parse("10:15");
    LocalDateTime evento = LocalDateTime.parse("2023-11-28T10:15:30");
    ```
    **Importante:** O formato da string deve corresponder ao padrão ISO 8601 por padrão. Para outros formatos, você pode utilizar `DateTimeFormatter`.
    
- **Usando o `DateTimeFormatter`:**
    ```java
    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
    LocalDate data = LocalDate.parse("28/11/2023", formatter);
    ```

### **A partir de um Instant:**
- **Convertendo um Instant para LocalDate, LocalTime ou LocalDateTime:**
    ```java
    Instant instant = Instant.now();
    LocalDate data = instant.atZone(ZoneId.systemDefault()).toLocalDate();
    LocalTime hora = instant.atZone(ZoneId.systemDefault()).toLocalTime();
    LocalDateTime dataHora = instant.atZone(ZoneId.systemDefault()).toLocalDateTime();
    ```

### **A partir de um Calendar:**
- **Convertendo um Calendar para LocalDate, LocalTime ou LocalDateTime:**
    ```java
    Calendar calendar = Calendar.getInstance();
    LocalDate data = calendar.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
    ```

### **Outros métodos úteis:**
- **Criando datas a partir de um dia do ano:**
   `{java}LocalDate diaDoAno = LocalDate.ofYearDay(2023, 100); // 100º dia de 2023`
    
- **Criando datas com base em campos:**
    `{java}LocalDate data = LocalDate.of(2023, Month.NOVEMBER, 28);`
    

### **Considerações importantes:**
- **Zona horária:** Ao converter um `Instant` ou um `Calendar` para `LocalDate`, `LocalTime` ou `LocalDateTime`, é crucial especificar a zona horária desejada usando `ZoneId`.
- **Formato:** Ao usar o método `parse()`, assegure-se que o formato da string esteja correto e corresponda ao padrão utilizado.
- **DateTimeFormatter:** O `DateTimeFormatter` permite personalizar a forma como as datas e horários são formatados e analisados.

**Exemplo completo:**
```java
import java.time.*;
import java.time.format.DateTimeFormatter;

public class ExemploCriacaoDatas {
    public static void main(String[] args) {
        // Usando now()
        LocalDate hoje = LocalDate.now();
        LocalTime agora = LocalTime.now();
        LocalDateTime nesteMomento = LocalDateTime.now();

        // Usando of()
        LocalDate natal = LocalDate.of(2023, 12, 25);
        LocalTime meiaNoite = LocalTime.of(0, 0);

        // Usando parse()
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        LocalDate dataFormatada = LocalDate.parse("28/11/2023", formatter);

        // Usando Instant
        Instant instant = Instant.now();
        LocalDate dataAPartirDeInstant = instant.atZone(ZoneId.systemDefault()).toLocalDate();

        // Imprimindo os resultados
        System.out.println(hoje);
        System.out.println(agora);
        System.out.println(nesteMomento);
        System.out.println(natal);
        System.out.println(meiaNoite);
        System.out.println(dataFormatada);
        System.out.println(dataAPartirDeInstant);
    }
}
```
---
## Formatando Data e Hora na Nova API
A nova API de datas e horas do Java 8 oferece uma maneira muito flexível e intuitiva de formatar datas e horas utilizando a classe `DateTimeFormatter`. Essa classe permite criar padrões personalizados para exibir datas e horas de acordo com suas necessidades específicas.

### O que é o DateTimeFormatter?
É uma classe que define regras para formatar e analisar datas e horas. Ela utiliza um padrão de formato para especificar como os componentes de uma data ou hora (ano, mês, dia, hora, minuto, segundo) devem ser representados em uma string.

### Criando um DateTimeFormatter
Você pode criar um `DateTimeFormatter` de diversas maneiras:

- **Padrões predefinidos:**
    ```java
    DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE; // Formato ISO para data
    DateTimeFormatter formatterHora = DateTimeFormatter.ofPattern("HH:mm:ss"); // Hora no formato 24h
    ```
    
- **Padrões personalizados:**
    `{java}DateTimeFormatter formatterBR = DateTimeFormatter.ofPattern("dd/MM/yyyy"); // Formato brasileiro`
    
### Formatando uma data ou hora
Para formatar uma data ou hora, você utiliza o método `format()` do objeto `DateTimeFormatter`:

```java
LocalDateTime agora = LocalDateTime.now();
String dataFormatada = formatterBR.format(agora);
System.out.println(dataFormatada); // Saída: 28/11/2023 (por exemplo)
```

### Padrões de formatação
Os padrões de formatação são compostos por letras que representam diferentes componentes da data e hora. Alguns dos padrões mais comuns são:

- **y:** Ano
- **M:** Mês
- **d:** Dia do mês
- **H:** Hora (24 horas)
- **m:** Minuto
- **s:** Segundo
- **S:** Fração de segundo

Você pode combinar esses padrões para criar formatos personalizados. Por exemplo:
- `yyyy-MM-dd HH:mm:ss` - Formato ISO 8601 completo
- `dd/MM/yyyy` - Formato brasileiro
- `EEEE, dd 'de' MMMM 'de' yyyy` - Dia da semana por extenso, dia do mês, mês por extenso e ano (por exemplo, "segunda-feira, 28 de novembro de 2023")

### Analisando uma string para obter uma data ou hora
O método `parse()` do `DateTimeFormatter` é utilizado para converter uma string formatada em um objeto de data ou hora:

```java
String dataString = "2023-11-28";
LocalDate data = LocalDate.parse(dataString);
```

### Exemplo completo:
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class FormatacaoDataHora {
    public static void main(String[] args) {
        LocalDateTime agora = LocalDateTime.now();

        // Formatos predefinidos
        String isoData = agora.format(DateTimeFormatter.ISO_LOCAL_DATE);
        String isoHora = agora.format(DateTimeFormatter.ISO_LOCAL_TIME);

        // Formato personalizado
        DateTimeFormatter formatterBR = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
        String dataHoraBR = agora.format(formatterBR);

        // Analisando uma string
        String dataString = "2023-11-28";
        LocalDate data = LocalDate.parse(dataString);

        System.out.println("ISO Data: " + isoData);
        System.out.println("ISO Hora: " + isoHora);
        System.out.println("Formato Brasileiro: " + dataHoraBR);
        System.out.println("Data a partir de string: " + data);
    }
}
```
---
