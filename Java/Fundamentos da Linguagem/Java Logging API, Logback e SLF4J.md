## Por que Fazer Logging?
**O logging é uma prática fundamental no desenvolvimento de software e desempenha um papel crucial na manutenção, depuração e otimização de aplicações.** Ao registrar informações sobre a execução de um programa, os logs fornecem um histórico detalhado que pode ser analisado posteriormente para identificar problemas, entender o comportamento do sistema e tomar decisões informadas.

**Principais Razões para Fazer Logging:**
* **Depuração:**
    * **Identificação de erros:** Ao registrar informações sobre exceções, erros e eventos inesperados, os logs ajudam a localizar a causa raiz de problemas e facilitar a correção de bugs.
    * **Rastreio de fluxo:** Ao registrar o fluxo de execução de uma aplicação, os logs permitem acompanhar a jornada de uma requisição desde a entrada até a saída, facilitando a identificação de pontos de falha.
* **Monitoramento:**
    * **Verificação da saúde do sistema:** Os logs podem ser utilizados para monitorar a performance de uma aplicação, identificar gargalos e detectar possíveis problemas de desempenho.
    * **Detecção de anomalias:** Ao analisar padrões nos logs, é possível identificar comportamentos anômalos que podem indicar ataques ou falhas de segurança.
* **Auditoria:**
    * **Registro de atividades:** Os logs podem ser utilizados para registrar todas as ações realizadas em um sistema, o que é fundamental para fins de auditoria e conformidade com regulamentações.
    * **Investigação de incidentes:** Em caso de incidentes de segurança, os logs podem fornecer pistas importantes para identificar a origem do problema e tomar as medidas necessárias.
* **Otimização:**
    * **Análise de performance:** Os logs podem ser utilizados para analisar o desempenho de diferentes partes de uma aplicação e identificar oportunidades de otimização.
    * **Identificação de gargalos:** Ao registrar informações sobre o tempo de execução de diferentes operações, os logs podem ajudar a identificar os pontos críticos que estão limitando a performance do sistema.

**Benefícios do Logging:**
* **Redução do tempo de resolução de problemas:** Ao ter acesso a informações detalhadas sobre o funcionamento da aplicação, é possível identificar e corrigir problemas de forma mais rápida.
* **Melhoria da qualidade do software:** O logging contribui para a criação de software mais robusto e confiável.
* **Aumento da segurança:** Ao registrar todas as atividades do sistema, os logs ajudam a proteger a aplicação contra ataques e fraudes.
* **Facilitação da colaboração:** Os logs podem ser compartilhados entre os membros da equipe, facilitando a colaboração e a resolução de problemas complexos.
---
## Principais Frameworks de Logging
* **Logback:** Considerado um dos frameworks mais populares e performáticos, o Logback oferece uma ampla gama de recursos, como filtros, appenders e encoders, além de ser altamente configurável através de arquivos XML. É amplamente utilizado em projetos Java devido à sua flexibilidade e eficiência.
* **Log4j:** Predecessor do Logback, o Log4j ainda é bastante utilizado em projetos mais antigos. Embora não seja tão moderno quanto o Logback, continua sendo uma opção robusta e confiável para muitas aplicações.
* **SLF4J:** Não é exatamente um framework de logging, mas sim uma fachada que abstrai a implementação do logging, permitindo que você troque o framework de logging subjacente sem precisar modificar seu código. SLF4J é comumente utilizado em conjunto com Logback ou Log4j.
* **Java Util Logging:** Framework de logging nativo do Java, oferece uma solução simples e básica para registrar informações. No entanto, pode ser limitado em termos de recursos e performance quando comparado a frameworks mais especializados como Logback e Log4j.
* **Outros:** Existem outros frameworks de logging disponíveis, como o Commons Logging, o JUL (Java Util Logging) e o Log4net (para .NET), cada um com suas próprias características e áreas de aplicação.

**Como escolher o framework ideal?**
A escolha do framework de logging ideal depende de diversos fatores, como:
* **Complexidade do projeto:** Para projetos simples, o Java Util Logging pode ser suficiente. Para projetos mais complexos, frameworks como Logback ou Log4j oferecem mais recursos e flexibilidade.
* **Performance:** Se a performance for uma preocupação, o Logback é geralmente considerado o mais rápido.
* **Facilidade de configuração:** A configuração dos frameworks pode variar, sendo o Logback conhecido por sua configuração XML intuitiva.
* **Comunidade:** A existência de uma comunidade ativa e documentação extensa pode ser um fator importante na escolha do framework.

**Características importantes de um framework de logging:**
* **Níveis de log:** Permitem controlar a quantidade de informações registradas, como DEBUG, INFO, WARN, ERROR.
* **Appenders:** Definem onde os logs serão armazenados, como em arquivos, console ou banco de dados.
* **Layout:** Formata as mensagens de log para facilitar a leitura e análise.
* **Filtros:** Permitem filtrar as mensagens de log com base em critérios específicos.
* **Performance:** Um bom framework de logging deve ter baixo impacto no desempenho da aplicação.
---
## Utilizando a Java Logging API (JUL)
A Java Logging API (JUL), também conhecida como `java.util.logging`, é um framework de logging integrado à linguagem Java. Embora seja mais simples que frameworks como Logback ou Log4j, ela oferece uma base sólida para o registro de informações em aplicações Java.

**Conceitos Básicos:**
* **Logger:** Um objeto que representa uma categoria de log.
* **Handler:** Define onde as mensagens de log serão enviadas (console, arquivo, etc.).
* **Formatter:** Formata as mensagens de log antes de serem enviadas para o handler.
* **Level:** Define a severidade de uma mensagem de log (SEVERE, WARNING, INFO, CONFIG, FINE, FINER, FINEST).

**Exemplo Básico:**
```java
import java.util.logging.Logger;

public class MeuPrograma {
    private static final Logger logger = Logger.getLogger(MeuPrograma.class.getName());

    public static void main(String[] args) {
        logger.info("Iniciando o programa.");

        // ... código do programa

        logger.severe("Ocorreu um erro grave.");
    }
}
```
**Explicação:**
1. **Obtendo um Logger:** A linha `Logger.getLogger(MeuPrograma.class.getName());` obtém um logger associado à classe `MeuPrograma`.
2. **Registrando Mensagens:** Os métodos `info`, `severe`, etc., são usados para registrar mensagens de diferentes níveis de severidade.
3. **Níveis de Log:** O nível `INFO` indica uma mensagem informativa, enquanto `SEVERE` indica um erro grave.

```java
// logger.info(String.format("Saque de R$%.2f realizado na conta %s", valorSaque, getAgencia() + "/" + getNumero()));

logger.log(Level.INFO, "Saque de R${0} realizado na conta {1}", new Object[] { valorSaque, getAgencia() + "/" + getNumero() });

```

**Configurando o JUL:**
A configuração do JUL pode ser feita de forma programática ou através de um arquivo de configuração. O arquivo de configuração geralmente é no formato `properties` e especifica os handlers, formatters e níveis de log.

**Exemplo de arquivo de configuração (logging.properties):**
```properties
handlers= java.util.logging.ConsoleHandler

java.util.logging.ConsoleHandler.level = ALL
java.util.logging.ConsoleHandler.formatter = java.util.logging.SimpleFormatter
```

**Carregando a configuração:**
```java
import java.util.logging.LogManager;

public class MeuPrograma {
    // ...

    public static void main(String[] args) throws Exception {
        LogManager.getLogManager().readConfiguration(
            MeuPrograma.class.getResourceAsStream("logging.properties"));
        // ...
    }
}
```

**Vantagens do JUL:**
* **Simples de usar:** Fácil de aprender e configurar.
* **Integrado ao Java:** Não requer bibliotecas externas.
* **Flexível:** Permite personalizar handlers, formatters e níveis de log.

**Limitações do JUL:**
* **Performance:** Pode não ser tão performático quanto frameworks como Logback para aplicações de alta carga.
* **Funcionalidades:** Oferece menos funcionalidades e flexibilidade em comparação com outros frameworks.
---
## Níveis de Log no JUL
Os níveis de log no Java Util Logging (JUL) são como um semáforo que controla a quantidade de informação que você deseja registrar sobre a execução de sua aplicação. Cada nível representa um grau de severidade ou importância de uma mensagem de log.

**Por que os níveis de log são importantes?**
* **Controle da verbosidade:** Ao definir um nível de log, você determina quais tipos de mensagens serão registradas.
* **Facilidade de depuração:** Durante o desenvolvimento, você pode registrar mensagens detalhadas (níveis mais baixos) para identificar problemas. Em produção, você pode reduzir o nível de log para evitar logs excessivos.
* **Análise de performance:** Ao registrar informações sobre o desempenho da aplicação, você pode identificar gargalos e otimizar o código.

**Os Níveis de Log no JUL:**
Os níveis de log no JUL são hierárquicos, ou seja, um logger com um determinado nível também registrará mensagens de níveis mais altos. Os níveis, do mais grave ao menos grave, são:
* **SEVERE:** Erros graves que podem causar a falha da aplicação.
* **WARNING:** Condições que podem levar a problemas no futuro.
* **INFO:** Informações gerais sobre o funcionamento da aplicação.
* **CONFIG:** Informações sobre a configuração da aplicação.
* **FINE:** Informações mais detalhadas para depuração.
* **FINER:** Informações ainda mais detalhadas.
* **FINEST:** Nível mais detalhado, geralmente usado para depuração muito específica.

**Exemplo:**
```java
import java.util.logging.Logger;

public class MeuPrograma {
    private static final Logger logger = Logger.getLogger(MeuPrograma.class.getName());

    public static void main(String[] args) {
        logger.fine("Entrando no método principal.");
        logger.info("Iniciando o processamento.");
        logger.warning("Um recurso pode estar esgotado.");
        logger.severe("Ocorreu um erro crítico.");
    }
}
```

**Configurando os Níveis de Log:**
Você pode configurar os níveis de log de forma programática ou através de um arquivo de configuração.

* **Programáticamente:**
```java
import java.util.logging.Level;
import java.util.logging.Logger;

// ...

logger.setLevel(Level.INFO); // Registrará apenas mensagens de nível INFO ou superior
```

* **Através do arquivo de configuração:**
```properties
handlers= java.util.logging.ConsoleHandler

java.util.logging.ConsoleHandler.level = INFO
```
---
## Criando logging.properties e Configurando Níveis de Log
O arquivo `logging.properties` é fundamental para personalizar o comportamento do Java Util Logging (JUL). Ele define onde os logs serão armazenados, como serão formatados e quais níveis de log serão registrados.

### Estrutura Básica do Arquivo
Um arquivo `logging.properties` típico possui a seguinte estrutura:
```properties
handlers= java.util.logging.ConsoleHandler

java.util.logging.ConsoleHandler.level = ALL
java.util.logging.ConsoleHandler.formatter = java.util.logging.SimpleFormatter
```
**Explicação:**
* **handlers:** Especifica quais *handlers* serão utilizados. Um *handler* define onde as mensagens de log serão enviadas (console, arquivo, etc.).
* **java.util.logging.ConsoleHandler.level:** Define o nível de log mínimo para o *handler* do console. Neste caso, `ALL` significa que todas as mensagens serão registradas.
* **java.util.logging.ConsoleHandler.formatter:** Define o formato das mensagens de log. `SimpleFormatter` é um formatador padrão que fornece informações básicas sobre a mensagem.

### Configurando Níveis de Log
Para configurar os níveis de log, você precisa modificar a propriedade `level` do *handler* desejado. Por exemplo, para registrar apenas mensagens de nível `INFO` ou superior:
```properties
handlers= java.util.logging.ConsoleHandler

java.util.logging.ConsoleHandler.level = INFO
java.util.logging.ConsoleHandler.formatter = java.util.logging.SimpleFormatter
```

**Outros Níveis de Log:**
* **SEVERE:** Erros graves
* **WARNING:** Avisos
* **INFO:** Informações gerais
* **CONFIG:** Informações de configuração
* **FINE:** Informações mais detalhadas
* **FINER:** Informações ainda mais detalhadas
* **FINEST:** Informações extremamente detalhadas

### Criando um Handler para Arquivo
Para registrar logs em um arquivo, você pode utilizar o *handler* `FileHandler`:
```properties
handlers= java.util.logging.FileHandler

java.util.logging.FileHandler.pattern = mylog.%g.log
java.util.logging.FileHandler.limit = 50000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
```
**Explicação:**
* **pattern:** Define o padrão do nome do arquivo de log. `%g` é um marcador que será substituído por um número sequencial.
* **limit:** Define o tamanho máximo em bytes de cada arquivo de log.
* **count:** Define o número máximo de arquivos de log que serão criados.

### Carregando o Arquivo de Configuração
Para carregar o arquivo `logging.properties`, utilize o seguinte código:
```java
import java.util.logging.LogManager;

public class MeuPrograma {
    public static void main(String[] args) throws Exception {
        LogManager.getLogManager().readConfiguration(
            MeuPrograma.class.getResourceAsStream("logging.properties"));
        // ...
    }
}
```

### Personalizando o Formato das Mensagens
Você pode personalizar o formato das mensagens de log utilizando diferentes formatadores. O `SimpleFormatter` é o mais simples, mas existem outros formatadores mais complexos que permitem formatar as mensagens de acordo com suas necessidades.

### Exemplo
```properties
handlers= java.util.logging.FileHandler

java.util.logging.FileHandler.pattern = mylog.%g.log
java.util.logging.FileHandler.limit = 50000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.level = INFO
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
```
Com este arquivo de configuração, os logs serão registrados em arquivos nomeados `mylog.1.log`, `mylog.2.log`, etc., cada um com no máximo 50.000 bytes. Serão criados no máximo 10 arquivos. Apenas mensagens de nível `INFO` ou superior serão registradas.

---
## Salvando Logs em Arquivos com FileHandler do JUL
O **FileHandler** é um componente essencial do Java Util Logging (JUL) que permite direcionar as mensagens de log para arquivos, possibilitando um armazenamento mais permanente e organizado das informações.

### Como Configurar o FileHandler
Para configurar o FileHandler, você precisa adicionar as seguintes propriedades ao seu arquivo `logging.properties`:

* **handlers:** Especifica qual handler será utilizado. Nesse caso, `java.util.logging.FileHandler`.
* **pattern:** Define o padrão do nome do arquivo de log.
* **limit:** Define o tamanho máximo (em bytes) de cada arquivo de log.
* **count:** Define o número máximo de arquivos de log que serão criados.
* **level:** Define o nível de log mínimo para o handler.
* **formatter:** Define o formatador que será utilizado para formatar as mensagens de log.

**Exemplo:**
```properties
handlers= java.util.logging.FileHandler

java.util.logging.FileHandler.pattern = mylog.%g.log
java.util.logging.FileHandler.limit = 50000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
```
**Explicação:**
* **pattern:** O padrão `mylog.%g.log` cria arquivos com nomes como `mylog.1.log`, `mylog.2.log`, etc. O `%g` é um marcador que é incrementado para cada novo arquivo.
* **limit:** Cada arquivo terá no máximo 50.000 bytes.
* **count:** Serão criados no máximo 10 arquivos de log.
* **level:** Todas as mensagens de log serão gravadas, independentemente do nível.
* **formatter:** O `SimpleFormatter` é um formatador padrão que fornece informações básicas sobre a mensagem.

### Personalizando o Formato das Mensagens
Para personalizar o formato das mensagens de log, você pode criar um formatador personalizado ou utilizar um dos formatadores pré-definidos do JUL. O `SimpleFormatter` é o mais simples, mas você pode utilizar outros formatadores mais complexos para incluir informações como data, hora, thread e classe.

### Carregando o Arquivo de Configuração
```java
import java.util.logging.LogManager;

public class MeuPrograma {
    public static void main(String[] args) throws Exception {
        LogManager.getLogManager().readConfiguration(
            MeuPrograma.class.getResourceAsStream("logging.properties"));
        // ...
    }
}
```

### Exemplo Completo
```java
import java.util.logging.Logger;

public class MeuPrograma {
    private static final Logger logger = Logger.getLogger(MeuPrograma.class.getName());

    public static void main(String[] args) {
        logger.info("Iniciando o programa.");

        // ... código do programa

        logger.severe("Ocorreu um erro grave.");
    }
}
```
Com este exemplo, todas as mensagens de log serão gravadas em arquivos de log com o padrão `mylog.%g.log`, com um tamanho máximo de 50.000 bytes e um total de 10 arquivos.

---
## Usando a Java Logging API (JUL) com SLF4J
O SLF4J (Simple Logging Facade for Java) é uma fachada de logging que abstrai a implementação do logging, permitindo que você troque o framework de logging subjacente sem precisar modificar seu código. Isso é especialmente útil quando você deseja migrar de um framework de logging para outro sem grandes alterações no código.

### Integração com JUL
Para integrar o JUL com o SLF4J, você precisa adicionar a dependência `slf4j-api` e `slf4j-jdk14` ao seu projeto. A dependência `slf4j-jdk14` é específica para o JUL.

**Exemplo de arquivo pom.xml (Maven):**
```xml
<dependencies>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.36</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-jdk14</artifactId>
        <version>1.7.36</version>
    </dependency>
</dependencies>
```

### Uso do SLF4J
Uma vez que as dependências estão adicionadas, você pode usar a API do SLF4J para registrar mensagens de log. O SLF4J fornece uma interface semelhante à do JUL, mas por trás dos panos, as mensagens são encaminhadas para o JUL.

**Exemplo:**
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MeuPrograma {
    private static final Logger logger = LoggerFactory.getLogger(MeuPrograma.class);

    public static void main(String[] args) {
        logger.info("Iniciando o programa.");

        // ... código do programa

        logger.error("Ocorreu um erro grave.");
    }
}
```

### Vantagens de Usar SLF4J com JUL
* **Abstração de implementação:** Você pode trocar o framework de logging subjacente sem alterar o código.
* **Facilidade de uso:** A API do SLF4J é semelhante à do JUL, facilitando a transição.
* **Flexibilidade:** Você pode usar o SLF4J com outros frameworks de logging, como Logback ou Log4j.
---
## Usando o Logback com SLF4J
* **Logback:** É um framework de logging de alto desempenho e flexível, que implementa a API SLF4J. Ele oferece uma ampla gama de recursos para configuração e personalização dos logs.

**Por que usar Logback com SLF4J?**
* **Desacoplamento:** O SLF4J permite desacoplar a sua aplicação da implementação específica do logging, facilitando a troca de frameworks no futuro.
* **Desempenho:** O Logback é conhecido por seu alto desempenho e escalabilidade, tornando-o ideal para aplicações de grande porte.
* **Flexibilidade:** O Logback oferece diversas opções de configuração, como diferentes appenders (console, arquivo, banco de dados), layouts e filtros.
* **Facilidade de uso:** A API do SLF4J é intuitiva e fácil de aprender.

**Como configurar Logback com SLF4J:**
1. **Adicionar as dependências:**
   ```xml
   <dependency>
       <groupId>org.slf4j</groupId>
       <artifactId>slf4j-api</artifactId>
       <version>1.7.36</version>
   </dependency>
   <dependency>
       <groupId>ch.qos.logback</groupId>
       <artifactId>logback-classic</artifactId>
       <version>1.5.6</version>
   </dependency>
   ```
2. **Criar o arquivo de configuração:**
   Crie um arquivo `logback.xml` na raiz do seu projeto (ou em um local especificado nas configurações do seu build). Este arquivo será usado para configurar o Logback.

**Exemplo de arquivo logback.xml:**
```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

3. **Usar a API SLF4J:**
   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;

   public class MeuPrograma {
       private static final Logger logger = LoggerFactory.getLogger(MeuPrograma.class);

       public static void main(String[] args) {
           logger.info("Iniciando o programa.");
           // ...
       }
   }
   ```

**Personalizando a configuração:**
* **Appenders:** Você pode definir vários appenders para enviar logs para diferentes destinos (console, arquivo, banco de dados, etc.).
* **Layouts:** Personalize o formato das mensagens de log usando diferentes layouts.
* **Filtros:** Filtre as mensagens de log com base em critérios específicos.
* **Níveis de log:** Configure os níveis de log para controlar a quantidade de informações registradas.

**Vantagens de usar Logback:**
* **Desempenho:** Logback é conhecido por seu alto desempenho, especialmente em cenários de alta carga.
* **Flexibilidade:** Oferece uma ampla gama de opções de configuração.
* **Comunidade:** Possui uma comunidade ativa e documentação extensa.
---
## Níveis de Log em Logback e SLF4J
Os níveis de log em Logback e SLF4J servem para classificar a importância das mensagens registradas, permitindo que você filtre e controle quais informações serão mostradas. Essa hierarquia é fundamental para depuração, monitoramento e análise de logs.

**Níveis Comuns:**
* **TRACE:** Nível mais detalhado, utilizado para rastrear o fluxo da aplicação em nível muito granular.
* **DEBUG:** Detalhes sobre o funcionamento interno da aplicação, útil para depuração.
* **INFO:** Informações gerais sobre o estado da aplicação, como inicialização, finalização e eventos importantes.
* **WARN:** Avisos sobre condições que podem indicar problemas futuros.
* **ERROR:** Erros que podem impactar a execução da aplicação.

**Hierarquia dos Níveis:**
A hierarquia dos níveis é importante, pois um logger configurado para um determinado nível também registrará mensagens de níveis superiores. Por exemplo, se um logger estiver configurado para o nível INFO, ele registrará mensagens de nível INFO, WARN e ERROR.

**Configurando os Níveis no Logback:**
O arquivo de configuração do Logback (geralmente `logback.xml`) permite definir os níveis de log para diferentes loggers.
```xml
<configuration>
    <logger name="com.mycompany.myapp" level="DEBUG" />
    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```
* **logger:** Define o nível de log para um logger específico (neste caso, para a classe `com.mycompany.myapp`).
* **root:** Define o nível de log padrão para todos os loggers que não foram explicitamente configurados.

**SLF4J e os Níveis:**
O SLF4J oferece os mesmos níveis de log que o Logback, mas a configuração é feita através do Logback. Ao usar o SLF4J, você está utilizando a API, enquanto o Logback é a implementação subjacente que define os níveis e a configuração.

**Exemplo de uso do SLF4J:**
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MeuPrograma {
    private static final Logger logger = LoggerFactory.getLogger(MeuPrograma.class);

    public static void main(String[] args) {
        logger.debug("Mensagem de debug");
        logger.info("Mensagem informativa");
        logger.warn("Aviso");
        logger.error("Erro grave");
    }
}
```

**Considerações Importantes:**
* **Escolha do nível:** A escolha do nível de log depende do ambiente e da finalidade do log. Em desenvolvimento, níveis mais detalhados (DEBUG, TRACE) são úteis para depuração, enquanto em produção, níveis mais altos (INFO, WARN, ERROR) são mais adequados para monitoramento.
* **Configuração flexível:** O Logback permite configurar os níveis de log de forma granular, permitindo que você defina diferentes níveis para diferentes loggers ou pacotes.
* **Formatação das mensagens:** Além do nível, você pode personalizar a formatação das mensagens de log para incluir informações como data, hora, thread, classe e outras informações relevantes.
---
## Configurando a Saída de Logs com logback.xml
O arquivo `logback.xml` é o coração da configuração do Logback, definindo para onde os logs serão enviados, qual o formato das mensagens e quais níveis de log serão registrados.

### Estrutura Básica do logback.xml
Um arquivo `logback.xml` típico possui a seguinte estrutura:
```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```
**Explicação:**
* **configuration:** Raiz do documento de configuração.
* **appender:** Define um destino para os logs. Neste caso, `STDOUT` envia os logs para o console.
* **encoder:** Define o formato das mensagens de log. O padrão `%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n` formata a data, thread, nível, logger e a mensagem.
* **root:** Define o nível de log padrão para todos os loggers que não foram explicitamente configurados.

### Personalizando a Saída de Logs
**1. Diferentes Appenders:**
* **FileAppender:** Escreve os logs em um arquivo.
* **RollingFileAppender:** Cria novos arquivos de log quando um arquivo atinge um determinado tamanho ou após um intervalo de tempo.
* **SMTPAppender:** Envia os logs por e-mail.
* **JDBCAppender:** Insere os logs em um banco de dados.

**Exemplo de FileAppender:**
```xml
<appender name="FILE" class="ch.qos.logback.core.file.FileAppender">
    <file>myapp.log</file>
    <encoder>
        <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
</appender>
```

**2. Níveis de Log:**
* **level:** Define o nível mínimo para registrar uma mensagem. Níveis comuns: TRACE, DEBUG, INFO, WARN, ERROR.
`{xml}<logger name="com.mycompany.myapp" level="DEBUG" />`

**3. Filtros:**
* **Filter:** Permite filtrar as mensagens de log com base em critérios como nível, marcador, etc.

**4. Formatação:**
* **pattern:** Personalize o formato da mensagem usando diferentes especificadores.

**Exemplo de configuração completa:**
```xml
<configuration>
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.file.RollingFileAppender">
        <file>myapp.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>myapp-%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
    </root>
</configuration>
```
Neste exemplo, os logs serão enviados tanto para o console quanto para um arquivo que será rotado diariamente, mantendo um histórico de 30 dias.

---
## Customizando o Padrão de Layout do Encoder no Logback
O padrão de layout do encoder no Logback define como as mensagens de log serão formatadas antes de serem enviadas para os appenders. Ele oferece uma grande flexibilidade para personalizar a aparência dos logs, permitindo incluir informações como data, hora, thread, nível, logger e a própria mensagem.

### Entendendo o padrão de layout
O padrão de layout é uma string que contém especificadores de conversão. Cada especificador representa um elemento da mensagem de log.

**Exemplo:**
`{xml icon}<pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>`
* **%d{HH:mm:ss.SSS}**: Data e hora no formato HH:mm:ss.SSS
* **[%thread]**: Nome da thread
* **%-5level**: Nível de log com 5 caracteres de largura, alinhado à esquerda
* **%logger{36}**: Nome do logger com no máximo 36 caracteres
* **- %msg%n**: Mensagem de log seguida de uma nova linha

### Especificadores de Conversão Comuns
* **%d**: Data (vários formatos disponíveis, como ISO8601)
* **%p**: Nível de log
* **%t**: Nome da thread
* **%c**: Nome da classe
* **%logger**: Nome do logger
* **%m**: Mensagem de log
* **%n**: Nova linha

### Personalizando o Layout
Você pode criar layouts personalizados combinando diferentes especificadores de conversão e utilizando expressões regulares.

**Exemplo:**
`{xml icon}<pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level [%marker] %logger{36} - %msg%n%throwable{full}</pattern>`

* **%d{yyyy-MM-dd HH:mm:ss.SSS}**: Data e hora em formato mais completo
* **[%marker]**: Marcador (se houver)
* **%throwable{full}**: Exceção completa, incluindo pilha de chamadas

### Outros Elementos do Layout
* **%X**: Propriedades MDC (Mapped Diagnostic Context)
* **%mdc**: Propriedades MDC
* **%colored**: Cores para destacar diferentes níveis de log

### Exemplo Completo com Cores e Marcadores
```xml
<configuration>
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%highlight(%d{HH:mm:ss.SSS}) %blue(%-5level) [%green(%thread)] %yellow(%logger{36}) - %msg%n%throwable{full}</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="CONSOLE" />
    </root>
</configuration>
```
Neste exemplo, os níveis de log são coloridos para facilitar a visualização.

### Utilizando Marcadores
Marcadores são uma forma de adicionar informações contextuais às mensagens de log. Eles podem ser usados para filtrar logs ou para personalizar o layout.
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.slf4j.Marker;
import org.slf4j.MarkerFactory;

// ...

Marker marker = MarkerFactory.getMarker("MY_MARKER");
logger.info(marker, "Mensagem com marcador");
```
---
## Salvando Logs em Arquivos com FileAppender do Logback
O **FileAppender** é um componente essencial do Logback que permite direcionar as mensagens de log para arquivos, possibilitando um armazenamento mais permanente e organizado das informações.

### Configurando o FileAppender
Para configurar o FileAppender, você precisa adicionar as seguintes informações ao seu arquivo `logback.xml`:

* **Nome do appender:** Um identificador único para o appender.
* **Classe do appender:** `ch.qos.logback.core.file.FileAppender`
* **Arquivo de destino:** O caminho completo do arquivo onde os logs serão armazenados.
* **Encoder:** Define o formato das mensagens de log.

**Exemplo:**
```xml
<configuration>
    <appender name="FILE" class="ch.qos.logback.core.file.FileAppender">
        <file>myapp.log</file>
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="INFO">
        <appender-ref ref="FILE" />
    </root>
</configuration>
```
**Explicação:**
* **appender name="FILE"**: Define um appender chamado "FILE".
* **file="myapp.log"**: Os logs serão escritos no arquivo "myapp.log".
* **encoder**: Define o formato das mensagens de log.

### Personalizando a Saída dos Logs
**1. Rotatividade de Arquivos:**
Para evitar que o arquivo de log cresça indefinidamente, você pode utilizar o `RollingFileAppender` e configurar uma política de rotação.

```xml
<appender name="ROLLING_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
    <file>myapp.log</file>
    <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
        <fileNamePattern>myapp-%d{yyyy-MM-dd}.log</fileNamePattern>
        <maxHistory>30</maxHistory>
    </rollingPolicy>
    <encoder>
        <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
</appender>
```

**2. Níveis de Log:**
Você pode configurar o nível de log mínimo para cada appender.
```xml
<logger name="com.mycompany.myapp" level="DEBUG">
    <appender-ref ref="FILE" />
</logger>
```

**3. Filtros:**
Utilize filtros para incluir ou excluir determinadas mensagens com base em critérios como nível, marcador, etc.

**4. Formatação:**
Personalize o formato das mensagens de log usando diferentes especificadores de conversão (veja a seção anterior sobre personalização do padrão de layout).

---
